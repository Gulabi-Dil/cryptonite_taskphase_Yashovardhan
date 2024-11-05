# Description:
This vault uses for-loops and byte arrays. The source code for this vault is here: VaultDoor3.java
# Hints:
Make a table that contains each value of the loop variables and the corresponding buffer index that it writes to.
# Solution:

I first tried copy pasting the same password type thing mentioned in the java code as the flag which was obviously incorrect. Then simple logic was to reverse the program, which I did in C.

```
#include <stdio.h>
#include <string.h>

int main() {
    char password[] = "jU5t_a_sna_3lpm12g94c_u_4_m7ra41";
    char buffer[33];  // Allocate one extra space for null-terminator
    int i;
    for (i = 0; i < 8; i++) {
        buffer[i] = password[i];
    }

    for (; i < 16; i++) {
        buffer[i] = password[23 - i];
    }

    for (; i < 32; i += 2) {
        buffer[i] = password[46 - i];
    }

    for (i = 31; i >= 17; i -= 2) {
        buffer[i] = password[i];
    }

    buffer[33] = '\0';
    printf("Correct password: %s\n", buffer);
    return 0;
}
```
Output: `Correct password: jU5t_a_s1mpl3_an4gr4m_4_u_c79a21`

# Flag:
>picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_c79a21}
