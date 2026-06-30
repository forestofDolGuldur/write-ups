foreign-program  
by Antonio-Dan Macovei
Category: Forensics

Description: We need you to help us find the treasures inside this file.

link to the challenge: https://app.cyber-edu.co/challenges/98d79d7e-62e1-410f-9b05-d9ce0fb73dca?tenant=unbreakable

In this ctf, we have a memory dump file, named foreign-program.dmp. The tools that I use are Volatiliy 2 and 3

**Q1. What is the name of the base operating system?Format flag: lowercase,no space**

For this question, We can use 2 methods:

1) Using strings and grep on the .dmp file.

Here we just use the command `$ strings foreign-program.dmp | grep -i 'windows'`, and we clearly see that the memory dump is taken from a windows machine.  
To find the exact Windows operating system we can use `$ strings foreign-program.dmp | grep -iE 'windows7|windows8|windows10'`.  
One of the lines that specify the OS is `C:\Windows10Upgrade\Windows10UpgraderApp.exe`, and now we clearly know that the memory dump was taken from a Windows 10 machine

2) Using Volatility

For this method, we run this command `$ vol -f ~/Desktop/foreign-program.dmp windows.info`.    
<img width="724" height="432" alt="image" src="https://github.com/user-attachments/assets/699110ce-f99c-44c8-b534-96d0a8dbc7dd" />

Here we see clearly that the machine was running Windows 10, from the `NtMajorVersion  10` line.

Answer: `windows10`

**Q2. The image contains evidence of running a special program (we'll call it program X). What is the name of this process? (Hint: it's not a default program)**

For this question we have to look up the processes that were running on the machine.  
For this one, we have to use `$ vol -f ~/Desktop/foreign-program.dmp windows.cmdline`.  
By carefully analyzing the output, we can see this line with the unusual program  
`5260    ubuntu2004.exe  "C:\Program Files\WindowsApps\CanonicalGroupLimited.Ubuntu20.04onWindows_2004.2022.8.0_x64__79rhkp1fndgsc\ubuntu2004.exe"`  

Answer: `ubuntu2004.exe`

**Q3. A file with an interesting extension was created and opened on the system. We must find its name inside the memory dump.**

The question tells us that the file was created and **opened**, that means that we have to use the same command above and see check notepad or photo/video/audio apps. 
This line: `1748    notepad.exe     "C:\Windows\system32\NOTEPAD.EXE" C:\Users\os3\Desktop\fietsteksthost.txt.txt` tells us exactly the name and the extension of the file.

Answer: `fietsteksthost.txt.txt`

**Q4. What is the PID of the process containing the memory of program X?**

For this question we have to know that WSL uses Dynamic Memory Allocation and the memory is stored in another process, named vmmem.
By looking from the same output, we see this line: `6568    vmmem   -`, and the PID of the proccess containing the memory of the program.

Answer: `6568`

**Q5. What is the IP address of the host?**

For this question, we have to use this command: `$ vol -f ~/Desktop/foreign-program.dmp windows.netscan` and check the machine's ip from the LocalAddr category.  

Answer: `192.168.122.80`

**Q6. What is the name of the PDF file hidden inside program X?**

For this question, we have to use this command: `$ vol -f ~/Desktop/foreign-program.dmp windows.filescan | grep ".pdf"`.  
After using the command we see this line: `0xe20aeef98610.0\Users\os3\Desktop\fietspapierhost.pdf`, and the .pdf file that was hidden inside the program.

Answer: `fietspapierhost.pdf`





