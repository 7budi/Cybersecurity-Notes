## IP Address
- What is IP address?
	- It is a unique identifying number assigned to every device connected to the internet.
	- it is made up of 1s and 0s that are change to human readable format.
	- its made up of 32bits (8+8+8+8= 4bytes).
	- https://media.licdn.com/dms/image/v2/D5622AQFuvCetIf6Eaw/feedshare-shrink_800/feedshare-shrink_800/0/1721178252055?e=2147483647&v=beta&t=HM41dAiUMfOD7EJSRZ_UXYFbrX5ZfOmEztc_uQRex-o
	- Public IPs can be rent from the ISP.
	- Layer 3.
## MAC Address
- Media Access Control is our physical address.
- Anything that is using Network interface have a mac address
- This mac's are important because they utilize layer 2 or switching and they are how we communicate over switch.
- The first 3 pairs are identifiers and the rest is unique number.

## What is TCP and UDP?

- TCP(Transmission Control Protocol) is a connection oriented protocol.
	- Best suited for high reliability.
	- It works on 3 way handshake (SYN, SYN ACK, ACK).
	- EX: Like wibesite (http,https),SSH,FTP(File Transfer Protoco).
- UDP(User Datagram Protocol) is a connection-less protocol. 
	- EX: DNS,Streaming
### Common Ports and Protocols
- TCP
	1. FTP(21)
	2. SSH(22) ->same as telnet but encrypted version. 
	3. Telnet(23) -> telnet is the ability to login in a machine remotely and it is in clear text. 
	4. SMTP(25)
	5. DNS(53) -> is a way to resolve IP addresses to Names.
	6. HTTP(80)/HTTPS(443)
	7. POP3(110)
	8. SMB(139+445) -> file share (SAMBA)
	9. IMAP(143)
- UDP
	1. DNS(53)
	2. DHCP(67,68)
	3. TFTP(69)
	4. SNMP(161)
## OSI Model
1. Physical : Data cables, cat6 , generally it is something that you plug in.
2. Data : Switching, MAC Addresses 
3. Network : IP Addresses , routing
4. Transport : TCP/UDP
5. Session : session management 
6. Presentation : WMV, JPEG, MOV
7. Application : HTTP , SMTP