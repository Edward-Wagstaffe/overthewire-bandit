<p align="center">
<a href="level-0→1.md">Previous Level: Level 0 → 1</a>
</p>

# [Bandit Level 1 → 2](https://overthewire.org/wargames/bandit/bandit2.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit1`
- **Password:** `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`

---

## Task 
The goal of this level is to **read a file called `-` in the home directory** using basic linux commands. 

## Steps
List Files:
```bash
ls
```

Read the file containing the flag:
```bash
cat ./-
```

## Flag 
```bash
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```


## Notes
- Learned to list files using `ls`.
- Learned to read a file using `cat`.
- Learned that `-` is a special character in Linux, usually used for command options.
- To access a file or directory named `-`, you must explicitly use `./-`, where `./` means “current directory".


<p align="center">
<a href="level-2→3.md">Next Level: Level 2 → 3</a>
</p>
