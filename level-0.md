# [Bandit Level 0](https://overthewire.org/wargames/bandit/bandit0.html)

## Info
- **Host:** `bandit.labs.overthewire.org`  
- **Port:** `2220`  
- **Username:** `bandit0`  
- **Password:** `bandit0`  

---

## Task 
The goal is to log in to the server via SSH using a **terminal / command prompt and understand the basic workflow of connecting to a remove machine.

## Steps
Connect via SSH in your terminal or command prompt:
```bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit0
```

After entering the password `bandit0`, you will be logged into the server.

Since this task was only to log in, this concludes level 0.

## Notes:
Learned basic SSH login with custom port.

*Next Level*: [Level 1](level-1.md)
