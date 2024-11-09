# Description: 
How about some hide and seek heh?
Look at this image here.

![atbash](https://github.com/user-attachments/assets/5e615883-39f0-4e6a-81ff-7885523610c4)


# Solution:
First checked the metadata of the image using a metadata viewer online. Didn't get anything so recalling the few steghide questions that I have solved before, I tried extracting hidden data using steghide (since the name also suggests hidden data).
Nothing about passphrase is mentioned so I jsut entered a blank passphrase (sometimes blank passphrases are set but they're not secure). It worked and the extracted data got written to `encrypted.txt`. 

`cat encrypted.txt` gave the ciphertext: `krxlXGU{zgyzhs_xizxp_1u84w779}`


Now, its obvious that the image was the mapping of the alphabets used in the cipher so after the respective mappings, I got the flag.

# Flag:
>picoCTF{atbash_crack_1f84d779}
