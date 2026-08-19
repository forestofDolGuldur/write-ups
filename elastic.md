elastic  
Category: Web/Pentest  

Description: Directory traversal vulnerability in Elasticsearch allows remote attackers to read arbitrary files via unspecified vectors related to snapshot API calls.  
Flag format: CTF{sha256}  

Link to the challenge: https://app.cyber-edu.co/challenges/98d79d7b-3cb1-4646-848c-de75a2b64f14?tenant=unbreakable

For this ctf, I had to find the CVE for the site, and to exploit it.

Firstly, after some research, I wanted to see if elasticsearch had snapshots, by using /_snapshot in the query, and it had. 

Secondly, I searched elasticsearch 1.3.4 vulnerability and found the CVE-2015-5531 vulnerability, and researching more, I found a script on github (`https://github.com/nixawk/labs/blob/master/CVE-2015-5531/exploit.py`), which could exploit the site.

After running it, with the IP and the file I wanted to read in parameters, I could read the whole file and get the flag from /etc/passwd.

<img width="1370" height="178" alt="image" src="https://github.com/user-attachments/assets/2c0e6376-e4a0-4593-9303-9cdcc86eb67a" />

Flag: `CTF{265b92ed0091f139fdcd438196426f205fed9b14bce765bafd8344b1d96183e5}`
