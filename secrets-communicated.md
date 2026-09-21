secrets-communicated  
Category: Forensics

Description: The #1 criminal on our Most Wanted List dropped their phone in an encounter with the police. We managed to dump the whole firmware of the phone. Your job is to find out what secrets are hidden in the phone and what did he send to his person of contact back home through an online chat service.  
Archive Password: Q3Cwi1T

For this ctf, I had to analyze an Android disk image by searching through Facebook databases and finding hidden files.

Firstly, I used `fdisk -l` on the image, to list the partition tables.  

<img width="451" height="904" alt="image" src="https://github.com/user-attachments/assets/fdef2685-ca6c-49b3-b52d-64d3dfdf77c7" />

The last table caught my eye, then I calculated the offset by doing $$4751360 * 512$$, which is $$2432696320$$.  

Now I used `sudo losetup -f -o 2432696320 this_is_it.img` and `losetup -a`, to see in which /dev/loop set up the image.  
Then I used `sudo mount /dev/loop7 temp_mount`.  

Then, after investigating for a little bit, I found in /media/0/Download a blank named file. I used `file *` to identify the file type.  

<img width="1018" height="39" alt="image" src="https://github.com/user-attachments/assets/eb4d0902-c419-43ff-a675-234ac19f0919" />

After discovering that it's a zip archive, I used `cp * temp_zip.zip` to make it easier to work with.  
I tried extracting but it required a password.  

After more time investigating, I found in /data/com.facebook.orca/databases a file named `threads_db2`, which is a SQLite 3 file.  
I opened it in https://sqliteviewer.app, and in Tabled -> messages, I found some interesting messages.  

<img width="1602" height="311" alt="image" src="https://github.com/user-attachments/assets/40eb293b-1973-4cb6-bc3c-109f063adc41" />

I tried the last message (the hash) as the password for the zip and it worked, and got the flag.

Flag: `HackTM{a1f6bb8b4f993e3fbea836b001339d5f2387043fe504ba290fbe9674de4a2a16}`
