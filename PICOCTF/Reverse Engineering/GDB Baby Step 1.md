# Description: 
Can you figure out what is in the eax register at the end of the main function? Put your answer in the picoCTF flag format: picoCTF{n} where n is the contents of the eax register in the decimal number base. If the answer was 0x11 your flag would be picoCTF{17}.
# Hints:
- gdb is a very good debugger to use for this problem and many others!
- main is actually a recognized symbol that can be used with gdb commands.
# Commands: 
```
1) yasho@DESKTOP-6ND4URA:~$ file debugger0_a
```
Output: 

debugger0_a: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=15a10290db2cd2ec0c123cf80b88ed7d7f5cf9ff, for GNU/Linux 3.2.0, not stripped
```
2) yasho@DESKTOP-6ND4URA:~$ hexdump -C debugger0_a | head
```
Output: 

The header file had ELF wrtten which means it runs on Linux, and it is also a 64-bit executable file. 

```
3) yasho@DESKTOP-6ND4URA:~$ ./debugger0_a
```
No output.
```
4) yasho@DESKTOP-6ND4URA:~$ gbd
```
Command not found.
```
5) yasho@DESKTOP-6ND4URA:~$ sudo apt install gbd
6) yasho@DESKTOP-6ND4URA:~$ gbd debugger0_a 
```
![image](https://github.com/user-attachments/assets/90909ad4-ca4f-4f44-b9ec-7cb698fe8802)

![image](https://github.com/user-attachments/assets/67eb9b6d-7bde-4e49-8e96-f54e0a00a677)

`disas` and `disassemble` both will work.


# Explanation:
[Refer to this too](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#understanding-gdb-and-elf-files)

This guide provides a detailed, simplified explanation of the GDB (GNU Debugger) session commands and outputs.

## Overview of GDB Commands and Outputs

1. **Starting GDB**:
   - You started GDB by typing `gdb debugger@a`.
   - GDB loaded and displayed some initial information, such as the version and licensing details.
   - It mentions that this version of GDB is configured for `x86_64-linux-gnu`, which means it’s designed for 64-bit Linux systems.

2. **Reading Symbols**:
   - GDB tries to read symbols from the file you’re debugging (in this case, `debugger@a`).
   - **Symbols** are the names and locations of functions and variables in your program, which help GDB understand what’s happening in your code.

3. **Listing Functions with `info functions`**:
   - You typed `info functions` to see all the functions available in your program.
   - GDB lists several functions, including system-level functions like `_init`, `_start`, and `__libc_csu_init`, as well as a function named `main`, which is typically where a C or C++ program starts running.
   - Functions highlighted in yellow, such as `_init` and `main`, are important for running and managing the program’s setup and cleanup tasks.

4. **Disassembling Code with `disassemble main`**:
   - You entered `disassemble main` to view the actual machine instructions for the `main` function.
   - **Disassembling** means GDB is showing the instructions that the CPU follows to execute the function.
   - Each line shown (e.g., `push %rbp`, `mov %rsp,%rbp`) is an instruction for the CPU.
   - Here’s what some of these commands mean:
     - **`push %rbp`**: Saves the current value of the `%rbp` register (which holds a reference to the current stack frame).
     - **`mov %rsp,%rbp`**: Sets up the stack frame for the function by moving the current stack pointer (`%rsp`) to the base pointer (`%rbp`).
     - **`mov $0x86342,%eax`**: Loads the number `0x86342` into a register called `%eax`. Registers are small storage locations in the CPU used to handle data quickly.
     - **`ret`**: Tells the CPU to return from the function.
5. **Printing the contents of the `eax` register**.
   These instructions might seem complex, but essentially, they’re setting up the function’s environment, performing actions, and then cleaning up after the function is done.


## Summary

- **GDB** is a tool for looking at the details of your program, such as functions and memory locations.
- **Disassemble**: GDB shows the CPU instructions in the `main` function. Each line represents an action the CPU takes to run your code.

In short, GDB is helping you look "under the hood" of your program by showing the raw instructions that the CPU runs.

# Flag:
>picoCTF{549698}

# References:
- [GDB](https://www.geeksforgeeks.org/gdb-step-by-step-introduction/)
- [GNU info 1](https://www.reddit.com/r/linux4noobs/comments/k740t9/what_is_gnu_what_does_gnu_stand_for_where_does_it/)
- [GNU info 2](https://www.reddit.com/r/linuxquestions/comments/1dcvvrx/eli5_what_exactly_gnulinux_and_whats_the/)
