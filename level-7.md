<p align="center">
<a href="level-5.md">Previous Level → Level 5</a>
</p>

# [Bandit Level 6](https://overthewire.org/wargames/bandit/bandit6.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit5`
- **Password:** `4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw`

---

## Task 
The goal of this level is to find a file with the following properties:
- owned by user bandit7
- owned by group bandit6
- 33 bytes in size

## Theory
This level introduces the concept of file ownership.
Each person in Linux is a **user**, and each user has a unique UID(User ID) e.g. root, john, bandit4, etc.
A **group** is a collection of users, each user belongs to a **primary group** and **secondary groups** e.g. `john` is in group `dev`. Files owned by group `dev` can be shared by all developers.
Every file has two owners:
- User owner -> the user who owns the file.
- Group owner -> the group that owns the file.
Using `ls -l`:
```bash
-rw-r--r-- 1 john dev 1200 Sep 13 10:00 notes.txt
```
`john` is the user owner.
`dev` is the group owner.

## Steps
Change current directory to `inhere`:
```bash
cd inhere
```
List all files:
```bash
ls -la
```
We can see 20 directories.
```bash
bandit5@bandit:~/inhere$ ls -la
total 88
drwxr-x--- 22 root bandit5 4096 Aug 15 13:16 .
drwxr-xr-x  3 root root    4096 Aug 15 13:16 ..
drwxr-x---  2 root bandit5 4096 Aug 15 13:16 maybehere00
drwxr-x---  2 root bandit5 4096 Aug 15 13:16 maybehere01
drwxr-x---  2 root bandit5 4096 Aug 15 13:16 maybehere02
drwxr-x---  2 root bandit5 4096 Aug 15 13:16 maybehere03
drwxr-x---  2 root bandit5 4096 Aug 15 13:16 maybehere04
drwxr-x---  2 root bandit5 4096 Aug 15 13:16 maybehere05
drwxr-x---  2 root bandit5 4096 Aug 15 13:16 maybehere06
drwxr-x---  2 root bandit5 4096 Aug 15 13:16 maybehere07
drwxr-x---  2 root bandit5 4096 Aug 15 13:16 maybehere08
drwxr-x---  2 root bandit5 4096 Aug 15 13:16 maybehere09
drwxr-x---  2 root bandit5 4096 Aug 15 13:16 maybehere10
drwxr-x---  2 root bandit5 4096 Aug 15 13:16 maybehere11
drwxr-x---  2 root bandit5 4096 Aug 15 13:16 maybehere12
drwxr-x---  2 root bandit5 4096 Aug 15 13:16 maybehere13
drwxr-x---  2 root bandit5 4096 Aug 15 13:16 maybehere14
drwxr-x---  2 root bandit5 4096 Aug 15 13:16 maybehere15
drwxr-x---  2 root bandit5 4096 Aug 15 13:16 maybehere16
drwxr-x---  2 root bandit5 4096 Aug 15 13:16 maybehere17
drwxr-x---  2 root bandit5 4096 Aug 15 13:16 maybehere18
drwxr-x---  2 root bandit5 4096 Aug 15 13:16 maybehere19
```
Each of these directories has a multitude of files.
Take `maybehere00` for instance:
```bash
bandit5@bandit:~/inhere$ ls -la maybehere00  
total 72
drwxr-x---  2 root bandit5 4096 Aug 15 13:16 .
drwxr-x--- 22 root bandit5 4096 Aug 15 13:16 ..
-rwxr-x---  1 root bandit5 1039 Aug 15 13:16 -file1
-rwxr-x---  1 root bandit5  551 Aug 15 13:16 .file1
-rw-r-----  1 root bandit5 9388 Aug 15 13:16 -file2
-rw-r-----  1 root bandit5 7836 Aug 15 13:16 .file2
-rwxr-x---  1 root bandit5 7378 Aug 15 13:16 -file3
-rwxr-x---  1 root bandit5 4802 Aug 15 13:16 .file3
-rwxr-x---  1 root bandit5 6118 Aug 15 13:16 spaces file1
-rw-r-----  1 root bandit5 6850 Aug 15 13:16 spaces file2
-rwxr-x---  1 root bandit5 1915 Aug 15 13:16 spaces file3
```
We could brute force print each file one by one until we find the flag but of course this is incredibly inefficient. 
If only there were a way to search for the file based on properties we were given...

The `find` command is used to search for files and directories based on specific criteria.
It just so happens that find has an option for each of them:
- `-user <username>`, finds files owned by a specific user.
- `-group <groupname>`, finds files belonging to a specific group.
- `-size +10M`, finds files greater than 10MB
- `-size -1k`, finds files smaller than 1kb.
- `-size 33c`, finds files that are exactly 33 bytes.  
Putting it all together:
```bash
find . -user bandit7 -group bandit6 -size 33c
```


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
<a href="level-6.md">Next Level → Level 6</a>
</p>
