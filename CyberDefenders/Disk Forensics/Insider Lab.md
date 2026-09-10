Insider Lab  
Difficulty: Easy

Scenario: After Karen started working for 'TAAUSAI,' she began doing illegal activities inside the company. 'TAAUSAI' hired you as a soc analyst to kick off an investigation on this case.  
You acquired a disk image and found that Karen uses Linux OS on her machine. Analyze the disk image of Karen's computer and answer the provided questions.  

For this lab, I had to use FTK Imager to analyze an GNU/Linux disk.

**Q1: Which Linux distribution is being used on this machine?**

I extracted /var/log/user.log, and used cat and grep -i "linux", to see the Linux distro that Karen used.  

Answer: `Kali`

**Q2: What is the MD5 hash of the Apache access.log file?**

I extracted /var/log/apache2/access.log, and used md5sum command to get the hash.  

Answer: `d41d8cd98f00b204e9800998ecf8427e`

**Q3: It is suspected that a credential dumping tool was downloaded. What is the name of the downloaded file?**

I went into /root/Downloads and found mimikatz_trunk.zip.  

Answer: `mimikatz_trunk.zip`

**Q4: A super-secret file was created. What is the absolute path to this file?**

I couldn't find the super-secret file, I looked a little bit into .bash_history, and there I could find the secret file.

Answer: `/root/Desktop/SuperSecretFile.txt`

**Q5: What program used the file didyouthinkwedmakeiteasy.jpg during its execution?**

By looking into the .bash_history file, I could see the the program used.

Answer: `binwalk`

**Q6: What is the third goal from the checklist Karen created?**

By extracting the /root/Desktop/Checklist file, I could find the goal.

Answer: `Profit`

**Q7: How many times was Apache run?**

By looking into /root/var/log/apache2, all the files are empty, so that means that Apache didn't run.

Answer: `0`

**Q8: This machine was used to launch an attack on another. Which file contains the evidence for this?**

In /root/Desktop, I found irZLAohL.jpeg, which contains the evidence.  

Answer: `irZLAohL.jpeg`

**Q9: It is believed that Karen was taunting a fellow computer expert through a bash script within the Documents directory. Who was the expert that Karen was taunting?**  

In /root/Documents/firstscript_fixed, I found this line: echo "Heck yeah! I can write bash too Young".  

Answer: `Young`

**Q10: A user executed the su command to gain root access multiple times at 11:26. Who was the user?**  

For this question, I looked into /var/log/auth.log, and used grep -i "su", and found that the user is "postgres".  

Answer: `postgres`

**Q11: Based on the bash history, what is the current working directory?**

By analyzing .bash_history and the last cd commands, I could see the current working directory.  

Answer: `/root/Documents/myfirsthack/`
