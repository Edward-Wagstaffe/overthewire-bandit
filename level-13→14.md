<p align="center">
<a href="level-12→13.md">Previous Level: Level 12 → 13</a>
</p>

# [Bandit Level 13 → 14](https://overthewire.org/wargames/bandit/bandit14.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit13`
- **Password:** `FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn`

---

## Task 
The goal of this level is to **use the given private key** to log into bandit14.  

The password for the next level ([level 14 → 15](level-14→15.md)) is found in **/etc/bandit_pass/bandit14** and can only be read by user **bandit14**.


## Steps    
Let's find out what the file is called and print the contents:
```bash
bandit13@bandit:~$ ls                                         
sshkey.private
bandit13@bandit:~$ cat sshkey.private                               
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAxkkOE83W2cOT7IWhFc9aPaaQmQDdgzuXCv+ppZHa++buSkN+
gg0tcr7Fw8NLGa5+Uzec2rEg0WmeevB13AIoYp0MZyETq46t+jk9puNwZwIt9XgB
ZufGtZEwWbFWw/vVLNwOXBe4UWStGRWzgPpEeSv5Tb1VjLZIBdGphTIK22Amz6Zb
ThMsiMnyJafEwJ/T8PQO3myS91vUHEuoOMAzoUID4kN0MEZ3+XahyK0HJVq68KsV
ObefXG1vvA3GAJ29kxJaqvRfgYnqZryWN7w3CHjNU4c/2Jkp+n8L0SnxaNA+WYA7
jiPyTF0is8uzMlYQ4l1Lzh/8/MpvhCQF8r22dwIDAQABAoIBAQC6dWBjhyEOzjeA
J3j/RWmap9M5zfJ/wb2bfidNpwbB8rsJ4sZIDZQ7XuIh4LfygoAQSS+bBw3RXvzE
pvJt3SmU8hIDuLsCjL1VnBY5pY7Bju8g8aR/3FyjyNAqx/TLfzlLYfOu7i9Jet67
xAh0tONG/u8FB5I3LAI2Vp6OviwvdWeC4nOxCthldpuPKNLA8rmMMVRTKQ+7T2VS
nXmwYckKUcUgzoVSpiNZaS0zUDypdpy2+tRH3MQa5kqN1YKjvF8RC47woOYCktsD
o3FFpGNFec9Taa3Msy+DfQQhHKZFKIL3bJDONtmrVvtYK40/yeU4aZ/HA2DQzwhe
ol1AfiEhAoGBAOnVjosBkm7sblK+n4IEwPxs8sOmhPnTDUy5WGrpSCrXOmsVIBUf
laL3ZGLx3xCIwtCnEucB9DvN2HZkupc/h6hTKUYLqXuyLD8njTrbRhLgbC9QrKrS
M1F2fSTxVqPtZDlDMwjNR04xHA/fKh8bXXyTMqOHNJTHHNhbh3McdURjAoGBANkU
1hqfnw7+aXncJ9bjysr1ZWbqOE5Nd8AFgfwaKuGTTVX2NsUQnCMWdOp+wFak40JH
PKWkJNdBG+ex0H9JNQsTK3X5PBMAS8AfX0GrKeuwKWA6erytVTqjOfLYcdp5+z9s
8DtVCxDuVsM+i4X8UqIGOlvGbtKEVokHPFXP1q/dAoGAcHg5YX7WEehCgCYTzpO+
xysX8ScM2qS6xuZ3MqUWAxUWkh7NGZvhe0sGy9iOdANzwKw7mUUFViaCMR/t54W1
GC83sOs3D7n5Mj8x3NdO8xFit7dT9a245TvaoYQ7KgmqpSg/ScKCw4c3eiLava+J
3btnJeSIU+8ZXq9XjPRpKwUCgYA7z6LiOQKxNeXH3qHXcnHok855maUj5fJNpPbY
iDkyZ8ySF8GlcFsky8Yw6fWCqfG3zDrohJ5l9JmEsBh7SadkwsZhvecQcS9t4vby
9/8X4jS0P8ibfcKS4nBP+dT81kkkg5Z5MohXBORA7VWx+ACohcDEkprsQ+w32xeD
qT1EvQKBgQDKm8ws2ByvSUVs9GjTilCajFqLJ0eVYzRPaY6f++Gv/UVfAPV4c+S0
kAWpXbv5tbkkzbS0eaLPTKgLzavXtQoTtKwrjpolHKIHUz6Wu+n4abfAIRFubOdN
/+aLoRQ0yBDRbdXMsZN/jvY44eM+xRLdRVyMmdPtP8belRi2E2aEzA==
-----END RSA PRIVATE KEY-----
```

Now we could just copy and paste this private key onto our machine but let's use `scp`(secure copy) instead because it securely transfers files **exactly as they are**, including binary data, without corruption or manual errors.

Logout of bandit13:
```bash
bandit13@bandit:~$ exit
logout
Connection to bandit.labs.overthewire.org closed.
```

On our local machine, let's use secure copy to copy the private key:
```bash
scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .

                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-0
bandit13@bandit.labs.overthewire.org's password: 
sshkey.private                             100% 1679     2.9KB/s   00:00
```
Now that we have the key on our local machine, let's try to login to bandit 14.
```bash
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-0
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0640 for 'sshkey.private' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "sshkey.private": bad permissions
```

We actually get an error because `ssh` is very picky about private key permissions.

Every file/directory has 3 permission sets:
- **Owner**: the user who owns the file
- **Group**: users in the file's group
- **Others**: everyone else

The permissions are:
- **r**(read): view contents
- **w**(write): modify/delete
- **x**(execute): run files or enter directories

Its represented as symbols, for example: `-rw-r--r--`
- The first char `-` means file, if it was `d` that means directory.
- Owner: `rw-`, Group: `r--`, Others: `r--`

This can also be represented as numbers where `r=4, w=2 and x=1` we add them up.  
e.g. `rw-` = 6, `r--` = 4, therefore `-rw-r--r--` is the same as `644`.


Back to our error from above, more specifically this part: `Permissions 0640 for 'sshkey.private' are too open.`  
The first `0` is a convention to show that this number is **octal**.  
The `640` represent the permission settings for `sshkey.private`, which means:
- Owner: read & write
- Group: read only
- Others: no access

Private keys for `ssh` are required to be `600`, that is, only the owner can read & write.  

Let's use the `chmod` command to change `sshkey.private` permissions:
```bash
chmod 600 sshkey.private
ls -l
total 4
-rw------- 1 you you 1679 Sep 15 13:31 sshkey.private
```
Then try logging into bandit14:
```bash
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```
Success!  

As logging into bandit14 is the sole objective of this level, we have successfully finished it.

## Notes
- **File permissions** define which users (owner, group, others) can read, write, or execute a file/directory.
- **SSH private keys** must be kept secret and readable only by their owner to be useable for authentication.
- The `chmod` command is used to change a file/directory's permissions.




<p align="center">
<a href="level-14→15.md">Next Level: Level 14 → 15</a>
</p>


