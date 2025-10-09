A continuation of the previous level.  

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
