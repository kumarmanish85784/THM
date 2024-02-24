export IP=10.10.150.148

NMAP Results
```

PORT   STATE SERVICE REASON  VERSION
22/tcp open  ssh     syn-ack OpenSSH 7.2p2 Ubuntu 4ubuntu2.6 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 1b:12:36:87:b9:d2:1b:18:cf:46:cf:21:69:e8:0d:be (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC/qto41iQN40MsuXJf8MIXvFBBbYr55dW2ypnEkkowHGwvFUCAjg117rIPPVKjuXvGLgBY1FxOvCYqmNveqpDs7UGdQA9hQrMBAX2kRaKkUX1EytDUBfhAGOUO8tk4AoSYUiwzyohfd4FdtU9FsGwwYCxhzjXgQ1gY9ye2x5Xj4O4i28nJwD/FGaJZw2ZoyeSigdL6sOwtUGgR1kw3ySyhSzNG3CU9fD6GcD7oLns8X74E7QIBD4PoZmPXGgMbGCZwJseGVWmGJipfWA/rgOunQ252s/kDxKkVBPzFP4LD7jnZ8nkB6rR+3fsh/6y8OsPiCBOra6P/sq/g6zIIqR+3
|   256 ed:5b:61:37:1b:08:82:cd:9a:c9:2f:0a:4c:59:e8:2f (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBOTT6VBxwW/m1Cdv3F2zHXjcZTrdlQFlQTUHMcxhW3qfqLQsVkEkpkQ+qGDbJH7qvifLYUlxXhPRHIQiW15sM1M=
|   256 5b:31:0f:45:2d:6a:96:21:54:d0:8a:0a:9b:28:17:8a (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAILQcmoXrLhrHPrYSLIPePrk/r7HxeNkSP5FUIFHatcUi
80/tcp open  http    syn-ack Apache httpd 2.4.18 ((Ubuntu))
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: Rick is sup4r cool
|_http-server-header: Apache/2.4.18 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Using Burp
```

 <!--

    Note to self, remember username!

    Username: R1ckRul3s       //username

  -->
```

http://10.10.150.148/robots.txt
```
Wubbalubbadubdub              //password

```

Gobuster
```
/login.php            (Status: 200) [Size: 882]
/assets               (Status: 301) [Size: 315] [--> http://10.10.150.148/assets/]
/portal.php           (Status: 302) [Size: 0] [--> /login.php]

```


Q1   What is the first ingredient that Rick needs?
```
mr. meeseek hair

```

Q2   What is the second ingredient in Rick’s potion?
```
1 jerry tear                  /home/rick/second\ ingredients

```


Q3   What is the last and final ingredient?
```
fleeb juice                   /root/3rd.txt

```




