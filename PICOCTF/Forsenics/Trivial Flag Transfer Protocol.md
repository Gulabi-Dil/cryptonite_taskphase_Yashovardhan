# Description:
Figure out how they moved the flag.
# Hints:
What are some other ways to hide data?
# Solution:

![image](https://github.com/user-attachments/assets/55ea1f96-20b3-4cf3-a03b-441d87eab83a)

_A .pcapng file is a Packet Capture Next Generation data file._

_The .pcapng file format is related to captured data packets over the network. The Packet Capture Next Generation file or the .pcapng file is a standard format for storing captured data._

In the header file, WireShark is mentioned so I looked it up on google and found out that it is a network analyzer that captures and displays network traffic in real time. So, I installed wireshark and opened the challenge's attachment file in it.

Here is how it looks:

![image](https://github.com/user-attachments/assets/5fa1b98c-862e-4688-bcc6-33167fb39dec)

Upon scrolling, I saw that there is TFTP everywhere (and also the challenge's name is trivial flag transfer protocol) so I googled it up and TFTP stands for Trivial File Transfer Protocol (confirmed that it has to do something with TFTP). 

After trying to think of what to do now and exploring the menu etc. I noticed a search bar above the contents of the file which said "Displayy Filter". So, as the name suggests, I typed in tftp and pressed entered which wasn't of any use since it just diplayed all data where tftp is used. So I googled Wireshark Dis[play filter and found out some things. I typed `tftp.` this time which showed a list of available fields. I tried `tftp.data` but no output. Then I tried `tftp.type` and got this

![image](https://github.com/user-attachments/assets/bb7574d6-4a2b-4f82-a090-fb8947b6f7d1)

Hmm it seems like its all the data that I need to use rn so then I looked up how to access files mentioned in wireshark. (file>export objects>TFTP>Save all).

I opened the instructions.txt file which had this text: 

`GSGCQBRFAGRAPELCGBHEGENSSVPFBJRZHFGQVFTHVFRBHESYNTGENAFSRE.SVTHERBHGNJNLGBUVQRGURSYNTNAQVJVYYPURPXONPXSBEGURCYNA`

I thought its some ciphertext and from previous novice ctf experience, I tried ROT13ing it.
```
1) echo GSGCQBRFAGRAPELCGBHEGENSSVPFBJRZHFGQVFTHVFRBHESYNTGENAFSRE.SVTHERBHGNJNLGBUVQRGURSYNTNAQVJVYYPURPXONPXSBEGURCYNA > output.txt
2) tr 'A-Za-z' 'N-ZA-Mn-za-m' < output.txt
```
Output: `TFTPDOESNTENCRYPTOURTRAFFICSOWEMUSTDISGUISEOURFLAGTRANSFER.FIGUREOUTAWAYTOHIDETHEFLAGANDIWILLCHECKBACKFORTHEPLAN`

After obvious spacing, it reads: `TFTP DOESNT ENCRYPT OUR TRAFFIC SO WE MUST DISGUISE OUR FLAG TRANSFER. FIGURE OUT A WAY TO HIDE THE FLAG AND I WILL CHECK BACK FOR THE PLAN`

It mentions "plan" and there's also a file named plan which has this text:

`VHFRQGURCEBTENZNAQUVQVGJVGU-QHRQVYVTRAPR.PURPXBHGGURCUBGBF`

I tried ROT13ing this too.
```
3) yasho@DESKTOP-6ND4URA:~$ echo VHFRQGURCEBTENZNAQUVQVGJVGU-QHRQVYVTRAPR.PURPXBHGGURCUBGBF > output.txt
4) yasho@DESKTOP-6ND4URA:~$ tr 'A-Za-z' 'N-ZA-Mn-za-m' < output.txt
```
Output: `IUSEDTHEPROGRAMANDHIDITWITH-DUEDILIGENCE.CHECKOUTTHEPHOTOS`

Again, after obvious spacing, it reads: `I USED THE PROGRAM AND HID IT WITH-DUE DILIGENCE. CHECKOUT THE PHOTOS`

Now it mentions program and there's also a file named program so I first checked its file type.

![image](https://github.com/user-attachments/assets/41a5b7c6-2b9c-428d-b484-54571ac0a1c8)

Since it said "package" I recalled installing packages using sudo apt install so I tried doing that, during which, one line appears

`Note, selecting 'steghide' instead of '/mnt/c/Users/hvpan/Downloads/program.deb'`

I looked up steghide.

![image](https://github.com/user-attachments/assets/461573ed-d877-41c7-b12b-d85192caa110)

It supports BMP files and when I exported objects of TFTP, there were 3 pictures with this extension so I further looked up how to access hidden data from steghide, for which I first had to install steghide. 

NOTE: steghide extration requires passphrase assigned to the concerned file.
```
5) yasho@DESKTOP-6ND4URA:~$ sudo apt install steghide
```
The command to be used to extract hidden data from the files is: `steghide extract -sf /filepath` (if passphrase is to be entered interactively)  `steghide extract -sf /filepath -p "<passphrase>"` (if passphrase is to be mentioned in the same line as command).

![image](https://github.com/user-attachments/assets/ab9c670a-ae48-478d-be80-2d6204b3bc68)

The statement `I USED THE PROGRAM AND HID IT WITH-DUE DILIGENCE.` suggests that the passphrase would be DUE DILIGENCE. I tried using it but didn't work so I used it without spaces and worked for `picture3.bmp`. Oh btw extension `.bmp` has to be mentioned in the file.

# Flag:
>picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}

# References:
- [Wireshark Display Filters](https://wiki.wireshark.org/DisplayFilters)
- [Steghide](https://steghide.sourceforge.net/)
- [Steganography](https://medium.com/the-kickstarter/steganography-on-kali-using-steghide-7dfd3293f3fa)

![image](https://github.com/user-attachments/assets/59c8e70d-3383-4df9-aa48-a0529ff926b1)

