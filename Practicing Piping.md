- [Unnamed Pipes](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#unnamed-pipes)
- [Named Pipes](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#named-pipes)
- [Process Substitutions](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#process-substitution)
- [Differences among Unnamed, Named Pipes and Process Substitutions](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#difference-between-unnamed-pipes-named-pipes-and-process-substitutions)
# AN OVERVIEW:
The mechanisms behind the handling of input and output on the commandline contribute to the commandline's power. Every process in Linux has three initial, standard channels of communication:
- Standard Input is the channel through which the process takes input. For example, your shell uses Standard Input to read the commands that you input.
- Standard Output is the channel through which processes output normal data, such as the flag when it is printed to you in previous challenges or the output of utilities such as `ls`.
- Standard Error is the channel through which processes output error details. For example, if you mistype a command, the shell will output, over standard error, that this command does not exist.

Because these three channels are used so frequently in Linux, they are known by shorter names: `stdin`, `stdout`, `stderr`.
## Redirection:
Redirection is the act of dictating where the inputs or outputs of your commands go. By default, commands receive data from standard input and then output the results in standard output.

One of the main areas where redirection proves useful is when working with commands and files. You can, for example, redirect the output of a command to a file instead of printing the output in the terminal. Alternatively, you can declare a certain file as an input to a command.

Some important file-redirection characters in Linux and what they do:
- \> directs the output of a command to a given file.
- < directs the contents of a given file to a command.
- \>\> directs the output of a command to a given file. Appends the output if the file exists and has content.
- << manually provides input to a command instead of redirecting a file's content to the command. The syntax is: `command << delimiter` this will initiate the input of commands and the delimiter acts as a full stop after we're done typing them.

example 1:
```
cat << ABC
Helloo
Byee
ABC
```
Output:

Helloo

Byee

example 2:
```
bc << EOF  // `bc` is a command line calculator to evaluate MULTIPLE operations. `expr` is a command line calculator to evaluate SINGLE operation
5 + 3
10 / 2
2^3
EOF
```
Output:

8

5

8

example 3:
```
grep "apple" << END
I love apples.
Bananas are great too.
An apple a day keeps the doctor away.
END
```
Output:

I love apples.

An apple a day keeps the doctor away.


- 2> directs error messages from a command to a given file.
- 2>> directs an error message from a command to a given file. Appends the error message if the file exists and has content.
- &> directs standard output and error to a given file.
- &>> directs standard output and error to a given file. Appends to the file if it exists and has contents.
`>>`

`Some rules followed throughout: IF FILE DOESN'T EXIST, IT IS CREATED AND THE OUTPUT IS REDIRECTED THERE. IF THE FILE EXISTS THEN THE REDIRECTION DEPENDS ON THE CHARACTER USED. > IS OVERWRITE/TRUNCATION REDIRECTION WHERE THE PREVIOUS CONTENTS WILL BE OVERWRITTEN WHEREAS >> IS APPENDING REDIRECTION WHERE NEW CONTENTS WILL BE ADDED WITH NO CHANGES TO THE PREVIOUS CONTENTS.`

`>, 2>, &> will redirect to it first by creating a new file (if doesn't exist); if the file exists then the content is OVERWRITTEN`

`>>, 2>>, &>> will redirect to it by first creating a new file (if doesn't exist); if the file exists then the content is APPENDED`
# Redirecting Output
### Commands:
```
1) hacker@piping~redirecting-output:~$ echo PWN > COLLEGE
```
### Flag:
>pwn.college{0iXS9iCmWmXJKqFOg7M4BQBl2rd.dRjN1QDL3cDN0czW}
### Explanation:
echo will output the argument but because of > it won't be shown in the standard output but will be redirected to a file named COLLEGE. 

# Redirecting More Output
### Commands:
```
1) hacker@piping~redirecting-more-output:~$ /challenge/run > myflag
2) hacker@piping~redirecting-more-output:~$ cat myflag
```
### Flag:
> pwn.college{oCgBdfesgLQ4BXr2gJ881gDtnIW.dVjN1QDL3cDN0czW}
### Explanation:
The command /challenge/run is executed whose output is redirected and stored in a new file called myflag instead of the standard output. Reading the myflag file using cat will give us the flag.

# Appending Output
### Commands:
```
1) hacker@piping~appending-output:~$ /challenge/run >> ~/the-flag
```
Message displayed after this: 

Success! You have satisfied all execution requirements.
I will write the flag in two parts to the file /home/hacker/the-flag! I'll do
the first write directly to the file, and the second write, I'll do to stdout
(if it's pointing at the file). If you redirect the output in append mode, the
second write will append to (rather than overwrite) the first write, and you'll
get the whole flag!
```
2) hacker@piping~appending-output:~$ cat the-flag
```
### Flag:
>pwn.college{IV8yjrvKdQlrrTcuE0rM0kFaoXm.ddDM5QDL3cDN0czW}
### Explanation:


# Redirecting Errors
### Commands:
```
1) hacker@piping~redirecting-errors:~$ /challenge/run > myflag 2> instructions
2) hacker@piping~redirecting-errors:~$ cat myflag
```
### Flag:
>pwn.college{UiAxjgbfrJz03CfMq8f0Tl25GHg.ddjN1QDL3cDN0czW}
### Explanation:
A File Descriptor (FD) is a number the describes a communication channel in Linux. We're already familiar with three:

`FD 0: Standard Input`

`FD 1: Standard Output`

`FD 2: Standard Error`

When you redirect process communication, you do it by FD number, though some FD numbers are implicit. For example, a > without a number implies 1>, which redirects FD 1 (Standard Output). Thus, the following two commands are equivalent:
```
hacker@dojo:~$ echo hi > asdf
hacker@dojo:~$ echo hi 1> asdf
```
Here, > will redirect the standard output of the command /challenge/run to myflag file and 2> will simultaenously redirect the standard error (the data is instructions here in this case) to a file named instructions. No output is shown in terminal due to the redirection but we can read the files using cat.

# Redirecting Input
### Commands:
```
1) hacker@piping~redirecting-input:~$ echo COLLEGE > PWN
2) hacker@piping~redirecting-input:~$ /challenge/run < PWN
```
### Flag:
>pwn.college{4FxI1x1EtOomXMTBrmTyuyjNVAk.dBzN1QDL3cDN0czW}
### Explanation:
First redirected the word COLLEGE to store it in a file named PWN using echo and >. Now, redirecting input was done by using < which redirects PWN to the command /challenge/run.

# Grepping Stored Results
### Commands:
```
1) hacker@piping~grepping-stored-results:~$ /challenge/run > /tmp/data.txt
2) hacker@piping~grepping-stored-results:~$ grep flag /tmp/data.txt
```
grep will output a big list of texts from the file which have the word flag in them but none of them was the flag. `We also can't use cat unlike previous challenges here because what we are reading is a TEXT DOCUMENT and not a file or directory.`

Recollecting the format of the flag i.e. pwn or the curly brackets {},
```
3) hacker@piping~grepping-stored-results:~$ grep { /tmp/data.txt
```
`NOTE: WE CAN'T USE {} FOR GREP TO SEARCH BECAUSE IT WILL CHECK THE ARGUMENT AS A WHOLE COLLECTIVELY, THUS USED ONLY ONE {`
### Flag:
>pwn.college{0PtJB1AnyNAg1xRWyolo9NyK1TZ.dhTM4QDL3cDN0czW}
### Explanation:
First redirected the standard output of the command /challenge/run to the file /tmp/data.txt and then used grep to search for the keywords which are present in the flag.

# Grepping Live Output
### Commands:
```
1) hacker@piping~grepping-live-output:~$ /challenge/run | grep pwn
```
### Flag:
>pwn.college{AgnAhPcB2jTgCy3MJr3gMqiFlEL.dlTM4QDL3cDN0czW}
### Explanation:
First ran the command /challenge/run whose output was used as input for grep pwn which will search pwn in the output of /challenge/run i.e. in the input of grep. The keyword selection was done like in previous challenge.

# Grepping Errors
### Commands:
```
1) hacker@piping~grepping-errors:~$ /challenge/run 2>&1 | grep pwn
```
### Flag:
>pwn.college{oiQKgHWgTjeL3leR3wesFogpaqC.dVDM5QDL3cDN0czW}
### Explanation:
The > operator redirects a given file descriptor to a file, and you've used 2> to redirect fd 2, which is standard error.

`The | operator redirects only standard output to another program, and there is no 2| form of the operator! It can only redirect standard output (file descriptor 1).`

As mentioned in the challenge, we are redirecting a file descriptor to another file descriptor first and then piping. Here, 2>&1 means the standard error of the command /challenge/run will be redirected to standard output (means that ANY ERROR MESSAGE WILL BE SENT TO THE SAME PLACE AS THE NORMAL OUTPUT (STDOUT).

Thus, it ultimately becomes the input for the grep after piping where grepping the keyword pwn will find the flag.

# Duplicating Piped Data with Tee
### Commands:
```
1)hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn | /challenge/college
```
Output: 

The input to 'college' does not contain the correct secret code! This code should be provided by the 'pwn' command. HINT: use 'tee' to intercept the output of 'pwn' and figure out what the code needs to be.
```
2) hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn
```
Output:

Processing...

You must pipe the output of /challenge/pwn into /challenge/college (or 'tee' for debugging).
```
3) hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/college
```
Output:

/challenge/secret needs to the on the receiving end of the output of '/challenge/pwn' (or 'tee' for debugging). 

`NOTE: Did cat /challenge/secret after this which showed no such file or directory found`
```
4) hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn | tee /challenge/secret | /challenge/college
```
Output:

The input to 'college' does not contain the correct secret code! This code should be provided by the 'pwn' command. HINT: use 'tee' to intercept the output of 'pwn' and figure out what the code needs to be.

`NOTE: Did cat /challenge/secret which showed:`

`Usage: /challenge/pwn --secret [SECRET_ARG]`

`SECRET_ARG should be "0fEtSxfi"`

_Shows that the output of the pwn command is not only piped to /challenge/college but also stored in the newly created file named /challenge/secret because of tee. The file stores the output generated by pwn command at that time._

**Did /challenge/pwn | /challenge/college after this followed by cat /challenge/secret which gave the same output as above. REASON: Since tee wasn't used, the output of pwn was directly piped to /challenge/college without any changes to the secret file. Thus upon doing cat, the already existing contents of the file were shown in output**
```
5) hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn --secret 0fEtSxfi | tee /challenge/secret | /challenge/college
```
Output:

Processing...

WARNING: you are overwriting file /challenge/secret with tee's output...

Correct! Passing secret value to /challenge/college...

Great job! Here is your flag:

pwn.college{0fEtSxfiOzkTBUf4l9iQoTqahi_.dFjM5QDL3cDN0czW}

`NOTE: Did cat /challenge/secret after this which gave the output:`

`SUPERSECRET:iOzk`

_This shows that upon passing the arguments to the pwn command, different output is generated compared to pwn without arguments. Now the contents of the secret file get overwritten by the new output thereby giving a different output after cat._

**If I do /challenge/pwn | tee /challenge/college after this followed by cat, output will be the previous one, not supersecret because the file gets overwritten due to tee.**
### Flag:
>pwn.college{0fEtSxfiOzkTBUf4l9iQoTqahi_.dFjM5QDL3cDN0czW}
### Explanation:
Explained everything above.

# Writing to Multiple Programs
### Commands:
```
1) hacker@piping~writing-to-multiple-programs:~$ /challenge/hack | tee /challenge/the | /challenge/planet
```
Output:

WARNING: it looks like you passed the path /challenge/the, instead of the substituted process, to tee. This will cause tee to try to write to the /challenge/the file, rather than have the shell launch the /challenge/the command and redirect tee's output to it.

/usr/bin/tee: /challenge/the: Permission denied
`NOTE: tee is designed to read from standard input and write to standard output and files. When you give it a file path (like /challenge/the), it assumes you're trying to write to a file, not execute a command. The correct way to execute a command with input from tee is to use process substitution. In bash, you use >(command) to specify that you want to run command and send input to it. `

`When I tried commands like: `

**/challenge/hack | tee /challenge/the | /challenge/planet** or **/challenge/hack | /challenge/planet | tee /challenge/the**

`the shell interpreted /challenge/the as a file path. Thus, tee tried to write to it as if it were a file instead of launching it as a command. This led to the warning about passing a path instead of using the substitution process.`
```
2) hacker@piping~writing-to-multiple-programs:~$ /challenge/hack | /challenge/the | /challenge/planet
```
Output: 

Are you sure you're properly redirecting input into '/challenge/planet'?
`The pipe (|) takes the output from /challenge/hack and tries to pass it directly to /challenge/the. However, if /challenge/the does not produce any output or cannot properly process the input from /challenge/hack, the result may not be what you expect.`
```
3) hacker@piping~writing-to-multiple-programs:~$ /challenge/hack
```
Output:

You must redirect my output into another command!

```4) hacker@piping~writing-to-multiple-programs:~$ /challenge/the```

Output: no output but able to write stuff in it.

```5) hacker@piping~writing-to-multiple-programs:~$ /challenge/planet```

Output: same ouput as that of 4)

`NOTE: There is no ouptut for 4) and 5) but they don't finsih either. The commands await i.e. blocking behavior.`
```
6) hacker@piping~writing-to-multiple-programs:~$ /challenge/hack | tee >(/challenge/the) | /challenge/planet
```
or 
```
6) hacker@piping~writing-to-multiple-programs:~$ /challenge/hack | tee >(/challenge/planet) | /challenge/the
```
Either of the two will do since there is no info about the commands hack, the and planet except that the output of hack is to be inputted in both planet and the.
### Flag: 
>pwn.college{UZ0vZopks4kvUjuYI1roIu3d9y2.dBDO0UDL3cDN0czW}
### Explanation:
Explanations of the first few commands are written above. 


Difference between 1) `/challenge/hack | tee >(/challenge/the) | /challenge/planet` and 2) `/challenge/hack | tee >(/challenge/the) | >(/challenge/planet)`:

_In both the commands, the common thing is that the output generated by hack is piped to tee. Tee redirects the output of hack to the process substituion the_

1) At the same time, `tee` sends another copy of the output to the command /challenge/planet by piping. Thus, commands `the` and `planet` both get the same input. They run concurrently, processing the same output from `hack` command.

2) However, the output to >(/challenge/planet) is different. Here, >(/challenge/planet) is treated as a separate process that is set up to receive input. The command >(/challenge/planet) does not directly get the output from tee. It’s treated as a separate context for input. As a result, /challenge/planet may not receive the same output from tee directly.

`NOTE: WHEN USING TEE TO GET INPUT FOR PROCESS SUBSTITUTIONS, ALWAYS KEEP IN MIND THAT THEY MUST BE PAIRED TOGETHER. IF THERE IS PIPING BETWEEN THEM THEN THE PROCESS SUBSTITUTION DOESN'T RECEIVE THE INPUT WHICH TEE OUTPUTS AND IT THUS ACTS AS AN INDEPENDENT COMMAND.`

**This is also why we don't get the same outputs from 1) and 2). For a clearer example:**
```
echo "Hello from hack" | tee >(echo "Hello from the") | echo "Hello from planet"
```
Here, let the commands from left to right be named as hack, the and planet respectively.

`Whenever there are process substitutions present, they are executed first regardless of the left to right rule. This task is done in the background before the shell starts reading thr command. After this, the commands are read:`

Output of hack is piped to tee which not only redirects it to stdout (but since there is a process substitution here, it redirects to `the`) but also to planet. 

**However, since `the` in >() has been executed already it can be seen as hack | tee "Hello from the" | planet. Tee is no more followed by a command which results in something called NOWHERE VISIBLE i.e. THE OUTPUT WON'T BE SEEN IN TERMINAL AS THE NAMED PIPE (FIFO) ISN'T CONNECTED TO TERMNIAL (IF THERE IS NO COMMAND WHICH CAN READ THE NAMED PIPE IN TERMINAL THEN THE PIPE IS NOT CONNECTED TO TERMINAL.)**


`Example of output VISIBLE through connection:`
```
echo "Hello from process substitution" | tee >(cat) | cat
```
_Here, the cat command is processed first in background and now it can be seen as echo "Hello from process substitution" | tee cat | cat. The output of left echo is piped to tee which duplicates it, makes 2 copies and sends to cat as well as right cat. Thus cat will read the output of left echo and display it in termnial and right cat will display the same string again._

Output:
Hello from process substitution

Hello from process substitution

`Example of Nowhere Visible:`
```
echo "Hello from process substitution" | tee >(cat) | echo "Visible output"
```
_Here, the cat command is processed first in background and now it can be seen as echo_ `"Hello from process substitution" | tee cat | echo "Visible output".` _Left echo's output is piped to tee which duplicates it, makes 2 copies and sends to cat as well as right echo. However cat command is a process substitution which creates a ``temporary`` named pipe (FIFO i.e. First in First out) which can't output in terminal unless explicitly enabled to do so i.e. it is not connected to terminal thus can't output in stdout. The copy sent to right echo acts as the echo's input and since anything that is input of an echo command returns the argument of echo,_

Output:

Visible output

# Split-Piping stderr and stdout:
### Commands:
```
1) hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack > >(/challenge/planet) 2> >(/challenge/the)
```
Can also be done using piping
```
1) hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack 2> >(/challenge/the) | /challenge/planet
```
### Flag:
>pwn.college{8sEaXI1u8M9GYUPf-0sLOCBCJ8U.dFDNwYDL3cDN0czW}
### Explanation:
In method 1, I redirected the stdout and stderr to respective COMMANDS (hence the usage of process substitutions aka temporary named pipes) where > `(i.e. 1> or stdout)` was used to redirect stdout to /challenge/planet and 2> `(i.e. stderr)` was used to redirect stderr to /challenge/the.

In method 2, I first redirected the stderr from /challenge/hack to process substitution of /challenge/the and then used piping to store stdout of hack in planet.

`NOTE: THIS ONLY WORKS BECAUSE THE DEFAULT PIPING FOR PIPES IS STDOUT.`

## Some References:
- Chatgpt for understanding some concepts, workings and errors, especially in Writing to Multiple Programs. (Solving was done by myself though)
- [Input Output Redirection](https://www.geeksforgeeks.org/input-output-redirection-in-linux/)
- [Redirection and Piping](https://www.freecodecamp.org/news/linux-terminal-piping-and-redirection-guide/#:~:text=What%20Is%20Redirection%20in%20Linux,working%20with%20commands%20and%20files.)
- [Process Substitutions 1](https://sysxplore.com/process-substitution-in-bash/) _To be read_
- [Process Substitutions 2](https://linuxhandbook.com/bash-process-substitution/) _To be read_
