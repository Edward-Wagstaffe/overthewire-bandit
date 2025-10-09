<p align="center">
<a href="level-25→26.md">Previous Level: Level 25 → 26</a>
</p>

# [Bandit Level 26 → 27](https://overthewire.org/wargames/bandit/bandit27.html)


**A continuation of the previous level.**

Now that we have a bash shell let's see what files are here:
```bash
bandit26@bandit:~$ ls
bandit27-do  text.txt
bandit26@bandit:~$ ./bandit27-do 
Run a command as another user.
  Example: ./bandit27-do id
```
We see something akin to [level 19 → 20](level-19→20.md), and we can run the command as another user and print the password file for bandit27.
```bash
bandit26@bandit:~$ ./bandit27-do cat /etc/bandit_pass/bandit27
upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB
```

## Flag
```bash
upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB
```

<p align="center">
<a href="level-27→28.md">Next Level: Level 27 → 28</a>
</p>
