# AlphaCTF2k24
## chaos
### Challenge Description

In this challenge, we explore the realm of cryptography created from chaos. The challenge provides a Python code snippet that generates a pseudo-random number generator (PRNG) output, which is then used to encrypt a flag using the AES encryption algorithm. The goal is to reverse engineer the PRNG to predict the AES key and decrypt the flag.

### Given Code Snippet

```python
#!/usr/bin/env python3

from Crypto.Util.number import bytes_to_long
from Crypto.Cipher import AES
from Crypto.Util.Padding import pad
from flag import FLAG
from random import getrandbits 

def getRandom(bits, rounds):
    for _ in range(rounds):
        a = getrandbits(bits)
        print(f'{a}')
    a = getrandbits(bits)
    return a.to_bytes(32, 'little')

key = getRandom(256, 100)
iv = b"alpha_gift_for_u"

cipher = AES.new(key, AES.MODE_CBC, iv)
enc = cipher.encrypt(pad(FLAG,AES.block_size))
print(f'enc={bytes_to_long(enc)}')

```

## Solution Approach

