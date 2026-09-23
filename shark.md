shark  
Category: Web  

Description: Exploit the shark and get the flag!  

Link to the challenge: https://app.cyber-edu.co/challenges/98d79d78-0a7b-4bad-937d-6dbb272d39a5?tenant=unbreakable

For this ctf, I exploited a site which was vulnerable by SSTI.  

Firstly, in the text input field, I entered `${7*7}`, and it returned me 49.  

<img width="283" height="117" alt="image" src="https://github.com/user-attachments/assets/d83bbaf5-8fdb-46dd-9e45-ee9c77e2586c" />

I used `curl -I http://34.107.28.150:31917` to get the HTTP header and I saw that the server is run on Flask.  

<img width="332" height="132" alt="image" src="https://github.com/user-attachments/assets/b3760465-62c0-46fb-a85d-4bbced4a0e79" />

Then I tried a basic payload for SSTI, which is `${__import__('os').popen('ls').read()}`, to read the files in the current directory.  
This payload worked, and I saw 2 files there.  

<img width="287" height="121" alt="image" src="https://github.com/user-attachments/assets/dc32587a-738a-41e3-b15b-ea9699083a5e" />

Then I replaces `ls` with `cat flag`, and got the flag.  

Flag: `CTF{4b08602e0090f81707b98ca687a5cacfd32888ffceef1d3cff2d99e6034b1e58}`
