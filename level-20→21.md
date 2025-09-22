<p align="center">
<a href="level-19→20.md">Previous Level: Level 19 → 20</a>
</p>

# [Bandit Level 20 → 21](https://overthewire.org/wargames/bandit/bandit21.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit20`
- **Password:** `0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO`

---

## Task 
The goal of this level is to use the setuid binary in the home directory to retrieve the password.  

The setuid binary works as follows, it makes a connection to localhost on the port that was specified as a command line argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will return the password for bandit21.


## Steps
We've used `nc`(netcat) before in [level 15 → 16](level-15→16.md). To create a server on localhost we can use the `-l` (listening) option. We can also use the `-p` option to specify a port.  
So what we can do is `echo` the current password and `|` pipe it to `nc` for a "one time" use. That is, `nc` will send the data on the next accepted connection and immediately see EOF on its stdin and exit. The listener stops.  

Additionally instead of using two terminals, we can use `&` at the end of the command to tell the shell to run that command **in the background**. The command starts running and the shell prompts returns immediately so we can type other commands while it's running.
```bash
bandit20@bandit:~$ echo 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO | nc -l -p 2222 &
[1] 1103532
```
- `[1]` = the job number the shell uses to keep track of background processes in this session.
- `1103532` = the process ID (PID), a unique identifier the OS gave this background process.
We can use this number with commands like `kill 1103532` to stop it.

Let's use the setuid binary to connect to our localhost server:
```bash
bandit20@bandit:~$ ls -l
total 16
-rwsr-x--- 1 bandit21 bandit20 15608 Aug 15 13:16 suconnect
bandit20@bandit:~$ ./suconnect 2222
Read: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
Password matches, sending next password
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
[1]+  Done                    echo 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO | nc -l -p 2222
```


## Flag
```bash
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
```

## Notes
- `nc -l`: The `-l` option makes netcat listen on a specified `-p` port, typically binding to localhost unless told otherwise.
- Adding `&` at the end of a command runs it as a background process.
- A daemon is a background process that starts without user interaction and often provides system or network services.

<p align="center">
<a href="level-21→22.md">Next Level: Level 21 → 22</a>
</p>


