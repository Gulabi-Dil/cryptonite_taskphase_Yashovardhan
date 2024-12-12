# Description:
Can you get sense of this `code file` and write the function that will decode the given encrypted file content.

Find the encrypted file here `flag_info` and code file might be good to analyze and get the flag.

# solution:
The code provided is:
```
from random import randint
import sys


def generator(g, x, p):
    return pow(g, x) % p


def encrypt(plaintext, key):
    cipher = []
    for char in plaintext:
        cipher.append(((ord(char) * key*311)))
    return cipher


def is_prime(p):
    v = 0
    for i in range(2, p + 1):
        if p % i == 0:
            v = v + 1
    if v > 1:
        return False
    else:
        return True


def dynamic_xor_encrypt(plaintext, text_key):
    cipher_text = ""
    key_length = len(text_key)
    for i, char in enumerate(plaintext[::-1]):
        key_char = text_key[i % key_length]
        encrypted_char = chr(ord(char) ^ ord(key_char))
        cipher_text += encrypted_char
    return cipher_text


def test(plain_text, text_key):
    p = 97
    g = 31
    if not is_prime(p) and not is_prime(g):
        print("Enter prime numbers")
        return
    a = randint(p-10, p)
    b = randint(g-10, g)
    print(f"a = {a}")
    print(f"b = {b}")
    u = generator(g, a, p)
    v = generator(g, b, p)
    key = generator(v, a, p)
    b_key = generator(u, b, p)
    shared_key = None
    if key == b_key:
        shared_key = key
    else:
        print("Invalid key")
        return
    semi_cipher = dynamic_xor_encrypt(plain_text, text_key)
    cipher = encrypt(semi_cipher, shared_key)
    print(f'cipher is: {cipher}')


if __name__ == "__main__":
    message = sys.argv[1]
    test(message, "trudeau")
```
The encryption may look difficult af but its easy, just a bit lengthy to understand.

It undergoes 2 rounds of encryption. In the first round, the reversed plaintext is being XORed with key_char, which selects characters from the text_key, `trudeau` according to the current iteration of the loop and the length of the text_key.
This gives us the semi_cipher which further undergoes encryption in the 2nd round. In the 2nd round, each character of the semi_cipher is multiplied with shared_key and 311 and the final ciphertext is stored in an array called cipher. The computation of keys can be done directly with the values of a,b given in the file provided and the function `generator` in the program. Before proceeding to the main task I had also run an if statement to confirm that shared_key=key, which is true.

So I wrote a decryption program:
```
import math

def generator(g, x, p):
    return pow(g, x) % p

a = 95
b = 21
p = 97
g = 31
u = generator(g, a, p)
v = generator(g, b, p)
key = generator(v, a, p)
b_key = generator(u, b, p)
shared_key = key

cipher=[237915, 1850450, 1850450, 158610, 2458455, 2273410, 1744710, 17447>textkey = "trudeau"
keylen = len(textkey)
semicipher = ""
for i in cipher:
    semicipher += chr(i//(shared_key*311))
print("Semi cipher = ", semicipher)
def dynamic_xor_decrypt(cipher_text, text_key):
    decrypted_text = ""
    key_length = len(text_key)
    for i, char in enumerate(cipher_text):
        key_char = text_key[i % key_length]
        decrypted_char = chr(ord(char) ^ ord(key_char))
        decrypted_text += decrypted_char
    return decrypted_text[::-1]
print(dynamic_xor_decrypt(semicipher,textkey))
```
Output:
```
Semi cipher =   FF]VBBD*SDV>␦3 1␦

picoCTF{custom_d2cr0pt6d_66778b34}
```
Got the flag!

# Flag:
>picoCTF{custom_d2cr0pt6d_66778b34}

# Mistakes:
One silly mistake I did at first was reversing the semicipher before the decryption which was giving me the incorrect output since I broke the reversal path during decryption.
```
def dynamic_xor_decrypt(semicipher, text_key):
    plain = ""
    key_length = len(text_key)
    for i, char in enumerate(semicipher[::-1]):
        key_char = text_key[i % key_length]
        decrypted_char = chr(ord(char) ^ ord(key_char))
        plain+=decrypted_char

print(dynamic_xor_decrypt(semicipher,textkey))
```
Pretty good challenge! :)
