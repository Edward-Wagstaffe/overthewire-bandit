<p align="center">
<a href="level-13→14.md">Previous Level: Level 13 → 14</a>
</p>

# [Bandit Level 14 → 15](https://overthewire.org/wargames/bandit/bandit15.html)

## Login Info
- **SSH:** `ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220`
- **Password:** private key from [level 13 → 14](level-13→14.md)

---

## Task 
The goal of this level is to submit the password of the current level to **port 30000** on **localhost**.  

## Steps
The password of the current level is found in **/etc/bandit_pass/bandit14**.  
Let's have a look:
```bash
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```
We are told to submit this password to `localhost` on port 30000.  

Localhost is the standard hostname that refers to our **own computer** and is mapped to the IP address **127.0.0.1** (IPv4). This is basically a **loopback address**, any network traffic sent to localhost stays within our machine which can be used for testing servers or services locally without internet.  

`nc` (netcat) is a fundamental networking utility that reads and writes data across network connections using TCP or UDP protocols.  

A service must have been setup on localhost:30000 for this level and it expects the password to be sent as plain text over the TCP connection.

Let's use `nc` to connect to localhost:30000 and use input redirection `<` to feed `nc` the password:
```bash
bandit14@bandit:~$ nc localhost 30000 < /etc/bandit_pass/bandit14
Correct!
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```


## Flag 
```bash
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo

```

## Notes
- **Localhost** is a hostname that refers to our own computer, mapped to 127.0.0.1, used to test services locally.
- `nc` (netcat) is a versatile networking tool for connecting to ports, sending/receiving data and acting as a simple client or server
- `<` redirection sends the contents of a file as input (stdin) to a command, similar to piping a file into it.



<p align="center">
<a href="level-15→16.md">Next Level: Level 15 → 16</a>
</p>



