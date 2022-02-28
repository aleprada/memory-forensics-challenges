
# Cyberdefenders: Deep Dive

## Description
You have given a memory image for a compromised machine. Analyze the image and figure out attack details.

## Solution
### 1) What profile should you use for this memory sample?

### 2)	What is the KDBG virtual address of the memory sample?

### 3)	There is a malicious process running, but it's hidden. What's its name?

### 4)	What is the physical offset of the malicious process?

### 5)	What is the full path (including executable name) of the hidden executable?

### 6)	Which malware is this?

### 7)	The malicious process had two PEs injected into its memory. What's the size in bytes of the Vad that contains the largest injected PE? Answer in hex, like: 0xABC

### 8)	This process was unlinked from the ActiveProcessLinks list. Follow its forward link. Which process does it lead to? Answer with its name and extension

### 9)	What is the pooltag of the malicious process in ascii? (HINT: use volshell)

### 10)	What is the physical address of the hidden executable's pooltag? (HINT: use volshell)
