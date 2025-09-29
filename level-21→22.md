<p align="center">
<a href="level-20→21.md">Previous Level: Level 20 → 21</a>
</p>

# [Bandit Level 21 → 22](https://overthewire.org/wargames/bandit/bandit22.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit21`
- **Password:** `EeoULMCra2q0dSkYj561DX7s1CpBuOBt`

---

## Task 
The goal of this level is to look in **/etc/cron.d/** for the configuration of **cron** and see what command is being executed.


## Steps
Let's change directories to /etc/cron.d/ and see whats inside:
```bash
bandit21@bandit:~$ cd /etc/cron.d/
bandit21@bandit:/etc/cron.d$ ls
behemoth4_cleanup  clean_tmp  cronjob_bandit22  cronjob_bandit23  cronjob_bandit24  e2scrub_all  leviathan5_cleanup  manpage3_resetpw_job  otw-tmp-dir  sysstat
```
Quick theory, `cron` is a **time based scheduler** in Unix like OS (Linux, BSD, macOS). It allows us to **automate tasks**, for example,  commands or scripts to run at specific times, dates or intervals.
These jobs are defined in a **crontab file**.
Each crontab represents a job with a time schedule and the command to run.  

They have the following structure:
```bash
* * * * * command_to_execute
| | | | |
| | | | └── Day of week (0–6, Sunday = 0)
| | | └──── Month (1–12)
| | └────── Day of month (1–31)
| └──────── Hour (0–23)
└────────── Minute (0–59)
```
Each file inside `/etc/cron.d/` contains cron jobs in the same format as crontab, but **with an extra field** for the **user** who should run the job.  

Since we are tackling bandit22, lets take a look in `cronjob_bandit22`:
```bash
bandit21@bandit:/etc/cron.d$ cat cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```
This means cronjob runs the `cronjob_bandit22.sh` file as the bandit22 user.
The `* * * * *` indicates every possible value for all fields and translates to, run the command every minute of everyhour of every day of every month, regardless of the day of the week.
Effectively, once per minute, 24 hours a day.  

Let's have a look in the bash file to see whats being executed:
```bash
bandit21@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```
Every time this runs, it sets the temporary file's permissions so that any user can read it and
writes the Bandit22 password into it.

Let's print the contents of the tmp file since we know the password is copied there:
```bash
cat /bandit21@bandit:/etc/cron.d$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
```

## Flag
```bash
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
```

## Notes
- `cron` runs tasks on a schedule and are stored in crontabs.
- Format: `minute hour day month weekday command_to_execute`.
- `&> /dev/null` is used to silence output.


<p align="center">
<a href="level-22→23.md">Next Level: Level 22 → 23</a>
</p>


