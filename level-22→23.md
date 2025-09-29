<p align="center">
<a href="level-21→22.md">Previous Level: Level 21 → 22</a>
</p>

# [Bandit Level 22 → 23](https://overthewire.org/wargames/bandit/bandit23.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit22`
- **Password:** `tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q`

---

## Task 
The goal of this level is to look in **/etc/cron.d/** for the configuration of **cron** and see what command is being executed.


## Steps
Let's change directories in to /etc/cron.d/ and take a look what's inside:
```bash
bandit22@bandit:~$ cd /etc/cron.d/
bandit22@bandit:/etc/cron.d$ ls
behemoth4_cleanup  clean_tmp  cronjob_bandit22  cronjob_bandit23  cronjob_bandit24  e2scrub_all  leviathan5_cleanup  manpage3_resetpw_job  otw-tmp-dir  sysstat
```
Now let's have a look inside `cronjob_bandit23`:
```bash
bandit22@bandit:/etc/cron.d$ cat cronjob_bandit23
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
```
Again we see something reminiscent of the previous level, lets print out the bash script and see what it is trying to do.
```bash
bandit22@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit23.sh
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```
`myname=$(whoami)`, this line is a command substitution, it will run a command and insert its output. The `myname` variable will be set to output of `whoami`. Since this cronjob is run by **bandit 23**, as shown in the cronjob, `* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null`. `myname` will be set to `bandit23`.

The second line is another command substitution, `mytarget` is set to the output of `echo I am user $myname | md5sum | cut -d ' ' -f 1`.
The `$myname` in this case, bash replaces it with the value stored in the variable, which we know will be `bandit23`.
So the message **"I am user bandit23"** is piped into `md5sum` and subsequently `cut -d ' ' -f 1`.
- `md5sum calculates and prints the MD5(message digest 5) **hash** of the piped message. It will output a 32 char hexadecimal checksum.
- `cut` is used to extract specific sections of text, like slicing columns or characters out of text. This simply removes the `-` seen at the end of the hash which indicates that the input came from stdin. (not a file).

So what's left is just the MD5 hash of **"I am user bandit23"**, and `mytarget` stores that hash.  

`cat /etc/bandit_pass/$myname > /tmp/$mytarget`
Since $myname = bandit23 and $mytarget = the hash of "I am user bandit23".
This command is copying the password of bandit23 into a tmp file named after the hash.
All we need to do is hash the message ourselves to figure out the tmp filename and print the contents of the tmp file.
```bash
bandit22@bandit:/etc/cron.d$ echo I am user bandit23 | md5sum | cut -d ' ' -f 1
8ca319486bfbbc3663ea0fbe81326349
bandit22@bandit:/etc/cron.d$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349         
0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
```
## Flag
```bash
0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
```

## Notes
- `$` in bash, expands variables, command outputs or special parameters into their values.
- `md5sum` generates a 32-char MD5 hash to check file or text integrity
- `cut` extracts specific characters, bytes, or columns from each line of input.



<p align="center">
<a href="level-23→24.md">Next Level: Level 23 → 24</a>
</p>


