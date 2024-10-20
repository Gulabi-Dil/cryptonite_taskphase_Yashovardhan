## Some basic info about variables in Linux:
- [Variables in Linux](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#types-of-variables-in-linux)
  
_**NOTE: `PATH` IS AN ENVIRONMENT VARIABLE.**_
# The PATH Variable
### Commands:
```
1) hacker@path~the-path-variable:~$ echo $PATH
```
Output:

`/run/challenge/bin:/run/workspace/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin`
```
2) hacker@path~the-path-variable:~$ PATH=""
3) hacker@path~the-path-variable:~$ echo $PATH
```
Output: _blank output_
```
4) hacker@path~the-path-variable:~$ /challenge/run
```
Output:

Trying to remove /flag...

/challenge/run: line 4: rm: No such file or directory

The flag is still there! I might as well give it to you!
### Flag:
>pwn.college{0lyzZA-3ZC2Gomm3uFyFJ1HMF48.dZzNwUDL3cDN0czW}
### Explanation:
`/challenge/run` actually has a program coded in it which has a line of code using `rm` (_this is confirmed by the final ouptut **/challenge/run: line 4: rm: No such file or directory**_).
When the `run` command is run and when its execution reaches `rm`, it will check the directories in PATH variable for the executable `rm` : if present then it will delete the flag, if not then it won't delete the flag.
Thus, I erased the entire PATH variable's contents so that when execution reaches `rm`, it will check in the PATH variable and since nothing is there in it, `rm` will fail and I got the flag successfully.

# Setting PATH variable
### Commands:
```
1) hacker@path~setting-path:~$ PATH=/challenge/more_commands
2) hacker@path~setting-path:~$ echo $PATH
```
Output:

`/challenge/more_commands`
```
3) hacker@path~setting-path:~$ /challenge/run
```
Output:

Invoking 'win'....

Congratulations! You properly set the flag and 'win' has launched!
### Flag:
>pwn.college{4U3MsRslC3K5eFPyP-k4N_KrRA8.dVzNyUDL3cDN0czW}
### Explanation:
`/challenge/run` contains a command `win` but this command exists in `/challenge/more_commands` directory which isn't present in the `PATH` variable. So, I overwrote the `PATH` variable with `/challenge/more_commands` and then ran `/challenge/run` and got the flag.

# Adding Commands
### Commands:
```
1) hacker@path~adding-commands:~$ touch win
2) hacker@path~adding-commands:~$ echo "cat /flag" > ~/win
3) hacker@path~adding-commands:~$ PATH=$PATH:~
4) hacker@path~adding-commands:~$ chmod a+x win
5) hacker@path~adding-commands:~$ /challenge/run
```
Output:

Invoking 'win'....
### Flag:
>pwn.college{M3WPm6Nphwn3gLjFa0XVigRbcHb.dZzNyUDL3cDN0czW}
### Explanation:
Created a file called `win` in `~` and redircted the output of `echo "cat /flag"` to `win` file. Since, the `~` directory isn't present in the `PATH` variable, I added this directory to the list of already existing directories in `PATH` so that when `win` is invoked by `/challenge/run` during its execution, it will first check if it is a builtin command or not, if not then it will go through the directories in `PATH` variable and find if the `win` file is present in any. If present, `win` will be invoked successfully (but before that, we need to make sure `win` is executable so that when it is invoked, it will execute the **_COMMAND_** `cat /flag`. Used `chmod a+x` for this)and `/challenge/run` will give us the flag else it will show **command not found**.
# Hijacking Commands
### Commands:
```
1) hacker@path~hijacking-commands:~$ echo cat /flag > rm
2) hacker@path~hijacking-commands:~$ PATH=~:$PATH
3) hacker@path~hijacking-commands:~$ chmod a+x rm
4) hacker@path~hijacking-commands:~$ /challenge/run
```
Output:

Trying to remove /flag...

Found 'rm' command at /home/hacker/rm. Executing!
### Flag:
>pwn.college{otDZ9DjSgm5Cr8nsjTl7K7kSuY7.ddzNyUDL3cDN0czW}
### Explanation:
**NOTE**: The shell checks the directories in the `PATH` variable in an order i.e. left to right. 

_**Example:**_

**If your `PATH` is set to `~/bin:/usr/local/bin:/usr/bin`, the shell will check `~/bin` first. If it finds the command there, it executes it. If not, it moves to `/usr/local/bin`, and then to `/usr/bin`.**

Here, we know that `/challenge/run`'s code has `rm` which will delete the flag but it doesn't have any command to read the flag. So, instead of letting `/challenge/run` executing the `rm` meant for _deleting_ the flag, I created a _duplicate `rm`_ to `read` the flag instead. BUT the catch is that the _duplicate `rm`_ must be invoked **BEFORE** the _actual `rm`._

**Note 2: actual `rm` is located in a directories mentioned in `PATH` which I found using `echo $PATH` and `which rm`**

Created a `win` file the same way as in previous challenge. This time, instead of _appending_ the `~` directory to `PATH` variable, I added the `~` directory at a position _before_ the existing directories in the PATH variable. What this will do is that the presence of `win` file will be checked from left to right in the list of directories in `PATH` and since I added `~` at such a position, `win` will be searched for in the `~` directory FIRST. Thus, the _duplicate `rm`_ will be invoked instead of _actual `rm`_ and file will be read successfully.

