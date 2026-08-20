gogu  
Category: Reverse Engineering

Description: For sure obfuscated values are secure.  
Flag format: ctf{sha256}

Link to the challenge: https://app.cyber-edu.co/challenges/98d79d58-84b4-46e7-aa20-79a8943ed54f?tenant=unbreakable

For this ctf, we have to analyze a Golang binary and deobfuscate it and get the flag.    
I was analysing it dynamiacally, because it's very hard to analyze it statically.  

Firstly I ran it and I got this string, which looks like a hash, probably the hash of the flag.  
<img width="275" height="100" alt="image" src="https://github.com/user-attachments/assets/357f9073-0461-4f01-b88b-b37179210294" />  

I opened it with gdb and put a catchpoint on the write call with `catch syscall write` command.  
Then I ran it again until I got the hash.  

<img width="812" height="522" alt="image" src="https://github.com/user-attachments/assets/6cb40fb6-3cfc-4ea0-babf-8865928a065c" />  

After this I went to see the virtual memory map of this proccess, with `info proc mappings`  

<img width="889" height="257" alt="image" src="https://github.com/user-attachments/assets/bc47bc96-8eb6-46b8-a702-35062d1e940c" />  

I searched for the flag in the heap regions with rw-p, and I decided to look for it in this offset:`0x000000c41fff8000 0x000000c420100000` with `dump memory dump.txt 0x000000c41fff8000 0x000000c420100000`.  
And after using `strings dump.txt` I could find the flag sitting right there.  

<img width="581" height="69" alt="image" src="https://github.com/user-attachments/assets/375e98ca-ab18-4705-b344-f0bbeeb9949b" />  

Flag: `ctf{1fe6954870babd55ba6e5dfa57d4ed11aabb70533397b985c890749cbfc7e306}`
