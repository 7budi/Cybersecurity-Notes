Note: Didn't as usual , had to got to /etc/host/ and add the ip and name.
## Recon
- There was nothing interesting in nmap , nikto and gobuster.
- So tried login in with random username and password.
- When the user name is correct it says password is wrong and when both are wrong it say username or password wrong.
- So i had to use hydra to find the password (brute-forcing).
	- hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.XXX.XXX http-post-form "/login.php:username=^USER^&password=^PASS^:F=Wrong Password" -V