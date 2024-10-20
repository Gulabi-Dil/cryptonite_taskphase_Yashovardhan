# Learning From Documentation
### Commands:
```
1) hacker@man~learning-from-documentation:~$ /challenge/challenge --giveflag
```
### Flag: 
>pwn.college{8tdqD-fGuzknza2vytsGL5ES9n4.dRjM5QDL3cDN0czW}
### Explanation:
In this challenge, the program is /challenge/challenge. The syntax is <command> <argument> and here we are running the program for --giveflag which becomes the argument.

# Learning Complex Usage
### Commands: 
```
1) hacker@man~learning-complex-usage:~$ cd / && ls
2) hacker@man~learning-complex-usage:/$ /challenge/challenge --printfile flag
```
### Flag: 
>pwn.college{4lcjQyTFHTfeN9wf45ukYqnXxxq.dVjM5QDL3cDN0czW
### Explanation: 
Since the directory in which the flag file is in is unknown, I used cd / to access root directory and did ls. There was a file named flag. Ran the command and got the flag.

# Reading Manuals
### Commands:
```
1) hacker@man~reading-manuals:~$ man challenge
2) hacker@man~reading-manuals:~$ /challenge/challenge --mrzqgu 780
```
### Flag:
>pwn.college{EN7mBF8VJrzqg0YAUAO6uOKCV1m.dRTM4QDL3cDN0czW}
### Explanation: man challenge printed the manual where there was an obvious clue in the sypnnsis. 

# Searching Manuals:
### Commands: 
```
1)hacker@man~searching-manuals:~$ man challenge
2) /flag
Output:-  --btc  This argument will give you the flag! (line 1760/1831)
3) hacker@man~searching-manuals:~$ cd / && ls
4) hacker@man~searching-manuals:/$ cd /challenge && ls
5) hacker@man~searching-manuals:/challenge$ /challenge/challenge --btc
```
### Flag:
>pwn.college{4-WARSXFcdQrxrQu7vHX9cwT2UQ.dVTM4QDL3cDN0czW}
### Explanation:
man challenge printed the manual with a big list of arguments. Searched for flag using /flag in the manual. Found the correct argument from the list. Changed to root directory and then ls. Accessed challenge directory which had another challenge directory. Ran the command and gave the argument --btc

# Searching for Manuals
### Commands:
```
1) hacker@man~searching-for-manuals:~$ man man
2) hacker@man~searching-for-manuals:~$ man -k challenge
Output:-
bbvnyyqgvn (1)       - print the flag!
3) hacker@man~searching-for-manuals:~$ man bbvnyyqgvn
Output(in description of manual):-
--bbvnyy NUM
              print the flag if NUM is 081
4) hacker@man~searching-for-manuals:~$ /challenge/challenge --bbvnyy 081
```
### Flag:
> pwn.college{0bRbvnD813S_y5y2qMgUFvEBneG.dZTM4QDL3cDN0czW}
### Explanation: 
man man ggave a manual of manuals with lists of commands and their usage. After reading a few, found the command -k which csearches for the argument in the entire list of manuals. Search was successful after which I opened the manual where the searched argument was present using man manual_name. Got the command for flag in its description.

# Helpful Programs:
### Commands: 
```
1) hacker@man~helpful-programs:/$ man -k challenge
Outpuit:- challenge: nothing appropriate (same output for man -k flag, man -k help)
2) hacker@man~helpful-programs:/$ /challenge/challenge --help
Output:- optional arguments:
  -h, --help            show this help message and exit
  --fortune             read your fortune
  -v, --version         get the version number
  -g GIVE_THE_FLAG, --give-the-flag GIVE_THE_FLAG
                        get the flag, if given the correct value
  -p, --print-value     print the value that will cause the -g option to give you the flag
3) hacker@man~helpful-programs:~$ /challenge/challenge -p
Output:- The secret value is: 587
4) hacker@man~helpful-programs:~$ /challenge/challenge -g
Output:-
usage: a challenge to make you ask for help [-h] [--fortune] [-v] [-g GIVE_THE_FLAG] [-p]
a challenge to make you ask for help: error: argument -g/--give-the-flag: expected one argument
5) hacker@man~helpful-programs:~$ /challenge/challenge -g 587
```
### Flag: 
>pwn.college{UvMe5Fw87RFiI6QySihxJ3hVUHs.ddjM4QDL3cDN0czW}
### Explanation: 
First asked for help using --help since there is nothing to start with. Got the arguments and first ran -p tto get secret value which in turn was used to get flag.

# Help for Builtins
### Commands:
```
1) hacker@man~help-for-builtins:~$ help challenge
Output:--
challenge: challenge [--fortune] [--version] [--secret SECRET]
    This builtin command will read you the flag, given the right arguments!

    Options:
      --fortune         display a fortune
      --version         display the version
      --secret VALUE    prints the flag, if VALUE is correct

    You must be sure to provide the right value to --secret. That value
    is "sHMaJ9ZH".
2) hacker@man~help-for-builtins:~$ challenge --secret sHMaJ9ZH
```
### Flag:
>pwn.college{sHMaJ9ZH3mtrtSi5uu-toUKsHSn.dRTM5QDL3cDN0czW}
### Explanation: 
Asked for help using help challenge where challenge is the command name in this challenge (and is also a builtin). Got the arguments using which I got the flag.
