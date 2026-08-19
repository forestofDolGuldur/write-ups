tartarsausage  
Category: Web  

Description: Find the sausage and be a king of "tar".  
Flag format: CTF{sha256}

Link to the challenge: https://app.cyber-edu.co/challenges/98d79d5b-3e34-458c-b623-e519193afb81?tenant=unbreakable

For this ctf, we have to exploit a site by using command injection with the tar linux command.

After doing some recon, I found in the source code another page  
<img width="810" height="403" alt="image" src="https://github.com/user-attachments/assets/cb4b36e6-d307-4e65-a104-fceebe1f9868" />  

It had an input field, where I pasted the options and parameters for the tar command:  

<img width="444" height="154" alt="image" src="https://github.com/user-attachments/assets/f501766c-5f91-4a31-9713-ca2688e2f736" />  

`-cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec='ls -lah'` 

And basically, with this payload I could list all the files from there.  

<img width="1917" height="71" alt="image" src="https://github.com/user-attachments/assets/36de3e01-4a4b-4fd6-a1b4-3b0277286ae0" />

I found this directory named `enhjenhzZGN3YWRzYWRhc2Rhc3NhY2FzY2FzY2FzY2FjYWNzZHNhY2FzY2Fzc2FjY2Fz`, which it seemed strange to me. I decided to take a look in the directory by pasting the name of it in the payload.  

And there I found a file name flag, and instead of `ls -lah` I used `cat` in the payload to read that file.

Flag: `ctf{e15918e70b7c3395bcb357b4ca5e95f868ebc462d33371a5f44a25c35f8faa45}`
