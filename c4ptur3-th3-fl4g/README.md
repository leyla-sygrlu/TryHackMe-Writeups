# c4ptur3-th3-fl4g

## [Task 1] Translation & Shifting

 ### 1. 
 We decode the leetspeak challenge string ("c4n y0u c4p7u23 7h3 f149?") into standard English plaintext ("can you capture the flag?").


### 2.Binary to Text Translator
We input structured binary blocks into the translator tool to convert machine-level byte representations into readable plaintext ("lets try some binary out!")
![2](t1.2.png)

### 3. Base32 Decoding
We decoded the Base32 string (MJQXGZJTGIQGS4ZAON2XAZLSEBRW63LNN5XCA2LOEBBVIRRHOM======) using base32 -d to extract the plaintext.

### 4. Base64 Decoding:
We processed the Base64 string (RWFjaCBCYXNlNlQgZGlnaXQgcMVwcmVzZW50cyBleGFjdGx5IDYgYml0cyBvZiBkYXRhLg==) using base64 -d to retrieve the readable message.

### 5. Hexadecimal Conversion:
We translated the hex-encoded byte sequence (68 65 78 61 64 65 63 69 6d 61 6c 20 6f 72 20 62 61 73 65 31 36 3f) into ASCII text using xxd -r -p.

![3-4-5](t1.(345).png)

### 6. ROT13 Decryption:
We decrypted the ROT13 encoded string (Ebgngr zr 13 cynprf!) using the tr command to reveal the plaintext message 
![6](t1.6.png)

### 7. ROT Cipher Analysis:
We decrypted the ROT-encoded ciphertext (*@F DA:? >6 C:89E C@F?5 323J C:89E C@F?5 Wcf E:>6DX) using automated tools to reveal the decoded plaintext.
![7](t1.7.png)

### 8. Morse Code Translation:
We decoded the audio-based Morse code input into the final plaintext string ("TELECOMMUNICATIONENCODING")
![8](t1.8.png)

### 9. Decimal Translation:
We converted the decimal ASCII values (85 110 112 97 99 107 32 116 104 105 115 32 66 67 68) into plaintext ("Unpack this BCD") using a decimal-to-ASCII converter.
![9](t1.9.png)

### 10. Multi-Layer Obfuscation Resolution:
We successfully processed a complex multi-layered payload through a CyberChef pipeline—combining Base64 decoding, Morse code translation, binary-to-ASCII conversion, ROT47 shifting, and decimal parsing—to reveal the final output string ("Let's make this a bit trickier...").
![10](t1.10.png)

