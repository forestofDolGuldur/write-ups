log-analysis 2  
by Volf

Descirption: We know for sure that an attacker used malicious binaries and scripts in order to compromise the host. Our specialists collected the artifacts using different open-source tools. Using your favorite text editor or Terminal commands please help us find answers to the following questions.

link to the challenge: https://app.cyber-edu.co/challenges/98d79d7c-4827-4d34-a68f-e1090b2e92f7?tenant=unbreakable

**Q1. Which is the machine id of the compromised host?**

For this challenge, we have multiple files and directories with bunch of different logs/command output:

`$ ls -l `
  
`drwxrwxr-x  2 kali kali   4096 Jun 26 09:47  bodyfile`  
`drwxrwxr-x  2 kali kali   4096 Jun 26 10:56  chkrootkit`  
`drwxrwxr-x  2 kali kali   4096 Jun 26 10:07  hash_executables`  
`drwxrwxr-x 10 kali kali   4096 Jun 26 09:47  live_response`  
`drwxrwxr-x 10 kali kali   4096 Jun 26 09:47 '[root]'`  
`-rw-r--r--  1 kali kali 576284 May 13  2022  uac.log`  
`-rw-r--r--  1 kali kali   2194 May 13  2022  uac.log.stderr`  

For this question, we can use 2 methods to get the answer:

1) Using grep through all files

For this method we gotta use this command: `$ find . -type f -exec strings {} + | grep -i 'machine'`.  
This command goes through all the files, and highlights the word 'machine', and the -i option is making sure that we highlight the word without case sensitivity.  
We get a lot of output, but we can see more lines like this: `_MACHINE_ID=8d200bff9e814d47830905ed77e21306`, where we can see that the machine id is 8d200bff9e814d47830905ed77e21306

Answer: `8d200bff9e814d47830905ed77e21306`

2) Finding files which contains the machine id

For this methon, we gotta use this command: `$ find . -type f -name "*machine*"`.  
This command finds all the files which names contains the word "machine". If we run this command, we get this line `./[root]/etc/machine-id`.  
If we open it, we get: `8d200bff9e814d47830905ed77e21306`

Answer: `8d200bff9e814d47830905ed77e21306`

**Q2. What is the name of the scheduled task created by the attacker on the compromised machine?**

For this question, we have to go to find the crontabs directory, and to read the name of the scheduled task.   
`$ cd \[root\]/var/spool/cron/crontabs`  
`$ ls -l`  
`-rw------- 1 kali kali 1111 May 13  2022 bitsentinel`  
`-rw------- 1 kali kali 1115 May 13  2022 root`  

Here, we have to read any of the 2 files, and we see this specific line: `0 5 * * 1 tar -zcf /home/bitsentinel/Desktop/1337kit/qSCYApUBSJH7y6Ww.ko`, and there we see the name of the task.

Answer: `qSCYApUBSJH7y6Ww.ko`


**Q3. Which antivirus is used by the compromised computer?**

For this question, we have to look into the live_response directory

`$ cd live_response`  
`$ ls -l`  
`drwxrwxr-x 2 kali kali 4096 Jun 26 09:47 containers`  
`drwxrwxr-x 2 kali kali 4096 Jun 26 09:47 hardware`  
`drwxrwxr-x 2 kali kali 4096 Jun 26 09:47 network`  
`drwxrwxr-x 2 kali kali 4096 Jun 26 09:47 packages`  
`drwxrwxr-x 3 kali kali 4096 Jun 26 09:47 process`  
`drwxrwxr-x 2 kali kali 4096 Jun 26 09:47 storage`  
`drwxrwxr-x 2 kali kali 4096 Jun 26 09:47 system`  
`drwxrwxr-x 2 kali kali 4096 Jun 26 09:47 vms`  

This directory shows us output from different commands, like uname -a, ps -ef, etc...

Firstly I went into the process directory, which had output from commands like ps -ef, pstree, lsof -nPl, and similar commands, to identify the antivirus. I was wrong, because the antivirus is working as a service, not process, and then I went into the system folder.

`$ cd system`  

Here are a lot of files, but the one we need is `service_--status-all.txt`, which is the output of the service --status-all command. When we open this text file, we see this specific line `[ + ]  clamav-freshclam` which shows what antivirus is used on this machine.

Answer: `clamav`


**Q4. Which is the latest command executed on the compromised machine?**

For this question, we have to go into the [root] directory, and we have to find the .bash_history file, which shows us what commands were used before.

`$ cd /\[root\]/home/bitsentinel`

`$ ls -la`
  
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


