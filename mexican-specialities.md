mexican-specialties  
Category: Forensics/Steganography  

Description: A friend from Mexico sent me the attached picture on Telegram. What does it mean?  
Flag is not in a standard format.  

Link to the challenge: https://app.cyber-edu.co/challenges/98d79d6d-3f06-4831-a073-fa49e8ad7f01?tenant=unbreakable

For this ctf, I've got an image, with some numbers.  
<img width="644" height="158" alt="image" src="https://github.com/user-attachments/assets/eeaffd5d-9e57-4079-a222-f0e118b8cac9" />

Firstly I've used binwalk to see if there are any hidden files, and there were some files.  

<img width="1010" height="187" alt="image" src="https://github.com/user-attachments/assets/4b857446-a0b4-4127-a891-f981ecb2a017" />

I've extracted them using `binwalk -e mexican_specialities.jpg` and looking in the output folder, there was an image file named `wheel.png`.  

<img width="1080" height="1118" alt="image" src="https://github.com/user-attachments/assets/37cb84db-b42b-4762-8d37-7915ede5efcf" />  

And what I had to do, is to decipher those numbers 2 by 2 from the original picture into the flag.  

Flag: `SISENIORILOVETACOBELLVERYVERYMUCH`
