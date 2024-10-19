# Listing Processes
### Commands:
```
1) hacker@processes~listing-processes:~$ ps -ef
```
Output:

| UID    | PID  | PPID | C | STIME | TTY  | TIME     | CMD                                                        |
|--------|------|------|---|-------|------|----------|------------------------------------------------------------|
| root   | 1    | 0    | 0 | 09:58 | ?    | 00:00:00 | /sbin/docker-init -- /nix/var/nix/profiles/default/bin/dojo-init /ru |
| root   | 7    | 1    | 0 | 09:58 | ?    | 00:00:00 | /run/dojo/bin/sleep 6h                                      |
| root   | 68   | 1    | 0 | 09:58 | ?    | 00:00:00 | /challenge/15216-run-21499                                  |
| root   | 72   | 68   | 0 | 09:58 | ?    | 00:00:00 | sleep 6h                                                    |
| hacker | 73   | 0    | 0 | 09:58 | pts/0| 00:00:00 | /run/dojo/bin/ssh-entrypoint                                |
| hacker | 79   | 0    | 0 | 09:58 | pts/1| 00:00:00 | /run/dojo/bin/ssh-entrypoint                                |
| hacker | 107  | 79   | 0 | 09:58 | pts/1| 00:00:00 | ps -ef                                                      |

A list of all processes was displayed.
`UID: User ID` `PID: Process ID` `PPID: Parent Process ID` `C: CPU Usage` `STIME: Start Time` `TTY: Terminal Type` `TIME: Total CPU time consumed` `CMD: Command`
```
2) hacker@processes~listing-processes:~$ /challenge/15216-run-21499
```
Output:

pwn.college{k2bVPvbwwQ6Hxikri3ytiqYbMVs.dhzM4QDL3cDN0czW}

Now I will sleep for a while (so that you could find me with 'ps').
### Flag:
>pwn.college{k2bVPvbwwQ6Hxikri3ytiqYbMVs.dhzM4QDL3cDN0czW}
### Explanation:
`ps` command either stands for "process snapshot" or "process status", and it lists processes. By default, `ps` just lists the processes running in your terminal, which honestly isn't very useful:
```
hacker@dojo:~$ ps
    PID TTY          TIME CMD
    329 pts/0    00:00:00 bash
    349 pts/0    00:00:00 ps
hacker@dojo:~$
```
_In the above example, we have the shell (bash) and the ps process itself, and that's all that's running on that specific terminal. We also see that each process has a numerical identifier (the Process ID, or PID), which is a number that uniquely identifies every running process in a Linux environment. We also see the terminal on which the commands are running (in this case, the designation pts/0), and the total amount of cpu time that the process has eaten up so far (since these processes are very undemanding, they have yet to eat up even 1 second!)._

There are two ways to specify arguments:
- **"Standard" Syntax**: you can use `-e` to list "every" process and `-f` for a "full format" output, including arguments. These can be combined into a single argument `-ef`.

- **"BSD" Syntax**: you can use `a` to list processes for all users, `x` to list processes that aren't running in a terminal, and `u` for a "user-readable" output. These can be combined into a single argument `aux`.

A breakdown of the columns in the process list:

- **UID**: User ID of the process owner. It indicates which user initiated the process.

- **PID**: Process ID, a unique identifier for each process.

- **PPID**: Parent Process ID, the ID of the process that started (or spawned) the current process.

- **C**: CPU usage, a measure of how much CPU time the process is consuming.

- **STIME**: Start time, the time when the process was started.

- **TTY**: Terminal type or device associated with the process. ? indicates that the process is not associated with any terminal. For example, pts/0 refers to the pseudoterminal.

- **TIME**: Total CPU time consumed by the process so far.

- **CMD**: Command used to start the process, including any arguments passed to it.
  There are many commonalities between `ps -ef` and `ps aux`: both display the _user (USER column), the PID, the TTY, the start time of the process (STIME/START), the total utilized CPU time (TIME), and the command (CMD/COMMAND)_. `ps -ef` additionally outputs the _Parent Process ID (PPID), which is the PID of the process that launched the one in question_, while `ps aux` outputs the _percentage of total system CPU and Memory that the process is utilizing._

**_`- o` option when can be used with ps to display particular columns (columns will be the arguments)_** 
# Killing Processes
 ### Commands:
 ```
 1)  ps -e | grep /challenge/dont_run
 ```
No output.
```
2) hacker@processes~killing-processes:~$ ps -ef | grep /challenge/dont_run
```
Output:

hacker        74      72  0 10:28 ?        00:00:00 /challenge/dont_run

hacker        96      76  0 10:29 pts/0    00:00:00 grep --color=auto /challenge/dont_run

```
3) hacker@processes~killing-processes:~$ kill 74
4) hacker@processes~killing-processes:~$ ps -ef              (to confirm killing of the process)
5) hacker@processes~killing-processes:~$ /challenge/run
```
Output: 

Great job! Here is your payment:

pwn.college{AWdLNTc9m59_xkpFMAoK1pVnfoI.dJDN4QDL3cDN0czW}
### Flag:
>pwn.college{AWdLNTc9m59_xkpFMAoK1pVnfoI.dJDN4QDL3cDN0czW}
### Explanation:
Searched the process using grep in ps -ef to get the its PID. Then killed the process using kill PID i.e. kill 74 follwoed by /challenge/run.

# Interrupting Processes:
### Commands:
```
1) hacker@processes~interrupting-processes:~$ /challenge/run
```
Output:

I could give you the flag... but I won't, until this process exits. Remember,you can force me to exit with Ctrl-C. Try it now!
^C
```
2) Ctrl + C
```
Output:

Good job! You have used Ctrl-C to interrupt this process! Here is your flag:

pwn.college{c7Wn81USY-Ro90mNEGyaJwmW-GH.dNDN4QDL3cDN0czW}
### Flag:
>pwn.college{c7Wn81USY-Ro90mNEGyaJwmW-GH.dNDN4QDL3cDN0czW}
### Explanation:
Ctrl + C **terminates** an ongoing process, typically used to interrupt those processes which are clogging up the terminal.

`NOTE: ^C is just a representation of Ctrl + C in the terminal. Typing ^C to end a process won't work.`

# Suspending Processes
### Commands:
```
1) hacker@processes~suspending-processes:~$ ps -ef
```
Output: List of processes doesn't contain the command /challenge/run.
```
2) hacker@processes~suspending-processes:~$ /challenge/run
```
Output: Showed some details of challenge etc but didn't end.
```
3) Ctrl + Z
4) hacker@processes~suspending-processes:~$ ps -ef
```
Output: List of processes contain an entry of command /challenge/run (_shows that doing Ctrl + Z doesn't `terminate` the process but `suspends` it until explicitly resumed._)
```
5) hacker@processes~suspending-processes:~$ /challenge/run
```
_Ran the commmand again which makes a copy of it in the list of processes thus having 2 entries of /challenge/run._
### Flag:
>pwn.college{ouGLZMYROQpDQeDSgqx0kdEljE7.dVDN4QDL3cDN0czW}
### Explanation: 
Crrl + Z is used to `suspend` an ongoing process. _Suspending a process doesn't shift it to the background, it still runs in the foreground but is just suspended._
_The command `jobs` will show the list of all suspended processes._
`NOTE: ^Z is just a representation of Ctrl + Z in the terminal. Typing ^Z to end a process won't work.`

# Resuming Processes:
### Commands:
```
1) hacker@processes~resuming-processes:~$ /challenge/run
2) Ctrl + Z
3) hacker@processes~resuming-processes:~$ fg
```
Output:

/challenge/run                          `(indicates that the command is now running again in the foreground)`

I'm back! Here's your flag:

pwn.college{MM7akG7gv24Fq9DgLIhvDxFzdTU.dZDN4QDL3cDN0czW}
### Flag:
>pwn.college{MM7akG7gv24Fq9DgLIhvDxFzdTU.dZDN4QDL3cDN0czW}
### Explanation:
Suspended processes REMAIN in the FOREGROUND. However, when we resume them, we have a choice of resuming them in background or foreground.

`fg` resumes the suspended command in foreground. `bg` resumes the suspended command in background. 

**NOTE**: In this challenge we had only 1 suspended process which did not require selecting particular processes for resuming. If there are more than one suspended processes and we do just `fg` or `bg` then it will **_ONLY RESUME THE MOST RECENTLY SUSPENDED PROCESS_**. There is no built-in command to resume all suspended processes at once.

# Backgrounding Processes
### Commands:
```
1) hacker@processes~backgrounding-processes:~$ /challenge/run
2) Ctrl + Z
3) hacker@processes~backgrounding-processes:~$ bg
4) hacker@processes~backgrounding-processes:~$ /challenge/run
```
### Flag:
>pwn.college{Q_qoZFbkE2OjBI2pXAnHcTsQ_rD.ddDN4QDL3cDN0czW}
### Explanation:
First ran the `run` command then suspended it followed by resuming it in background using `bg`. Now `run` is RUNNING (NOT SUSPENDED) but in background. Launched `run` again in foreground using `/challenge/run`.

# Foregrounding Processes
### Commands:
```
1) hacker@processes~foregrounding-processes:~$ /challenge/run
2) Ctrl + Z
3) hacker@processes~foregrounding-processes:~$ bg
4) fg
```
After resuming in bg, it waits for `fg` _which typically doesn't happen but here there is special handling of program. Background processes don't interact with the user like this._
### Flag:
>pwn.college{E9hYTi9oCSlxN25NYhrZ6S-Nn0w.dhDN4QDL3cDN0czW}
### Explanation:
Done above.

**NOTE**: After `fg`, in the output, it first displayed the name of process `/challenge/run` which is just indicating that it is resumed in foreground. This is also why name of process isn't displayed when resumed in background.

# Starting Background Processes:
### Commands:
```
1) hacker@processes~starting-backgrounded-processes:~$ /challenge/run &
```
Output: [1] 82  
(+ some text blah blah and flag)
### Flag:
>pwn.college{kL0dqhv2ro6jrbhLjCzwisgdy0a.dlDN4QDL3cDN0czW}
### Explanation:
The `&` symbol instructs commands to run in a background process and immediately returns to the command line for additional commands.
**NOTE**: In output, `[1]` is the _job number_  (not the UID) and `82` is the _PID_.

# Process Exit Codes:
```
1) hacker@processes~process-exit-codes:~$ /challenge/get-code
```
Outout: Exiting with an error code!
```
2) hacker@processes~process-exit-codes:~$ echo $?
```
Output: 107
```
3) hacker@processes~process-exit-codes:~$ /challenge/submit-code 107
```
### Flag:
>pwn.college{k0f-R9u60cCCNU4eKG2zbTwO5Fh.dljN4UDL3cDN0czW}
### Explanation:
/challenge/get-code exits with an exit code which is I stored in the special veriable `?` using $?. Passed it as argument of /challenge/submit-code.

**NOTE**: The exit code for /challenge/get-code here is random.
