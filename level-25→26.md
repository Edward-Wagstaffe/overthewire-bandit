<p align="center">
<a href="level-24→25.md">Previous Level: Level 24 → 25</a>
</p>

# [Bandit Level 25 → 26](https://overthewire.org/wargames/bandit/bandit26.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit25`
- **Password:** `iCi86ttT4KSNe1armKiwbQNmB3YJP3q4`

---

## Task 
The goal of this level is to log in to bandit26, but as easy as that sounds, the shell for bandit26 is not **/bin/bash**, but something else. We are to find out what it is, how it works and how to break out of it.

## Steps
Doing a quick `ls`:
```bash
bandit25@bandit:~$ ls                                                                                                                                            
bandit26.sshkey
```
We find the ssh private key to log into bandit26.  

Let's copy the contents of the key to our own system (we also need to limit the permissions of the key), and try logging into bandit26:
```bash
chmod 600 sshkey25.private
ssh -i sshkey25.private bandit.labs.overthewire.org -p 2220 -l bandit26
...

  Enjoy your stay!

  _                     _ _ _   ___   __  
 | |                   | (_) | |__ \ / /  
 | |__   __ _ _ __   __| |_| |_   ) / /_  
 | '_ \ / _` | '_ \ / _` | | __| / / '_ \ 
 | |_) | (_| | | | | (_| | | |_ / /| (_) |
 |_.__/ \__,_|_| |_|\__,_|_|\__|____\___/ 
Connection to bandit.labs.overthewire.org closed.
```
The connection was closed as there was no interactive shell defined for user bandit26 in `/etc/passwd`.  

Let's log back into bandit25 and see what is defined for bandit26:
```bash
bandit25@bandit:~$ cat /etc/passwd | grep bandit26
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
```
Each line in `/etc/passwd` represents one user account and has seven fields, separated by colons `:`.  

`username:password:UID:GID:comment:home_directory:shell`  

- `username` - the login name(bandit25, bandit26, etc...).
- `password` - usually an `x` or `*` meaning the encrypted password is stored in `/etc/shadow`.
- `UID` - the user ID number.
- `GID` - the user's primary group ID.
- `comment` - optional description.
- `home_directory` - path to the user's home folder.
- `shell` - the program executed when the user logs in (e.g. /bin/bash)

In our case, bandit26 has `/usr/bin/showtext` set as their shell. Let's investigate further:
```bash
bandit25@bandit:~$ cat /usr/bin/showtext
#!/bin/sh

export TERM=linux

exec more ~/text.txt
exit 0
```
What we see here is a script that is executed when we log in to bandit26, more specifically, it opens a file called `text.txt` with the `more` command.  

`more` is a linux command that lets us view text files one screen at a time. When a file is too long to fit on one screen, instead of flooding the terminal it pauses after each page.
Now when we logged into bandit26 with the private key we never got to see this as our terminal size was large enough to accomodate the text.
If we **make our terminal window really small** before we log in to bandit26, we should be able to see the interactive mode of `more`.
From there we can use `v` to go into vim (text editor) and enter **command-line mode**  by typing `:` followed by our command.
```bash
❯ ssh -i sshkey25.private bandit.labs.overthewire.org -p 2220 -l bandit26
...

  Enjoy your stay!

  _                     _ _ _   _
__   __  
 | |                   | (_) | |_
_ \ / /  
 | |__   __ _ _ __   __| |_| |_  
 ) / /_  
--More--(50%)
```
After typing `v` to enter vim, you can resize your terminal back to your preferred size.  
`:shell` command in vim should give us a shell, however it will use the user's default shell. So what we need to do is change the default shell to something more familiar like `/bin/bash`.
We can do that with the `:set` command:
```bash
  _                     _ _ _   ___   __
 | |                   | (_) | |__ \ / /
 | |__   __ _ _ __   __| |_| |_   ) / /_
 | '_ \ / _` | '_ \ / _` | | __| / / '_ \
 | |_) | (_| | | | | (_| | | |_ / /| (_) |
 |_.__/ \__,_|_| |_|\__,_|_|\__|____\___/
~                                                                                                                                                                                                                              
~                                                                                                                     
~                                                                                                                     
~                                                                                                                     
:set shell=/bin/bash
:shell
bandit26@bandit:~$ 
```
Now that we have a bash shell let's see what files are here:
```bash
bandit26@bandit:~$ ls
bandit27-do  text.txt
bandit26@bandit:~$ ./bandit27-do 
Run a command as another user.
  Example: ./bandit27-do id
```
We see something akin to [level 20 → 21](level-20→21.md), and we can run the command as another user and print the password file for bandit27.
```bash
bandit26@bandit:~$ ./bandit27-do cat /etc/bandit_pass/bandit27
upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB
```

## Flag
```bash
upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB
```

## Notes
- `/etc/passwd` is the system file that stores user account information separated by `:`. The last field specifies which shell the user runs when logging in.
- `more` displays text one screen at a time, letting us scroll through long files with space or enter. While in this interactive mode pressing `v` tells it to launch the vim editor (on most linux systems).
- Vim's command mode is entered by preceeding the command with `:` allowing us to run commands like saving, quitting or editing files such as changing the default shell with `:set shell=/bin/bash`.


<p align="center">
<a href="level-26→27.md">Next Level: Level 26 → 27</a>
</p>


