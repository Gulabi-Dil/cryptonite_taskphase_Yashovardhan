# Level Goal
The password for the next level is stored in a file called - located in the home directory.
### Commands:
```
1) ssh bandit1@bandit.labs.overthewire.org -p 2220
```
**NOTE: We need to login to every new level using `SSH`. To logout from the current server, use the command `exit` then login to the required server using the above command (username changes accordingly)**
```
2) bandit1@bandit:~$ ls
```
Output:
`-`
```
3) bandit1@bandit:~$ cat -
```
^C
_There was no output since the hyphen was interpreted as the symbol used to write **OPTIONS**, instead of the file name `-`. Since, the command was incomplete, shell was awaiting user input and hence exhibited blocking behavior, which was stopped using `Ctrl + C`._
```
4) bandit1@bandit:~$ cat ./-
```
_Used the relative path of the file `-` so that `-` is interpreted as a file name and not the symbol for OPTIONS._
### References provided:
[Special Characters in Linux](https://linux.die.net/abs-guide/special-chars.html)
