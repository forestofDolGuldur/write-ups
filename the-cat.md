the-cat
Category: Network

Description: We know yakuhito's been playing in our internal network for over a year, but we never managed to kick him out. Last week, he made the big screen at the entrance play nyan cat.

Link to the challenge: https://app.cyber-edu.co/challenges/98d79d5e-64b9-46c8-a7b3-9d5cc8856b99?tenant=unbreakable

For this ctf, I had to analyze a network traffic capture, extract secret keys and get the original file containing the flag.  

Firstly, I looked into TCP streams, and on the 121st stream, I found some secret keys.  

<img width="1894" height="854" alt="image" src="https://github.com/user-attachments/assets/34e068f2-fb23-4b9c-9cfc-72b12739f51e" />

I extracted them, and pasted them into a txt file.  
Then I went back on Wireshark -> Edit -> Preferences -> Protocols -> TLS and selected the file containing the keys on (Pre)-Master-Secret log filename.  

After that, I searched into the unencrypted traffic, and on the 120th TCP stream I identified a zip file, by its header, and also by the name.  

<img width="1910" height="885" alt="image" src="https://github.com/user-attachments/assets/32e4c22c-5010-4662-bb85-d2a7cb314880" />  

To extract this zip file, I switched the stream from show as ASCII to Raw, then I found the magic bytes, and copied the rest of the data until the end of the client packet.
Now I pasted this into a file, then used this command to make a file which is actually the zip file.

```
xxd -r -p tempzipfile.txt > nyan.zip
```

I extracted the zip file, then I ran the bash script, and got the flag.

Flag: `X-MAS{yeah_nyan_is_cool_but_have_you_ever_Y3VybCAtcyAtTCBiaXQubHkvMTBoQThpQyB8IGJhc2gK-ea8f6adb7605962d}`
