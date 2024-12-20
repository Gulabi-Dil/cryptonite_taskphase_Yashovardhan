# Description:
Can you handle APKs?
Download the android apk `here`.

# Solution:
Downloaded the apk file and it was jut apk file, not in the form of a zip folder so I had to use this [site](http://www.javadecompilers.com/apk) for disassembling the apk file.
I had also opened the apk file using notepad and obviously searched words like pico, flag etc. and surprisingly enough, the word flag was indeed present! It was the path of the file `flag.txt`: res/color/flag.txt

So, now that I know the file's path I just followed it on the website where I had decompiled the apk. `flag.txt` contents: 
```
7069636f4354467b6178386d433052553676655f4e5838356c346178386d436c5f37303364643965667d
```
I converted this hex data to ascii and got the flag.
# Flag:
>picoCTF{ax8mC0RU6ve_NX85l4ax8mCl_703dd9ef}
