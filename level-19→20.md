<p align="center">
<a href="level-18→19.md">Previous Level: Level 18 → 19</a>
</p>

# [Bandit Level 19 → 20](https://overthewire.org/wargames/bandit/bandit20.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit19`
- **Password:** `cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8`

---

## Task 
The goal of this level is to use the setuid binary in the homedirectory.  
Execute it without arguments to find out how to use it.  
The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

## Steps
Let's run the binary to find out how to use it:
```bash
bandit19@bandit:~$ ls
bandit20-do
bandit19@bandit:~$ ./bandit20-do 
Run a command as another user.
  Example: ./bandit20-do id
```
Looks like this binary lets us run a command as if we were bandit20, lets print out the password for bandit20 by leveraging this:
```bash
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```
## Flag
```bash
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```

## Notes
To run a binary, ensure it has execute permissions (chmod +x file), then run it with ./file if in the current directory.

<p align="center">
<a href="level-20→21.md">Next Level: Level 20 → 21</a>
</p>


