# Description:
Our data got corrupted on the way here. Luckily, nothing got replaced, but every block of 3 got scrambled around! The first word seems to be three letters long, maybe you can use that to recover the rest of the message.
Download the corrupted message `here`.
# Solution:
The provided text is 

`heTfl g as iicpCTo{7F4NRP051N5_16_35P3X51N3_V091B0AE}2`

The question says that every BLOCK OF 3 is scrambled so I first divided the entire text into blocks of 3 characters (including the spaces) and noticed a pattern. To avoud confusion, I replaced all spaces in the text with `$` and separated the blocks with spaces.
So, now it can be seen as: 
```
heT fl$ g$a s$i icp CTo
```
Only did this much so far to confirm the pattern. Say, the correct positions are denoted by 123, in the corrupted text it is 231. So I just rearranged them all and got the flag.
After rearrangement: `The flag is picoCTF{7R4N5P051N6_15_3XP3N51V3_109AB02E}`
# Flag:
>picoCTF{7R4N5P051N6_15_3XP3N51V3_109AB02E}
