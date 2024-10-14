## Some basic info about permissions:

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

