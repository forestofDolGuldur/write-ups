yachtclub  
Category: Web  

Description: From finding that one vulnerability to exploiting it, there is an entirely new science behind it.  
Flag format: UNR{xxxx-xxxx...}  

Link to the challenge: https://app.cyber-edu.co/challenges/98d79d6a-1f99-4294-a167-ba7d224da5f9?tenant=unbreakable

For this ctf, I used dirsearch and sqlmap to indentify some entry points and to use SQLi on a MySQL DBMS.

Firstly, I've used dirsearch to enumerate the entry points, and found the README.md file.    

<img width="412" height="384" alt="image" src="https://github.com/user-attachments/assets/7c7e84ef-6595-44c8-bd1a-eaa2a5654860" />  

After entering /README.md, found the steps to get the flag.  

<img width="506" height="79" alt="image" src="https://github.com/user-attachments/assets/45cb663c-cbc4-47a9-8814-231ba0c0cf4e" />  

After reading this file, my first thought was to use sqlmap.
Firstly, I used `sqlmap -u http://34.159.137.78:32606/msg.php?id=-1` and found that the DBMS was MySQL and that it was injectible.  

Then I used `--dbs` options to map the databases, and found these 2 databases.

<img width="234" height="53" alt="image" src="https://github.com/user-attachments/assets/aab828f8-c49e-4ba3-a2ca-f8f3d07b096f" />  

After that, I entered `-D s-d2-c2s-l1136-yachtclub --tables` options to map the tables from that database.

<img width="287" height="86" alt="image" src="https://github.com/user-attachments/assets/0600a766-7fdc-4781-9e9d-6a3d65c744e6" />

Then I added `-T 'message' --columns` options, to map the columns of that table.

<img width="296" height="200" alt="image" src="https://github.com/user-attachments/assets/1d5184d4-dba4-4ae4-91a2-b31ed3ac2a1c" />  

I found the `specialflag` column, and read it using `--dump` option.

<img width="538" height="138" alt="image" src="https://github.com/user-attachments/assets/43ff327c-88e5-4266-9081-e83997cacb5f" />  

After dumping the column, I got the flag.  
Flag: `UNR{65lpfq-ledl5y-akac7d-nldamn-yjyst5-lbe65i-n55wfj-qmkdcu}`
