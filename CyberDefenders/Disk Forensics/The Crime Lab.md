The Crime Lab  
Difficulty: Easy

For this lab, I used ALEAPP to analyze an Android disk, and to answer the 6 questions based on the information I had.

**Q1: Based on the accounts of the witnesses and individuals close to the victim, it has become clear that the victim was interested in trading. This has led him to invest all of his money and acquire debt. Can you identify the SHA256 of the trading application the victim primarily used on his phone?**  

For this question, I had to look on the `installedappsGass` page, and the only app which is related to crypto, is Olymptrade.  

<img width="1307" height="652" alt="image" src="https://github.com/user-attachments/assets/b0a1ea3e-9c12-4938-8c84-77b38c616dbe" />

Answer: `4f168a772350f283a1c49e78c1548d7c2c6c05106d8b9feb825fdc3466e9df3c`

**Q2: According to the testimony of the victim's best friend, he said, "While we were together, my friend got several calls he avoided. He said he owed the caller a lot of money but couldn't repay now". How much does the victim owe this person?**  

For this question, I had to look in SMS Messages or GoogleMessages tab, and there was a single message from +201172137258, which is actually the number which the victim ignored when he called.  

<img width="1066" height="774" alt="image" src="https://github.com/user-attachments/assets/4e160afb-6b78-4f32-b1d3-44c083300856" />

<img width="961" height="686" alt="image" src="https://github.com/user-attachments/assets/d752a925-9440-48e2-ab3e-94e1acff8fea" />  

Answer: `250000`

**Q3: What is the name of the person to whom the victim owes money?**  

Here I looked into contacts, to see if the victim has the numbers in contacts, also with the name.  
And +201172137258 is the phone number the victim was receiving calls from and avoiding them.   

<img width="1420" height="678" alt="image" src="https://github.com/user-attachments/assets/f94a3ba0-ad0d-4173-9626-0d07e9db7a3d" />

Answer: `Shady Wahab`

**Q4: Based on the statement from the victim's family, they said that on September 20, 2023, he departed from his residence without informing anyone of his destination. Where was the victim located at that moment?**

In Recent Activity tab, I found this screenshot from Google Maps, containing the location the victim was at that moment.  

<img width="1491" height="397" alt="image" src="https://github.com/user-attachments/assets/5cd1f495-95ac-4140-a62f-e91a020a1307" />

<img width="374" height="814" alt="image" src="https://github.com/user-attachments/assets/a75fa204-d2cd-41f3-8e94-32cea282491d" />

Answer: `The Nile Ritz-Carlton`  

**Q5: The detective continued his investigation by questioning the hotel lobby. She informed him that the victim had reserved the room for 10 days and had a flight scheduled thereafter. The investigator believes that the victim may have stored his ticket information on his phone. Look for where the victim intended to travel.**  

In the Google Photos tab, I could see a plane ticket picture, with the destination to Las Vegas.  

<img width="1574" height="673" alt="image" src="https://github.com/user-attachments/assets/b10b6cbb-d710-449b-9ea7-743a625b6667" />

<img width="1920" height="618" alt="image" src="https://github.com/user-attachments/assets/e171aabb-21a4-45ea-8070-796726edd252" />

Answer: `Las Vegas`

**Q6: After examining the victim's Discord conversations, we discovered he had arranged to meet a friend at a specific location. Can you determine where this meeting was supposed to occur?**  

By going to the discordChats tab, I saw the second message, containing the location.  

<img width="1203" height="377" alt="image" src="https://github.com/user-attachments/assets/b20fea6e-a81e-4e0b-a316-e4b721630b82" />

Answer: `The Mob Museum`
