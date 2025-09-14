<p align="center">
<a href="level-6→7.md">Previous Level: Level 6 → 7</a>
</p>

# [Bandit Level 7 → 8](https://overthewire.org/wargames/bandit/bandit8.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit7`
- **Password:** `morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj`

---

## Task 
The goal of this level is to find the flag in **data.txt** next to the word **millionth**.

## Steps
Let's see how many lines data.txt has using the `wc` command
```bash
bandit7@bandit:~$ wc -l data.txt                                        
98567 data.txt
```
Almost 100 000 lines.    
Let's print out the first 10 lines to get a feel of what the contents is like using the `head` command.
```bash
bandit7@bandit:~$ head data.txt
aileron's	OZ18kr0JQ4foUlDQ203BRlnggygCfwOL
Gallo	hBQB8IHbDxu0M4Zax1MUkhhA6A1Xpm3g
jewelers	731Lz9zm2R8Pu5d7vxdNqAfndtgdseIC
Kepler	7ELccFIE0sltZWtAFQfTkwwEL3s6KhmP
vinegary	NJnwsaqp7xYe6fdmRvftOfcK9YLGxWfC
stool	4Scu7Gb5VKY06zopnkqNohznDxV6wI1X
rotisseries	tUH4vKiK9dLcNIRkEtRFCidprOdXAxmv
Billie's	m9jn7053akOsAmsDUiu41tnpkPDq8zdj
ejaculation's	sE1cJ1Oz56mz02ODIbGHGdMwrdSNfdlz
Phaethon	D63ocDs9dgeCQ0sYiaBDgIxPkEtNDXjk
```
Each line is a key-value pair, where a word is associated with its corresponding flag. The target word is **millionth**, so we’ll use `grep` to search for all occurrences of millionth.
```bash
bandit7@bandit:~$ grep "millionth" data.txt
millionth	dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```
And just like that, we’ve obtained the flag, as it appeared only once in the file.

## Flag 
```bash
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```


## Notes
- `wc -l`, command is useful for quickly counting lines in a file, helping us to gauge file size.
- `head` command lets us preview the beginning of a file, making it easy to inspect content without printing out the entire file.
- `grep` is a powerful tool for quickly locating specific words or patterns in files. 



<p align="center">
<a href="level-8→9.md">Next Level: Level 8 → 9</a>
</p>

