custom-ENDIAN  
Category: Cryptography  

Description: Cineva a realizat niste modificari pe fisierul custom.png atasat. Mă puteți ajuta să recuperez mesajul secret din el?  

Link to the challenge: https://app.cyber-edu.co/challenges/9b7be8fa-7b1a-4e1a-abfe-935038dd0ed2?tenant=rocsc  

For this ctf, I had to identify the endianness and to make a python script to repair the file and to get the flag.  

Firstly I used xxd to see the endinness.  

<img width="552" height="359" alt="image" src="https://github.com/user-attachments/assets/01d48a28-a369-40bd-86f8-a4a9ce62e986" />  

Here I could see the scrambled PNG header and the flag there.  
The endianness is: Byte1 Byte4 Byte2 Byte3.  

I made an python script which repairs the endianness:  
```
with open("custom.png", "rb") as f:
    data = bytearray(f.read())

pad = len(data) % 4
if pad:
    data.extend(b'\x00' * (4 - pad))

out = bytearray(len(data))

for i in range(0, len(data), 4):
    b1 = data[i]
    b4 = data[i+1]
    b2 = data[i+2]
    b3 = data[i+3]
    
    out[i]   = b1
    out[i+1] = b2
    out[i+2] = b3
    out[i+3] = b4

with open("repaired.png", "wb") as f:
    f.write(out)
```

After using this script, I could see the Joker image and after using xxd, I could see the flag:  

<img width="556" height="365" alt="image" src="https://github.com/user-attachments/assets/fce937c4-ba1e-43e7-a53c-de1a2dea3109" />  

Flag: `ctf{cfb7d769f497097e0866e22090bc1e8e17c44c6c20f6817a195cc511e8062225}`

