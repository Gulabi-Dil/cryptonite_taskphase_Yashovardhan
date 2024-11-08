# Description:
You will find the flag after decrypting this file
Download the encrypted flag `here`.
# Solution:
Encrypted Flag is: `xqkwKBN{z0bib1wv_l3kzgxb3l_949in1i1}`
Since the name itself says rotation and the encrypted flag is also suggesitng that, I tried ROT13ing it first.
```
1) yasho@DESKTOP-6ND4URA:~$ echo "xqkwKBN{z0bib1wv_l3kzgxb3l_949in1i1}" | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```
Output: `kdxjXOA{m0ovo1ji_y3xmtko3y_949va1v1}`

Didn't work so I checked the number of shifts by comparing K of KBN with C of CTF. The shift is 18 alphabets so I revised the rotation.
```
2) yasho@DESKTOP-6ND4URA:~$ echo "xqkwKBN{z0bib1wv_l3kzgxb3l_949in1i1}" | tr 'A-Za-z' 'S-ZA-Rs-za-r'
```
And it worked. Ez
# Flag:
>picoCTF{r0tat1on_d3crypt3d_949af1a1}
