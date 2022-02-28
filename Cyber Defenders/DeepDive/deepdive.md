
# Cyberdefenders: Deep Dive

## Description
You have given a memory image for a compromised machine. Analyze the image and figure out attack details.

## Solution
### 1) What profile should you use for this memory sample?
```
vol.py -f banking-malware.vmem imageinfo
```

### 2)	What is the KDBG virtual address of the memory sample?
```
vol.py -f banking-malware.vmem imageinfo
```

### 3)	There is a malicious process running, but it's hidden. What's its name?
```
vol.py -f banking-malware.vmem --profile Win7SP1x64_24000 psxview

```
There is one process that pslist and psscan has not detected. That's the answer.

### 4)	What is the physical offset of the malicious process?

```
vol.py -f banking-malware.vmem --profile Win7SP1x64_24000 psxview
```

### 5)	What is the full path (including executable name) of the hidden executable?
```
vol.py -f banking-malware.vmem --profile Win7SP1x64_24000 filescan | grep "vds_ps.exe"

```

### 6)	Which malware is this?
```
vol.py -f banking-malware.vmem --profile Win7SP1x64_24000 procdump --offset=0x000000007d336950 -D .
md5sum executable.2448.exe
```
Check out the md5 hash on VirusTotal.

### 7)	The malicious process had two PEs injected into its memory. What's the size in bytes of the Vad that contains the largest injected PE? Answer in hex, like: 0xABC
```
vol.py -f banking-malware.vmem --profile Win7SP1x64_24000 malfind --offset=0x000000007d336950

vol.py -f banking-malware.vmem --profile Win7SP1x64_24000 vadinfo -a 0x2a10000 | grep "0x0000000002a10000"
vol.py -f banking-malware.vmem --profile Win7SP1x64_24000 vadinfo -a 0x2a80000 | grep "0x0000000002a80000"

```

### 8)	This process was unlinked from the ActiveProcessLinks list. Follow its forward link. Which process does it lead to? Answer with its name and extension
```
vol.py -f banking-malware.vmem --profile Win7SP1x64_24000 volshell
cc(offset=0x000000007d336950, physical=True)
proc().ActiveProcessLinks.Flink

```

### 9)	What is the pooltag of the malicious process in ascii? (HINT: use volshell)
```
vol.py -f banking-malware.vmem --profile Win7SP1x64_24000 volshell

dt( "_POOL_HEADER" ,0x000000007d336950, space=addrspace().base)

```

### 10)	What is the physical address of the hidden executable's pooltag? (HINT: use volshell)
```
vol.py -f banking-malware.vmem --profile Win7SP1x64_24000 volshell

dt( "_POOL_HEADER" ,0x000000007d336950, space=addrspace().base)

```