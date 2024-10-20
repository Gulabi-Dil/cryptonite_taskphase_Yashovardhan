# Chaining with Semicolons
### Commands:
```
1) hacker@chaining~chaining-with-semicolons:~$ /challenge/pwn ; /challenge/college
```
### Flag: 
>pwn.college{cHJPouj9Hx2JBDu1rhuWMB4GxWe.dVTN4QDL3cDN0czW}
### Explanation:
[Refere to this](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Operators%20differences%20(extra).md#the-semicolon-)

# Your First Shell Script
### Commands:
```
1) hacker@chaining~your-first-shell-script:~$ echo /challenge/pwn > x.sh && echo /challenge/college >> x.sh
2) hacker@chaining~your-first-shell-script:~$ bash x.sh
```
### Flag: 
>pwn.college{kPuT8QoHj59aGxUhqJPXAN5olDw.dFzN4QDL3cDN0czW}
### Explanation:
Used redirection to store the output of `echo` command in a file named `x` with an extension `.sh` This extension is used for shell scripts. When the file is run using `bash`, it does not read the contents like that of a file but rather executes them as commands.

# Redirecting Script Ouptut
### Commands:
**NOTE: Used the same script file which I created for the previous challenge.**
```
1) hacker@chaining~redirecting-script-output:~$ bash x.sh | /challenge/solve
```
### Flag:
>pwn.college{w3MUjo-n2LJLaEaNmihYpAE4guP.dhTM5QDL3cDN0czW}
### Explanation:
The output of `bash x.sh` is piped to the command `/challenge/solve` which gave the flag.

# Executable Shell Scripts
### Commands:
```
1) hacker@chaining~executable-shell-scripts:~$ echo /challenge/solve > y.sh
2) hacker@chaining~executable-shell-scripts:~$ ls -l
```
A list of files and directories under the home directory was displayed among which was

`-rw-r--r-- 1 hacker hacker   17 Oct 18 11:27  y.sh`
```
3) hacker@chaining~executable-shell-scripts:~$ chmod u+x y.sh
4) hacker@chaining~executable-shell-scripts:~$ ./y.sh
```
### Flag:
>pwn.college{QaUHWGCmvnRBhLsP36CGRW2uMq5.dRzNyUDL3cDN0czW}
### Explanation:
Instead of using `bash` I made the file `y.sh` executable by changing the file permissions using `chmod` followed by executing it (since its in the current directory i.e. home directory, I used `./`)

## Some References:
[Bashing](https://www.geeksforgeeks.org/what-is-hashing/)
