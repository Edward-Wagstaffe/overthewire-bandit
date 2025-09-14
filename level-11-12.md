<p align="center">
<a href="level-10→11.md">Previous Level: Level 10 → 11</a>
</p>

# [Bandit Level 11 → 12](https://overthewire.org/wargames/bandit/bandit12.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit11`
- **Password:** `dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr`

---

## Task 
The goal of this level is to find the flag in **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions.

## Steps
Print out data.txt:
```bash
bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf 7k16JArUVv5LxVuJfsSVdbbtaHGlw9D4
```

Shifting characters of the alphabet is called a **Caesar cipher**.
It is a simple encryption method used historically by Julius Caesar, and is a type of **substitution cipher** where each letter in the plaintext is replaced by a letter **a fixed number of poisitons down the alphabet**.
In this case, 13 characters, which is actually a very common shift and has its own name **ROT13**.  

We can use the `tr` command to **translate or delete** characters from input text.
An example of translation using ranges like a-z and A-Z:
```bash
echo "abc" | tr 'a-z' 'A-Z'
# Output: ABC
```


An example of deleting characters using the `-d` option:
```bash
echo "hello 123" | tr -d '0-9'
# Output: hello
```

We can pipe the output of `cat data.txt` into the `tr` command and provide the character set to shift the characters back 13 positions:
```bash
bandit11@bandit:~$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```
- `'A-Za-z'` = the full alphabet in uppercase and lowercase.
- `'N-ZA-Mn-za-m'` maps each letter 13 positions forward in the alphabet.



## Flag 
```bash
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

## Notes
- The **Ceasar cipher** is a **substitution cipher** that shifts each letter in the plaintext by a fixed number of positions.
- **ROT13** is a common 13-character shift.
- `tr` is a powerful tool for character transformations.


<p align="center">
<a href="level-12→13.md">Next Level: Level 12 → 13</a>
</p>

