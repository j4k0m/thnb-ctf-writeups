# thnb-ctf-writeups
Writeups for the challenges I made for THNB national CTF

## Another Easy Crypto

```python
from Crypto.Cipher import AES

def decrypt(key, enc):
    try:
        cipher = AES.new(key, AES.MODE_ECB)
        return cipher.decrypt(enc)
    except Exception:
        pass
    return 0

with open("flag.dat", "rb") as flag:
    flag = flag.read()
    print("FLAG: ", flag)

for key in open("/usr/share/wordlists/rockyou.txt", "rb"):
    key = key.strip()
    padded_key = key + bytes(b"\x00" * (16 - len(key)))
    decrypted = decrypt(padded_key, flag)
    if decrypted != 0:
        if b'thnb{' in decrypted:
            print(decrypted)
```

convert hexa flag to bin for better result (https://tomeko.net/online_tools/hex_to_file.php?lang=en) 

![image](https://user-images.githubusercontent.com/48088579/163746213-2876af5f-0793-48f4-bbee-9c3f65821a75.png)

## Shuffled

```python
print("".join(chr(max(list(map(ord, line)))) for line in open("flag.txt", "r").readlines()))
```

![image](https://user-images.githubusercontent.com/48088579/163746279-19d6ac89-8308-40d8-96e2-d4ea38eb576d.png)

## this is super easy

```python
flag = [0x75, 0x69, 0x6f, 0x63, 0x7a, 0x4e, 0x6f, 0x32, 0x5e, 0x62, 0x69, 0x35, 0x73, 0x5e, 0x79, 0x6e, 0x53, 0x7c]

for i in range(0, 255):
    c = "".join(list(map(chr, [j ^ i for j in flag])))
    if "thnb{" in c:
        print(c)
```

![image](https://user-images.githubusercontent.com/48088579/163746296-1ca173f6-96cd-4a57-b134-049aa9e1e72e.png)

## 1337 Director

```python
from itertools import cycle

flag = [0x38, 0x09, 0x0f, 0x10, 0x19, 0x24, 0x19, 0x2d, 0x56, 0x43, 0x32, 0x25, 0x09,0x3e, 0x02, 0x1a,0x56, 0x1b, 0x13, 0x19,0x51,0x00,0x3d, 0x01, 0x09, 0x29, 0x24, 0x3a, 0x07, 0x14]

base = "Larbi"

def xor(key):
    key = key.encode("utf-8")
    xored = ''.join(chr(c^k) for c,k in zip(flag, cycle(key)))
    if "thnb" in xored:
        print(xored)

def decrypt(char):
    i = 1
    new_string = ""
    while i < len(base):
        new_string = base[:i] + char + base[i:]
        xor(new_string)
        i += 1

for i in range(33, 126):
    char = chr(i)
    decrypt(char)
```

or you can do it manually.

![image](https://user-images.githubusercontent.com/48088579/163746340-2f2242eb-f593-4f2a-a137-3c1e7cda9de5.png)

![image](https://user-images.githubusercontent.com/48088579/163746352-fc1c6189-6df0-490e-8cd2-0ad94ae42231.png)


## Easy Crypto

```python
flag = [12644, 10088, 11330, 8918, 14268, 2058, 8360, 4680, 2340, 2640, 2244, 8360, 11118, 2340, 2640, 4680, 8360, 2744, 6630, 2640, 800, 8360, 2058, 8360, 5244, 1968, 6794, 2244, 8360, 5100, 13328, 2340, 4148, 12198, 2340, 2640, 2058, 4020, 14750]

for i in flag:
    for j in range(33, 126):
        if pow(j,2)-(7*j) == i:
            print(chr(j), end="")
```

![image](https://user-images.githubusercontent.com/48088579/163746375-5b4fbc26-96d3-4188-a08a-27fdc2c9f866.png)


## Loader
Soon..
