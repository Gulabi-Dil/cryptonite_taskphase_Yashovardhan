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

# Not Noice
## Description:
You finally find your way to the center of the maze! However, you quickly realize that IOI has discovered your presence. An urgent audio message echoes around you: "There has been a breach in the servers! Send backup immediately! They must not find their way to theâ€¦" You strain to catch the rest, but the recording abruptly devolves into a chaotic mix of beeps and garbled words. Can you decipher the true message hidden within the noise?
## Attachment:
https://drive.proton.me/urls/N2ATEN2EMR#001mtOYLDqOq
## Writeup:
The audio file sounded like Morse code so I used an [online Morse audio decoder](https://morsecode.world/international/decoder/audio-decoder-adaptive.html) and got the flag `OASIS{5P3CT0GR4M_15_TH3_C00L35T}`

# Nom-Nom
## Description:
The control room door looms before you, locked yet again. Frustration rises, but this isnâ€™t the time to give in. The door is guarded by a â€¦ PACMAN?!!. But he doesnâ€™t seem to be moving.. and giving you way. He looks hungry and angry?
## Attachment:
https://pacman.oasis.cryptonite.live/
## Writeup:
Knew it has to do something with inspect. Tried editing the codes in elements tab and writing codes in console tab to identiy myself as the admin. Didn't work so I went through the remaining tabs in inspect. In the Application tab, the cookies section had an entry which said the value of admin is _false_. I edited it to _true_ and refreshed the page. It worked and the pacman ate the balls and displayed the flag `OASIS{p@cman_l!k3d_y0ur_c00k!3_<3}`

# Quence your thirst
## Description:
How could the IOI overlook such a critical flaw? You now possess administrative privileges! Surveying your surroundings, you notice the monitor displaying a series of commands accessible only to the admin. However, another security measure is in placeâ€”it's encrypted, and only the true admin knows the key. Can you crack this encryption scheme?
## Attachment:
https://drive.proton.me/urls/ZJSW96F7XM#TqIaYLkuvsQD
## Writeup:
Used cipher identifier in [boxentriq](https://www.boxentriq.com/code-breaking/cipher-identifier) to identify the type of cipher. Copy paste the cipher text in an online tool to decode the given type of cipher.

#### Plain Text:
AS THE PROTAGONIST STUMBLED INTO THE HEART OF THE IOIS TRAP THE WALLS AROUND HIM FLICKERED WITH SCORCHING HEAT A MASSIVE IMPENETRABLE FIREWALL ROARED IN EVERY DIRECTION CUTTING OFF HIS ESCAPE THE IOI HAD ANTICIPATED HIS INFILTRATION AND THIS WAS THEIR FINAL GAMBIT TO STOP HIM BUT ARTEMIS HAD LEFT HIM WITH A GIFT A COMPUTER TERMINAL IN THE CENTER OF THE CHAMBER THE SCREEN BLINKED TO LIFE AWAITING INPUT WITH A FLASH OF INSPIRATION HE REALISED WHAT HE NEEDED TO DO ADMIN PRIVILEGES HAD BEEN UNLOCKED THE COMMANDS HE EGGSECUTED HERE COULD DISMANTLE THE FIREWALL AND ALLOW HIM TO REACH THE HEART OF THE VIRUS IF HE FOLLOWED THE CORRECT ORDER THE LIST OF ADMIN COMMANDS APPEARED ON THE SCREEN ADMIN COMMAND LIST FIREWALL BYPASS

1 VERIFY THE CURRENT STATUS OF THE FIREWALL SCANNING FOR VULNERABILITIES IN THE DEFENSE SYSTEMS

2 DISABLE THE FIREWALLS AUTOREPAIR MECHANISM WHICH REGENERATES ANY BREACHED SECTIONS

3 DISPLAY ALL ACTIVE FIREWALL LAYERS THIS REVEALS THE NUMBER OF DEFENSIVE LAYERS AND THEIR RESPECTIVE CONFIGURATIONS

4 MANUALLY DISABLE THE THIRD FIREWALL LAYER WHICH HAS BEEN IDENTIFIED AS THE STRONGEST BARRIER PROTECTING THE CORE

5 SCAN FOR MALICIOUS PATTERNS THAT MIGHT BE HIDDEN INSIDE THE FIREWALL CODE THIS HELPS NEUTRALISE ANY TRAPS LAID BY IOI

6 ISOLATE THE SIGNATURE FILE USED BY IOI TO SUSTAIN THE FIREWALLS INTEGRITY

7 OVERRIDE THE FIREWALLS ENCRYPTION WITH THE HIGHEST LEVEL ADMIN PRIVILEGES BREAKING IOIS CONTROL OVER IT

8 EGGSECUTE A COMPLETE SHUTDOWN OF ALL FIREWALL LAYERS LEAVING THE SYSTEM UNPROTECTED FOR A BRIEF MOMENT

9 RESET THE ACCESS CONTROLS TO OASIS GATEWAYS ALLOWING UNRESTRICTED MOVEMENT THROUGH THE SERVERS THE TERMINAL BEEPED WITH EACH SUCCESSFUL COMMAND EGGSECUTION AND THE HEAT 
AROUND HIM BEGAN TO FADE WITH EVERY FIREWALL LAYER DEACTIVATED THE PATH FORWARD BECAME CLEARER HE WAS ALMOST THROUGH ONLY ONE FINAL COMMAND TO DISABLE THE LAST OF IOIS TRAPS AND HE WOULD HAVE ACCESS TO THE VIRUS CONTROLS THE FATE OF THE OASIS WAS NOW IN HIS HANDS.
HTTPS://KATB.IN/YXNZORQJ
## Writup (continued):
The link is altered though. Upon one to one mapping of the letters T,U,Z,I,O,Y,P from the link `DLLWB://RGLM.QZ/TUZIOYPJ` cipher text to the plain text `HTTPS://KATB.IN/YXNZORQJ`, I found out that only 4 of 8 characters have the correct positions so I used PnC for the positions of the remaining letters. Made the combinations manually. A combination finally matched and I got the flag `oasis{fr3qu3nt_j4!l_br34k1ng_m4k3s_!t_t00_3asy_fr}`

# Git Gud
## Description:
You decrypt the code and follow all the commands. However, as you think you have breached the firewall, the screen goes black and random numbers start glitching on the screen. You realize that the OASIS realizes that they have left admin privileges and are messing with the computer in order for you not to be able to perform the final push.
## Attachment:
https://drive.proton.me/urls/NPCS7GTQPM#EDDwiQ6UtuK tehe disthin likes olso laters.
## Description:
The attachment shared is actually a zip fie which upon extraction will show that there's a research paper on RPO. The flag is spelled out in the git commit messages shown through `git log`. Solve the shell command: `git log | grep '    ' | tac | tr -d ' ' | tr -d '\n'`

Instead of solving the command, we can also see the pdf which contains the flag written in the form of commits in git. Got all the characters together and got the flag `OASIS{g3t_gu663r_4t_g!t!!`

# Stairway to Heaven
## Description:
The ground beneath you trembles as Tetris blocks rain from the shadows, cascading down like a storm. At first, panic sets in, but then you realize: these blocks aren't meant to crush youâ€”they're your escape. Each piece, carefully arranged, could form a staircase to the control room floating above in the void. It's time to use them strategically and rise to safety. Stack the blocks and find your way out!
## Attachment:
https://drive.proton.me/urls/NMT01V9DBW#zn1evKwtdD4y
## Writeup:
The attached file is an executable game. Executed the file in linux terminal which displayed a heavily pixelated image. Then didn't get any idea what to do after it. Teammate found some series of readable numbers in the middle of the file. Seemed like ASCII values so we converted that to plain text and got the flag `OASIS{v34y_f4ncy_AN5I}`

# I have been falling for 30 minutes!
## Description:
It hits you! The IOI uses an encrypted communication service to control the virus's every move. Your mission is clear: sever the link between the IOI and the virus to isolate and defeat it. However, you linger too long in one place, and the IOI catches wind of your plan. Fortunately for them, they have a firewall jail just beneath the surface. The ground trembles and splits open, sending you plummeting into the abyss. You land with a resounding THUD, surrounded by towering firewalls. You see a computer in the middle of the cell, and feel like you can use it to your advantage. Can you break free from this digital prison? 
## Attachment:
https://firewall.oasis.cryptonite.live/
## Writeup:
After going through the website properly, saw that it had 6 web pages. The roles were in increasing order of heirarchy which made me think if there's any role higher than the 5 mentioned in the website for which I tried editing the URL to `userid=6`. This gave the flag `OASIS{T00_m4ny_h0urs_4nd_wh3r3_d1d_1t_l34d}`

# Heads up, tails down
## Description:
Finally, you step into the admin control room. Decay has overtaken the spaceâ€”screens flicker, panels glitch, and virus-riddled code runs rampant across every surface. The system is on the brink of collapse. You sit at the central terminal, but it's unresponsive, frozen by the infection. It's up to you to repair the system and revive the decaying screens. Only then can you regain control.
## Attachment:
https://drive.proton.me/urls/475BPAQZ44#S4D5x7911lhg
## Writeup:
Tried reading the raw data/metadata of the attached file but didn't work. Then spent a lot of time trying to uncorrupt the file online but in vain. Finally, read about magic bytes, a differentiator among different kinds of files. All files are recognized differently by their unique magic bytes i.e. the initial bytes in hex analysis. Searched up the magic bytes of a `.png` file and edited the bytes of the corrupted file online using a [hex editor](https://hexed.it/). Saved this file and it was actually an image which had a drawing of cryptonite logo and the flag `OASIS{h34d_c4rr135}`

# All that for a Drop of Blood
## Description:
As the terminal roars back to life, a single message blinks on the screen: "START GAME." You're no longer just a playerâ€”you're in the endgame now. The keyboard before you looks deceptively simple, but nothing you try gets past the loading screen. Something is clearly wrong. Can you uncover the hidden flaw and push beyond this stagnant start?
## Attachment:
https://startgame.oasis.cryptonite.live/
## Writeup:
First need to set your UserAgent to OASISPlayer and send a POST request on /game endpoint.

The response is: errorMessage "Can you give me the name of the Student Project organizing this event as a url parameter 'name'?"

So send a POST request with query parameter name=Cryptonite to /game like so: /game?name=Cryptonite. (Uppercase or lowercase dosen't matter).

The response is : errorMessage "Do you know you can chain query parameters? Add a 'rank' parameter and give the current CTFTime rank of the project on /givemetheFlag".

So send a POST request with query parameter name=Cryptonite&rank=4 to /givemetheFlag like so: /givemetheFlag?name=Cryptonite&rank=4.

`OASIS{G37_d035_n07_4lw4y5_G37_th1ng5}`
