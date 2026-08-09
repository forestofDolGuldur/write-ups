blacklisting  
Category: Web  

Description: I think my blacklist is going to prevent any vulnerability!  
Flag format: CTF{sha256}  

Link to the challenge: https://app.cyber-edu.co/challenges/98d79d72-b3c4-4fcd-b52e-7da852865f57?tenant=unbreakable

First time entering the site, it just shows me some php code.

<img width="293" height="292" alt="image" src="https://github.com/user-attachments/assets/dd0bb579-0532-47a5-add9-db38e7e6a584" />

So basically what I needed to do, is to craft a query to get the flag.  

For the first block of code, I saw `$_GET['start']`, and knew that I had to include `start` in my query  
For now, the query is: `http://34.40.82.22:32095/?start`

For the second block of code, I saw that no spaces are allowed in the query.  
For now, the query is: `http://34.40.82.22:32095/?start&secrets`

For the third block of code, I saw that the output from the `$value` variable is concatenating with `/usr/bin/find . ` command.  
And the last line of code shows that the output of the command can be read.  
To read contents of the secrets.php file, I used a command injection, in the secrets input field, I entered `;base64<secrets.php`, because cat and strings wouldn't work.  
And after entering the whole query (`http://34.40.82.22:32095/?start&secrets=;base64%3Csecrets.php`), I could see the index.php and secrets.php files, and also the contents of secrets.php, encoded in base64  

<img width="1092" height="46" alt="image" src="https://github.com/user-attachments/assets/ddc4cb9e-a02a-4dbd-b257-65c163ac23a2" />

And after using CyberChef to decode the strings, I could get the flag.

Flag: `CTF{3b2ceb0403300535fcd4808e8cbdb3cc3bd8f8b674527adce2915467f182faa4}`
