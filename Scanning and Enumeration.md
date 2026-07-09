## Nmap

- It is designed to scan networks and identify which hosts
are available on the network using raw packets, and services and applications, including the
name and version, where possible. It can also identify the operating systems and versions of
these hosts. Besides other features, Nmap also offers scanning capabilities that can
determine if packet filters, firewalls, or intrusion detection systems (IDS) are configured as
needed.
syntax:
nmap < scan types> < options> < target>
- the TCP-SYN scan ( -sS ) is one of the default settings unless we have defined otherwise and is also one of the most popular scan methods
- -sS for stealth scaning SYN SYNACK RST.
- -T4  for fast scan.
- -p- to scan all ports.
- -p to scan specific ports.
- -A to get every info. 
- -sU UDP scan.
- sudo nmap -sn 192.168.1.0/24 finding devices on a local network using ARP.


## DirBuster

- DirBuster is a powerful tool used to discover hidden directories and files on a web server by running a dictionary attack
- To do a search in terminal : 
	- dirbuster -H -u http://172.16.199.129 -l /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt
## SMB 

- Server Message Block is a file share , that regulate access to file and directories and other network resources such as printer , router, or interfaces released for the network. 
- Information exchange between different system processes and also be handled on the SMB protocol.
- SMB uses TCP protocol, which provide a three-way handshake before a connection is established between the client and server.
### SAMBA
- Is an alternative implementation for SMB, which is developed for unix-based os.
- Samba implements the common internet file system(CIFS) protocol.
- A "**workgroup**" is a group name that identifies an arbitrary collection of computers and their resources on an SMB network.

## Metasploit

- Metasploit is the world's most widely used penetration testing framework. It can be considered a "Swiss army knife" for security professionals because it provides the tools needed to simulate real cyberattacks. Instead of building your own tools from scratch for every test, Metasploit provides a massive collection of pre-built, ready-to-use components.
- To start metasploit on your terminal just type **msfconsole**.
	- EX:
		msfconsole <- will start metasploite 
		search smb <- will search every payload for smb
		use auxiliary/scanner/smb/smb_version < - after finding the payload we can start it like this .
		info for more information about the payload.