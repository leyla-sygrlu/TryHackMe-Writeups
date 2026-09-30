# Crack the Hash Write-up

An easy-level TryHackMe room focusing on Password Cracking and Hashing Functions.

**Author:** Leyla Soyuğurlu

## [Task 1] Level 1

### Hash 1
**Hash:** `48bb6e862e54f2a795ffc4e541caed4d`

**Analysis & Exploitation:**
Initially, the `hashid` tool was utilized to determine the hashing algorithm. The tool suggested **MD2** as the most probable candidate based on the 32-character string length constraint. However, since relying solely on automated outputs can be misleading, the obsolescence of MD2 and the high prevalence of **MD5** in modern CTF environments were taken into consideration. 

It was hypothesized that MD5 was the correct algorithm. To validate this, the MD2 suggestion was bypassed, and a dictionary attack targeting the MD5 architecture was initiated using **John the Ripper** and the standard `rockyou.txt` wordlist:

```bash
echo "48bb6e862e54f2a795ffc4e541caed4d" > hash1.txt
john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash1.txt
````
The hypothesis proved correct, and the engine successfully cracked the hash almost instantaneously.

Cracked Password: easy
