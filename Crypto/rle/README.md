# RLE 

```
[0:4:0b:26:2f:2f:0:2:3f:70:0:4:07:3f:22:3c:0:2:3e:7b]CPPZ

-> Hello World!


[0:3:1f:2d:24:0:4:2b:27:25:2d:0:1:79:0:4:36:2d:62:1a:0:2:0e:19:0:1:14]HHYBMR

-> Welcome to XCTF


[0:1:1f:0:2:19:0e:0:4:0c:31:18:3f:0:1:2c:0:2:0f:1c:0:3:37:3c:35:0:4:21:3d:0a:10:0:3:2a:27:2b:0:3:28:25:22:0:4:22:1a:12:24:0:1:22:0:3:1e:12:34:0:1:3e:0:4:39:26:3a:2c:0:3:2a:11:1a:0:3:3e:0e:13:0:1:3c:0:3:14:08:24:0:3:2e:33:31:0:3:37:21:21:0:3:31:37:36:0:2:77:2b]GZJBPRUDLEQANINQYKCRXV

-> ?
```

## Solution

We can recognize a same format for the given messages:
'''
[<encrypted code>]<KEY>
'''

Further inspection in the encrypted code, we see hex numbers with 1 or 2 digits.
Another observation is that after each string `0:<n>:` are n two-digit hex numbers. Counting the number of 2-digit hex numbers, we find that it is the same as the length of the decoded string.
-> Each 2-digit hex number represents an ASCII character
The task now is to find the correct key for decryption.

Notice that the number of sequences of consecutive 2-digit hex numbers is exactly the length of <KEY>. Therefore, there should be connection between each hex sequence with the corresponding character in <KEY>.
Our best guest is to XOR each number in each sequence with the respective character in <KEY>.

Python code for decryption:
```
def decrypt(message):
    tmp = message.split(']')
    enc = tmp[0][1:]
    key = tmp[1]

    ans = []
    i = -1
    flag = False
    for s in enc.split(':'):
        if s == '0':
            flag = True
        elif flag:            
            i += 1
            flag = False
        else:
            c = int(s, base=16)^ord(key[i])
            ans.append(chr(c))
            
    return ''.join(ans)
    
message1 = '[0:4:0b:26:2f:2f:0:2:3f:70:0:4:07:3f:22:3c:0:2:3e:7b]CPPZ'
print(decrypt(message1))
message2 = '[0:3:1f:2d:24:0:4:2b:27:25:2d:0:1:79:0:4:36:2d:62:1a:0:2:0e:19:0:1:14]HHYBMR'
print(decrypt(message2))
message3 = '[0:1:1f:0:2:19:0e:0:4:0c:31:18:3f:0:1:2c:0:2:0f:1c:0:3:37:3c:35:0:4:21:3d:0a:10:0:3:2a:27:2b:0:3:28:25:22:0:4:22:1a:12:24:0:1:22:0:3:1e:12:34:0:1:3e:0:4:39:26:3a:2c:0:3:2a:11:1a:0:3:3e:0e:13:0:1:3c:0:3:14:08:24:0:3:2e:33:31:0:3:37:21:21:0:3:31:37:36:0:2:77:2b]GZJBPRUDLEQANINQYKCRXV'
print(decrypt(message3))
```

Flag:
```
XCTF{Run_Length_Encoding_Was_Supposed_To_Be_Compression!}
```
