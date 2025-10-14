<p align="center">
<a href="level-28→29.md">Previous Level: Level 28 → 29</a>
</p>

# [Bandit Level 29 → 30](https://overthewire.org/wargames/bandit/bandit30.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit29`
- **Password:** `4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7`

---

## Task 
The goal of this level is to git clone a repository at `ssh://bandit29-git@localhost/home/bandit29-git/repo` via the port 2220. The password for bandit29-git is the same as for the user bandit29.  

## Steps
Create a temporary directory to work in and switch to it:
```bash
bandit29@bandit:~$ mktemp -d                                
/tmp/tmp.VkhTLRUfPq
bandit29@bandit:~$ cd /tmp/tmp.VkhTLRUfPq                                 
bandit29@bandit:/tmp/tmp.VkhTLRUfPq$ 
```

Clone the repo with `git clone`:
```bash
bandit29@bandit:/tmp/tmp.VkhTLRUfPq$ git clone ssh://bandit29-git@localhost:2220/home/bandit29-git/repo
...
Receiving objects: 100% (16/16), done.
Resolving deltas: 100% (2/2), done.
```
Change directories into `repo` and `ls -la`:
```bash
bandit29@bandit:/tmp/tmp.VkhTLRUfPq$ cd repo
bandit29@bandit:/tmp/tmp.VkhTLRUfPq/repo$ ls -la
total 16
drwxrwxr-x 3 bandit29 bandit29 4096 Oct 14 03:23 .
drwx------ 3 bandit29 bandit29 4096 Oct 14 03:22 ..
drwxrwxr-x 8 bandit29 bandit29 4096 Oct 14 03:23 .git
-rw-rw-r-- 1 bandit29 bandit29  131 Oct 14 03:23 README.md
```
Let's read the README.md:
```bash
bandit29@bandit:/tmp/tmp.ZeYylBBk7i/repo$ cat README.md 
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: <no passwords in production!>
```
The `<no passwords in production!>` might suggest that there is a development branch.
We can check what other branches exist with `git branch -a`:
```bash
bandit29@bandit:/tmp/tmp.ZeYylBBk7i/repo$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev
  remotes/origin/master
  remotes/origin/sploits-dev
bandit29@bandit:/tmp/tmp.ZeYylBBk
```
There is indeed a `/dev` branch, let's switch to it with `git checkout dev`:
```bash
bandit29@bandit:/tmp/tmp.ZeYylBBk7i/repo$ git checkout dev
branch 'dev' set up to track 'origin/dev'.
Switched to a new branch 'dev'
```
read the README.md:
```bash
bandit29@bandit:/tmp/tmp.ZeYylBBk7i/repo$ ls -la
total 20
drwxrwxr-x 4 bandit29 bandit29 4096 Oct 14 03:47 .
drwx------ 3 bandit29 bandit29 4096 Oct 14 03:29 ..
drwxrwxr-x 2 bandit29 bandit29 4096 Oct 14 03:47 code
drwxrwxr-x 8 bandit29 bandit29 4096 Oct 14 03:47 .git
-rw-rw-r-- 1 bandit29 bandit29  134 Oct 14 03:47 README.md
bandit29@bandit:/tmp/tmp.ZeYylBBk7i/repo$ cat README.md 
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL
```

## Flag
```bash
qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL
```

## Notes
- Git branches lets us work on different versions or features of a project in isolation.
- **Production** refers to the live, public version of a system that real users interact with.
- **Development** is the private, internal environment used for building, testing, and experimenting with new code.

<p align="center">
<a href="level-30→31.md">Next Level: Level 30 → 31</a>
</p>


