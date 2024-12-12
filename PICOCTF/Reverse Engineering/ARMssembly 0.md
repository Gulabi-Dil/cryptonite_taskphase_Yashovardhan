# Description:
What integer does this program print with arguments 266134863 and 1592237099? 

File: `chall.S` 

Flag format: picoCTF{XXXXXXXX} -> (hex, lowercase, no 0x, and 32 bits. ex. 5614267 would be picoCTF{0055aabb})

The file provided is:
```
	.arch armv8-a
	.file	"chall_1.c"
	.text
	.align	2
	.global	func
	.type	func, %function
func:
	sub	sp, sp, #32
	str	w0, [sp, 12]
	mov	w0, 68
	str	w0, [sp, 16]
	mov	w0, 2
	str	w0, [sp, 20]
	mov	w0, 3
	str	w0, [sp, 24]
	ldr	w0, [sp, 20]
	ldr	w1, [sp, 16]
	lsl	w0, w1, w0
	str	w0, [sp, 28]
	ldr	w1, [sp, 28]
	ldr	w0, [sp, 24]
	sdiv	w0, w1, w0
	str	w0, [sp, 28]
	ldr	w1, [sp, 28]
	ldr	w0, [sp, 12]
	sub	w0, w1, w0
	str	w0, [sp, 28]
	ldr	w0, [sp, 28]
	add	sp, sp, 32
	ret
	.size	func, .-func
	.section	.rodata
	.align	3
.LC0:
	.string	"You win!"
	.align	3
.LC1:
	.string	"You Lose :("
	.text
	.align	2
	.global	main
	.type	main, %function
main:
	stp	x29, x30, [sp, -48]!
	add	x29, sp, 0
	str	w0, [x29, 28]
	str	x1, [x29, 16]
	ldr	x0, [x29, 16]
	add	x0, x0, 8
	ldr	x0, [x0]
	bl	atoi
	str	w0, [x29, 44]
	ldr	w0, [x29, 44]
	bl	func
	cmp	w0, 0
	bne	.L4
	adrp	x0, .LC0
	add	x0, x0, :lo12:.LC0
	bl	puts
	b	.L6
.L4:
	adrp	x0, .LC1
	add	x0, x0, :lo12:.LC1
	bl	puts
.L6:
	nop
	ldp	x29, x30, [sp], 48
	ret
	.size	main, .-main
	.ident	"GCC: (Ubuntu/Linaro 7.5.0-3ubuntu1~18.04) 7.5.0"
	.section	.note.GNU-stack,"",@progbits
```
# Solution:
First I checked the file type using 
```
yasho@DESKTOP-6ND4URA:~$ file /mnt/c/Users/hvpan/Downloads/chall.S
````
Output: `/mnt/c/Users/hvpan/Downloads/chall.S: assembler source, ASCII text`

I looked up what assembler source code is on google and got to know this:

**_The Assembler is a Software that converts an assembly language code to machine code. It takes basic Computer commands and converts them into Binary Code that Computer's Processor can use to perform its Basic Operations. These instructions are assembler language or assembly language._**

I searched if there is any site which converts assembly code to our human readable program and ended up with this [site](https://www.codeconvert.ai/assembly-to-c-converter). I converted the assembly code to C program and got this:
```
#include <stdio.h>
#include <stdlib.h>

int func1(int a, int b) {
    if (b <= a) {
        return a;
    } else {
        return b;
    }
}

int main(int argc, char *argv[]) {
    int a, b;
    if (argc > 2) {
        a = atoi(argv[1]);
        b = atoi(argv[2]);
        int result = func1(a, b);
        printf("Result: %d\n", result);
    }
    return 0;
}
```
Funciton `func1` returns the greater number of the two inputs. Main function will run only if 2 arguments are passed to the program. `atoi` is a C program funciton which converts string to integer.
So, I ran this program in VS Code terminal with the arguments 
```
PS C:\Users\hvpan\OneDrive\Desktop\MIT Y1\CODING AND APPS> gcc  handling1.c -o handling1
PS C:\Users\hvpan\OneDrive\Desktop\MIT Y1\CODING AND APPS> ./handling1 266134863 1592237099
```
`Result: 1592237099`

Converting the result to hexadecimal, we get `5EE79C2B`. Got the flag!

# Flag:
>picoCTF{5EE79C2B}
