# Level Goal
The password for the next level is stored in a hidden file in the inhere directory.
### Commands:
```
1) ssh bandit3@bandit.labs.overthewire.org -p 2220
```
Entered the password obtained from Level 2 to login.
```
2) bandit3@bandit:~$ ls
```
`inhere`
```
3) bandit3@bandit:~$ cd inhere
4) bandit3@bandit:~/inhere$ ls
5) bandit3@bandit:~/inhere$ ls -a
```
Output: 

`...Hiding-From-You`
```
6) bandit3@bandit:~/inhere$ cat ...Hiding-From-You
```
_NOTE: `...` is included in the name of the file._

