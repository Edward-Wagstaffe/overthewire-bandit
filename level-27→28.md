<p align="center">
<a href="level-26→27.md">Previous Level: Level 26 → 27</a>
</p>

# [Bandit Level 27 → 28](https://overthewire.org/wargames/bandit/bandit28.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit27`
- **Password:** `upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB`

---

## Task 
The goal of this level is to git clone a repository at `ssh://bandit27-git@localhost/home/bandit27-git/repo` via the port 2220. The password for bandit27-git is the same as for the user bandit27.  

## Steps
Create a temporary directory to work in and switch to it:
```bash
bandit27@bandit:~$ mktemp -d
/tmp/tmp.IIbyjgEymm
bandit27@bandit:~$ cd /tmp/tmp.IIbyjgEymm
```
From here we can clone the repo with `git clone`:
```bash
bandit27@bandit:/tmp/tmp.IIbyjgEymm$ git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo 
Cloning into 'repo'...
...
Receiving objects: 100% (3/3), done.
bandit27@bandit:/tmp/tmp.wHil5HKsSu$ ls -la                                        
total 1284
drwx------     3 bandit27 bandit27    4096 Oct  9 08:14 .
drwxrwx-wt 17039 root     root     1302528 Oct  9 08:15 ..
drwxrwxr-x     3 bandit27 bandit27    4096 Oct  9 08:14 repo
bandit27@bandit:/tmp/tmp.wHil5HKsSu$ ls repo
README
bandit27@bandit:/tmp/tmp.wHil5HKsSu$ cat repo/README
The password to the next level is: Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN
```

## Flag
```bash
Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN
```

## Notes
- Git is a version control system. It helps us to track changes in files and coordinate work on those files among multiple people.
- A repository (repo) is a folder that stores a project and its history. Can be local or remote.
- When we run `git init` or clone a repo. Git creates a `.git` directory inside the project. It contains all the data Git needs to track your project's history, branches commmits and configs.
- Although not required, a `README`, is a text file that explains the project. 


<p align="center">
<a href="level-28→29.md">Next Level: Level 28 → 29</a>
</p>


