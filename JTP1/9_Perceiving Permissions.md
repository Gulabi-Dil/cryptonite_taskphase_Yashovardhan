## Some basic info about permissions:
-[File types](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#file-types)
-[Understanding file permissions](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#understanding-file-permissions)
# Channging File Ownership
### Commands:
```
1) hacker@permissions~changing-file-ownership:~$ cat /flag
```
Output: Permission denied
```
2) hacker@permissions~changing-file-ownership:/$ cd / && ls -l
```
Output: A big list of files and directories under the root directory was displayed among which was

`-r--------    1 root root   58 Oct 20 12:48 flag`
```
3) hacker@permissions~changing-file-ownership:/$ chown hacker /flag
4) hacker@permissions~changing-file-ownership:/$ cat /flag
```
### Flag: 
>pwn.college{cAfKNJRihfR_XFEqG-TeSlIZ3vA.dFTM2QDL3cDN0czW}
### Explanation:
`chown` changes the ownership of a file hence affecting its permissions as well.

# Groups and Files
### Commands:
```
1) hacker@permissions~groups-and-files:~$ cd / && ls -l
```
Output: A big list of files and directories under the root directory was displayed among which was

`-r--r-----    1 root root   58 Oct 14 05:40 flag`.
```
2) hacker@permissions~groups-and-files:/$ cat flag
```
Output: 

cat: flag: Permission denied
```
3) hacker@permissions~groups-and-files:/$ chgrp hacker flag
4) hacker@permissions~groups-and-files:/$ cat flag
```
### Flag:
>pwn.college{4YQytfikPEdMPELqdrOBKo5x5HE.dFzNyUDL3cDN0czW}
### Explanation:
We already know about the `ls` command. `-l` will display the output of `ls` in a long list format. Since the permission of flag file is with the root, simply catting the file as hacker user won't work. Thus, changed its group from root to hacker and read the file.

# Fun with Group Names
### Commands:
```
1) hacker@permissions~fun-with-groups-names:~$ id
```
Output:

`uid=1000(hacker) gid=1000(grp15373) groups=1000(grp15373)`

_This gave us the group name we're in because it's not hacker in this challenge._
```
2) hacker@permissions~fun-with-groups-names:~$ cd / && ls -l
3) hacker@permissions~fun-with-groups-names:/$ cat flag
```
Output:2) Same list as previous challenge. 3) Same output as previous challenge
```
4) hacker@permissions~fun-with-groups-names:/$ chgrp grp15373 flag
5) hacker@permissions~fun-with-groups-names:/$ cat flag
```
### Flag:
>pwn.college{4NBtGJUXRzjUyqalQGWY0zqBkWM.dJzNyUDL3cDN0czW}
### Explanation:
Same as previous challenge but we are not in the hacker group. So, to know the name of group I'm in, I used `id` which diplayed my group name.

# Changing Permissions
### Commands:
```
1) hacker@permissions~changing-permissions:~$ cd / && ls -l
```
Output: A big list of files and directories under the root directory was displayed among which was

`-r--------    1 root root   58 Oct 15 05:53 flag`

_The `r` means that file is `readable` by the root user `ONLY`. The `-` in the rest of the permission details denote that there's no other permission for user,group and other users/world._
```
2) hacker@permissions~changing-permissions:/$ cat flag
```
Output: 

cat: flag: Permission denied

_Since I'm not the root user, I can't read the file._
```
3) hacker@permissions~changing-permissions:/$ chmod o+r flag
4) hacker@permissions~changing-permissions:/$ cat flag
```
### Flag:
>pwn.college{0c-44nZxOy-C6r7UiNPA6zEXKIi.dNzNyUDL3cDN0czW}
### Explanation: 
Initial explanation done above. The command `chmod` changes the permissions of a file. The synatx is `chmod [OPTIONS] MODE FILE`. 

`Options` is where we will specify whom we are giving to or taking permissions from and what permissions they are. `+` will add a permission whereas `-` will remove a permission. We can specify multiple at once. For example: 

`u+r` adds read access to the user's permissions
`g+wx` adds write and execute access to the group's permissions
`o-w` removes write access for other users
`a-rwx` removes all permissions for the user, group, and world

We can also put u,g or o all at once like `ug+rw`.

**NOTE: TYPICALLY, YOU NEED TO HAVE WRITE ACCESS TO THE FILE IN ORDER TO CHANGE ITS PERMISSIONS. In this challenge, though, chmod is made all-powerful.**

# Executable Files
### Commands:
```
1) hacker@permissions~executable-files:/$ cd / && ls -l
```
Output: 

Output: A big list of files and directories under the root directory was displayed among which was

`drwxr-xr-x    1 root root 4096 Oct 15 06:11 challenge`
```
2) hacker@permissions~executable-files:/$ /challenge/run
```
Output:

ssh-entrypoint: /challenge/run: Permission denied
```
2) hacker@permissions~executable-files:/$ chmod u+x /challenge/run
3) 2) hacker@permissions~executable-files:/$ /challenge/run
```
### Flag:
>pwn.college{0T2_LGnEHKre7ZKUO2jSWpMG4rB.dJTM2QDL3cDN0czW}
### Explanation:
The permission to execute is not present so we need to add this permission to the hacker user. The user and group of /challenge/run are hacker and hacker (checked by going to challenge directory and doing ls -l).

The command `chmod u+x /challenge/run` will add the permission of executing the `run` file.

# Permission Tweaking Practice
### Commands:
```
1) hacker@permissions~permission-tweaking-practice:~$ /challenge/run
```
Current: `rw-r--r--`    Needed: `rw-rw-r--`
```
2) hacker@permissions~permission-tweaking-practice:~$ chmod g+w /challenge/pwn
```
Current: `rw-rw-r--`    Needed: `-w--w-r--`
```
3) hacker@permissions~permission-tweaking-practice:~$ chmod ug-r /challenge/pwn
```
Current: `-w--w-r--`    Needed: `------r--`
```
4) hacker@permissions~permission-tweaking-practice:~$ chmod ug-w /challenge/pwn
```
Current: `------r--`    Needed: ` r-xr-xr-x`
```
5) hacker@permissions~permission-tweaking-practice:~$ chmod ugo+rx /challenge/pwn
```
Current: ` r-xr-xr-x`    Needed: ` rwxrwxrwx`
```
6) hacker@permissions~permission-tweaking-practice:~$ chmod a+w /challenge/pwn
```
Current: ` rwxrwxrwx`    Needed: `rwxrw-rw-`
```
7) hacker@permissions~permission-tweaking-practice:~$ chmod go-x /challenge/pwn
```
Current: `rwxrw-rw-`    Needed: `rwx------`
```
8) hacker@permissions~permission-tweaking-practice:~$ chmod go-rwx /challenge/pwn
```
Current: `rwx------`    Needed: `-w-------`
```
9) hacker@permissions~permission-tweaking-practice:~$ chmod u-rx /challenge/pwn
```
Output:

You set the correct permissions!

You've solved all 8 rounds! I have changed the ownership

of the /flag file so that you can 'chmod' it. You won't be able to read

it until you make it readable with chmod!

Current permissions of "/flag": `---------`
```
10) hacker@permissions~permission-tweaking-practice:~$ chmod u+r /flag
11) hacker@permissions~permission-tweaking-practice:~$ cat /flag
```
### Flag:
>pwn.college{QGUr0BW3-1e5kpvKs4b2iG4LK30.dBTM2QDL3cDN0czW}
### Explanation:
Kept changing permissions as per the prompts.


# Permissions Setting Practice
### Commands:
```
1) hacker@permissions~permission-tweaking-practice:~$ /challenge/run
```
Current: ` rw-r--r--`    Needed: `---rw--wx`
```
2) hacker@permissions~permission-tweaking-practice:~$ chmod u=-,g=rw,o=wx /challenge/pwn
```
Current: `---rw--wx`    Needed: `-wxr--r--`
```
3) hacker@permissions~permission-tweaking-practice:~$ chmod u=wx,g=r,o=r /challenge/pwn
```
Current: `-wxr--r--`    Needed: `rw-rw-r-x`
```
4) hacker@permissions~permission-tweaking-practice:~$ chmod u=rw,g=rw,o=rx /challenge/pwn
```
Current: `rw-rw-r-x`    Needed: `rwxrwxr-x`
```
5) hacker@permissions~permission-tweaking-practice:~$ chmod u=rwx,g=rwx,o=rx /challenge/pwn
```
Current: `rwxrwxr-x`    Needed: `---rw-rwx`
```
6) hacker@permissions~permission-tweaking-practice:~$ chmod u=-,g=rw,o=rwx /challenge/pwn
```
Current: `---rw-rwx`    Needed: `r-x---r--`
```
7) hacker@permissions~permission-tweaking-practice:~$ chmod u=rx,g=-,o=r /challenge/pwn
```
Current: `r-x---r--`    Needed: `r---wx-wx`
```
8) hacker@permissions~permission-tweaking-practice:~$ chmod u=r,g=wx,o=wx /challenge/pwn
```
Current: `r---wx-wx`    Needed: `---rwxrw-`
```
9) hacker@permissions~permission-tweaking-practice:~$ chmod u=-,g=rwx,o=rw /challenge/pwn
```
Output:

You set the correct permissions!

You've solved all 8 rounds! I have changed the ownership

of the /flag file so that you can 'chmod' it. You won't be able to read

it until you make it readable with chmod!

Current permissions of "/flag": `---------`
```
10) hacker@permissions~permission-tweaking-practice:~$ chmod u=r /flag
11) hacker@permissions~permission-tweaking-practice:~$ cat /flag
```
### Flag:
>pwn.college{Aw-BhwqnG0eld24jJA6Xr42X0BI.dNTM5QDL3cDN0czW}
### Explanation:
In addition to adding and removing permissions, as in the previous level, `chmod` can also simply set permissions altogether, overwriting the old ones. This is done by using `=` instead of `-` or `+`. For example:

- `u=rw` sets read and write permissions for the user, and wipes the execute permission
- `o=x` sets only executable permissions for the world, wiping read and write
- `a=rwx` sets read, write, and executable permissions for the user, group, and world!

We can **chain multiple modes by using `,`. This will come in handy when we want to set different permissions for user, group and other users respectively.**

Example:
`chmod u=rw,g=r /challenge/pwn` will set the user permissions to read and write, and the group permissions to read-only.

`chmod a=r,u=rw /challenge/pwn` will set the user permissions to read and write, and the group and world permissions to read-only.

Additionally, you can zero out permissions with `-`:

`chmod u=rw,g=r,o=- /challenge/pwn` will set the user permissions to read and write, the group permissions to read-only, and the world permissions to nothing at all.

**NOTE: IF `-` IS USED AFTER `=` THEN IT WILL ZERO OUT ALL PERMISSIONS OF USER/GROUP/OTHER USERS. IF `-` IS USED IMMEDIATELY AFTER `u`,`g` or `o`, IT WILL REMOVE SPECIFIC BITS OF THE PERMISSION (LIKE WE SAW IN PREVIOUS CHALLENGE).**

# The SUID bit
### Commands:
```
1) hacker@permissions~the-suid-bit:~$ cd /challenge && ls -l
```
Output: A list of files and directories under the challenge directory was displayed among which was

`-rwxr-xr-x 1 root root  155 Jul 12 10:30 getroot`
```
2) hacker@permissions~the-suid-bit:/challenge$ cat /flag
```
cat: /flag: Permission denied
```
3) hacker@permissions~the-suid-bit:/challenge$ chmod u+s /challenge/getroot
4) hacker@permissions~the-suid-bit:/challenge$ /challenge/getroot
```
Output:

SUCCESS! You have set the suid bit on this program, and it is running as root!

Here is your shell...

`root@permissions~the-suid-bit:/challenge#`
```
5) root@permissions~the-suid-bit:/challenge# cat /flag
```
### Flag:
>pwn.college{o7rPLPMRfc57XNawJoUoAgDdCUP.dNTM2QDL3cDN0czW}
### Explanation:
Already explained everything in detail [here](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#setuid)

After setting the setuid to the program /challenge/getroot followed by running it, a root shell was initiated which gave me

### Some references:
[chown command](https://www.geeksforgeeks.org/chown-command-in-linux-with-examples/)
