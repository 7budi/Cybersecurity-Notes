## Recon
- nmap search:
	- PORT     STATE SERVICE     VERSION
		21/tcp   open  ftp         vsftpd 3.0.5 <- very secure file transfer protocol 
		22/tcp   open  ssh         OpenSSH 8.2p1 Ubuntu 4ubuntu0.13 (Ubuntu Linux; protocol 2.0)
		139/tcp  open  netbios-ssn Samba smbd 4
		445/tcp  open  netbios-ssn Samba smbd 4
		3128/tcp open  http-proxy  Squid http proxy 4.10 <- a widely used, open-source caching and forwarding web proxy that acts as an intermediary between clients and destination servers
		3333/tcp open  http        Apache httpd 2.4.41 ((Ubuntu)) 
- Nothing interesting found so since there is a web server running on port 3333 lets do a brute force directories.
- And a directory called  /internal is found which we can upload a file into it.
## Gaining access 
- While checking which type of file can be uploaded by using burpsuite or manual it accepts a .phtml file.
- So we can make a reverse shell with the php-reverse-shell.php file after changing it to php-reverse-shell.phtml.
- then we listen in our machine , nc -lvnp  4444 , so when we go to the /internal/php-reverse-shell.phtml it will give us a shell.
## Privilege Escalation 
- 