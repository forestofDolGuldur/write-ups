authorization  
Category: Web  

Description: Can you be a master of recon!  
Flag format: CTF{sha256}  

Link to the challenge: https://app.cyber-edu.co/challenges/98d79d74-989d-4ce8-8f59-2a85644002e6?tenant=unbreakable  

For this ctf I had to identify the entry points, and get authorization using a JWT token to get the flag.  

First, I used dirsearch to find all entry points.  

<img width="394" height="120" alt="image" src="https://github.com/user-attachments/assets/e9310e60-e721-45d0-9db2-f4721a0d868a" />

`client_secrets.json` appeared to be very intresting, because entering it I've saw some interesting things: `{ "username": "admin", "password": "admin" }`

In `robots.txt` I've saw `/auth` but I already saw that in dirsearch.

`/auth` has 405 error, so I opened Burp Suite and tried to the request into POST.  

<img width="1577" height="710" alt="image" src="https://github.com/user-attachments/assets/4f21f012-816e-4186-af65-ac617f143e53" />  
<img width="1577" height="713" alt="image" src="https://github.com/user-attachments/assets/4cd071e7-e0f9-492b-85ab-7b5def23be64" />  

Now I tried entering `{ "username": "admin", "password": "admin" }`, but the same error appeared, and after that I tried entering `Content-Type: application/json` in the header, and got a JWT token. 

<img width="1581" height="413" alt="image" src="https://github.com/user-attachments/assets/53fa9817-ddc7-47f4-a441-1cb187a5de84" />

Now I went into `/secrets` page, using Burp Suite, and entering in the header `Authorization: JWT eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE3ODc4NDE3ODksImlhdCI6MTc4Nzg0MTQ4OSwibmJmIjoxNzg3ODQxNDg5LCJpZGVudGl0eSI6MX0.ocpu8rHhcJ8ELbQgSfttZ2d_7WihGNtIYIot99taSjQ`  

And it worked, and got the flag. 

<img width="1580" height="419" alt="image" src="https://github.com/user-attachments/assets/a788cd14-ece0-42bd-8314-5e92fd58de29" />

Flag: `CTF{5b7cc033a48df4958a076286420b4a91631defa16be26409afbdf1e053367b21}`
