AndroidBreach Lab  
Difficulty: Medium  

Scenario: At BrightWave Company, a data breach occurred due to an employee's lack of security awareness, compromising his credentials. The attacker used these credentials to gain unauthorized access to the system and exfiltrate sensitive data. During the investigation, the employee revealed two critical points: first, he stores all his credentials in the notes app on his phone, and second, he frequently downloads APK files from untrusted sources. Your task is to analyze the provided Android dump, identify the malware downloaded, and determine its exact functionality.  

This lab has a Windows 10 virtual machine, with many forensic tools, 

**Q1: What suspicious link was used to download the malicious APK from your initial investigation?**

After using aleappGUI.exe, I went into the web interface, and to "Chrome - Downloads-01", where I found the link.  

<img width="1598" height="495" alt="image" src="https://github.com/user-attachments/assets/4b2ffd0e-523a-40aa-a314-0ba172eb14a1" />

Answer: `https://ufile.io/57rdyncx`

**Q2: What is the name of the downloaded APK?**

For this question, I went to data/media/0/Downloads, to find the actual file which was downloaded.  

<img width="773" height="485" alt="image" src="https://github.com/user-attachments/assets/0da39087-91a7-4b72-a43d-2da03326e31e" />

Answer: `Discord_nitro_Mod.apk`

**Q3: What is the malicious package name found in the APK?**

After finding the apk file, I pasted it in jadx GUI and looked for the package name in AndroidManifest.xml, and found the name right there.  

<img width="971" height="607" alt="image" src="https://github.com/user-attachments/assets/249f183c-0806-4e63-8a16-cd3d69d2a88e" />

Answer: `com.example.keylogger`

**Q4: Which port was used to exfiltrate the data?**

After searching for a little bit, I found this SendEmail class, and also the port.  

<img width="1291" height="640" alt="image" src="https://github.com/user-attachments/assets/df667b77-67ce-4772-8fee-cfaf6dc2f9ce" />

Andwer: `465`

**Q5: What is the service platform name the attacker utilized to receive the data being exfiltrated?**

The line above the one with the port, is the name of the platform that attacker used.  

Answer: `mailtrap.io`

**Q6: What email was used by the attacker when exfiltrating data?**

For this question, I had to see which other class used the SendEmail class.  
I found that the BroadcastForAlarm uses SendEmail, with the email sent as parameter in plain text.

<img width="851" height="324" alt="image" src="https://github.com/user-attachments/assets/db6da476-8ff5-4008-9374-a3b1b9f665d2" />

Answer: `APThreat@gmail.com`

**Q7: The attacker has saved a file containing leaked company credentials before attempting to exfiltrate it. Based on the data, can you retrieve the credentials found in the leak?**

I saw that there was a file saved with the leaked information, as seen in the picture above.  
After searching the config.txt file in File Explorer, I opened it and found leaked information including the credentials.  

<img width="298" height="76" alt="image" src="https://github.com/user-attachments/assets/6320629c-1806-4e6d-9520-92fc32aa5710" />


Answer: `hany.tarek@brightwave.com:HTarek@9711$QTPO309`

**Q8: The malware altered images stored on the Android phone by encrypting them. What is the encryption key used by the malware to encrypt these images?**

I found a class named AESUtils, and the encrypt function.

<img width="608" height="277" alt="image" src="https://github.com/user-attachments/assets/4d473caf-b197-47ed-b880-40e797fce122" />

After I found that the encrypt function was used in another class, the key was encoded in base64.

<img width="871" height="374" alt="image" src="https://github.com/user-attachments/assets/184d9cc9-ac6e-41cd-98b5-19fe112e7802" />

After decoding it in CyberChef, I could get the key.

Answer: `9bY$wQ7!cTz465TX`

**Q9: The employee stored sensitive data in their phone's gallery, including credit card information. What is the CVC of the credit card stored?**

In data/media/0/Pictures I found 2 pictures, which didn't work, but in .aux folder, I found another picture, which I could open, and luckily it had the CVC there.

<img width="1890" height="657" alt="image" src="https://github.com/user-attachments/assets/253b0104-1751-441a-9402-29a8fd9cfe93" />

Answer: `128`
