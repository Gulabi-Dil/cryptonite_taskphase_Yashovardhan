# Description: 
For what argument does this program print `win` with variables 68, 2 and 3? 

File: `chall_1.S` 

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
Like the previious challenge, I used the same site to convert the given assembly code to C program and ended up with this:
```
#include <stdio.h>
#include <stdlib.h>

int func(int a) {
    int b = 68;
    int c = 2;
    int d = 3;
    int result;

    result = b << c; // Equivalent to lsl
    result = result / d; // Equivalent to sdiv
    result = result - a; // Equivalent to sub

    return result;
}

int main(int argc, char *argv[]) {
    int a;

    if (argc > 1) {
        a = atoi(argv[1]);
    } else {
        a = 0; // Default value if no argument is provided
    }

    int result = func(a);
    
    if (result == 0) {
        puts("You win!");
    } else {
        puts("You Lose :(");
    }

    return 0;
}
```
Now, we need to find the argument for which the output of the program will be "You win!". After inspecting the program its understood that output will be "You win!" when the result of the function `func` will be 0. So, I manually computed the value of a needed for this to hold true.
Going through the function `func` in reverse:
```
1. 0=result -a ----> result=a
2. a=result/d  ----> a=(b<<c)/d ----> a=272/3 ----> a=90
```
So, a=90 which is 0x5A in hex. To satisfy the length of the flag, I padded six 0s before 5A. Got the flag!

# Flag:
>picoCTF{0000005A}
