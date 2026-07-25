## Recon
- PORT      STATE SERVICE      VERSION
	135/tcp   open  msrpc        Microsoft Windows RPC
	139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
	445/tcp   open  microsoft-ds Windows 7 Professional 7601 Service Pack 1 microsoft-ds (workgroup: WORKGROUP)
	3389/tcp  open  tcpwrapped
	5357/tcp  open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
	8000/tcp  open  http         Icecast streaming media server
- since icecast is vulnerable to CVE-2004-1561 we can us metasploit to gain access.
## Gain Access 
- Using metasploit and using exploit/windows/http/icecast_header we can gain a meterpreter.

## Escalation 
- Even though we got meterpreter but we still don have authority so we background the session and use suggester, and it gives back results that we can use , we will use exploit/windows/local/bypassuac_eventvwr.
- we set the sesssion and run it and we get another meterpreter, we can check the process that run ps.
- Then we can try to migrate to one of the process that will work ,after that we get authority.
- We can load kiwi to help us even more and after kiwi is loaded we can use the command creds_all to get the password of the user.