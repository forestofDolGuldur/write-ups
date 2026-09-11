surfing  
Category: Network

Description: Someone leaked the flag over the internet.  
Find the flag. Flag format CTF{sha256}

Link to the challenge: https://app.cyber-edu.co/challenges/98d79d72-c995-4924-9682-cb4f5eaf37e4?tenant=unbreakable

For this ctf, I was given a text file containing SSL/TLS keys, and with it I had to decrypt the network traffic and get the flag.  

Firstly, I went to Edit -> Preferences -> Protocols -> TLS -> (Pre)-Master-Secret log filename, and selected keys.log, which is the file containing the keys.  

Now, I tried entering CTF{ in the display filter, because there were almost 200k packets and there was no point in looking in all of them, and found the first part of the flag.  

<img width="1908" height="842" alt="image" src="https://github.com/user-attachments/assets/9f9d0e26-cf8b-4b1b-bdfe-0a08f81ace53" />

There was also "flag1", so I looked for the rest of the flag.  
After searching for "flag2" and "flag3", got all the parts, and reconstructed the flag.

Flag: `CTF{4fa27628dd9210775c76263c0d6bef0f86b80e3fef78c072879d639e34ba6734}`
