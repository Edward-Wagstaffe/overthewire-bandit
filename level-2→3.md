<p align="center">
<a href="level-1→2.md">Previous Level: Level 1 → 2</a>
</p>

# [Bandit Level 2 → 3](https://overthewire.org/wargames/bandit/bandit3.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit2`
- **Password:** `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`

---

## Task 
The goal of this level is to **read a file called `--spaces in this filename--` in the home directory** using basic linux commands. 

## Steps
List Files:
```bash
ls
```

Read the file containing the flag:
```bash
cat ./--spaces\ in\ this\ filename--
```
Or
```bash
cat ./"--spaces in this filename--"
```

## Flag 
```bash
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```


## Notes
- Learned that `--` is also special character in Linux, used for command options/arguments.
- To access a file or directory beginning with `--`, use the same logic as level 2, e.g. `./--filename`.
- Files with spaces must be referenced using `\` or quotes, e.g. `file \name` or `"file name"`
- Practiced handling filenames with special characters and spaces.


<p align="center">
<a href="level-3→4.md">Next Level: Level 3 → 4</a>
</p>
