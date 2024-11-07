# Description:
Revisit the last transmission. We think this `transmission` contains a hidden message. There are also some clues `clue 1`, `clue 2`, `clue 3`.
# Solution:
Got the three clues using:
```
1) yasho@DESKTOP-6ND4URA:~$ qsstv &
2) yasho@DESKTOP-6ND4URA:~$ pavucontrol &
3) yasho@DESKTOP-6ND4URA:~$ pactl load-module module-null-sink sink_name=virtual-cable
4) yasho@DESKTOP-6ND4URA:~$ paplay -d virtual-cable /mnt/c/Users/hvpan/Downloads/clue1.wav
5) yasho@DESKTOP-6ND4URA:~$ paplay -d virtual-cable /mnt/c/Users/hvpan/Downloads/clue2.wav
6) yasho@DESKTOP-6ND4URA:~$ paplay -d virtual-cable /mnt/c/Users/hvpan/Downloads/clue3.wav
```
![Screenshot (4642)](https://github.com/user-attachments/assets/b16576bf-b98e-43fd-831f-29dff8cb9a3d)

![Screenshot (4643)](https://github.com/user-attachments/assets/66bf7971-238f-4f19-93cd-eaf52182baad)

![Screenshot (4644)](https://github.com/user-attachments/assets/24377cd9-395d-425c-8653-8010a6963e95)

First I looked up Alan Eliasen and turns out its a steganography tool and from the first clue its understood that the passphrase for the transmission audio file is `hidden_stegosaurus`.

```
7) yasho@DESKTOP-6ND4URA:~$ steghide extract -sf messagem00n2.wav -p hidden_stegosaurus
```
Output: `wrote extracted data to "steganopayload12154.txt".`
```
8) yasho@DESKTOP-6ND4URA:~$ cat steganopayload12154.txt
```
#Flag:
>picoCTF{the_answer_lies_hidden_in_plain_sight}

Easyyy but m00nwalks are always fun
