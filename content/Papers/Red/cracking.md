
> **Note**: Some WPA cracking using hashcat has been covered in [[WPA2]] 

---
### identification
```bash
haiti samples $REF
hashid
hash-identifier
```

---
#### Distributed cracking

> ref: https://hackingvision.com/2020/03/30/distributed-hash-cracking-hashcat-hashtopolis-tutorial/

**TODO**
https://hashcat.net/forum/thread-3386.html

---

> source : https://medium.com/@petergombos/lm-ntlm-net-ntlmv2-oh-my-a9b235c58ed4

Once you captured a NTLMv2 hash (for example with responder), you can crack it with the following:

example ntlmv2 hash.txt:
```
sql_svc::sequel:339330ba58f04310:BF0E6C684DE32264FED24BCACCE23C95:010100000000000080E3E62D5E49D901176CC45D75E3713A0000000002000800430043005200340001001E00570049004E002D005000480054004200510035005A005A0037004900540004003400570049004E002D005000480054004200510035005A005A003700490054002E0043004300520034002E004C004F00430041004C000300140043004300520034002E004C004F00430041004C000500140043004300520034002E004C004F00430041004C000700080080E3E62D5E49D901060004000200000008003000300000000000000000000000003000002FC72D2C16CA1C3877FB2DBA65EEFD0CE9C35C5D1F1ABC50C506B6198F8EC5580A001000000000000000000000000000000000000900200063006900660073002F00310030002E00310030002E00310036002E00390030000000000000000000
```

```
john --format=netntlmv2 hash.txt
hashcat -m 5600 -a 3 hash.txt
```

---

## Apply password variations

#### Creating a custom wordlist
> see [[Wordlist Generation]]

#### Rules
- OneRuleToRuleThemAll / OneRuleToRuleThemStill
- Best64

#### Munge
- https://github.com/Th3S3cr3tAg3nt/Munge
- https://github.com/iq-thegoat/Munge

[Video by John Hammond : Hacking Complex Passwords with Rules & Munging](https://www.youtube.com/watch?v=nNvhK1LUD48)

---
More reading:
- https://github.com/hashtopolis/server
- https://hackingvision.com/2020/03/30/distributed-hash-cracking-hashcat-hashtopolis-tutorial/