safe-password  
Category: OSINT  

Description:  
Another breach in the company... Haven't they learned anything? It's frustrating to witness the same mistake repeatedly. After all, it's not rocket science to implement basic cybersecurity measures like using non-pwned passwords.It looks like one has been seen more than 80 times before.  
Can you help me find that one?  

Flag format: CTF{sha256(password)}  

Link to the challenge: https://app.cyber-edu.co/challenges/9b9d86ae-275c-409a-8d5d-ad7b4fce2405?tenant=unbreakable

For this ctf, I had a file containing a lot of passwords, and I had to check each one to see how many times it got pwned.  
The site I'm gonna use is `https://haveibeenpwned.com/Passwords`  

After checking the bottom part of the text file, which had easier passwords, I found `Bubblegum123!` which has been pwned 2,207 times (at this moment when I did the ctf).

Flag: `CTF{fdc852bc63a266c8c38db64bef90d62d53ddeef00aa85df7b941ac780b3d75d8}`
