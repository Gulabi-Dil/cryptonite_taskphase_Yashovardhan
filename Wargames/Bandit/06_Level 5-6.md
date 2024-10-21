# Level Goal
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

- human-readable
- 1033 bytes in size
- not executable
### Commands:
```
1) ssh bandit5@bandit.labs.overthewire.org -p 2220
```
Entered the password obtained from Level 4 to login.
```
2) bandit5@bandit:~$ ls
```
`inhere`
```
3) bandit5@bandit:~$ cd inhere && ls
```
Output:

`maybehere00  maybehere02  maybehere04  maybehere06  maybehere08  maybehere10  maybehere12  maybehere14  maybehere16  maybehere18`

`maybehere01  maybehere03  maybehere05  maybehere07  maybehere09  maybehere11  maybehere13  maybehere15  maybehere17  maybehere19`
```
4) bandit5@bandit:~/inhere$ find -type f -size 1033c
```
Output: 

`./maybehere07/.file2`
```
5) bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
```

Since there are way too many directories and I don't know where the required file is located in, I used the `find` command.

The **syntax** of the `find` command is: ``find [path] [options] [expression]``

Didn't write anything in path because I don't the location of the file and I'm in the parent directory anyway. `find` will search for the file in the entire parent directory. In options, I wrote `-type f` to specify and let bash know that it has to look for a **file** whose size is 1033 bytes (this `option` isn't really needed here but will be required when there is more than just a file which is of the same size.). In `-size 1033c`, `-size` specifies the size of the file I'm searching for and `1033c` means I'm looking for files that are exactly 1033 bytes in size.
The `c` stands for _**bytes**_. Without the `c`, the size would be interpreted in blocks, a basic unit of storage on a filesystem (typically 512 bytes per block).
### Some References:
[find command in Linux](https://www.geeksforgeeks.org/find-command-in-linux-with-examples/)
