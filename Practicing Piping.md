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
- ><<
- 2> directs error messages from a command to a given file.
- 2>> directs an error message from a command to a given file. Appends the error message if the file exists and has content.
- &> directs standard output and error to a given file.
- &>> directs standard output and error to a given file. Appends to the file if it exists and has contents.
`>>`

`Some rules followed throughout: IF FILE DOESN'T EXIST, IT IS CREATED AND THE OUTPUT IS REDIRECTED THERE. IF THE FILE EXISTS THEN THE REDIRECTION DEPENDS ON THE CHARACTER USED. > IS OVERWRITE/TRUNCATION REDIRECTION WHERE THE PREVIOUS CONTENTS WILL BE OVERWRITTEN WHEREAS >> IS APPENDING REDIRECTION WHERE NEW CONTENTS WILL BE ADDED WITH NO CHANGES TO THE PREVIOUS CONTENTS.`

`>, 2>, 8> will redirect to it first by creating a new file (if doesn't exist); if the file exists then the content is OVERWRITTEN`

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


