Tomcat Takeover Lab  
Difficulty: Easy

Scenario: The SOC team has identified suspicious activity on a web server within the company's intranet. To better understand the situation, they have captured network traffic for analysis. The PCAP file may contain evidence of malicious activities that led to the compromise of the Apache Tomcat web server. Your task is to analyze the PCAP file to understand the scope of the attack.  

For this lab, I used Wireshark

**Q1: Given the suspicious activity detected on the web server, the PCAP file reveals a series of requests across various ports, indicating potential scanning behavior. Can you identify the source IP address responsible for initiating these requests on our server?**

For this question, I went to Statistics -> Conversation to see the IP which had the most packets.  

<img width="1338" height="212" alt="image" src="https://github.com/user-attachments/assets/de16bf80-3c4a-46ee-a196-b5072aec149a" />

Here, I found 14.0.0.120 as the IP which sent a lot of packets.  

Answer: `14.0.0.120`

**Q2: Based on the identified IP address associated with the attacker, can you identify the country from which the attacker's activities originated?**

For this question, I used ipshu.com, and searched up the IP, and found that the attacker is from China.

Answer: `China`

**Q3: From the PCAP file, multiple open ports were detected as a result of the attacker's active scan. Which of these ports provides access to the web server admin panel?**

By looking into TCP stream 2, I found in the HTTP header the port 8080.  

<img width="1272" height="974" alt="image" src="https://github.com/user-attachments/assets/72df0d31-1ec6-420f-a271-22bb1f577387" />

Answer: `8080`

**Q4: Following the discovery of open ports on our server, it appears that the attacker attempted to enumerate and uncover directories and files on our web server. Which tools can you identify from the analysis that assisted the attacker in this enumeration process?**

For this question, I searched in the Packet Bytes for User-Agent, and on TCP stream 9447 I found that the attacker was using gobuster.  

<img width="1268" height="999" alt="image" src="https://github.com/user-attachments/assets/3b19cdfa-04ce-4e93-9dfa-bce3606806fe" />

Answer: `gobuster`

**Q5: After enumerating directories on our web server, the attacker made numerous requests to identify administrative interfaces. Which directory related to the admin panel did the attacker uncover? (Provide the path including the leading slash, e.g. /path)**

After investigating more into TCP streams, on stream 9453 I found the path.  

<img width="1272" height="1006" alt="image" src="https://github.com/user-attachments/assets/a4ea1b7b-3fc1-4ddb-8e82-e4dfacf32ff4" />

Answer: `/manager`

**Q6: After accessing the admin panel, the attacker brute-forced the login. What credentials did the attacker successfully use? (Provide them in username:password format)**

After looking more into TCP streams, on stream 9460 I found a base64 encoded text in the HTTP header.  

<img width="1268" height="1001" alt="image" src="https://github.com/user-attachments/assets/52664185-52fd-42ee-b07e-4b45247a4141" />

After decoding it, I found the credentials

Answer: `admin:tomcat`

**Q7: Once inside the admin panel, the attacker attempted to upload a file with the intent of establishing a reverse shell. Can you identify the name of this malicious file from the captured data?**

On the same TCP stream, I could see a file named JXQOZY.war, and the zip archive attached.  

Answer: `JXQOZY.war`

**Q8: After the attacker established a reverse shell on our server, the payload connects back to the attacker's machine. From the analysis, what is the callback destination in IP:port format?**

On the next TCP stream, I found the Linux commands that were ran and captured.  

<img width="1273" height="1008" alt="image" src="https://github.com/user-attachments/assets/4c048aea-24f4-40b0-b5c6-49d012b41d76" />

Answer: `14.0.0.120:443`
