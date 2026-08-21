templates  
Category: Web  

Description: We need a developer to make a small debug on our application.  
Flag format: UNR{}  

Link to the challenge: https://app.cyber-edu.co/challenges/98d79d6f-4e15-4f3a-be6e-2a67db59cc37?tenant=unbreakable

For this ctf, I used dirsearch to search all the directories on the instance.

First time entering the site, it shows `Maintenance Mode On` and a blue square. After using `dirsearch -u 34.141.35.247:30410`, I've saw `/flag` endpoint

<img width="387" height="325" alt="image" src="https://github.com/user-attachments/assets/ceff9da4-3a36-4117-9f01-d961606c2733" />

And by entering `34.141.35.247:30410/flag`, I could see the flag right there.

Flag: `UNR{26ym3y-aqqqep-idhz4s-boxxwi-o5enrq-tpviyj-sp5wjw-dszds3}`
