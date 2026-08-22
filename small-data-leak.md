small-data-leak  
Category: Web  

Description: I do not know what is wrong /user?id=. It's not working at all. All I know is that an attacker is asking us for a ransom...  
Flag format: CTF{sha256}  

Link to the challenge: https://app.cyber-edu.co/challenges/98d79d5c-2457-4e3c-9bc2-5570004865e2?tenant=unbreakable  

For this ctf, I've used sqlmap to map the database, and to use SQL injection to get the flag.

Firstly, I've used dirsearch to see if there are any hidden endpoints, but there were only `/register` and `/user`.  
But when I tried to enter /user?id=', I got this SQLAlchemy error:  
<img width="1156" height="155" alt="image" src="https://github.com/user-attachments/assets/28605c5a-575a-46e9-bc09-b7a0f79a3742" />  
And then I knew it was a SQL injection. 

I tried `sqlmap -u http://35.242.207.227:32352/user?id=1`, and saw that the database is PostgreSQL.  
<img width="1011" height="373" alt="image" src="https://github.com/user-attachments/assets/d61e203b-a417-46ad-9ff0-4378dc01a891" />  

After this, I used `--dbs` option, to map all databases, and found the a "public" database.  
<img width="415" height="118" alt="image" src="https://github.com/user-attachments/assets/8c079d07-068e-4a35-85bb-b2921b29605c" />  

Then I used `-D public --tables` option to enumerate the database tables, and found a part of the flag.  
<img width="558" height="119" alt="image" src="https://github.com/user-attachments/assets/dcc02124-7206-4e2c-b9d3-516baf61fe72" />  
Now what I had to do, is to enumerate the table columns of that database table.

I added `-T 'ctf{57b23475b9b02093a9eb5d7df5f07957e2b2dc724443d6b08961fbe3387' --columns` options, and found the rest of the flag.  
<img width="596" height="153" alt="image" src="https://github.com/user-attachments/assets/1854719f-e6c5-40c8-bfe2-fe9969e6143f" />  

Flag: `ctf{57b23475b9b02093a9eb5d7df5f07957e2b2dc724443d6b08961fbe3387cf91f}`
