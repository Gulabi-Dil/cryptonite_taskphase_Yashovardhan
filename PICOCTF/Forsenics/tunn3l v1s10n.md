# Description:
We found this `file`. Recover the flag.
# Solution:
First checked the file type and the hex header data:
```
yasho@DESKTOP-6ND4URA:~$ file /mnt/c/Users/hvpan/Downloads/tunn3l_v1s10n
/mnt/c/Users/hvpan/Downloads/tunn3l_v1s10n: data
yasho@DESKTOP-6ND4URA:~$ hexdump -C /mnt/c/Users/hvpan/Downloads/tunn3l_v1s10n | head
00000000  42 4d 8e 26 2c 00 00 00  00 00 ba d0 00 00 ba d0  |BM.&,...........|
00000010  00 00 6e 04 00 00 32 01  00 00 01 00 18 00 00 00  |..n...2.........|
00000020  00 00 58 26 2c 00 25 16  00 00 25 16 00 00 00 00  |..X&,.%...%.....|
00000030  00 00 00 00 00 00 23 1a  17 27 1e 1b 29 20 1d 2a  |......#..'..) .*|
00000040  21 1e 26 1d 1a 31 28 25  35 2c 29 33 2a 27 38 2f  |!.&..1(%5,)3*'8/|
00000050  2c 2f 26 23 33 2a 26 2d  24 20 3b 32 2e 32 29 25  |,/&#3*&-$ ;2.2)%|
00000060  30 27 23 33 2a 26 38 2c  28 36 2b 27 39 2d 2b 2f  |0'#3*&8,(6+'9-+/|
00000070  26 23 1d 12 0e 23 17 11  29 16 0e 55 3d 31 97 76  |&#...#..)..U=1.v|
00000080  66 8b 66 52 99 6d 56 9e  70 58 9e 6f 54 9c 6f 54  |f.fR.mV.pX.oT.oT|
00000090  ab 7e 63 ba 8c 6d bd 8a  69 c8 97 71 c1 93 71 c1  |.~c..m..i..q..q.|
```
The file command didn't give any useful info tbh but the header file mentions BM implying that its a bmp file. So I changed the extension of the file to `.bmp` and tried opening it but it didn't open, saying that the format isn't supported. Since I have solved a few challenges like these before, I used hex editor and googled, asked chatgpt to give me the magic bytes for `.bmp` files. Took a while to get the correct bytes TT

Changed the bytes accordingly.

![WhatsApp Image 2024-12-12 at 15 04 09_c3a1f8c4](https://github.com/user-attachments/assets/34f8be6c-99c5-40f8-bf1f-873ecbe99022)

Saved the file and opened it. It was showing this image:

![WhatsApp Image 2024-12-12 at 15 06 01_03098a02](https://github.com/user-attachments/assets/9dec4c8e-af84-4ca6-b7e6-97b95f83a579)

The color combination is so weird I thought I'm wearing 3D glasses bruh

Anyways, didn't really get the flag. After pondering for a good while, I remembered something that chatgpt mentioned about the height and width of the image, i.e. the dimensions. Quickly looked it up and got the bytes for adjusting the size. Modified accordingly:

![WhatsApp Image 2024-12-12 at 15 03 26_ffbba36e](https://github.com/user-attachments/assets/e79e9843-183a-4cc0-b705-5700d0f6f0fa)

Then opened the image and yayyayayya got the flag!

![WhatsApp Image 2024-12-12 at 15 09 13_72750ab8](https://github.com/user-attachments/assets/5d9bb9d5-399f-4f64-b45e-9ab7ce033dc3)

# Flag:
>picoCTF{qu1t3_a_v13w_2020}
