# Level Goal
The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.
### Commands:
```
1) ssh bandit4@bandit.labs.overthewire.org -p 2220
```
Entered the password obtained from Level 3 to login.
```
2) bandit3@bandit:~$ ls
```
`inhere`
```
3) bandit3@bandit:~$ cd inhere && ls
```
Output:

`-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09`

_Same problem like the `-` file. Once again, used the relative path of the file to cat it. Kept catting every file from the beginnning until I found the human-readable (i.e. normal alphanumeric characters) password._

```
4) bandit4@bandit:~/inhere$ cat ./-file07
```
Got the password for next Level.
