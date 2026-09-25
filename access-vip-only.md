access-vip-only  
Category: Forensics  

Description: "We have a malicious employee who attempts to make other people join a secret club. The main message is “ come join us, we have a lot of money” . All we know is that he managed to look to something over the internet "  
Flag format: ctf{sha256}  

Link to the challenge: https://app.cyber-edu.co/challenges/f232c950-12b4-11eb-bf77-ed4a11422a38?tenant=cyberedu

For this challenge, I had to use volatility 2 to analyze a memory dump and extract some files in order to get the flag.  

Firstly I used `imageinfo` on volatility 2 to see which profile I should use for this memory dump.  

<img width="1244" height="218" alt="image" src="https://github.com/user-attachments/assets/380dcfa8-ca30-4884-a523-0cda7b33e9e9" />

After writing `--profile=Win7SP1x64` I could start using the commands.  
I used `--profile=Win7SP1x64 filescan | grep "Desktop"`, to see which files are on the desktop, because most of the relevant files are there.  

<img width="1260" height="515" alt="image" src="https://github.com/user-attachments/assets/02501dc0-99b2-408f-9adf-75f56b34fa03" />

Then I used `--profile=Win7SP1x64 dumpfiles --dump-dir=~/Desktop/accessvip -Q 0x000000007ee72200`, to extract the second `flag.ra` file. By the extension, I knew that this is actually a rar file.  
After I extracted the file, I renamed the file and used `file` to see if it's a valid rar file.  

<img width="258" height="40" alt="image" src="https://github.com/user-attachments/assets/c513473a-3409-455a-9353-c5a644a64771" />

I tried opening the archive, but it was password protected, and I used John to crack the password.  
I used `rar2john flag.rar > rarhash.txt` and `john --wordlist=/usr/share/wordlists/rockyou.txt rarhash.txt` to crack the password, and after a couple of seconds, I got the password.  

<img width="713" height="170" alt="image" src="https://github.com/user-attachments/assets/b30e0571-17e6-4dd5-806a-ba88a206442e" />

After unzipping the archive, I got the flag.  

Flag: `ctf{B8FA9EFBC8C8F043AFCA1B60F8F4C5245C54B5FF5BFB0603A71071F66C1EF295}`
