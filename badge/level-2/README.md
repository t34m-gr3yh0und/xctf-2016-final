#Puzzle - badge level two 

We are given this cipher (with the phrase a bit off)
```
HMYGR3CTFAOTB3QSK4ICFMCLMQ3U5QSUMX<<<<<<
```

By looking at the ascii table and given the hint, we realised that by incrementing the < by 1 bit, we will get =. Thus we decide to increment the whole string by 1 bit. 

Result
``` 
INZHS4DUGBPUC4RTL5JDGNDMNR4V6RTVNY======
```

Looking at the string, it appears to be a base32 encoded message. Decoding the message will return: 
```
Crypt0_Ar3_R34lly_Fun
```
