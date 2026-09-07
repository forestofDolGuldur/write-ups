silent-beacon  
Category: Network  

Description: The flag transmision had an insecure channel. Find it!  
Flag format: ctf{sha256}  

Link to the challenge: https://app.cyber-edu.co/challenges/9ea4a653-f197-4d6a-bc56-f508f3079157?tenant=unbreakable  

For this ctf, I had to extract a mp3 file from some packets with OBEX protocol.  

Firstly, I opened Wireshark to analyze the .pcap file, and after a little bit I found this packet, and then I knew I had to extract a mp3 file.  

<img width="1245" height="470" alt="image" src="https://github.com/user-attachments/assets/3767a238-530a-47db-b4e8-25ef6072052c" />

Now, I had to extract the data from all the packets with OBEX protocol, and 685 and 162 length, using TShark:  

```
tshark -r capture.pcap -Y "obex && (frame.len == 685 || frame.len == 162)" -T pdml > obex_data
```

Then I extracted the data from the value parameter.  

```
grep 'name="obex.header.value.byte_sequence"' obex.xml | sed -E 's/.*value="([^"]+)".*/\1/' > obex_values
```

Then I removed the newlines, and I remained only with the hex values.  

```
tr -d '\n' < obex_values > obex_last
```

After this I used xxd to make the file listenable.  

```
xxd -r -p obex_last extracted.mp3
```

Now the flag is listenable, but to make it easier, I put the mp3 file into an audio to text site.  

<img width="520" height="46" alt="image" src="https://github.com/user-attachments/assets/c86fc80b-1cfa-48bc-a927-937209ccd946" />

Flag: CTF{32faf5270d2ac7382047ac3864712cd8cb5b8999511a59a7c5cb5822e0805b91}
