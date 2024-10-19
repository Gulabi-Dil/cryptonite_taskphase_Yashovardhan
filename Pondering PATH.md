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

# 
