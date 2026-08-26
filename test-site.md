test-site  
Category: Web  

Description: The developers are pretty lazy, they haven't finished anything! Hint: Everything is running on localhost. (optional/it costs points)  
Flag format: CTF{sha256}  

Link to the challenge: https://app.cyber-edu.co/challenges/9b39255a-900d-4465-8430-48bd3ae03b18?tenant=rocsc

For this ctf, I had to find an entry point, and then modify the request header  

Firstly, I used gobuster to find the entry points.  

<img width="786" height="392" alt="image" src="https://github.com/user-attachments/assets/db693ce5-2490-4228-b980-d7db1e72e923" />  

Now that I found `/testsite`, I pasted it in browser, and it redirected me to localhost:8889  

<img width="1919" height="840" alt="image" src="https://github.com/user-attachments/assets/002b1f47-5d40-48bf-b0db-32be0b4f4c49" />

After this I knew that I had to use Burp Suite to modify the request header into localhost:8889.  
And after intercepting a request and modifying the header, I could get the flag.  

<img width="1255" height="577" alt="image" src="https://github.com/user-attachments/assets/e082d151-814d-4fcd-816a-62d3a5dbf30b" />

Flag: `CTF{17125bc21c5f6aa9d599471bb87dabc2a784377e76007448b517ecda99a3d83a}`

