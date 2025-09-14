<p align="center">
<a href="level-8→9.md">Previous Level: Level 8 → 9</a>
</p>

# [Bandit Level 9 → 10](https://overthewire.org/wargames/bandit/bandit10.html)

## Login Info
- **SSH:** `ssh bandit.labs.overthewire.org -p 2220 -l bandit9`
- **Password:** `4CKMh1JI91bUIZZPXDqGanal4xvAg0JM`

---

## Task 
The goal of this level is to find the flag in **data.txt** in one of the few human-readable strings, **preceded by several ‘=’ characters**.

## Steps

Let's print out the first line to get a feel of what the contents is like by using `head` and specifying `-n 1` for one line.
```bash
bandit9@bandit:~$ head -n 1 data.txt                                            
�s�z���tvFJg����9
��H������r�      �Bz������7��.ؓs�Z�@���E���p\�J��
           G5*M'Jg��[�JuA���V��0��B��H��G��KY��
                                               �e��c���sE>Id#{��#��0)�g�b��%�<��
                                                                               ��'EB�� >-��RpV�RhG�Y6�׿ʝ�4bo`K��݊��~����O"��f��zg��%���0�����a������^�����dԂS�}��&��B�Yk�Q���VN5ZTH��R�ec���ԌG�+�~�����}�Ax�fR��VK����|��F%�%����.}���5�6�a�0�`���Y�׫�$`��2�X���O�懤"�j.;����w�7\4�\�]�4/���9~T4��4��օ��Ze�ŗ�Q�:c
                                                                ���O�S�
                                                                      ���_
                                                                          [�LkoVw��d�0q�j��`�D
              �pA�s�r���е�G��_i�*�`j�dI�/���[W���v-�$.`[۪"���򂀘�>K3Z�9B�p2��7h���F�
```
Since the file contains non-text(binary) data, the terminal tried to display it as text, resulting in weird unintelligible symbols.
To extract the human-readable text, we can use the `strings` command.    
The `strings` command scans a file and prints sequences of printable **ASCII or Unicode chracters.**

Let's use the `strings` command and pipe the output to `grep` several **'='** characters:
```bash
bandit9@bandit:~$ strings data.txt | grep "===="
========== theg
========== password
========== is
========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

## Flag 
```bash
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

## Notes
- `strings` extracts readable text from binary files, ignoring non-printable bytes.



<p align="center">
<a href="level-10→11.md">Next Level: Level 10 → 11</a>
</p>

