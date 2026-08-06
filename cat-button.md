cat-button   
Category: Web  


Description: Are you an admin?  
Flag format: CTF{sha265}  

Link to the challenge: https://app.cyber-edu.co/challenges/98d79d66-2f34-4cee-b1ff-9d338127eddf?tenant=unbreakable


For this ctf, we have to crack the cookie signature and modify it, to get the admin role and get the flag.


First time entering the site, we see this Nyan Cat page, with a button on the lower part of the screen
<img width="1920" height="958" alt="image" src="https://github.com/user-attachments/assets/b87ec23e-ffbb-4db3-a19d-d6281dfcd600" />

By pressing on the button, it redirects to another page, saying this  

<img width="326" height="48" alt="image" src="https://github.com/user-attachments/assets/11bab183-00cd-4929-a571-5f3c759e47d7" />

Now we clearly know that we have to modify the cookie to get the admin role.  
By pressing F12 and going to the Storage tab we see this cookie sitting there. 

<img width="993" height="207" alt="image" src="https://github.com/user-attachments/assets/31e8427f-1ff2-4ea9-b9dd-63da7d010a87" />

I copied it and went to jwt.io (CyberChef can also be used, because the cookie is encoded in base64) and paste the cookie

<img width="1343" height="731" alt="image" src="https://github.com/user-attachments/assets/301cded4-2807-4829-82da-63e5dd48bacd" />

We see the string 

``{``  
  ``"admin": false``  
``}``  

And we have to change it from false to true. But we need the signature.

To crack the signature, I used John. Firstly, i pasted the strings into a text file `echo -n 'eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZG1pbiI6ZmFsc2V9.k2RUNg6FlRlfDjQUAQmDzPLrzZL0_sarBgiWtNr4cpE' > cookie.txt
` and then I used this command `john --format=HMAC-SHA256 --wordlist=/usr/share/wordlists/rockyou.txt cookie.txt` to crack the signature

<img width="768" height="174" alt="image" src="https://github.com/user-attachments/assets/0327288e-72f4-46b9-a825-d95fb7c633b6" />

And as we see, we got the signature `secret`

Now we go back on jwt.io and modify the admin field from false to true, using the word secret as the signature

<img width="1331" height="748" alt="image" src="https://github.com/user-attachments/assets/71e0a9e6-31a8-422e-8d12-82444052d592" />

Now we replace the original cookie with our modified one and we get the flag

<img width="823" height="47" alt="image" src="https://github.com/user-attachments/assets/41f27577-5d12-4a94-9adf-d168a399b779" />

Flag: `CTF{98ed1dfbddd3510841cdeb99916a6a7534f224f5ae9841758708046540237987} `
