# Description:
A new modular challenge!

Download the message `here`.

Take each number mod 41 and find the modular inverse for the result. Then map to the following character set: 1-26 are the alphabet, 27-36 are the decimal digits, and 37 is an underscore.

Wrap your decrypted message in the picoCTF flag format (i.e. picoCTF{decrypted_message})
# Solution: 
Looked up what mod inverse is and how to calculate it. Wrote a program for it in C.
```
#include<stdio.h>
int main()
{
    int cipher[]={268, 413, 438, 313, 426, 337, 272, 188, 392, 338, 77, 332, 139, 113, 92, 239, 247, 120, 419, 72, 295, 190, 131};
    int i,j,modinv[23];
    for(i=0;i<23;i++)
    {
        
        for(j=0;j<41;j++)
        {
            if((cipher[i]*j)%41==1)
            modinv[i]=j;
        }
    }
    char dec[]={'0','1','2','3','4','5','6','7','8','9'};
    
   
    char flag[23];
    for(i=0;i<23;i++)
    {
        if(modinv[i]>=1 && modinv[i]<=26)
        flag[i]=(char)(modinv[i]-1+'A');
        else if(modinv[i]>=27 && modinv[i]<=36)
        {
           flag[i]=(char)(modinv[i]-27+'0');
        }
        else
        flag[i]='_';
    }
    printf("Flag is: ");
    for(i=0;i<23;i++)
    printf("%c",flag[i]);
}
```
# Flag:
>picoCTF{1NV3R53LY_H4RD_8A05D939}
