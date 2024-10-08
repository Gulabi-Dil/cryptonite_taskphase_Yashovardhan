# Printing Variables
### Commands:
```
1) hacker@variables~printing-variables:~$ echo $FLAG
```
### Flag:
>pwn.college{QhTMLJsDbvF4UEuRFSLPhCcT8vZ.ddTN1QDL3cDN0czW}
### Explanation:
Here, FLAG is a variable/identifier. Values of variables and commands in linux can be read by using $. Here, $FLAG gave the output of the variable FLAG.

# Setting Variables
### Commands:
```
1) hacker@variables~setting-variables:~$ PWN=COLLEGE
```
### Flag:
>pwn.college{gUTdP8OY9M7fSHfD5D_FAn0tGUT.dlTN1QDL3cDN0czW}
### Explanation:
Initiializtion of the verb PWN was done using =. However, `$` IS `NOT` USED BECAUSE IT IS ONLY FOR READING THE VALUE  OF VARIABLE/FUNCTION.
# Multi-word Variables
### Commands:
```
1) hacker@variables~multi-word-variables:~$ PWN="COLLEGE YEAH"
```
Ouptut:

You've set the PWN variable properly! As promised, here is the flag:

pwn.college{MgUWIDxEGw133C83U6vg0toX7ry.dBjN1QDL3cDN0czW}

### Flag:
>pwn.college{MgUWIDxEGw133C83U6vg0toX7ry.dBjN1QDL3cDN0czW}
### Explanation:
`NOTE: SPACE ENDS THE ARGUMENT FOR VARIABLE. THUS, " " ARE USED FOR INPUTTING MULTIPLE WORDS IN THE VARIABLE.

# Exporting Variables
### Commands:
```
1) hacker@variables~exporting-variables:~$ COLLEGE=PWN
```
Output:

You've set the COLLEGE variable to the proper value!
```
2) hacker@variables~exporting-variables:~$ export PWN=COLLEGE
```
Output:

You've set the PWN variable to the proper value!

You've set the COLLEGE variable to the proper value!
```
3) hacker@variables~exporting-variables:~$ /challenge/run
```
Output:

CORRECT!
You have exported PWN=COLLEGE and set, but not exported, COLLEGE=PWN. Great job! Here is your flag:

pwn.college{49dpq_dtFm1gRMjVJk6hExVwcg9.dJjN1QDL3cDN0czW}

You've set the PWN variable to the proper value!

You've set the COLLEGE variable to the proper value!

### Flag:
>pwn.college{49dpq_dtFm1gRMjVJk6hExVwcg9.dJjN1QDL3cDN0czW}
### Explanation:
The variable college is not to be exported so first wrote COLLEGE=PWN. Then I exported PWN=COLLEGE. 

_We are running a shell (parent shell by default) which is the primary environment where we execute commands, define variables and run programs. Parent shell comprises of many child shells (or child processes). The `export` command copies `VARIABLES` AND `FUNCTIONS` **ONLY** and transfers the copy to **ALL** the child processes of the parent shell. The variables or functions which couldn't be accessed by the child processes earlier could now be accessed after exporting._

- When you run a command in the shell (without explicitly starting a specific child process), that command itself becomes a child process of the current shell. Every time you execute a command in the shell, a new process is created to run that command. This new process is considered a child process of the parent shell, even though you didn’t explicitly mention creating one.
  - Working:
  - 1. **Parent Shell**: The shell you’re working in is the parent process.
    2. **Running a Command**: When you run any command, like ls, echo, or even a script, the shell creates a child process to execute that command. The shell acts as the parent, and the command runs in its own separate process (the child).
    3. **Command as a child process**: Suppose you run `ls`. The `ls` command is executed as a child process of your shell. Similarly, if you run a script or any other program, it becomes a child process of your shell.
    4. **How the Child Process is Created**: The shell uses system calls like fork() (in Unix-like systems) to create the child process. The child process then runs the command while the parent shell waits for it to finish.
    5. **Each Command is a New Child Process**: Every time you run a new command, the shell spawns a new child process to handle that specific task. Even if you run multiple commands in a row, each command is executed in its own child process.

Here, the `export` command copies the variable PWN (PWN=COLLEGE) to all the child processes. The command /challenge/run also acts as child process and since it could access variable PWN, it ran successfully and gave the flag. If PWN was not exported, it would exist only in the environment of the parent shell (where you defined it), but it wouldn't be available to the /challenge/run command, since child processes (like /challenge/run) do not automatically inherit non-exported variables.

`NOTE 1: Child processes get a copy of the parent shell's environment, not the same environment. Exporting a variable allows child processes to access it, but changes in a child process don’t affect the parent shell. The exported variable is available in the parent shell and passed to child processes, but each operates independently.`

`NOTE 2: When a child process is created, it inherits the parent shell’s environment, including any exported variables that existed at the time of its creation.`

`If you change or unset a variable in the parent shell after the child process has been started, those changes do not propagate to the child process. The child process continues to operate with the environment it inherited at the time it was created.`

`After the child process is started, it has its own separate environment. Any changes to variables within the parent shell will not affect the child process, and vice versa.`

# Printing Exported Variables
### Commands:
```
1) hacker@variables~printing-exported-variables:~$ env
```
Output: A big list of variables was printed among which was FLAG which contained fllag in it.
### Flag:
>pwn.college{Qvh1FwBe2Vj6qLce-Q2FcgJwrgP.dhTN1QDL3cDN0czW}
### Explanation:
`env` prints **every exported variable** set in your shell. The value of a variable from the list can be read as echo $VARIABLE_NAME but since the use of `echo` is restricted in this challenge, we can search using `grep`.

`env | grep FLAG` will search for FLAG in the list and print it.

There is also a command to print a **particular variable's value**:

** `printenv FLAG` It will directly print the value of FLAG.

# Storing Command Output:
### Commands:
```
1) hacker@variables~storing-command-output:~$ PWN=$(/challenge/run)
```
Output:

Congratulations! You have read the flag into the PWN variable. Now print it out
```
2) hacker@variables~storing-command-output:~$ echo $PWN
```
### Flag:
>pwn.college{EYTYM8NNDPrqtVfBI8T-IhK4UpD.dVzN0UDL3cDN0czW}
### Explanation:
The output of the command /challenge/run had to be entered in the variable PWN which was done by PWN=$(/challenge/run). `$` is used for **command substitution** which allows the output of a command to be captured and stored in a variable.

`The $() syntax tells the shell to run the command inside the parentheses and replace the entire expression with the output of that command.`

PWN is then ready by echo $PWN.

# Reading Input
### Commands:
```
1) hacker@variables~reading-input:~$ read PWN
```
COLLEGE   //input
Can also be done this way:
```
1) hacker@variables~reading-input:~$ read -p "INPUT: " PWN
```
INPUT: COLLEGE   //input
Output:

You've set the PWN variable properly! As promised, here is the flag:
### Flag:
>pwn.college{kbpNIHKrKMCVoBWndJ8wwi9zfh1.dhzN1QDL3cDN0czW}
### Explanation:
The `read` command gets input from user.

The `-p` option allows you to provide a prompt message that will be displayed to the user before they enter their input.
The syntax `-p "INPUT: " ` indicates that the shell will show the message "INPUT: " as a prompt. Whereas the simple command `read` is ONLY to take input, nothing else.

# Reading Files:
### Commands:
```
1) hacker@variables~reading-files:~$ read PWN < $(/challenge/read_me)
```
Output:

You appear to be invoking a subshell. This could be, for example, because you are doing something like `PWN=$(echo COLLEGE)`. Instead, you must use `read` to set the PWN variable.

ssh-entrypoint: $(/challenge/read_me): ambiguous redirect
```
2) hacker@variables~reading-files:~$ read PWN < /challenge/read_me
```
Output:

You've set the PWN variable properly! As promised, here is the flag:
### Flag:
>pwn.college{Y6OD3Fnrvb2DLr4ejPj25Y_8WB0.dBjM4QDL3cDN0czW}
### Explanation:
The command substitution `$(/challenge/read_me)` produces output (let's say it prints some text), but using < with that output is incorrect because < expects a **file path**, not the text output of a command. In contrast, when you use `$(cat ...)`, the output of cat is directly assigned to a variable without the need for redirection.

## Some Extra Reference
- [Parent shell and Child Processes](https://www.geeksforgeeks.org/difference-between-process-parent-process-and-child-process/)
