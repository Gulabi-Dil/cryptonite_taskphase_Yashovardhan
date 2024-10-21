# Level Goal
The password for the next level is stored somewhere on the server and has all of the following properties:

- owned by user bandit7
- owned by group bandit6
- 33 bytes in size
### Commands:
```
1) ssh bandit6@bandit.labs.overthewire.org -p 2220
```
Entered the password obtained from Level 5 to login.
```
2) bandit6@bandit:~$ ls
```
`inhere`
```
3) bandit6@bandit:~$ cd inhere && ls -a
```
Nothing of use in `inhere` directory.
```
4) bandit6@bandit:~$ find / -user bandit7 -group bandit6 -size 33c
```
A big list of files was displayed and all of them had permissions denied except 1 i.e. `/var/lib/dpkg/info/bandit7.password`.

_Used the `file` command like in previous level but this time with different specifications as required. `/` is written after `find` which means `find` command will search for the file in `/` directory. I'm currently in the home directory._
```
5) bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
```
Got the password for the next Level.
