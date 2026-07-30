- A buffer overflow is when an attacker write more than what is expected in a certain part of the memory, and that overflow flows to other part of memory.
- https://www.google.com/url?sa=t&source=web&rct=j&url=https%3A%2F%2Fwww.packtpub.com%2Fen-IN%2Fproduct%2Fmastering-metasploit-second-edition-9781786463166%2Fchapter%2F3-the-exploit-formulation-process-3%2Fsection%2Fexploiting-stack-based-buffer-overflows-with-metasploit-ch03lvl1sec28%3Fsrsltid%3DAfmBOoo1zLD4WIu7-B9fXv1qlkBWGX-GP_Uj7jOH_8_oRjSv_iqrRmrP&ved=0CBYQjRxqFwoTCICP_fHF85UDFQAAAAAdAAAAABA3&opi=89978449
- https://www.google.com/url?sa=t&source=web&rct=j&url=https%3A%2F%2Fwww.semanticscholar.org%2Fpaper%2FThe-Buffer-Overflow-Attack-and-How-to-Solve-Buffer-ALHusayn%2Fd59f80861f46722e4086b824e7de9c4ce52f5b35&ved=0CBYQjRxqGAoTCICP_fHF85UDFQAAAAAdAAAAABCMAQ&opi=89978449https://www.google.com/url?sa=t&source=web&rct=j&url=https%3A%2F%2Fwww.semanticscholar.org%2Fpaper%2FThe-Buffer-Overflow-Attack-and-How-to-Solve-Buffer-ALHusayn%2Fd59f80861f46722e4086b824e7de9c4ce52f5b35&ved=0CBYQjRxqGAoTCICP_fHF85UDFQAAAAAdAAAAABCMAQ&opi=89978449
- stack grows up to lower addresses.
- ESP: register conatins the memory address to the top of the stack.
- EBP:register contains the memory address to the bottom of the stack.

## Spiking 
- Spiking is the first step you take to find a vulnerability.
- It is a process of probing an application to dicover which command or input are susceptible to buffer overflow.
- 