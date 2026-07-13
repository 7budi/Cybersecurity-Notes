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

