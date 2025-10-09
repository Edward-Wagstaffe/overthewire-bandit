<p align="center">
<a href="level-26→27.md">Previous Level: Level 26 → 27</a>
</p>

# [Bandit Level 27 → 28](https://overthewire.org/wargames/bandit/bandit27.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit27`
- **Password:** `upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB`

---

## Task 
The goal of this level is to git clone a repository at `ssh://bandit28-git@localhost/home/bandit28-git/repo` via the port 2220. The password for bandit28-git is the same as for the user bandit28.  

## Steps
Create a temporary directory to work in and switch to it:
```bash
bandit27@bandit:~$ mktemp -d
/tmp/tmp.IIbyjgEymm
bandit27@bandit:~$ cd /tmp/tmp.IIbyjgEymm
```
From here we can clone the repo:
```bash
bandit27@bandit:/tmp/tmp.IIbyjgEymm$ git clone ssh://bandit28-git@localhost/home/bandit28-git/repo
Cloning into 'repo'...
...
Receiving objects: 100% (3/3), done.
```


## Notes


<p align="center">
<a href="level-28→29.md">Next Level: Level 28 → 29</a>
</p>


