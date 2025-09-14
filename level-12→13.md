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


From the first line: `00000000: 1f8b 0808 0933 9f68 0203 6461 7461 322e  .....3.h..data2.`  
We can identify that data.txt begins with `1f 8b` which corresponds to a `.gz` file.
Therefore, we need to decompress data.txt using `gzip`.

Let's make a temporary directory in /tmp with `mktemp -d`(your dir will be given a different name):
```bash
bandit12@bandit:~$ mktemp -d                                              
/tmp/tmp.TEdr4aK3wp
```
Then, let's make a copy of data.txt and place it in our temp directory:
```bash
bandit12@bandit:~$ cp data.txt /tmp/tmp.TEdr4aK3wp
```
And change directories to that directory:
```bash
bandit12@bandit:~$ cd /tmp/tmp.TEdr4aK3wp
```
Before decompressing, we should first reconstruct the original file from the hexdump using `xxd` and the reverse option `-r`.
```bash
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ xxd -r data.txt original_data
```
Here, I've named the output file as `original_data` but you could call it whatever you want.
Let's see what it looks like now using `head`:
```bash
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ head -n 1 original_data 
�       3�hdata2.binH��BZh91AY&SY��������ϯ�����߿���ݾ�����_�o�������:�@����FA�������&@
����dbhhh�P��        �MMLDF�
�4��hѣM4�x�2 ���  '����d���*�-�u��g#�Ƌ|b��u8�e�R$��
                                                   3�!�6�����[<���\A�
     t�bV�R�7��Z��ؓ&&籏�v����<,�%�̇Y�T6Jg��:�أh��g�Q�+ѲL��03�z��bş�	ï�v��i�hͶm^;���zEqp��L����
```

We can decompress `-d` files using `gzip` and opt to keep the original compressed file just in case with `-k`.
If you tried to decompress `original_data`, `gzip` would complain and throw an error: `original_data: unknown suffix -- ignored`.  

To solve this, we need to add the `.gz` suffix, and rename `original_data` to `original_data.gz` with `mv`.
```bash
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ mv original_data original_data.gz
```
We can now decompress the file, and then use `ls` to check the contents of our tmp dir.
```bash
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ gzip -dk original_data.gz
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ ls
data.txt  original_data  original_data.gz
```
By using `head` to display the first line in `original_data`, the file produced from the decompression, we can see:
```bash
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ head -n 1 original_data
BZh91AY&SY��������ϯ�����߿���ݾ�����_�o�������:�@����FA�������&@
����dbhhh�P��                                                 �MMLDF�
�4��hѣM4�x�2 ���  '����d���*�-�u��g#�Ƌ|b��u8�e�R$��
                                                   3�!�6�����[<���\A�
                                                                     t�bV�R�7��Z��ؓ&&籏�v����<,�%�̇Y�T6Jg��:�أh��g�Q�+ѲL��03�z��bş�	ï�v��i�hͶm^;���zEqp��L����
```
Since the content is still unreadable, let's create a hexdump of it to analyze its contents.
```bash
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ xxd original_data hexdump_data
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ head hexdump_data                                                             
00000000: 425a 6839 3141 5926 5359 be9d 9d96 0000  BZh91AY&SY......
00000010: 1fff fffe 7ffb cfaf 7f9e fff7 eeff dfbf  ................
00000020: f7fe f7dd be9d b7bf 9f9f 5fca 6fff fed6  .........._.o...
00000030: fbfe ffb0 013a b304 0340 d000 0000 d001  .....:...@......
00000040: a003 d400 0003 4641 a190 0000 0019 0001  ......FA........
00000050: 9006 8681 91a3 2613 400c 8c4d 0f4d 4c44  ......&.@..M.MLD
00000060: 0346 8d0d 1a00 01a6 8680 0001 a064 6268  .F...........dbh
00000070: 6868 0000 068f 5000 d01a 069a 0cd4 068c  hh....P.........
00000080: 8018 9a68 3464 d006 4d00 003a 681a 34d0  ...h4d..M..:h.4.
00000090: 0d00 01a1 a191 a000 0003 234d 0323 4190  ..........#M.#A.
```
From the first line:
`00000000: 425a 6839 3141 5926 5359 be9d 9d96 0000  BZh91AY&SY......`
Refering to the table above, we can see that the header here corresponds to 
a file signature of type `Bzip2`, as it starts with `425a 68`.  

With `original_data` still in its raw form, we can append the `.bz2` suffix, decompress it using `bzip2`, and then display the resulting file.
```bash
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ mv original_data original_data.bz2
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ ls
data.txt  hexdump_data  original_data.bz2  original_data.gz
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ bzip2 -dk original_data.bz2        
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ ls
data.txt  hexdump_data  original_data  original_data.bz2  original_data.gz
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ head -n 1 original_data
%	�3�/bLa4.bin��OH�q��8c�FH��y�w�������<�2�(��:�.%�x��
              �zH���<�I+�~.��s�F
                                ��״F���Q
```
Since the content is still unreadable, let's create a hexdump of it to analyze its contents.  
```bash
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ xxd original_data hexdump_data2
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ head hexdump_data2 
00000000: 1f8b 0808 0933 9f68 0203 6461 7461 342e  .....3.h..data4.
00000010: 6269 6e00 edd1 4f48 9371 18c0 f19f 3863  bin...OH.q....8c
00000020: 9717 4648 d81c eea5 a5c3 0279 df77 efd6  ..FH.......y.w..
00000030: 1f08 d61f 8684 8694 18b3 3cbc 32a4 1528  ..........<.2..(
00000040: ea1b 6811 db3a ac2e 0325 a578 a193 170d  ..h..:...%.x....
00000050: 2509 8a04 0f33 e8ac d382 082f 624c 0c86  %....3...../bL..
00000060: 7a48 87a2 b53c 16e4 492b f87e 2ecf 03cf  zH...<..I+.~....
00000070: 73fb 460c d3f0 d7b4 46db c5fe 510a 02ba  s.F.....F...Q...
00000080: be3b 0b7e 999a fe73 57fd 8a7e 2ae0 5375  .;.~...sW..~*.Su
00000090: 5515 8aaa 6aba 2664 451c 80bb dda6 d125  U...j.&dE......%
```
At this stage, it’s the same process again—we recognize the `gzip` header from before.  
Let's append the `.gz` suffix, decompress it using `gzip`, and then display the resulting file:
```bash
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ mv original_data original_data2.gz
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ gzip -dk original_data2.gz
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ cat original_data2             data5.bin0000644000000000000000000002400015047631411011242 0ustar  rootrootdata6.bin0000644000000000000000000000033615047631411011251 0ustar  ro��V�+�ц��2ԶZ��"2�:%'�t*T���0Y�����i�2'����JR�Y  �ܑN$Wx�
```
We can actually see what looks like two file names in there, `data5.bin` and `data6.bin`. This is a **t**ape **ar**chive `tar`.

Let's append the `.tar` suffix, extract it using `tar`, and then display the resulting file:
```bash
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ mv original_data2 original_data2.tar
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ tar -xf original_data2.tar
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ head data5.bin
data6.bin0000644000000000000000000000033615047631411011251 0ustar  rootrootBZh91AY&SYq]��V�+�ц��2ԶZ��"2�:%'�t*T���0Y�����i�2'����JR�Y  �ܑN$Wx
```
Looks like we have to do it again.
```bash
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ tar -xf data5.bin          
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ ls
data5.bin  data.txt      hexdump_data2      original_data2.tar  original_data.gz
data6.bin  hexdump_data  original_data2.gz  original_data.bz2
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ cat data6.bin
��V�+�ц��2ԶZ��"2�:%'�t*T���0Y�����i�2'����JR�Y  �ܑN$Wx�
```
Because the content remains unreadable, we’ll continue our approach, using hexdumps as needed for analysis.
```bash
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ xxd data6.bin data6hexdump
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ head -n 1 data6hexdump                     
00000000: 425a 6839 3141 5926 5359 715d fde3 0000  BZh91AY&SYq]....
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ mv data6.bin data6.bz2
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ bzip2 -dk data6.bz2 
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ ls
data5.bin  data6hexdump  hexdump_data2       original_data.bz2
data6      data.txt      original_data2.gz   original_data.gz
data6.bz2  hexdump_data  original_data2.tar
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ cat data6
data8.bin0000644000000000000000000000011715047631411011250 0ustar  rootroot�     3�hdata9.bin
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ tar -xf data6.tar
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ ls
data5.bin  data6hexdump  data8.bin  hexdump_data   original_data2.gz   original_data.bz2
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ cat data8.bin
�       3�hdata9.bin
�.6*K	q)w��>�2A1
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ xxd data8.bin
00000000: 1f8b 0808 0933 9f68 0203 6461 7461 392e  .....3.h..data9.
00000010: 6269 6e00 0bc9 4855 2848 2c2e 2ecf 2f4a  bin...HU(H,.../J
00000020: 51c8 2c56 70f3 374d 2977 2b4e 3648 4e4a  Q.,Vp.7M)w+N6HNJ
00000030: f4cc f430 c8b0 f032 4a0d cd2e 362a 4b09  ...0...2J...6*K.
00000040: 7129 77cc e302 003e de32 4131 0000 00    q)w....>.2A1...
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ mv data8.bin data8.gz
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ gzip -dk data8.gz
bandit12@bandit:/tmp/tmp.TEdr4aK3wp$ cat data8
The password is FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```




## Flag 
```bash
FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

## Notes
- `xxd` converts a file to a hexdump allowing for inspection of binary data and can reverse hexdump `-r` back into the original binary data.
- **Magic numbers** are specific byte sequences at the start of a file that identify its type or format e.g. `1F 8B` for `gzip` and `42 5A 68` for `bzip2`.
- `tar`: A utility that bundles multiple files into a single archive.



<p align="center">
<a href="level-13→14.md">Next Level: Level 13 → 14</a>
</p>


