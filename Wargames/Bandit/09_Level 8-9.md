# Level Goal
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once.
### Commands:
```
1) ssh bandit8@bandit.labs.overthewire.org -p 2220
```
Entered the password obtained from Level 7 to login.
```
2) bandit8@bandit:~$ ls
```
`data.txt`
```
3) bandit8@bandit:~$ cat data.txt
```
A big af list of password type strings was displayed. I explored and learnt about the `sort` and `uniq` commands.
```
4) bandit8@bandit:~$ sort data.txt | uniq -u
```
This gave me the password for the next Level.
### Explanation:
The `sort` command follows these features as stated below:  

- Lines starting with a number will appear before lines starting with a letter.

- Lines starting with a letter that appears earlier in the alphabet will appear before lines starting with a letter that appears later in the alphabet.

- Lines starting with a uppercase letter will appear before lines starting with the same letter in lowercase.

The `uniq` command in Linux is a command-line utility that reports or filters out the _repeated lines_ in a file. In simple words, `uniq` is the tool that helps to detect the _**ADJACENT duplicate lines**_ and also deletes the _duplicate lines_. `uniq` filters out the _**adjacent**_ matching lines from the input file(that is required as an argument) and writes the filtered data to the output file (if output file is not mentioned then it is shown in stdout.)
**NOTE: When I say "_adjacent lines_", I mean that `uniq` can only compare lines that are _next to each other_ in the file.**

For example, a file has this:
```
apple
banana
apple
orange
grape
banana
```
Without sorting, `uniq` would only see "apple" and "banana" as duplicates if they are next to each other. If you sorted the file first, it would look like this:
```
apple
apple
banana
banana
grape
orange
```
Now, `uniq` can easily see that "apple" and "banana" are duplicates.

When you run `uniq -u` after sorting, it will _identify lines that do not have duplicates next to them_, thus allowing you to find lines that occur only once throughout the entire file.
### Some References:
[sort command](https://www.geeksforgeeks.org/sort-command-linuxunix-examples/)

[uniq command](https://www.geeksforgeeks.org/uniq-command-in-linux-with-examples/)
