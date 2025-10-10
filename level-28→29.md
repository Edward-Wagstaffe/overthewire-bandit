<p align="center">
<a href="level-27→28.md">Previous Level: Level 27 → 28</a>
</p>

# [Bandit Level 28 → 29](https://overthewire.org/wargames/bandit/bandit29.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit28`
- **Password:** `Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN`

---

## Task 
The goal of this level is to git clone a repository at `ssh://bandit28-git@localhost/home/bandit28-git/repo` via the port 2220. The password for bandit28-git is the same as for the user bandit28.  

## Steps
Create a temporary directory to work in and switch to it:
```bash
bandit28@bandit:~$ mktemp -d
/tmp/tmp.Xjp6R6mtp0
bandit28@bandit:~$ cd /tmp/tmp.Xjp6R6mtp0
bandit28@bandit:/tmp/tmp.Xjp6R6mtp0$ 
```

Clone the repo with `git clone`:
```bash
bandit28@bandit:/tmp/tmp.Xjp6R6mtp0$ git clone ssh://bandit28-git@localhost:2220/home/bandit28-git/repo
Cloning into 'repo'...
...
Receiving objects: 100% (9/9), done.
Resolving deltas: 100% (2/2), done.
```
Change directories into `repo` and `ls -la`:
```bash
bandit28@bandit:/tmp/tmp.Xjp6R6mtp0$ cd repo
bandit28@bandit:/tmp/tmp.Xjp6R6mtp0/repo$ ls -la
total 16
drwxrwxr-x 3 bandit28 bandit28 4096 Oct 10 07:57 .
drwx------ 3 bandit28 bandit28 4096 Oct 10 07:57 ..
drwxrwxr-x 8 bandit28 bandit28 4096 Oct 10 07:57 .git
-rw-rw-r-- 1 bandit28 bandit28  111 Oct 10 07:57 README.md
```
Let's read the README.md:
```bash
bandit28@bandit:/tmp/tmp.Xjp6R6mtp0/repo$ cat README.md
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: xxxxxxxxxx
```
We see the password here has been censored, let's check the commit history with `git log`:
```bash
bandit28@bandit:/tmp/tmp.Xjp6R6mtp0/repo$ git log
commit 710c14a2e43cfd97041924403e00efb00b3a956e (HEAD -> mas
ter, origin/master, origin/HEAD)
Author: Morla Porla <morla@overthewire.org>
Date:   Fri Aug 15 13:16:10 2025 +0000

    fix info leak

commit 68314e012fbaa192abfc9b78ac369c82b75fab8f
Author: Morla Porla <morla@overthewire.org>
Date:   Fri Aug 15 13:16:10 2025 +0000

    add missing data

commit a158f9a82c29a16dcea474458a5ccf692a385cd4
Author: Ben Dover <noone@overthewire.org>
Date:   Fri Aug 15 13:16:10 2025 +0000

    initial commit of README.md
```
We can see 3 different commits here, the one that says "fix info leak" is particularly interesting let's have a look with `git show`:
```bash
bandit28@bandit:/tmp/tmp.Xjp6R6mtp0/repo$ git show 710c14a2e43cfd97041924403e00efb00b3a956e
commit 710c14a2e43cfd97041924403e00efb00b3a956e (HEAD -> master, origin/maste
r, origin/HEAD)
Author: Morla Porla <morla@overthewire.org>
Date:   Fri Aug 15 13:16:10 2025 +0000

    fix info leak

diff --git a/README.md b/README.md
index d4e3b74..5c6457b 100644
--- a/README.md
+++ b/README.md
@@ -4,5 +4,5 @@ Some notes for level29 of bandit.
 ## credentials
 
 - username: bandit29
-- password: 4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7
+- password: xxxxxxxxxx
```
The `@@ -4,5 +4,5 @@` line just shows where in the file the change happened (around line 4).  
Lines starting with - were removed.  
Lines starting with + were added.

## Flag
```bash
4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7
```

## Notes
- `git log` shows the history of commits, including who made them, when, and their messages.
- `git show <commit-hash>` displays the exact changes made in a specific commit.
- By using `git log` to find an earlier commit and `git show` to view its content, you can reveal old versions of files—such as when a password was exposed before being removed.

<p align="center">
<a href="level-29→30.md">Next Level: Level 29 → 30</a>
</p>


