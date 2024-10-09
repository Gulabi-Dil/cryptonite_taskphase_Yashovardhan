# Ready Player One?
## Description:
Instead of being greeted by the familiar login screen, you find yourself enveloped by darkness, a very distorted sound playing around you. He tries to remove his headset but a warning pops up reading, "Any attempts to logout of the OASIS will result in full character deletion. PROCEED CAREFULLY". What?! What is happening here? Decode the secret message to find out. The flag format is OASIS{ALL_CAPS}.
## Attachment:
https://drive.proton.me/urls/DG7JWJR6F8#7VaiabqOGg82
## Writeup:
The audio indicates the dot dash pattern of Morse code. Decoded the morse code using an [online decoder](https://morsecode.world/international/decoder/audio-decoder-adaptive.html).
The decoded message was the flag `OASIS{M0R5E_M4N1PU7470R}`

# Arte-Miss?
## Description:
As the darkness recedes, Halliday's voice echoes with the chilling news that Innovative Online Industries (IOI) has seized control of the OASIS. A virus has infected the main server, sparking widespread panic as players lose their progress. Amidst the chaos, Artemis materializes before you, her avatar flickering erratically. With a sense of urgency, she thrusts a file into your hand and whispers something unintelligible before dissolving into a cascade of pixels. Stunned and disoriented, you scrutinize the mysterious file, desperate to understand its significance. Just then, a calming voice cuts through the turmoilâ€”it's Artemis, speaking from the real world. She reveals that the file holds the key to liberating the OASIS from IOI's grip. Though she was captured and her character deleted, she managed to pass this vital piece of information to you in a final act of defiance. Find the flag hidden in the file.
## Attachment:
https://drive.proton.me/urls/VDMJTAVBH4#nCpqsQV4fGjN
## Writeup:
Tried to find some clues in the photo itself initially but didn't found anything. Then thought of reading its raw data or metadata. First found the metadata using an [online tool](https://www.metadata2go.com/result#j=64e564af-4c8c-44ba-85e3-2465f64e84ba).
In the metadata, the artist's name was the flag `OASIS{m4ta_af_04515}`

# This or that?
## Description:
Recognizing the phrase, a golden key materializes in your hand. Your eyes fall upon an engraving on the keyâ€”a sequence of characters: 036363127c7c60001a117c6463170b, and on the opposite side, the words ARTEMIS_WHISPER. The cryptic string seems like a puzzle in itself. As you examine it, you realize that the key's true value might not lie in its size but in the secret it carries. The numbers and letters might be concealing a deeper meaning, one that could unlock the door if only you can decipher it. The characters may need to be transformed or combined in a specific way, **exclusively**, or through an unconventional method, to reveal the key's true purpose. The flag format is OASIS{ALL_CAPS}.
## Writeup:
036363127c7c60001a117c6463170b looks hexadecimal text so first tried to convert hexadecimal to normal text using an [online tool](https://www.duplichecker.com/hex-to-text.php)
but the converted text was smething weird and barely readable. Then read the description again and again and found the clue:

_The characters may need to be transformed or combined in a specific way, **exclusively**, or through an unconventional method, to reveal the key's true purpose._ 

Remembered about the XOR thing I did during the layered challenge by cryptonite and the words `key`, `transformed` and `combined` sort of confirmed my guess. Used an [online tool](https://md5decrypt.net/en/Xor/) to perform the XOR decryption and got the part of the flag we write inside {}: B17W153_MY573RY. Thus flag is: `OASIS{B17W153_MY573RY}`

# Jekylle and Hide!
## Description:
As you discover the secret of the key, it enlarges and splits into two parts, flying to different areas of the library. You try to follow one, but it's too fast and quickly hides among the books. To recover the key, you need to inspect every part of the library to find both pieces. 
## Attachment:
https://jekylle-and-hide.oasis.cryptonite.live
## Writeup:
First wrote my OASIS site username in the search bar but didn't work. Then I skimmed through all the photos and tried finding clues or patterns hidden in them, if any but failed. Since it's a website, I opened inspect element and went through the elements, source tabs. The books.js file in the source tab had a variable initialized as `OASIS{th15_15_part1_`.

In the code, there was an if statement i.e. `if (inputValue === desiredValue)` which made me realize that the username for website will be the first half of the flag. Entered the username after which it was asking for a pin.

Since there was nothing else in books.js which seemed like a clue, I read the style.css file in the source tab which had an input value mentioned i.e. `7928` so I entered it as pin which gave me the second half of the flag `@nd_h3r3_go35_1h3_n3xt!!}`.

Another method was I saw just now while doing writeups was:
I read the file script.js in the source tab which had a variable initialized as `@nd_h3r3_go35_1h3_n3xt!!}`. The format was that of a flag, the second half of the flag, to be precise. `@nd_h3r3_go35_1h3_n3xt!!}` Thus got the flag 'OASIS{th15_15_part1_@nd_h3r3_go35_1h3_n3xt!!}'

# Keynough is enough
## Description:
You find both parts of the key and reach the door, but realize that in order to activate the keyhole you need to decipher an inscription: KHAAH{W1C3J7_C1O3F3G3} on the door. Artemis suggests you WHISPER to it. To crack the code, consider a method that involves a repeating patternâ€”like adding a touch of vinegar to a recipe to reveal its true flavor. The flag format is OASIS{ALL_CAPS}.
## Writeup:
Since the word decipher is used, it is understood that the provided inscription is a cipher text. The word `vinegar` was a clue that vigenere cipher decoder has to be used for decoding.

Used an [online vigenere cipher decoder](https://cryptii.com/pipes/vigenere-cipher) and used WHISPER as key and got the flag `OASIS{S1L3N7_V1G3N3R3}`

# BasiKEllY:
## Description:
The keys, as if possessed by some unseen force, and become one. They now begin to whisper. Their voice, a soft murmur, weaves a cryptic sequence of letters and numbers: J5AVGSKTPNWDA53LGN4V65BQGBPXGMDGORPXG4BQNMZW4XZTNB6Q==== The string seems nonsensical at first glance, but you sense a hidden message within. Your task is clear: decrypt the enigma whispered by the key.
## Writeup:
Used an online [Multi Decoder](https://www.cachesleuth.com/multidecoder/) and decoded the text `J5AVGSKTPNWDA53LGN4V65BQGBPXGMDGORPXG4BQNMZW4XZTNB6Q====`. Since there were too many decryptions, I searched the page for OASIS and found the flag in base32 section. Flag was `OASIS{l0wk3y_t00_s0ft_sp0k3n_3h}`

# Knock Knock
## Description:
At last, the key darts towards the door, a keyhole materializes, and the door swings open. Author''s Note: I don''t know about you, but I was definitely growing tired of this key. You find yourself standing at the entrance of a labyrinth. The only way out is to navigate through the labyrinth itself. However, the entrance is guarded by an image recognition system. A QR code is pasted on the wall beside it. Your task is clear: bypass the system to gain entry.
## Attachment:
https://drive.proton.me/urls/8MH5Q996T8#TPFQm3DTEwN5
## Writeup:
The QR code image had distortions/drawings over it which made it unable to get scanned. I tried searching for online tools which could somehow clear the drawings but didn't find any. Then I tried editing the QR photo by adjusting color shemes, saturation, brightness etc. which got rid of the drawing. Scanned the QR and got the flag `OASIS{qu3u3r_r3c0v3r3r}`

# Microsoft StrongEdge
## Description:
Upon repairing the QR code, you scan it and discover it contains a file. As you meticulously sift through its contents, nothing of value seems to emerge. The mystery deepensâ€”where could the next clue be hidden? The flag is concealed within the file. Sharpen your skills and uncover them!
## Attachment:
https://drive.proton.me/urls/3TZSZBC8EC#y0jTotNueZ83
## Writeup:
First tried looking for anything in the file but didn't find anything. Then opend the view tab and used Slide Master to check for anything that was hidden as clue in the formatting of the ppt but found nothing. Then changed the file from .pptx to .zip and extracted its contents, browswing through which I found an image file which contained `BNFNV{e0g4g0e_0s_cc75}` and a number `13`. 

Since the format is that of the flag, the number was a clue for using a cipher. Searched in google the type of ciphers and found `ROT13` (because of the number 13). Used an [online ROT13 cipher decoder](https://rot13.com/) which gave me the flag `OASAI{r0t4t0r_0f_pp75}` 

# 
