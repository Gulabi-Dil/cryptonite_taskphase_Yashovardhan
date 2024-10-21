# Level Goal
The password for the next level is stored in a file called spaces in this filename located in the home directory.
### Commands:
```
1)  ssh bandit2@bandit.labs.overthewire.org -p 2220
```
Entered the password obtained from level 1 to login.
```
2) bandit2@bandit:~$ ls
```
Output:
`spaces in this filename`
```
3) bandit2@bandit:~$ cat spaces in this filename
```
Output:

cat: spaces: No such file or directory

cat: in: No such file or directory

cat: this: No such file or directory

cat: filename: No such file or directory

**_NOTE: Can't use spaces in the arguments because that changes the entire meaning._**
```
4) bandit2@bandit:~$ cat "spaces in this filename"
```
_[can use single quotes also]_

or 
```
4) bandit2@bandit:~$ cat spaces\ in\ this\ filename
```
Got the password for next Level.
### Explanation:
If you have a filename with spaces on a Linux system, wrapping your filename in quote marks (both single and double quotes work) or putting a `\` before the spaces (acts like an escape sequence) lets Bash treat it correctly.
### Some References:
[Filename with spaces](https://linuxhandbook.com/filename-spaces-linux/)
