<p align="center">
<a href="level-9→10.md">Previous Level: Level 9 → 10</a>
</p>

# [Bandit Level 10 → 11](https://overthewire.org/wargames/bandit/bandit11.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit10`
- **Password:** `FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey`

---

## Task 
The goal of this level is to find the flag in **data.txt**, which contains base64 encoded data.

## Steps
Let's see how many lines there are in data.txt:
```bash
bandit10@bandit:~$ wc -l data.txt
1 data.txt
```
Since there's only a single line lets print it out:
```bash
bandit10@bandit:~$ cat data.txt       
VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmozcVJyCg==
```
Here we are introduced to `base64`, which is a **binary to text encoding scheme** used to represent binary data e.g. images, files, keys, etc... in **ASCII text**. This makes it easy to store or transmit over systems that only handle text. Often padded with '=' to make the output a multiple of 4 characters.    

Base64 is named for the 64 characters it uses to represent binary data as text:
- A-Z (26)
- a-z (26)
- 0-9 (10)
- '\+' (1)
- '/' (1)
Total: 64

So what we are looking at when we `cat` data.txt is the Base-64 encoded version of some text.    
We can decode it with the `base64` command with the option `-d` for decode mode.
```bash
bandit10@bandit:~$ base64 -d data.txt                      
The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

## Flag 
```bash
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

## Notes
- **Encoding** converts data from one format to another for storage, transmission, or readability; **it does not hide or encrypt data**.
- **Base-64** a common encoding scheme that represents binary data as ASCII text.
- `base64` (linux command) can encode a file to Base64 or decode Base64 text back to its original form.


<p align="center">
<a href="level-11→12.md">Next Level: Level 11 → 12</a>
</p>

