malicious-workflow  
Category: Forensics  

Description: “Jack is a pro with consoles, all kinds of consoles. He managed to multiply a secret file from his workplace. Could you please see what it is about, we have extracted this file from his PC?”  
Flag format: ctf{sha256}  

Link to the challenge: https://app.cyber-edu.co/challenges/9b390d69-ddaf-47aa-ac7c-ba3f6ca78c79?tenant=rocsc  

For this ctf, I had to use volatility 3 to extract the file containing the flag.  

Firstly, I used `windows.info` to see if the memory dump was taken from a Windows machine.  

<img width="1082" height="433" alt="image" src="https://github.com/user-attachments/assets/e00a4beb-7e2f-4239-a3f9-a8e14aeda117" />  

From this output, we see that the memory dump was taken from a Windows 7 machine.  

Now, knowing that the memory dump is a Windows one, I used `windows.filescan | grep -i "flag"`, to see if there is a file named flag.  

<img width="635" height="76" alt="image" src="https://github.com/user-attachments/assets/aad3908a-31bc-4348-bb7d-d9f9ff4499d3" />

And here I saw the flag.txt file. I extracted it using `-o flag windows.dumpfiles --physaddr 0x7fb16070`, to extract the content of the file into the flag directory.  

After using cat on the extracted file, I could get the flag.  

<img width="582" height="77" alt="image" src="https://github.com/user-attachments/assets/4967b416-9f3b-4ae8-9d28-9c16352b750c" />

Flag: `ctf{FBAE5EBCAA81F0983F0D2806A98239AACF040E2AABEDCD1E910234F7237D03F2}`
