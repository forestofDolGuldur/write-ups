AGoodOne  
Category: Reverse Engineering  

Description: One would simply want to be with the rest.  
NOTE: The format of the flag is CTF{}, for example: CTF{foobar}. The flag must be submitted in full, including the CTF and curly bracket parts.  

Link to the challenge: https://app.cyber-edu.co/challenges/98d79d69-d472-46ae-8900-230c472fa2ff?tenant=unbreakable  

For this the I had to analyze a binary, to understand how the flag was encrypted and how to get the flag back.  

Firstly, I used strings to do some recon on the binary, and I could see some strings there including enc_flag, Correct Password!, and >#&v$qt$prr##tur}s$w#!'#&$!t} #qr $r}!qws$qr!u|r$q| v}uv#r |&u |s8.    

<img width="575" height="617" alt="image" src="https://github.com/user-attachments/assets/56dd5691-3516-42c7-ba0f-54823c2777f9" />  

I tried running the binary and pasted random numbers, to see if I get something useful, and I kinda saw a pattern there.  

<img width="317" height="485" alt="image" src="https://github.com/user-attachments/assets/78e79a59-a5c3-4fef-bc45-a6c56320e4d8" />            

<br>

<img width="405" height="582" alt="image" src="https://github.com/user-attachments/assets/88beeb8b-f327-4435-b851-cbfac1c14220" />  

After decompiling (and after renaming some variables), in this main function, I saw that I couldn't have more than 2 arguments, and if the return value of check_password() is True, it puts a strings from up there.  

<img width="448" height="375" alt="image" src="https://github.com/user-attachments/assets/208845e9-ddf1-4630-a301-e2a1248a2e71" />

This function has a for loop, from i=0 to the length of the argument, incrementing by 1. The password is stored in cVar1. For sVar2, I had to check enc_flag, which is an array in the .rodata section, containing the encrypted flag. also sVar2 stored the length of that array.  

```
                             DAT_00102008                                    XREF[2]:     check_password:00101323(*), 
                                                                                          001043e0(*)  
        00102008 06              ??         06h
        00102009 11              ??         11h
        0010200a 03              ??         03h
        0010200b 3e              ??         3Eh    >
        0010200c 23              ??         23h    #
        0010200d 26              ??         26h    &
        0010200e 76              ??         76h    v
        0010200f 24              ??         24h    $
        00102010 71              ??         71h    q
        00102011 74              ??         74h    t
        00102012 24              ??         24h    $
        00102013 70              ??         70h    p
        00102014 72              ??         72h    r
        00102015 72              ??         72h    r
        00102016 23              ??         23h    #
        00102017 23              ??         23h    #
        00102018 74              ??         74h    t
        00102019 75              ??         75h    u
        0010201a 72              ??         72h    r
        0010201b 7d              ??         7Dh    }
        0010201c 73              ??         73h    s
        0010201d 24              ??         24h    $
        0010201e 77              ??         77h    w
        0010201f 23              ??         23h    #
        00102020 21              ??         21h    !
        00102021 27              ??         27h    '
        00102022 23              ??         23h    #
        00102023 26              ??         26h    &
        00102024 24              ??         24h    $
        00102025 21              ??         21h    !
        00102026 74              ??         74h    t
        00102027 7d              ??         7Dh    }
        00102028 20              ??         20h     
        00102029 23              ??         23h    #
        0010202a 71              ??         71h    q
        0010202b 72              ??         72h    r
        0010202c 20              ??         20h     
        0010202d 24              ??         24h    $
        0010202e 72              ??         72h    r
        0010202f 7d              ??         7Dh    }
        00102030 21              ??         21h    !
        00102031 71              ??         71h    q
        00102032 77              ??         77h    w
        00102033 73              ??         73h    s
        00102034 24              ??         24h    $
        00102035 71              ??         71h    q
        00102036 72              ??         72h    r
        00102037 21              ??         21h    !
        00102038 75              ??         75h    u
        00102039 7c              ??         7Ch    |
        0010203a 72              ??         72h    r
        0010203b 24              ??         24h    $
        0010203c 71              ??         71h    q
        0010203d 7c              ??         7Ch    |
        0010203e 20              ??         20h     
        0010203f 76              ??         76h    v
        00102040 7d              ??         7Dh    }
        00102041 75              ??         75h    u
        00102042 76              ??         76h    v
        00102043 23              ??         23h    #
        00102044 72              ??         72h    r
        00102045 20              ??         20h     
        00102046 7c              ??         7Ch    |
        00102047 26              ??         26h    &
        00102048 75              ??         75h    u
        00102049 20              ??         20h     
        0010204a 7c              ??         7Ch    |
        0010204b 73              ??         73h    s
        0010204c 38              ??         38h    8
        0010204d 00              ??         00h
```

And for the result variable, result is already 0, and it ORs with $sVar2 \oplus cVar1 \oplus len$  

for the right part:  
$sVar2 \oplus len = temp-Var$  
$temp-Var \oplus cVar1 = final-value$  
And $final-value$ has to be 0, because 0 OR 0 = 0, and the result must remain 0.  
By entering 1 as the argument, I got 117117. 1 in decimal is 49, so: $cVar1 \oplus 49 = 117 => cVar1 = 68$, which is D in decimal. I tried entering D, and got this:  

<img width="233" height="79" alt="image" src="https://github.com/user-attachments/assets/a4de3a24-2e31-4f74-a030-06a74488781f" />

I tried xoring with 68 in decimal but it wouldn't work, but I tried with 69 which is the length of the string, and I got the flag

<img width="1273" height="585" alt="image" src="https://github.com/user-attachments/assets/01d8ffce-d06d-44ba-b22a-a27b51757195" />

Now the last thing I had to do is to put CTF in front of it, and submit the flag.

Flag: CTF{fc3a41a577ff10786a2fdbfcad18ef47ea78d426a47d097a49e3803f7e9c0e96}
