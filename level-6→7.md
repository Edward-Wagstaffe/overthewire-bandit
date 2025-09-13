<p align="center">
<a href="level-5→6.md">Previous Level: Level 5 → 6</a>
</p>

# [Bandit Level 6 → 7](https://overthewire.org/wargames/bandit/bandit7.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit6`
- **Password:** `HWasnPhtq9AVKe0dmk45nxy20cvUa6EG`

---

## Task 
The goal of this level is to find a file on the **server** with the following properties:
- owned by user bandit7
- owned by group bandit6
- 33 bytes in size

## Steps
We no longer have the familiar `inhere` directory. We are to search the entire server for this file.  
Change current directory to the root directory:
```bash
cd /
```
List all files:
```bash
ls -la
```
```bash
bandit6@bandit:/$ ls -la
total 740
drwxr-xr-x   31 root root   4096 Sep 11 18:18 .
drwxr-xr-x   31 root root   4096 Sep 11 18:18 ..
drwxr-xr-x    2 root root   4096 Aug 15 13:16 behemoth
lrwxrwxrwx    1 root root      7 Apr 22  2024 bin -> usr/bin
drwxr-xr-x    2 root root   4096 Feb 26  2024 bin.usr-is-merged
drwxr-xr-x    5 root root   4096 Jul 31 10:14 boot
drwxr-xr-x   16 root root   3340 Sep 11 18:18 dev
drwxr-xr-x    7 root root   4096 Aug 15 13:17 drifter
drwxr-xr-x  128 root root  12288 Aug 20 16:10 etc
drwxr-xr-x    3 root root   4096 Aug 15 13:17 formulaone
drwxr-xr-x  150 root root   4096 Aug 15 13:18 home
drwxr-xr-x    9 root root   4096 Aug 15 13:17 krypton
lrwxrwxrwx    1 root root      7 Apr 22  2024 lib -> usr/lib
lrwxrwxrwx    1 root root      9 Aug 15 13:09 lib32 -> usr/lib32
lrwxrwxrwx    1 root root      9 Apr 22  2024 lib64 -> usr/lib64
drwxr-xr-x    2 root root   4096 Apr  8  2024 lib.usr-is-merged
lrwxrwxrwx    1 root root     10 Aug 15 13:09 libx32 -> usr/libx32
drwx------    2 root root  16384 Jul 31 10:07 lost+found
drwxr-xr-x    3 root root   4096 Aug 15 13:17 manpage
drwxr-xr-x    2 root root   4096 Aug 15 13:18 maze
drwxr-xr-x    2 root root   4096 Jul 31 10:04 media
drwxr-xr-x    2 root root   4096 Jul 31 10:04 mnt
drwxr-xr-x    2 root root   4096 Aug 15 13:18 narnia
drwxr-xr-x    6 root root   4096 Aug 15 13:11 opt
dr-xr-xr-x  618 root root      0 Sep 11 18:17 proc
drwx------    7 root root   4096 Sep  3 08:14 root
drwxr-xr-x   30 root root    980 Sep 12 09:43 run
lrwxrwxrwx    1 root root      8 Apr 22  2024 sbin -> usr/sbin
drwxr-xr-x    2 root root   4096 Mar 31  2024 sbin.usr-is-merged
drwx------    6 root root   4096 Jul 31 10:15 snap
drwxr-xr-x    2 root root   4096 Jul 31 10:04 srv
dr-xr-xr-x   13 root root      0 Sep 11 18:31 sys
drwxrwx-wt 1820 root root 626688 Sep 13 11:22 tmp
drwxr-xr-x   14 root root   4096 Aug 15 13:16 usr
drwxr-xr-x    2 root root   4096 Aug 15 13:18 utumno
drwxr-xr-x   14 root root   4096 Aug 20 16:10 var
drwxr-xr-x    2 root root   4096 Aug 15 13:19 vortex
```

This level introduces the concept of file ownership.    
Each person in Linux is a **user**, and each user has a unique UID(User ID) e.g. root, john, bandit4, etc.    
A **group** is a collection of users, each user belongs to a **primary group** and **secondary groups** e.g. `john` is in group `dev`. Files owned by group `dev` can be shared by all developers.
Every file has two owners:
- User owner → the user who owns the file.
- Group owner → the group that owns the file.

An example from our `ls -la` output:
```bash
drwxr-xr-x    2 root root   4096 Aug 15 13:16 behemoth
```
- `root` is the user owner(LHS).
- `root` is the group owner(RHS).

We are looking for a file that has `bandit7` as user owner, `bandit6` as group owner and has a size of 33 bytes.

The `find` command is used to search for files and directories based on specific criteria.
It just so happens that find has an option for each of our criteria:
- `-user <username>`, finds files owned by a specific user.
- `-group <groupname>`, finds files belonging to a specific group.
- `-size +10M`, finds files greater than 10MB
- `-size -1k`, finds files smaller than 1kb.
- `-size 33c`, finds files that are exactly 33 bytes.  
Putting it all together:
```bash
find ./ -user bandit7 -group bandit6 -size 33c
```
Running this command gives us a long list that include errors:
```bash
bandit6@bandit:/$ find ./ -user bandit7 -group bandit6 -size 33c
find: ‘./sys/kernel/tracing/osnoise’: Permission denied
find: ‘./sys/kernel/tracing/hwlat_detector’: Permission denied
find: ‘./sys/kernel/tracing/instances’: Permission denied
find: ‘./sys/kernel/tracing/trace_stat’: Permission denied
find: ‘./sys/kernel/tracing/per_cpu’: Permission denied
find: ‘./sys/kernel/tracing/options’: Permission denied
find: ‘./sys/kernel/tracing/rv’: Permission denied
find: ‘./sys/kernel/debug’: Permission denied
find: ‘./sys/fs/pstore’: Permission denied
find: ‘./sys/fs/bpf’: Permission denied
find: ‘./root’: Permission denied
find: ‘./boot/lost+found’: Permission denied
find: ‘./boot/efi’: Permission denied
find: ‘./run/udisks2’: Permission denied
find: ‘./run/chrony’: Permission denied
find: ‘./run/user/11022’: Permission denied
find: ‘./run/user/8003’: Permission denied
find: ‘./run/user/12000’: Permission denied
find: ‘./run/user/11031’: Permission denied
find: ‘./run/user/11023’: Permission denied
find: ‘./run/user/11010’: Permission denied
find: ‘./run/user/11003’: Permission denied
...
```

We can use `2>/dev/null` to redirect error messages so they don't show up on the terminal.
- `2` refers to file descriptor 2, which is the standard error.
- `>` redirection operator.
- `/dev/null` is the special "black hole" file that discards anything written to it. I found this particularly cool.
So lets append this to our command from above to locate the file containing the flag:
```bash
find ./ -user bandit7 -group bandit6 -size 33c 2>/dev/null
./var/lib/dpkg/info/bandit7.password
```
Read the file containing the flag:
```bash
cat ./var/lib/dpkg/info/bandit7.password
```

## Flag 
```bash
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```


## Notes
- Linux assigns each file a **user owner** and a **group owner** to control who can read, write or execute it.
- /dev/null discards any data sent to it, acting like a "black hole" for output or errors in this case.



<p align="center">
<a href="level-7→8.md">Next Level: Level 7 → 8</a>
</p>
