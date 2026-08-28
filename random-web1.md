random-web1  
Category: Web  

Description: Source code everywhere!  
Flag format: CTF{}  

Link to the challenge: https://app.cyber-edu.co/challenges/98d79d70-1a38-40a2-a876-2290d2a17952?tenant=unbreakable  

For this ctf, I had to exploit a site which uses php, by using command injection.  
First time entering the site, it wouldn't show anything, but by viewing the source code using CTRL+U, there was a comment, saying `/?source`.  
After entering it, I could see the whole php code.  

<img width="499" height="286" alt="image" src="https://github.com/user-attachments/assets/27f7794f-504d-43a3-9b59-bd35072a5d60" />

For the variable p, the code erases every non-ASCII character, the word flag from it, and limits the string to 9 characters.    

I tried entering `/?p=;ls` in the query, and I could see `flag.php` and `index.php` right there.  
Using the word flag in the query wouldn't work, because it would erase it.    
I used `?p=;cat$IFS*.php` to read all the .php files. It showed nothing, but by viewing the source code, I could see the flag commented.  

<img width="521" height="359" alt="image" src="https://github.com/user-attachments/assets/8661c906-61aa-42d2-b605-51a91ca21335" />

Flag: CTF{a9b6b13862f0a8d1312d777a91a596eba7cb010f}
