# cat Command
### **Commands**:
```
1) hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
```  
 ### **Flag**:   
 >pwn.college{UTyxIV8TryQxDTFpSoUEDXeIZrr.dFzN1QDL3cDN0czW}

### **Explanation**: 
Read the file using cat. Here the flag file is locaated in the home directory which is also the cwd hence no need of using paths.

# catting Absolute Paths
### Commands:
```
1) hacker@commands~catting-absolute-paths:~$ cat /flag
```
### Flag: 
>pwn.college{4mWbHEg-OWrXyJwzr9sVQ5Xvwls.dlTM5QDL3cDN0czW}


### Explanation: 
Read the file using cat. Here the flag file is located in the root directory unlike the previous challenge. Thus we had to mention the absolute path to access the file and read its contents.
(In summary, cat flag is for reading file in current directory (relative path) and cat /flag is for reading file in different directory i.e. root directory (absolute path))


# More catting Practice
### Commands:
```
1) hacker@commands~more-catting-practice:~$ cat /usr/lib/rustlib/flag  
```
### Flag: 
>pwn.college{AKqn11NV58U1Fvy6_gWTl8bZEph.dBjM5QDL3cDN0czW}
### Explanation: 
Used the absolute path to access the file in that location and read it using cat.


# Grepping for a needle in haystack
### Commands:
```
1) hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
```
### Flag: 
>pwn.college{04jgsHXfmWLIVh62AzHylOY_Aew.ddTM4QDL3cDN0czW}
### Explanation:
Searched for the search-string in the file which we located using the absolute path.


# Listing files
### Commands:
```
1) hacker@commands~listing-files:~$ cd /challenge
2) hacker@commands~listing-files:/challenge$ ls
Output:- 22403-renamed-run-6849  DESCRIPTION.md
3) hacker@commands~listing-files:/challenge$ /challenge/22403-renamed-run-6849
```
### Flag: 
>pwn.college{ApCWQpK8kON9vTVxr1qaiLgz0w8.dhjM4QDL3cDN0czW}
### Explanation: 
First changed the directory and then ls to see all files contained in it. 


# Touching files
### Commands:
```
1) hacker@commands~touching-files:~$ cd /tmp
2) hacker@commands~touching-files:/tmp$ touch pwn
3) hacker@commands~touching-files:/tmp$ touch college
   
[NOTE: COMMANDS 2 AND 3 CAN BE CLUBBED INTO ONE I.E. hacker@commands~touching-files:/tmp$ touch pwn college. JUST KEEP WRITING THE NAMES OF FILES YOU WANT TO ADD AFTER TOUCH]

5) hacker@commands~touching-files:/tmp$ ls
6) hacker@commands~touching-files:/tmp$ /challenge/run
```
### Flag:
>pwn.college{8cQ0no3jTx1UOYQjiOTil1AeenS.dBzM4QDL3cDN0czW}
### Explanation: 
[NOTE: TMP DIRECTORY IS A TEMPORARY DIRECTORY WHICH STORES DATA FOR A SHORT PERIOD OF TIME. ITS FILES WILL BE DELETED WHEN THE SYSTEM IS REBOOTED.]

First changed the directory to tmp (temporary directory). Then created two files using touch and did ls again to check if addition of files was successful or not. At last, ran the command /challenge/run to get the flag.


# Removing files
### Commands: 
```
1) hacker@commands~removing-files:~$ ls
Output:-  Desktop   delete_me  '~'
2) hacker@commands~removing-files:~$ rm delete_me
3) hacker@commands~removing-files:~$ /challenge/check
```
### Flag: 
>pwn.college{4pJ-mes9xmwvZ4o8Uuc5xkClK3z.dZTOwUDL3cDN0czW}
### Explanation: 
First did ls to check all the files in the home directory then removed the filed delete_me using rm and ran /challenge/check to get flag.


# Hidden Files
### Commands: 
```
1) hacker@commands~hidden-files:~$ cd /
2) hacker@commands~hidden-files:/$ ls 
3) hacker@commands~hidden-files:/$ ls -a
4) hacker@commands~hidden-files:/$ cat .flag-78952281023936
```
### Flag: 
>pwn.college{8WQMREl8vq_hB5e14PqhHiJr6jt.dBTN4QDL3cDN0czW}
### Explanation: 
Changed to root directory, did ls then did ls -a and found the hidden files. REad the hidden flag file using cat.


# An Epic Filesystem Quest
### Commands: 
```
1) hacker@commands~an-epic-filesystem-quest:~$ cd /
2) hacker@commands~an-epic-filesystem-quest:/$ ls
3) hacker@commands~an-epic-filesystem-quest:/$ cat flag
```
Output:- Permission denied.
```
4) hacker@commands~an-epic-filesystem-quest:/$ cat INSIGHT
5) hacker@commands~an-epic-filesystem-quest:/$ cd /usr/local/lib/python3.8/dist-packages/pwnlib/encoders
6) hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/pwnlib/encoders$ ls
7) hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/pwnlib/encoders$ cat INFO
8) hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/pwnlib/encoders$ ls /opt/linux/linux-5.4/include/linux/netfilter
9) hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/pwnlib/encoders$ cat /opt/linux/linux-5.4/include/linux/netfilter/BRIEF-TRAPPED
10) hacker@commands~an-epic-filesystem-quest:/opt/pwndbg/.venv/lib/python3.8/site-packages/plumbum/cli$ cd  /opt/pwndbg/.venv/lib/python3.8/site-packages/plumbum/cli && ls -a
11) hacker@commands~an-epic-filesystem-quest:/opt/pwndbg/.venv/lib/python3.8/site-packages/plumbum/cli$ cat .SECRET
12) hacker@commands~an-epic-filesystem-quest:/opt/pwndbg/.venv/lib/python3.8/site-packages/plumbum/cli$ cd /usr/share/emacs/26.3/etc/images/custom && ls
13) hacker@commands~an-epic-filesystem-quest:/usr/share/emacs/26.3/etc/images/custom$ cat HINT
14) hacker@commands~an-epic-filesystem-quest:/usr/share/emacs/26.3/etc/images/custom$ cd /opt/linux/linux-5.4/include/config/check && ls
15) hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/include/config/check$ cat NOTE
16) hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/include/config/check$ cd  /opt/busybox/busybox-1.33.2/include/config/feature/insmod/try && ls -a
17) hacker@commands~an-epic-filesystem-quest:/opt/busybox/busybox-1.33.2/include/config/feature/insmod/try$ cat .SPOILER
18) hacker@commands~an-epic-filesystem-quest:/opt/busybox/busybox-1.33.2/include/config/feature/insmod/try$ cd /usr/share/javascript/mathjax/jax/output/SVG/fonts/Gyre-Termes/Symbols/Regular && ls
19) hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/jax/output/SVG/fonts/Gyre-Termes/Symbols/Regular$ cat LEAD
20) hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/jax/output/SVG/fonts/Gyre-Termes/Symbols/Regular$ cd /opt/aflplusplus/frida_mode/test/cmplog && ls
21) hacker@commands~an-epic-filesystem-quest:/opt/aflplusplus/frida_mode/test/cmplog$ cat WHISPER
```
### Flag: 
>pwn.college{YkhdBFikovVzSJv4T3cw8q41N3M.dljM4QDL3cDN0czW}
### Explanation: 
Kept on changing directories and doing ls and ls -a to find the clue files and used cat to read them. 

[NOTE: `&&` CAN BE USED TO PERFORM `MULTIPLE` OPERATIONS IN 1 COMMAND.]

**EXAMPLE 1**: `cd /path && ls` 

**EXAMPLE 2**: `cd /path && ls && cat file_name`

Basically its changing the directory AND doing ls and in second its ALSO reading a file whose name we already know. THIS HELPS IN REDUCING THE LINES OF CODE AND IS EFFICIENT.

`NOTE: && WILL  PERFORM THE COMMAND ON ITS RIGHT` **_IF AND ONLY IF_** `THE COMMAND ON ITS LEFT IS PERFORMED SUCCESSFULLY. FOR MORE DETAILS, REFER TO` [THIS](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/506c982c9505ad48f194f7f04e4715d880d63698/Operators%20differences%20(extra).md)


# Making Directories
### Commands: 
```
1) hacker@commands~making-directories:~$ cd /tmp
2) hacker@commands~making-directories:/tmp$ mkdir pwn && ls
3) hacker@commands~making-directories:/tmp$ cd pwn
4) hacker@commands~making-directories:/tmp/pwn$ touch college && ls
5) hacker@commands~making-directories:/tmp/pwn$ /challenge/run
```
(All these commands can be done in a single line as well: hacker@commands~making-directories:\~$ cd /tmp && ls && mkdir pwn && ls && cd pwn && touch college && /challenge/run But I guess it may be confusing in later stages where we solve big and complex codes)

[NOTE: When we do mkdir and cd after mkdir, we don't use / because we are adding the directory in the cwd. If we write / it means we are trying to add the directory in the root directory which requires superuser (root) permissions]

### Flag: 
>pwn.college{wGuoBQQN5sf7-zJ0Ulns097c5CN.dFzM4QDL3cDN0czW}
### Explanation: 
Created a directory pwn in /tmp and created a file in it.

# Finding Files
### Commands:
```
1) hacker@commands~finding-files:~$ find -nme flag
2) hacker@commands~finding-files:~$ cd /
3) hacker@commands~finding-files:/$ find -name flag
```
Output is a big list of directories and files, most of which deny access and as mentioned in the challenge, the flag isn't present there. Towards the end there are a few paths of which one is a file. Keep checking every path using cd first until you reach the one which isn't a directory. cat the file and it will give the flag. BUT we didn't know which path is of directory or file so we have to check all of them and their contents initially.
```
4) hacker@commands~finding-files:/$ cat /usr/lib/python3/dist-packages/jedi/third_party/typeshed/stdlib/3/http/flag
```
### Flag: 
>pwn.college{ci7Ktk-H6n7PALLUMJc2y4kdCBD.dJzM4QDL3cDN0czW}
### Explanation: First check for files or directories named flag in \~. Since no output, cd to root directory and check. Rest of the steps are mentioned above.

# Linking Files
### Commands: 
```
1) hacker@commands~linking-files:~$ /flag
```
Output: ssh-entrypoint: /flag: Permission denied
```
2) hacker@commands~linking-files:~$ /challenge/catflag
```
Output:

About to read out the /home/hacker/not-the-flag file!

cat: /home/hacker/not-the-flag: No such file or directory
```
3) hacker@commands~linking-files:~$ ln -s /flag ~/not-the-flag
4) hacker@commands~linking-files:~$ /challenge/catflag
```
### Flag:
>pwn.college{MlH0LP6b4oFDx4ivhx2ra9sqJyo.dlTM1UDL3cDN0czW}
### Explanation:
/flag has no perissions to access it but it contains the flag. Also, as mentioned in the descritpion of the challenge, the command /challenge/catflag is programmed with permission to read the /home/hacker/not-the-flag file. Thus, I created a symlink (soft link) to /flag using `ln -s og_file's_name symlink's_name`. This file /home/hacker/not-the-flag "pretends" to be /flag. Ran the command /challenge/catflag which read the home hacker file and got the flag.

## Some References:
- [Hard and Soft Links in Linux](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/edit/main/Extra%20topics.md#file-linking-in-unix-like-systems)
