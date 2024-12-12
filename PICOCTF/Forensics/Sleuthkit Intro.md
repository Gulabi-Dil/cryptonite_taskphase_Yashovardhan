# Description
Download the disk image and use mmls on it to find the size of the Linux partition. Connect to the remote checker service to check your answer and get the flag.

Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.

`Download disk image`

Access checker program: nc saturn.picoctf.net 51215
# Solution:
It was a gz compressed file so decompressed it first using `gzip -d disk.img.gz` and then did `mmls disk.img` which gave info about partitions of the disk:
```
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000204799   0000202752   Linux (0x83)
```
The size of the Linux partition is given in the length column i.e. 202752. 

Now according to the question, I ran the nc command: `nc saturn.picoctf.net 51215` and it asked for input interactively:
```
What is the size of the Linux partition in the given disk image?
Length in sectors: 202752
```
Output: 

`Great work!`

`picoCTF{mm15_f7w!}`

# Flag:
>picoCTF{mm15_f7w!}
