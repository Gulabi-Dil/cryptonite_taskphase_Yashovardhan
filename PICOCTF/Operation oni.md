# Description:
Download this disk image, find the key and log into the remote machine.

Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.

`Download disk image`

Remote machine: `ssh -i key_file -p 55718 ctf-player@saturn.picoctf.net`

# Solution:
I downloaded the attachment first and it was named `disk.img.gz` means its a compressed file so I decompressed it.
```
1) yasho@DESKTOP-6ND4URA gzip -d /mnt/c/Users/hvpan/Downloads/disk.img.gz
2) yasho@DESKTOP-6ND4URA file /mnt/c/Users/hvpan/Downloads/disk.img
```
Output:

`/mnt/c/Users/hvpan/Downloads/disk.img: DOS/MBR boot sector; partition 1 : ID=0x83, active, start-CHS (0x0,32,33), end-CHS (0xc,223,19), startsector 2048, 204800 sectors; partition 2 : ID=0x83, start-CHS (0xc,223,20), end-CHS (0x1d,81,52), startsector 206848, 264192 sectors`

Didn't understand much but it definitely isn't just a single file seeing it has partitions so asked Chatgpt about it. It said that it's a disk so I tried looking up info about disks in linux. Will have to understand a lot in depth so I just glanced over the required stuff for now. Disk is a storage space and it’s often split into partitions—kind of like dividing a warehouse into separate rooms, each for a specific purpose (like the OS, user files, or backup). You can then set up a **filesystem** on each partition to organize files and folders.

_Note: I was confusing filesystem with disk before. Filesystem is just the way of organizing files and directories for efficient access whereas disk is a storage space._ 

I looked up methods to access contents of disk on google but search results were very vast so I used chatgpt to explain. Now, accessing can be done with or without mounting. 

**_Mounting is the process of making a storage device, like a disk or USB drive, accessible in your computer’s filesystem so that you can view and interact with its contents. When you mount a disk in Linux, you're essentially telling the operating system where to "attach" that device so it can be used as part of the directory structure._**

Was very confused at first so I had created a new separate directory for any such challenges I may encounter in CTFs later, followed by moving `disk.img` to `/mnt/CTFSpace`.
```
3) yasho@DESKTOP-6ND4URA sudo mkdir /mnt/CTFSpace
4) yasho@DESKTOP-6ND4URA sudo mv /mnt/c/Users/hvpan/Downloads/disk.img /mnt/CTFSpace
```

![WhatsApp Image 2024-11-08 at 08 38 58_6f27085e](https://github.com/user-attachments/assets/1705936f-d1d8-4432-8c15-3bdc89e286e3)

This showed the partitions of the disk but not of much use.

Mounting was a bit confusing so I just searched how to access a disk without mounting and found out about sleuthkit. The Sleuth Kit is a library and collection of Unix- and Windows-based utilities for extracting data from disk drives and other storage so as to facilitate the forensic analysis of computer systems.

Looked up its commands
```
5) yasho@DESKTOP-6ND4URA:~$ sudo apt install sleuthkit
```

![image](https://github.com/user-attachments/assets/561fcb13-72f7-4d24-8fec-eaf96aa29308)

```
6) yasho@DESKTOP-6ND4URA:~$ fls -o 206848 /mnt/CTFSpace/disk.img 470
```
Output: 

`r/r 2344:       .ash_history`

`d/d 3916:       .ssh`
```
7) yasho@DESKTOP-6ND4URA:~$ fls -o 206848 /mnt/CTFSpace/disk.img 3916
```
Output: 

`r/r 2345:       id_ed25519`

`r/r 2346:       id_ed25519.pub`
```
8) yasho@DESKTOP-6ND4URA:~$ icat -o 206848 /mnt/CTFSpace/disk.img 2345
9) yasho@DESKTOP-6ND4URA:~$ icat -o 206848 /mnt/CTFSpace/disk.img 2346
10) yasho@DESKTOP-6ND4URA:~$ icat -o 206848 /mnt/CTFSpace/disk.img 2345 > output.txt
11) yasho@DESKTOP-6ND4URA:~$ chmod 600 output.txt
```

![image](https://github.com/user-attachments/assets/df6707e1-698f-4b9b-a244-a7ec8a638a91)

# Flag:
>picoCTF{k3y_5l3u7h_af277f77}

Will explore more about all this in depth later

# References/to be read:
[Sleuthkit](https://www.kali.org/tools/sleuthkit/)

Chatgpt
