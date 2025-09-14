<p align="center">
<a href="level-11→12.md">Previous Level: Level 11 → 12</a>
</p>

# [Bandit Level 12 → 13](https://overthewire.org/wargames/bandit/bandit13.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit12`
- **Password:** `7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4`

---

## Task 
The goal of this level is to find the flag in **data.txt**, which is a hexdump of a file that has been repeatedly compressed.

We're also told that it might be useful to create a directory under /tmp using the `mktemp -d` command, copying data.txt with `cp` and renaming with `mv`.

## Steps
Let's print out data.txt:
```data
bandit12@bandit:~$ cat data.txt
00000000: 1f8b 0808 0933 9f68 0203 6461 7461 322e  .....3.h..data2.
00000010: 6269 6e00 0148 02b7 fd42 5a68 3931 4159  bin..H...BZh91AY
00000020: 2653 59be 9d9d 9600 001f ffff fe7f fbcf  &SY.............
00000030: af7f 9eff f7ee ffdf bff7 fef7 ddbe 9db7  ................
00000040: bf9f 9f5f ca6f fffe d6fb feff b001 3ab3  ..._.o........:.
00000050: 0403 40d0 0000 00d0 01a0 03d4 0000 0346  ..@............F
00000060: 41a1 9000 0000 1900 0190 0686 8191 a326  A..............&
00000070: 1340 0c8c 4d0f 4d4c 4403 468d 0d1a 0001  .@..M.MLD.F.....
00000080: a686 8000 01a0 6462 6868 6800 0006 8f50  ......dbhhh....P
00000090: 00d0 1a06 9a0c d406 8c80 189a 6834 64d0  ............h4d.
000000a0: 064d 0000 3a68 1a34 d00d 0001 a1a1 91a0  .M..:h.4........
000000b0: 0000 0323 4d03 2341 9034 1a00 00c8 320d  ...#M.#A.4....2.
000000c0: 001a 1880 3401 8406 9a68 00d1 a34d 34d1  ....4....h...M4.
000000d0: 7808 0920 2027 a994 91db 6412 de13 8af2  x..  '....d.....
000000e0: 7f2a f82d c875 b4c2 6723 afc6 8b7c 62ad  .*.-.u..g#...|b.
000000f0: a375 3887 65c0 1718 5224 81c3 0b33 8e21  .u8.e...R$...3.!
00000100: c736 e901 b187 8c9f 5b3c a81e f09d ec5c  .6......[<.....\
00000110: 41c0 0b74 ca62 56e6 8452 ce37 8889 5ab7  A..t.bV..R.7..Z.
00000120: d5d8 9316 1d26 26e7 b18f e376 b6b9 02ec  .....&&....v....
00000130: 0880 aa07 3c2c fd25 03ba cc87 59fa 5436  ....<,.%....Y.T6
00000140: 4a67 b193 3aec d8a3 6813 92e6 67ce 5118  Jg..:...h...g.Q.
00000150: b22b d1b2 114c 9fb6 3033 d37a 86b2 62c5  .+...L..03.z..b.
00000160: 9fb1 09c3 afcb 76ab ab69 e168 cdb6 6d5e  ......v..i.h..m^
00000170: 3b86 91a9 7a45 0371 70de ca02 4ce5 1de9  ;...zE.qp...L...
00000180: f996 0ae0 2c33 a0ca ceeb 1d0a 02a7 3160  ....,3........1`
00000190: 9746 3cd6 c5c1 433b 991f 9989 5ab3 cbf2  .F<...C;....Z...
000001a0: 0759 072f 8b6f 08af f163 c149 8879 f738  .Y./.o...c.I.y.8
000001b0: 6241 3876 4edf 6038 0b60 277c d2ca 7908  bA8vN.`8.`'|..y.
000001c0: b1f3 a93c 23d0 277b 215c 7498 b2a1 01dd  ...<#.'{!\t.....
000001d0: 563b be47 3fdc a008 0f08 82c7 2044 c8da  V;.G?....... D..
000001e0: a241 c91c c3ee f1a1 9b98 25eb 5212 3fb1  .A........%.R.?.
000001f0: e545 2469 108f 7f01 e7c9 faed cd3e 9f08  .E$i.........>..
00000200: 97bc 1b04 a087 e826 0993 65d3 13b6 5365  .......&..e...Se
00000210: 3c6d 10e5 1d85 66ab 0497 6242 8799 8112  <m....f...bB....
00000220: 61a0 87dc fcfb 9274 774a c918 d5ce 3c0f  a......twJ....<.
00000230: d346 95c8 1e30 42a6 a3b7 a93b 67f3 186c  .F...0B....;g..l
00000240: 904c 842c 30c5 e1b2 b841 05e0 7144 2a60  .L.,0....A..qD*`
00000250: ca14 0a52 f589 fe2e e48a 70a1 217d 3b3b  ...R......p.!};;
00000260: 2c19 d8f7 0e48 0200 00                   ,....H...
```
This is a **hexdump**.
A hexdump is a way to display a file's contents in **hexadecimal(base16)** instead of plain text. Computers store all files as bytes, and many files like executables, images or compressed files contain **non-printable bytes** that we can't read directly. A hexdump makes these bytes visible and interpretable.

The structure is as such (from the first line of data.txt):
- `00000000:` shows the position of the first byte in the file.
- The hexadecimal bytes (in pairs): `1f8b 0808 0933 9f68 0203 6461 7461 322e`
- `.....3.h..data2.` the ASCII representation, with non-printable bytes as a dot `.`

We've been told that the file has been **repeatedly compressed**, this can be seen by the specific **"magic numbers"** or **headers** at the start that identify the file type.
For example:
| File Type  | Header (Hex)        | Notes                         |
|-----------|-------------------|-------------------------------|
| Gzip      | 1F 8B             | Very common in Linux (.gz)    |
| Bzip2     | 42 5A 68          | Corresponds to ASCII `BZh`    |
| Zip       | 50 4B 03 04       | .zip archives                 |
| Tar.gz    | Gzip header + tar | Usually .tar.gz               |
| 7z        | 37 7A BC AF 27 1C | 7-Zip archives                |
| XZ        | FD 37 7A 58 5A 00 | XZ compressed files           |
| RAR       | 52 61 72 21 1A 07 00 | RAR archives              |


  




## Flag 
```bash
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

## Notes



<p align="center">
<a href="level-13→14.md">Next Level: Level 13 → 14</a>
</p>


