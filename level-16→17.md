<p align="center">
<a href="level-15→16.md">Previous Level: Level 15 → 16</a>
</p>

# [Bandit Level 16 → 17](https://overthewire.org/wargames/bandit/bandit17.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit16`
- **Password:** `kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx`

---

## Task 
The goal of this level is to send the current level’s password to **localhost** on a port between **31000-32000**, more specifically, a port that has a server listening on them and uses SSL/TLS.


## Steps
First we should scan the port ranges using `nmap`(network mapper).  
`nmap` probes IP ranges and ports to determine, what services and versions are running, it can also do basic OS/service fingerprinting.

Let's use the following nmap command (might take awhile to finish):
```bash
bandit16@bandit:~$ nmap -sV 127.0.0.1 -p 31000-32000
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-09-17 03:32 UTC
Stats: 0:01:57 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 80.00% done; ETC: 03:34 (0:00:29 remaining)
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00021s latency).
Not shown: 996 closed tcp ports (conn-refused)
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
31691/tcp open  echo
31790/tcp open  ssl/unknown
31960/tcp open  echo
Nmap done: 1 IP address (1 host up) scanned in 163.09 seconds
```
There are a few open ports, but we only need to focus on those offering SSL/TLS. That narrows it down to ports **31518** and **31790**.  
Port **31518** is running the echo service, which simply returns whatever data is sent to it.  
Port **31790** is running an unknown service, making it a more interesting target to investigate.  

Let's try connect to it as we've done in [level 15 → 16](level-15→16.md), and submit the password:
```bash
bandit16@bandit:~$ openssl s_client -connect localhost:31790              
CONNECTED(00000003)
...
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
KEYUPDATE
```
We are faced with this **KEYUPDATE** message, which we are hinted to look at the "CONNECTED COMMANDS" section in the `openssl` manpage.  

```text
CONNECTED COMMANDS¶

If a connection is established with an SSL server then any data received from the server is
displayed and any key presses will be sent to the server. If end of file is reached then the
connection will be closed down. When used interactively (which means neither -quiet nor
-ign_eof have been given), then certain commands are also recognized which perform special
operations. These commands are a letter which must appear at the start of a line.
They are listed below.

    Q

    End the current SSL connection and exit.

    R

    Renegotiate the SSL session (TLSv1.2 and below only).

    k

    Send a key update message to the server (TLSv1.3 only)

    K

    Send a key update message to the server and request one back (TLSv1.3 only)
```

Since the password to the current level so happens to begin with a `k`, the SSL server thinks we are issuing a special **KEYUPDATE** command. To handle this, we should use the `-quiet` option which will omit a lot of the details about the SSL handshake, certificates and session info.
It only shows the actual input/output stream from the connection.  

Let's to connect again with `-quiet` and submit the password:
```bash
bandit16@bandit:~$ openssl s_client -connect localhost:31790 -quiet
...
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
Correct!
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----
```

## Flag
```bash
n/a: RSA PRIVATE KEY given.
```

## Notes
`nmap` is a network scanning tool used to discover hosts, open ports and running services on a network. For this particular level we leveraged the `-sV` option which tells nmap to perform service version detection, meaning it tries to determine what software and version is running on each open port, and `-p` which lets us specify which port(s) to scan.


<p align="center">
<a href="level-17→18.md">Next Level: Level 17 → 18</a>
</p>


