<p align="center">
<a href="level-17→18.md">Previous Level: Level 17 → 18</a>
</p>

# [Bandit Level 18 → 19](https://overthewire.org/wargames/bandit/bandit19.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit18`
- **Password:** `x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO`

---

## Task 
The goal of this level is to read the password within the **readme** file in the homedirectory, however someone has modified **.bashrc** to log out when we connect with ssh.


## Steps
We should use the `-t` option, which opens a pseudo terminal (software that emulates a physical terminal), this way we are able to run the `sh` command that opens up one of the oldest linux shells the **Bourne shell**, that way we aren't kicked out by the configured **.bashrc** and we can run commands like `ls` and `cat` to read the file.
```bash
❯ ssh bandit.labs.overthewire.org -p 2220 -l bandit18 -t "sh"
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-0
bandit18@bandit.labs.overthewire.org's password: 
$ ls
readme
$ cat readme    
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
```

Alternatively, we can use **ssh command execution**.  
When you run `ssh user@host command`, SSH executes the command directly in a non-interactive shell, skipping your default login shell; the default shell only starts when you log in without specifying a command.  
So all we need to do is append `cat readme` to the end of the ssh command:
```bash
❯ ssh bandit.labs.overthewire.org -p 2220 -l bandit18 cat readme
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-0
bandit18@bandit.labs.overthewire.org's password: 
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
```

## Flag
```bash
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
```

## Notes
- The `-t` flag forces allocation of a pseudo-terminal, allowing interactive commands or alternate shells to run properly over SSH.
- **SSH Command Execution** & **Default Shell**: `ssh user@host command` runs the command on the remote host in a non-interactive shell, skipping the default login shell unless no command is specified.

<p align="center">
<a href="level-19→20.md">Next Level: Level 19 → 20</a>
</p>


