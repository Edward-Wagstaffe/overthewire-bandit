# [Bandit Level 4](https://overthewire.org/wargames/bandit/bandit4.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit3`
- **Password:** `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx`

---

## Task 
The goal of this level is to **read a hidden file in the inhere directory**.

## Steps
Change current directory to `inhere`:
```bash
cd inhere
```
List all files (including hidden):
```bash
ls -a
```
There is a hidden file called `...Hiding-From-You`  
Read the hidden file:
```bash
cat ...Hiding-From-You
```

## Flag 
```bash
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```


## Notes
- The `cd` command moves us from the current working directory to another.
- The `-a` option tells `ls` to show all files, including hidden ones.
- Hidden files always start with a `.`



<p align="center">
<a href="level-5.md">Next Level → Level 5</a>
</p>
