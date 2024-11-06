# Description:
We found this weird message being passed around on the servers, we think we have a working decryption scheme.
Download the message here.

Take each number mod 37 and map it to the following character set: 0-25 is the alphabet (uppercase), 26-35 are the decimal digits, and 36 is an underscore.
Wrap your decrypted message in the picoCTF flag format (i.e. picoCTF{decrypted_message})
# Solution:
Wrote a program for it in C.

```
#include<stdio.h>
int main()
{
    int cipher[]={128,322,353,235,336,73,198,332,202,285,57,87,262,221,218,405,335,101,256,227,112,140};
    int i,j;
    char dec[]={'0','1','2','3','4','5','6','7','8','9'};
    int rem[22];
    for(i=0;i<22;i++)
    {
         rem[i]=cipher[i]%37;
    }
    char flag[22];
    for(i=0;i<22;i++)
    {
        if(rem[i]>=0 && rem[i]<=25)
        flag[i]=(char)(rem[i]+'A');
        else if(rem[i]>=26 && rem[i]<=35)
        {
           flag[i]=dec[rem[i]-26];
        }
        else
        flag[i]='_';
    }
    printf("Flag is: ");
    for(i=0;i<22;i++)
    printf("%c",flag[i]);
}
```

Output: `Flag is: R0UND_N_R0UND_79C18FB3`

# Flag:
>picoCTF{R0UND_N_R0UND_79C18FB3}
