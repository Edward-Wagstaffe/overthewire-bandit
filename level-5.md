<p align="center">
<a href="level-4.md">Previous Level → Level 4</a>
</p>

# [Bandit Level 5](https://overthewire.org/wargames/bandit/bandit5.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit4`
- **Password:** `2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ`

---

## Task 
The goal of this level is to read the only **human readable** file in the inhere directory.

## Steps
Change current directory to `inhere`:
```bash
cd inhere
```
List all files:
```bash
ls -la
```
We can see 10 files.
```bash
bandit4@bandit:~/inhere$ ls -al
total 48
drwxr-xr-x 2 root    root    4096 Aug 15 13:16 .
drwxr-xr-x 3 root    root    4096 Aug 15 13:16 ..
-rw-r----- 1 bandit5 bandit4   33 Aug 15 13:16 -file00
-rw-r----- 1 bandit5 bandit4   33 Aug 15 13:16 -file01
-rw-r----- 1 bandit5 bandit4   33 Aug 15 13:16 -file02
-rw-r----- 1 bandit5 bandit4   33 Aug 15 13:16 -file03
-rw-r----- 1 bandit5 bandit4   33 Aug 15 13:16 -file04
-rw-r----- 1 bandit5 bandit4   33 Aug 15 13:16 -file05
-rw-r----- 1 bandit5 bandit4   33 Aug 15 13:16 -file06
-rw-r----- 1 bandit5 bandit4   33 Aug 15 13:16 -file07
-rw-r----- 1 bandit5 bandit4   33 Aug 15 13:16 -file08
-rw-r----- 1 bandit5 bandit4   33 Aug 15 13:16 -file09
```
The `file` command tells us what kind of data a file holds e.g. binaries, PDF, ASCII text, etc.  
Instead of checking each file one by one, we can use the wildcard `*` that matches zero or more characters in a filename.  
Applying the techniques learned in [level 2](level-2.md) to correctly reference the file whose name begins with `-`.  
```bash
file ./-*
```
Output:
```bash
bandit4@bandit:~/inhere$ file ./*
./-file00: Non-ISO extended-ASCII text, with no line terminators, with overstriking
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
```
  
We can see that file -file07 is the only one of type 'ASCII', which is indeed human readable.  
Read -file07 and obtain the flag:
```bash
cat ./-file07
```

## Flag 
```bash
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```


## Notes
- The `file` command identifies the type of a file based on its contents, not just its name.
- The `*` wildcard matches zero or more characters in filenames, useful for pattern matching. 



<p align="center">
<a href="level-5.md">Next Level → Level 5</a>
</p>
