log-analysis 2
by Volf

Descirption: We know for sure that an attacker used malicious binaries and scripts in order to compromise the host. Our specialists collected the artifacts using different open-source tools. Using your favorite text editor or Terminal commands please help us find answers to the following questions.

link to the challenge: https://app.cyber-edu.co/challenges/98d79d7c-4827-4d34-a68f-e1090b2e92f7?tenant=unbreakable

Q1.
Which is the machine id of the compromised host?

For this challenge, we have multiple files and directories with bunch of different logs/command output:

`$ ls -l 
total 588 
drwxrwxr-x  2 kali kali   4096 Jun 26 09:47  bodyfile
drwxrwxr-x  2 kali kali   4096 Jun 26 10:56  chkrootkit
drwxrwxr-x  2 kali kali   4096 Jun 26 10:07  hash_executables
drwxrwxr-x 10 kali kali   4096 Jun 26 09:47  live_response
drwxrwxr-x 10 kali kali   4096 Jun 26 09:47 '[root]'
-rw-r--r--  1 kali kali 576284 May 13  2022  uac.log
-rw-r--r--  1 kali kali   2194 May 13  2022  uac.log.stderr`

For this question, 




Q4.
Which is the latest command executed on the compromised machine?

For this question, we have to go into the [root] directory, and we have to find the .bash_history file, which shows us what commands were used before.

`$ cd /\[root\]/home/bitsentinel`

`$ ls -la`

`total 40`
`drwxrwxr-x 5 kali kali 4096 Jun 26 09:47 .`
`drwxrwxr-x 4 kali kali 4096 Jun 26 09:47 ..`
`-rw------- 1 kali kali 1744 May 12  2022 .bash_history`
`-rw-r--r-- 1 kali kali  220 Mar 14  2022 .bash_logout`
`-rw-r--r-- 1 kali kali 3771 Mar 14  2022 .bashrc`
`drwxrwxr-x 3 kali kali 4096 Jun 26 09:47 Desktop`
`drwxrwxr-x 3 kali kali 4096 Jun 26 09:47 .local`
`drwxrwxr-x 3 kali kali 4096 Jun 26 09:47 .mozilla`
`-rw-r--r-- 1 kali kali  807 Mar 14  2022 .profile`
`-rw------- 1 kali kali 2719 May 13  2022 .viminfo`

Here we see the .bash_history file, let's read it and see the latest command that was executed.
There are a lot of commands, but the one that we needed to find is `sudo reboot`
Answer: `sudo reboot`


