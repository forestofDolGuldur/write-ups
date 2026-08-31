Ray3  
Category: Reverse Engineering  

Description: All the information you need is in the attachment file.  
The format of the flag is CTF{sha256}  
After decrypting the message you'll have to calculate the sha256 value and submit the flag -> CTF{sha_256_message_of_your_message}  
The flag must be submitted in full, including the CTF and curly bracket parts.  

Link to the challenge: https://app.cyber-edu.co/challenges/98d79d77-8d15-4669-8bac-7401aa61cce8?tenant=unbreakable  

For this ctf, I had to analyze and decrypt an encrypted message, and sending it as an argument when running the binary.  

Firstly, by looking at the main function, this binary takes the environment variable `whoami` and checks if it has the value `yeyy`.  
I did that by typing `export whoami=yeyy` in terminal.  

In the check function, I had a vector, and some integers, which most of them I renamed, to be more easy to analyze the binary.    

<img width="415" height="567" alt="image" src="https://github.com/user-attachments/assets/f48a5757-3057-4ef9-8313-613f1fbcc7c6" />  
<br>
<img width="534" height="229" alt="image" src="https://github.com/user-attachments/assets/fcb9dfb8-62b6-4f46-9055-0049a976a37f" />  

For this block of code, it checks if the argument is 17 characters long, if yes it sums all the characters from the whoami environment variable (yeyy) into yeyy_var variable, which is an integer, so it basically is 'y' + 'e' + 'y' + 'y' => 464 in decimal.  
Then it goes into a for loop and it adds or subtracts 4 based on the parity, if the position of the vector is even, it adds 4, if the position is odd, it subtracts 4.  
After that, the character is getting XORed with 464/0x1e, which is 464/30, which is 15 (rounded because it's an int), and after this, the character is put back in the V vector.  

<img width="355" height="258" alt="image" src="https://github.com/user-attachments/assets/57c53db5-734b-4356-8c0e-0edf02603340" />  

This block of code put the characters from the V vector into S vector, but reversed.  
And since we have the S vector's values, I did an python script to xor the characters with 15 and add/subtract 4 depending on the parity of the position.

```
S = [
    0x66, 0x7E, 0x7D, 0x6A, 0x77, 0x65, 0x7C, 0x50, 
    0x6C, 0x51, 0x7C, 0x69, 0x6C, 0x6F, 0x7C, 100, 0x44 
]

S_rev = S[::-1]

parola = ""
for j in range(len(S_rev)):
    val = S_rev[j] ^ 15 
    if j % 2 == 0:
        val -= 4 
    else:
        val += 4 
        
    parola += chr(val)

print(f"Message: {parola}")
```

After running it, I got this output: `Good_job_continue`  
And if I run the binary with this argument, I get `Flag format: ctf{Good_job_continue}`, which is actually the print_flag function.  

The last thing I had to do is to calculate the SHA256 sum and to wrap it in CTF{}.

Flag: `CTF{62745be9d3888d69b35b0f80ec06c91e4d30ac5c42a2e18b0ee467108018f45e}`
