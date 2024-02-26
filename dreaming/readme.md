export IP=10.10.206.63

# Nmap Scans
```
PORT   STATE SERVICE REASON  VERSION
22/tcp open  ssh     syn-ack OpenSSH 8.2p1 Ubuntu 4ubuntu0.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 76:26:67:a6:b0:08:0e:ed:34:58:5b:4e:77:45:92:57 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDDwLHu8L86UCKGGVbbYL07uBhmOh9hWLPtBknNwMgULG3UGIqmCT3DywDvtEYZ/6D97nrt6PpsVAu0/gp73GYjUxvk4Gfog9YFShodiB/VJqK4RC23h0oNoAElSJajjEq6JcVaEyub6w8Io50fk4nNhf8dPx0YSaRjKANr9mET6s+4cUNBAF/DknsZw6iYtafzxIQTAtgSX6AtXTXRf5cpdF02wwYvUo1jVSYdXL+Oqx19UADVhQib4Pt5gLAiwuFkoJjnN1L6xwkTjd+sUPVlhQ/6yHfB826/Qk55DWoUrnABfe+3jngyPvjl1heYDuPx01rtDvlDDGAwvriwR7XmX+8X7MZ9E9QOx/m2gEHZ83kuJ9jNLB6WjlqCyA4Zes+oHWbM9Q/nJ/UVQGdfcDS65edQ5m/fw2khqUbCeSFcuD3AQvUJvvFrfg/eTNnhpee/WYJjyZO70tlzhaT/oJheodQ1hQyfgnjwToy/ISHn9Yp4jeqrshBUF87x9kUuLV0=
|   256 52:3a:ad:26:7f:6e:3f:23:f9:e4:ef:e8:5a:c8:42:5c (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBCmisKYJLewSTob1PZ06N0jUpWdArbsaHK65lE8Lwefkk3WFAwoTWvStQbzCJlo0MF+zztRtwcqmHc5V7qawS8E=
|   256 71:df:6e:81:f0:80:79:71:a8:da:2e:1e:56:c4:de:bb (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIK3j+g633Muvqft5oYrShkXdV0Rjn2S1GQpyXyxoPJy0
80/tcp open  http    syn-ack Apache httpd 2.4.41 ((Ubuntu))
| http-methods: 
|_  Supported Methods: GET POST OPTIONS HEAD
|_http-title: Apache2 Ubuntu Default Page: It works
|_http-server-header: Apache/2.4.41 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

```

# Gobuster
```
Progress: 3772 / 438325 (0.86%)[ERROR] Get "http://10.10.167.73/system.xml": context deadline exceeded (Client.Timeout exceeded while awaiting headers)
/app                  (Status: 301) [Size: 310] [--> http://10.10.167.73/app/]

```


# view-source:http://10.10.167.73/app/pluck-4.7.13/?file=dreaming
```
<a href="/app/pluck-4.7.13/login.php">admin</a>

```

# searchsploit 
```


 Exploit Title                                                                                                                       |  Path
------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Pluck CMS 4.7.13 - File Upload Remote Code Execution (Authenticated)                                                                 | php/webapps/49909.py
------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results
```

# test.py
```
cat test.py
import requests

#Todo add myself as a user
url = "http://127.0.0.1/app/pluck-4.7.13/login.php"
password = "HeyLucien#@1999!"

data = {
        "cont1":password,
        "bogus":"",
        "submit":"Log+in"
        }

req = requests.post(url,data=data)

if "Password correct." in req.text:
    print("Everything is in proper order. Status Code: " + str(req.status_code))
else:
    print("Something is wrong. Status Code: " + str(req.status_code))
    print("Results:\n" + req.text)

```

# lucien flag
```
THM{TH3_L1BR4R14N}

```

# sudo -l 
```
User lucien may run the following commands on dreaming:
    (death) NOPASSWD: /usr/bin/python3 /home/death/getDreams.py

```

# /opt/getDreams.py
```
cat getDreams.py
import mysql.connector
import subprocess

# MySQL credentials
DB_USER = "death"
DB_PASS = "#redacted"
DB_NAME = "library"

import mysql.connector
import subprocess

def getDreams():
    try:
        # Connect to the MySQL database
        connection = mysql.connector.connect(
            host="localhost",
            user=DB_USER,
            password=DB_PASS,
            database=DB_NAME
        )

        # Create a cursor object to execute SQL queries
        cursor = connection.cursor()

        # Construct the MySQL query to fetch dreamer and dream columns from dreams table
        query = "SELECT dreamer, dream FROM dreams;"

        # Execute the query
        cursor.execute(query)

        # Fetch all the dreamer and dream information
        dreams_info = cursor.fetchall()

        if not dreams_info:
            print("No dreams found in the database.")
        else:
            # Loop through the results and echo the information using subprocess
            for dream_info in dreams_info:
                dreamer, dream = dream_info
                command = f"echo {dreamer} + {dream}"
                shell = subprocess.check_output(command, text=True, shell=True)
                print(shell)

    except mysql.connector.Error as error:
        # Handle any errors that might occur during the database connection or query execution
        print(f"Error: {error}")

    finally:
        # Close the cursor and connection
        cursor.close()
        connection.close()

# Call the function to echo the dreamer and dream information
getDreams()


```

# cat .bash_history 
```
cd ~~
cd ~
clear
ls
mysql -u lucien -plucien42DBPASSWORD
ls -la
cat .bash_history 
cat .mysql_history 

```

```
# MySQL credentials
DB_USER = "death"
DB_PASS = "!mementoMORI666!"
DB_NAME = "library"

```

# death_flag.txt
```

THM{1M_TH3R3_4_TH3M}
```
























