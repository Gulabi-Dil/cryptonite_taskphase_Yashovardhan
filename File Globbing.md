# AN OVERVIEW:
Wildcards are special symbols used to represent unknown or variable parts of a file name, command, or search pattern. They help you match multiple files or items without specifying each one exactly. Wildcards are common in computer systems, especially in file searches and commands.
Here are the main wildcards:

\* (asterisk), ? (question mark), [] (square brackets)

Wildcards are especially useful when you're working with many files or when you don't know the exact name of what you're looking for.

Globs are patterns that use wildcards to match file names or paths. In simpler terms, globs are a way to use wildcards to search for files or directories without typing their exact names.

Here are the basic glob symbols:

\* – This means "anything." It matches any number of characters.

Example: *.txt finds all files that end with .txt.

? – This means "one character." It matches just one character.

Example: file?.txt finds file1.txt, file2.txt, but not file10.txt (since that's two characters after file).

[ ] – You can put a set of characters inside brackets to match any one of them.

Example: file[12].txt finds file1.txt or file2.txt.

{ } – This lets you pick from a list of options.

Example: file.{txt,pdf} finds file.txt and file.pdf. 

In short, globs are like wildcards for matching file names.

# Matching with *
### Commands:
```
1) hacker@globbing~matching-with-:~$ cd /chal*
```
Output:- You specified the path to 'cd' to in more than 4 characters. Disallowed!

`Tried /cha* as well but even that was invalid`
```
2) hacker@globbing~matching-with-:~$ cd /ch*
3) hacker@globbing~matching-with-:/challenge$ /challenge/run
```
### Flag:
>pwn.college{kzPSEhNb2Rd6Bt3QSdiJusRN9xy.dFjM4QDL3cDN0czW}
### Explanation:
When it encounters a * character in any argument, the shell will treat it as "wildcard" and try to replace that argument with any files that match the pattern.

When zero files are matched, by default, the shell leaves the glob unchanged. Example:
```
hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: nope_*
Look: nope_*
```
The * matches any part of the filename except for / or a leading . character. Example:
```
hacker@dojo:~$ echo ONE: /ho*/*ck*
ONE: /home/hacker
hacker@dojo:~$ echo TWO: /*/hacker
TWO: /home/hacker
hacker@dojo:~$ echo THREE: ../*
THREE: ../hacker
```
The / and * themselves are counting as individual characters thereby leaving us with just two characters to make the glob with. This is the reason /chal*, /cha* were incorrect. The * will match any number of characters after ch. Here, it matches to challenge.

# Matching with ?
### Commands:
```
1)hacker@globbing~matching-with-:~$ cd /?ha??enge
2) hacker@globbing~matching-with-:/challenge$ /challenge/run
```
The second command can also be written as:
```
2) hacker@globbing~matching-with-:/challenge$ /?ha??enge/run
```
### Flag:
>pwn.college{APMOY-gs8ni5SxGZnswI3fjf5na.dJjM4QDL3cDN0czW}
### Explanation: 
When it encounters a ? character in any argument, the shell will treat it as single-character wildcard. This works like *, but only matches one character. 

`NOTE: ? CANNOT BE USED FOR TWO CHARACTERS, SAY AB. FOR 2 CHARACTERS, ?? MUST BE USED`

# Matching with [ ]
### Commands:
```
1) hacker@globbing~matching-with-:~$ cd /challenge/files
2) hacker@globbing~matching-with-:/challenge/files$ /challenge//run file_[bash]
```
### Flag:
>pwn.college{cB2BrMLsm0DDcTqLeF3q5FHOtq8.dNjM4QDL3cDN0czW}
### Explanation:
The square brackes are, essentially, a limited form of ?, in that instead of matching any character, [ ] is a wildcard for some subset of potential characters, specified within the brackets. For example, [pwn] will match the character p, w, OR n.

# Matching Paths with [ ]
### Commands:
```
1) hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[bash]
```
### Flag:
>pwn.college{8IYJCtUbn5hGv9VwBdRvS5rkmiB.dRjM4QDL3cDN0czW}
### Explanation:
The [ ] glob will match any character from b, a, s, h.
# Mixing Globs
### Commands:
```
1) hacker@globbing~mixing-globs:~$ cd /challenge/files && ls
```
After doing ls, a list of words is printed whose first letters are unique.
```
2) hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]
```
Output:- Your expansion did not expand to the requested files (challenging, educational,
pwning). Instead, it expanded to:
[cep]

`Tried many manyy combinaitons such as [ceph], [[challengeeducationalpwning]], [cep*] but non of them were valid. For example, [[challengeeducationalpwning]] gave the error: your argument is too long! It must be 6 characters or less`
```
3) hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]*
```
### Flag:
>pwn.college{cf8k6jRKw2TAdphfWr1zvllPABz.dVjM4QDL3cDN0czW
### Explanation: 
The symbol [ ] itself counts as 2 characters thus leaving us with 4 characters to make the glob with. [ ] matches any character which among others is present in the glob. 
After doing ls, a list of words is printed whose first letters are unique which narrows down the argument for the glob. Sincethe first letter is unique for every word, I used [cep] which will match the first letter with c, e or p.

Then * is used after [cep] because * matches any number of characters thus it will match the rest of the word after the first letter is matched.

`NOTE: *[cep] is INCORRECT because it would evaluate to matching any number of characters first and then matching c, e or p at the last letter which is INCOORECT.`

`NOTE: WE CANNOT USE A GLOB WITHIN ANOTHER GLOB. THUS [*], [{}], [?], {*}, {?} ARE INVALID. HOWEVER, COMBINATIONS CAN BE USED WITH INDEPENDENT USAGE OF GLOBS SUCH AS [ ]*, *[ ], [ ]? AND SO ON.`
### Key Takeaway:
1. Globs cannot be used within other globs.
2. The symbol of glob itself counts as characters.

# Exclusionary Globbing:
### Commands:
```
1) hacker@globbing~exclusionary-globbing:~$ cd /challenge/files
2) hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [!pwn]*
```
### Flag:
>pwn.college{gm8qFj0k9EHJmXV0cqhrJVYNSPo.dZjM4QDL3cDN0czW}
### Explanation: 
If the first character in the brackets is a ! or (in newer versions of bash) a ^, the glob inverts, and that bracket instance matches characters that aren't listed.

Same concept as previous challenge. The ! or ^ in [ ] will match characters except the ones present in the [ ] i.e [!pwn] or [^pwn] will match any character except p, w or n. The * after this glob will match the rest of the file name.

## Some References
1) [Wildcard characters](https://en.wikipedia.org/wiki/Wildcard_character)
2) [Globs](https://en.wikipedia.org/wiki/Glob_(programming))
3) Some google help and chatgpt for examples. 
