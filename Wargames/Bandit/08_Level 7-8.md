# Level Goal
The password for the next level is stored in the file data.txt next to the word "millionth".
### Commands:
```
1) ssh bandit7@bandit.labs.overthewire.org -p 2220
```
Entered the password obtained from Level 6 to login.
```
2) bandit7@bandit:~$ ls
```
`data.txt`
```
3) bandit7@bandit:~$ grep millionth data.txt
```
Output: 

`millionth       dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc`

Got the password for next Level.
