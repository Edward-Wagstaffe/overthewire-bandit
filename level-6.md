<p align="center">
<a href="level-5.md">Previous Level: Level 4 → 5</a>
</p>

# [Bandit Level 5 → 6](https://overthewire.org/wargames/bandit/bandit6.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit5`
- **Password:** `4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw`

---

## Task 
The goal of this level is to find a file with the following properties:
- human-readable
- 1033 bytes in size
- not executable


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

The `find` command is used to search for files and directories based on specific criteria.  
- `-type f`, limits results to regular files.
- `-executable`, matches executable files, but we want non-executable files so we can negate the condition with `!`, leaving us with `! -executable`.
- `-size 1033c`, lets us specify file size with units, `c` stands for bytes.    


Now `find` does not have an option to find human readable files, we can combine `find` with `file` by using `-exec file {} \;`.
- `-exec`, runs a command on each file that find locates.
- `{}`, placeholder for the current file found by `find`.
- `\;`, indicates the end of the command.

The pipe `|` in Linux is a way to send the output of one command as input to another command. This lets us chain commands together.
`| grep "ASCII text"`, only shows us files that are human-readable.

Putting it all together:
```bash
find ./ -type f ! -executable -size 1033c -exec file {} \; | grep "ASCII text"
```
```bash
bandit5@bandit:~/inhere$ find ./ -type f ! -executable -size 1033c -exec file {} \; | grep "ASCII text"
./maybehere07/.file2: ASCII text, with very long lines (1000)
```
  
We can see that file `.file2` in the `maybehere07` directory matches the criteria.

Read .file2 and obtain the flag:
```bash
cat ./maybehere07/.file2
```

## Flag 
```bash
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```


## Notes
- The `find` command searches for files and directories recursively based on criteria like name, type, size, etc.
- Pipe `|` sends the output of one comand as input to another command for further processing.
- `grep`, filters input to show only lines that match the pattern / text.



<p align="center">
<a href="level-7.md">Next Level: Level 6 → 7</a>
</p>
