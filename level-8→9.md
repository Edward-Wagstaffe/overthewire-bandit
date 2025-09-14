<p align="center">
<a href="level-7→8.md">Previous Level: Level 7 → 8</a>
</p>

# [Bandit Level 8 → 9](https://overthewire.org/wargames/bandit/bandit9.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit8`
- **Password:** `dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc`

---

## Task 
The goal of this level is to find the flag in **data.txt** and is the only line of text that **occurs only once.**

## Steps
Let's see how many lines data.txt has using the `wc` command
```bash
bandit8@bandit:~$ wc -l data.txt
1001 data.txt
```
1001 lines.  
Let's print out the first 10 lines to get a feel of what the contents is like using the `head` command.
```bash
bandit8@bandit:~$ head data.txt
ZzQDv5Imr9y5XSYGD3r61uP1fjXAhuod
bjQCibPw40urmZNBNNpv8zTOaFVFWSbv
uG6s7CFzkh4lqmcJtwLIxa4sU1v8gkhU
WkcJmDs54n2OynP1oYNjZ64kXa4KjVJY
KtzxzcvxasfTcGEobGpZ9SDoCGtiCqoa
ZzQDv5Imr9y5XSYGD3r61uP1fjXAhuod
EVUICc3XWvOsOyCzwfBk4lP9Phrq0yrx
CIf7GKFmEHSYJ4mkTGHkKrqxcJkCHmXx
Y8fwKYAyzkZ1H4TVJYjw2R9xPgrHpapw
lb1yDCOh6q8AV5p7twYZSSzuEysSae4n
```
Since each line could be a flag, manually scanning for the single occurrence would be extremely tedious.

The `uniq` command is used to filter out or report repeated lines in a file. It only works on consecutive duplicate lines, so it's often paried with `sort`.
Some interesting options include:
- `-c`, which prints each unique line preceded by the number of times it occurs.
- `-d`, which prints only the duplicate lines.
- `-u`, which prints only the lines that are unique (the one we want).

Let's `sort` data.txt then pipe the output to `uniq` with the `-u` option:
```bash
bandit8@bandit:~$ sort data.txt | uniq -u                    
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```


## Flag 
```bash
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

## Notes
- `sort` arranges lines of a file in alphabetical or numerical order.
- `uniq` filters out duplicate consecutive lines or reports them.
- Use `sort | uniq` to find unique values, count occurrences, or identify duplicates, which is useful for filtering data or spotting flags.



<p align="center">
<a href="level-9→10.md">Next Level: Level 9 → 10</a>
</p>

