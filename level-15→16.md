<p align="center">
<a href="level-14→15.md">Previous Level: Level 14 → 15</a>
</p>

# [Bandit Level 15 → 16](https://overthewire.org/wargames/bandit/bandit16.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit15`
- **Password:** `8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo`

---

## Task 
The goal of this level is to send the current level’s password to **localhost** on **port 30001** over an **SSL/TLS-encrypted connection**.


## Steps
`openssl` is a toolkit for encryption, key and certificate management, hashing, and testing SSL/TLS connections.  

In our case we want to use the **"testing SSL/TLS connections"** functionality.  
We can do this with `openssl s_client`, which establishes a secure SSL/TLS connection to a server, allowing us to interact with the service by sending and receiving data over the encrypted channel.  

Let's connect to localhost on port 30001 and submit the password:
```bash
bandit15@bandit:~$ openssl s_client -connect localhost:30001
CONNECTED(00000003)                                        
Can't use SSL_get_servername
depth=0 CN = SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN = SnakeOil
verify return:1
---
Certificate chain
...
...
...
---
read R BLOCK
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
Correct!
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx

closed
```
## Flag
```bash
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```
## Notes
- `openssl s_client` connects to a server over SSL/TLS, enabling secure sending and receiving of data while showing certificate and connection details.



<p align="center">
<a href="level-16→17.md">Next Level: Level 16 → 17</a>
</p>


