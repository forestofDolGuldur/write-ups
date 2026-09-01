mongoose  
Category: Web  

Description: Challenge name is all you need to get it started!  
Flag format ctf{sha256}  

Link to the challenge: https://app.cyber-edu.co/challenges/98d79d6f-9395-40a3-a64b-a56aec752af3?tenant=unbreakable  

For this ctf, I had an admin login page, which I had to exploit. But the flag was sitting in plain sight in a .js file.  
On the login page, I used CTRL+U to see the source code of the page, and found login.js  

<img width="585" height="470" alt="image" src="https://github.com/user-attachments/assets/76fe8f92-90d6-43b0-b03a-13fbe9cf774b" />  

After entering it, I could see the JS code, and the flag.  

<img width="945" height="442" alt="image" src="https://github.com/user-attachments/assets/b568c84e-5d8d-4fa6-9940-629cfce2a770" />  

Flag: `ctf{d130ca6ea8c05c8cf7dcf76dae146f2fcfd62be082e9acb9aa2f0a5934e4eee1}`  
