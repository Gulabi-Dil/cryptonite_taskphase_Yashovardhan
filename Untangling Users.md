# Becoming root with su
### Commands:
```
1) hacker@users~becoming-root-with-su:~$ cat /flag
```
cat: /flag: Permission denied
```
2) hacker@users~becoming-root-with-su:~$ su
```
The shell asked for password so I entered `hack-the-planet`.
```
3) hacker@users~becoming-root-with-su:~$ cat /flag
```
### Flag:
>pwn.college{4G6fzXYkTLw4u39OqvQbv-nhibi.dVTN0UDL3cDN0czW}
### Explanation:
The `su` command stands for substitute user which basically switches users. `su` is a **setuid binary**.

A **setuid binary** is an executable file (`binary`) in a Unix-like operating system that has the _setuid (Set User ID) bit set_. This bit allows the program to run with the _privileges of the file's owner rather than the privileges of the user who runs the program._
Because it has the SUID bit set, `su` runs as root. Running as root, it **can start a root shell**! Of course, `su` is discerning: **before allowing the user to elevate privileges to root, it checks to make sure that the user knows the root password.** This check against the root password is what obsoletes `su`. Modern systems very rarely have root passwords, and different mechanisms are used to grant administrative access.

# Other Users with su
### Commands:
```
1) hacker@users~other-users-with-su:~$ su zardus
```
The shell asked for password so I entered `dont-hack-me`.
```
2) zardus@users~other-users-with-su:/home/hacker$ /challenge/run
```
### Flag:
>pwn.college{MYjkOFB1BVLScJRlWf01DWGVoaL.dZTN0UDL3cDN0czW}
### Explanation:
With no arguments, `su` will **start a root shell** (after authenticating with root's password). However, you can also give a username as an argument to switch to that user instead of root.
For example:
```
hacker@dojo:~$ su some-user
Password:
some-user@dojo:~$
```
Here, after doing `su zardus` I entered the password and became zardus.

# 
