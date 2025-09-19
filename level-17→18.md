<p align="center">
<a href="level-16→17.md">Previous Level: Level 16 → 17</a>
</p>

# [Bandit Level 17 → 18](https://overthewire.org/wargames/bandit/bandit18.html)

## Login Info
- **SSH:** `ssh -i sshkey17.private bandit17@bandit.labs.overthewire.org -p 2220`
- **Password:** Private key from [level 16 → 17](level-16→17.md)

---

## Task 
The goal of this level is to find the password by comparing the two files in the home directory: **passwords.old** and **passwords.new**.


## Steps
Simply use the `diff` command compares two files line by line and shows you the differences between them:
```bash
bandit17@bandit:~$ diff passwords.old passwords.new
42c42
< gvE89l3AhAhg3Mi9G2990zGnn42c8v20
---
> x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```

- passwords.old has the  `gvE89l3AhAhg3Mi9G2990zGnn42c8v20` old line (<)  
- passwords.new has the `x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO` new line (>)

## Flag
```bash
x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```

## Notes
`diff` compares two files line by line and shows the differences. It marks changes with codes like `42c42`, where the numbers are line numbers from each file and the letter shows the type of change (`a` = add, `d` = delete, `c` = change). Lines from the first file are shown with `<`, and lines from the second file are shown with `>`.


<p align="center">
<a href="level-18→19.md">Next Level: Level 18 → 19</a>
</p>


