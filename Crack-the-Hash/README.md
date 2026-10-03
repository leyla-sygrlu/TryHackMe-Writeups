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
![Hash 1 Analysis](img/hash1.jpeg)


### Hash 2
**Hash:** `CBFDAC6008F9CAB4083784CBD1874F76618D2A97`

**Analysis & Exploitation:**
The `hashid` tool identified the given hash as **SHA-1**. To exploit this, a dictionary attack was initiated using John the Ripper with the `--format=raw-sha1` flag and the standard `rockyou.txt` wordlist.

During the exploitation phase, an interesting caching mechanism of John the Ripper was documented. The initial execution successfully cracked the hash. When a redundant execution was attempted for verification, the engine returned a `"No password hashes left to crack"` message. This demonstrates the tool's internal optimization: successfully cracked hashes are permanently stored in the `john.pot` cache file, preventing the engine from wasting computational resources on previously resolved hashes.

```bash
john --format=raw-sha1 --wordlist=/usr/share/wordlists/rockyou.txt hash2.txt
Loaded 1 password hash (Raw-SHA1 [SHA1 256/256 AVX2 8x3])
No password hashes left to crack (see FAQ)
```
The cached password was successfully retrieved.

Cracked Password: password123
![Hash 2 Analysis](img/hash2.jpeg)


### Hash 3
**Hash:** `1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032`

**Analysis & Exploitation:**
The provided hash consisted of 64 hexadecimal characters, which strongly indicated the **SHA-256** algorithm. Instead of expending local computational resources and time on a brute-force or dictionary attack, a more efficient methodology was chosen. 

The hash was queried against **CrackStation**, an online database utilizing massive pre-computed lookup tables. This approach is highly effective for unsalted, standard cryptographic hashes. The database successfully identified the hash type as SHA-256 and immediately returned the plaintext equivalent.

Cracked Password: letmein
![Hash 3 CrackStation](img/hash3.jpeg)


### Hash 4
**Hash:** `$2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom`

**Analysis & Exploitation:**
The `hashid` tool identified this target as a **Bcrypt (Blowfish)** hash. A local dictionary attack was initially attempted using John the Ripper. However, due to the inherent key-stretching mechanism of Bcrypt (configured with a high cost factor of 12, resulting in 4096 iterations), the local computational overhead was deemed highly inefficient. The ETA projected several days for completion.

```bash
john --format=bcrypt --wordlist=/usr/share/wordlists/rockyou.txt hash4.txt
# Loaded 1 password hash (bcrypt [Blowfish 32/64 X3])
# Cost 1 (iteration count) is 4096 for all loaded hashes
```
To optimize the exploitation phase and conserve computational resources, a strategic pivot was made to query external compromised credential databases. The hash was submitted to Hashes.com, which successfully matched the Bcrypt hash against its pre-computed records.

Cracked Password: bleh
![Hash 4 Local Attempt](img/hash4.1.jpeg)
![Hash 4 Hashes.com](img/hash4.2.jpeg)


### Hash 5
**Hash:** `279412f945939ba78ce0758d3fd83daa`

**Analysis & Exploitation:**
The length and character set of the hash (32 hexadecimal characters) strongly suggested an algorithm from the Message-Digest (MD) family, such as MD4 or MD5. To ensure operational efficiency and bypass local computational constraints, the hash was processed through **CrackStation**. 

The lookup table successfully matched the string, confirming the algorithm as **MD4** and immediately returning the plaintext password.

**Cracked Password:** `Eternity22`

![Hash 5 CrackStation](img/hash5.jpeg)
