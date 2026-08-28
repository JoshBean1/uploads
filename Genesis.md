
## Recon

Subnet is 10.10.110.0/24

Host discovery:

```bash
[kali@gremlins] [26AUG25|13:55] [~] $> nmap 10.10.110.0/24 -sn
Starting Nmap 7.99 ( https://nmap.org ) at 2026-08-25 14:04 -0400
Nmap scan report for 10.10.110.2
Host is up (0.028s latency).
Nmap scan report for 10.10.110.3
Host is up (0.031s latency).
Nmap scan report for 10.10.110.5
Host is up (0.031s latency).
Nmap scan report for 10.10.110.10
Host is up (0.032s latency).
Nmap scan report for 10.10.110.12
Host is up (0.031s latency).
Nmap scan report for 10.10.110.20
Host is up (0.039s latency).
Nmap scan report for 10.10.110.25
Host is up (0.033s latency).
Nmap scan report for 10.10.110.45
Host is up (0.036s latency).
Nmap scan report for 10.10.110.58
Host is up (0.035s latency).
Nmap scan report for 10.10.110.60
Host is up (0.031s latency).
Nmap scan report for 10.10.110.78
Host is up (0.033s latency).
Nmap scan report for 10.10.110.102
Host is up (0.035s latency).
Nmap scan report for 10.10.110.119
Host is up (0.029s latency).
Nmap scan report for 10.10.110.205
Host is up (0.035s latency).
Nmap scan report for 10.10.110.213
Host is up (0.034s latency).
Nmap scan report for 10.10.110.254
Host is up (0.029s latency).
Nmap done: 256 IP addresses (16 hosts up) scanned in 5.20 seconds
```

| Host            | IP   |
| --------------- | ---- |
|                 | .2   |
| DC01-PHOBOS     | .3   |
| SRV01-ARTEMIS   | .5   |
|                 | .10  |
|                 | .12  |
| WS01-ERIS       | .20  |
| WS02-ATHENA     | .25  |
|                 | .45  |
| SQL01-HERA      | .58  |
|                 | .60  |
|                 | .78  |
|                 | .102 |
|                 | .119 |
|                 | .205 |
| WEBWIN01-APOLLO | .213 |
|                 | .254 |

```bash
nmap 10.10.110.0/24 -p- -sV
```




### Host 10.10.110.3 (DC-1-PHOBUS)

```text
Nmap scan report for 10.10.110.3
Host is up (0.030s latency).
Not shown: 65510 closed tcp ports (reset)
PORT      STATE SERVICE       VERSION
53/tcp    open  domain        Simple DNS Plus
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2026-08-25 18:24:16Z)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: genesis.local, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: genesis.local, Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
9389/tcp  open  mc-nmf        .NET Message Framing
47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49671/tcp open  msrpc         Microsoft Windows RPC
49678/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
49679/tcp open  msrpc         Microsoft Windows RPC
49682/tcp open  msrpc         Microsoft Windows RPC
49686/tcp open  msrpc         Microsoft Windows RPC
49691/tcp open  msrpc         Microsoft Windows RPC
49699/tcp open  msrpc         Microsoft Windows RPC
Service Info: Host: DC01-PHOBOS; OS: Windows; CPE: cpe:/o:microsoft:windows

```

- Nothing from rpc
- No smb access


### 10.10.110.5

```text
Nmap scan report for 10.10.110.5
Host is up (0.030s latency).
Not shown: 65524 closed tcp ports (reset)
PORT      STATE SERVICE       VERSION
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

```

- anonymous smb access, nothing interesting

### 10.10.110.10

```text
Nmap scan report for 10.10.110.10
Host is up (0.027s latency).
Not shown: 65533 closed tcp ports (reset)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.4p1 Debian 5+deb11u3 (protocol 2.0)
3306/tcp open  mysql   MariaDB 5.5.5-10.5.23
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

- poked sql, tried root:root, root:

### 10.10.110.12

```text
Nmap scan report for 10.10.110.12
Host is up (0.031s latency).
Not shown: 65532 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.5
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.7 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.52 ((Ubuntu))
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
```

- anonymous ftp available, no files
- ovpn template on web server, points to fw.genesis.local

### 10.10.110.20

```text
Nmap scan report for 10.10.110.20
Host is up (0.029s latency).
Not shown: 65523 closed tcp ports (reset)
PORT      STATE SERVICE       VERSION
21/tcp    open  ftp           Microsoft ftpd
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?
5040/tcp  open  unknown
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC
49670/tcp open  msrpc         Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```

- found pentest_report.txt on ftp with anonymous login
- CREDS test:t3st123
- tested against ssh, ftp, smb, rdp, winrm, mssql


### 10.10.110.25

```text
Nmap scan report for 10.10.110.25
Host is up (0.029s latency).
Not shown: 65522 closed tcp ports (reset)
PORT      STATE SERVICE       VERSION
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?
5040/tcp  open  unknown
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC
49670/tcp open  msrpc         Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```

- anon access to smb, found wp-config.php.bak
```text
/** MySQL database username */   
define( 'DB_USER', 'Ferus' );                                                    
/** MySQL database password */                                                   
define( 'DB_PASSWORD', 'MeatLoaf007' );  
```

sql CREDS Ferus:MeatLoaf007
- creds do not work remotely for sql server

### 10.10.110.45

```text
Nmap scan report for 10.10.110.45
Host is up (0.028s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.7 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.52 ((Ubuntu))
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

- /notes/ found on webapp, seems to be nothing?

### 10.10.110.58

```text
Nmap scan report for 10.10.110.58
Host is up (0.030s latency).
Not shown: 65521 closed tcp ports (reset)
PORT      STATE SERVICE      VERSION
135/tcp   open  msrpc        Microsoft Windows RPC
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
1433/tcp  open  ms-sql-s     Microsoft SQL Server 2019 15.00.2000
5985/tcp  open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
47001/tcp open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
49664/tcp open  msrpc        Microsoft Windows RPC
49665/tcp open  msrpc        Microsoft Windows RPC
49666/tcp open  msrpc        Microsoft Windows RPC
49667/tcp open  msrpc        Microsoft Windows RPC
49668/tcp open  msrpc        Microsoft Windows RPC
49669/tcp open  msrpc        Microsoft Windows RPC
49670/tcp open  msrpc        Microsoft Windows RPC
49748/tcp open  ms-sql-s     Microsoft SQL Server 2019 15.00.2000
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

```

- anon smb, folder 'zach'
- Provider=SQLOLEDB.1;Password=x5Chuz8XbM
CREDS zach:x5Chuz8XbM


### 10.10.110.60

```test
Nmap scan report for 10.10.110.60
Host is up (0.031s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.7 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Werkzeug httpd 2.0.2 (Python 3.10.12)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

- /products is not interesting

### 10.10.110.78

```text
Nmap scan report for 10.10.110.78
Host is up (0.027s latency).
Not shown: 65527 closed tcp ports (reset)
PORT      STATE SERVICE          VERSION
22/tcp    open  ssh              OpenSSH 8.9p1 Ubuntu 3ubuntu0.7 (Ubuntu Linux; protocol 2.0)
6123/tcp  open  spark            Apache Spark
8081/tcp  open  blackice-icecap?
38283/tcp open  spark            Apache Spark
38817/tcp open  spark            Apache Spark
39803/tcp open  unknown
44223/tcp open  spark            Apache Spark
44565/tcp open  printer
2 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit.cgi?new-service :
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port8081-TCP:V=7.99%I=7%D=8/25%Time=6A8DE45D%P=x86_64-pc-linux-gnu%r(Ge
SF:tRequest,93B,"HTTP/1\.1\x20200\x20OK\r\nContent-Type:\x20text/html\r\nD
SF:ate:\x20Tue,\x2025\x20Aug\x202026\x2018:53:02\x20GMT\r\nExpires:\x20Tue
SF:,\x2025\x20Aug\x202026\x2018:58:02\x20GMT\r\nCache-Control:\x20private,
SF:\x20max-age=300\r\nLast-Modified:\x20Tue,\x2025\x20Aug\x202026\x2018:53
SF::02\x20GMT\r\ncontent-length:\x202137\r\n\r\n<!--\n\x20\x20~\x20License
SF:d\x20to\x20the\x20Apache\x20Software\x20Foundation\x20\(ASF\)\x20under\
SF:x20one\n\x20\x20~\x20or\x20more\x20contributor\x20license\x20agreements
SF:\.\x20\x20See\x20the\x20NOTICE\x20file\n\x20\x20~\x20distributed\x20wit
SF:h\x20this\x20work\x20for\x20additional\x20information\n\x20\x20~\x20reg
SF:arding\x20copyright\x20ownership\.\x20\x20The\x20ASF\x20licenses\x20thi
SF:s\x20file\n\x20\x20~\x20to\x20you\x20under\x20the\x20Apache\x20License,
SF:\x20Version\x202\.0\x20\(the\n\x20\x20~\x20\"License\"\);\x20you\x20may
SF:\x20not\x20use\x20this\x20file\x20except\x20in\x20compliance\n\x20\x20~
SF:\x20with\x20the\x20License\.\x20\x20You\x20may\x20obtain\x20a\x20copy\x
SF:20of\x20the\x20License\x20at\n\x20\x20~\n\x20\x20~\x20\x20\x20\x20\x20h
SF:ttp://www\.apache\.org/licenses/LICENSE-2\.0\n\x20\x20~\n\x20\x20~\x20U
SF:nless\x20required\x20by\x20applicable\x20law\x20or\x20agreed\x20to\x20i
SF:n\x20writing,\x20software\n\x20\x20~\x20distributed\x20under\x20the\x20
SF:License\x20is\x20distributed\x20on\x20an\x20\"AS\x20IS\"\x20BASIS,\n\x2
SF:0\x20~\x20WITHOUT\x20WARRANTIES\x20OR\x20CONDITIONS\x20OF")%r(FourOhFou
SF:rRequest,A7,"HTTP/1\.1\x20404\x20Not\x20Found\r\nContent-Type:\x20appli
SF:cation/json;\x20charset=UTF-8\r\ncontent-length:\x2074\r\n\r\n{\"errors
SF:\":\[\"Unable\x20to\x20load\x20requested\x20file\x20/nice\x20ports,/Tri
SF:nity\.txt\.bak\.\"\]}")%r(SIPOptions,AE,"HTTP/1\.1\x20404\x20Not\x20Fou
SF:nd\r\nContent-Type:\x20application/json;\x20charset=UTF-8\r\nAccess-Con
SF:trol-Allow-Origin:\x20\*\r\nConnection:\x20keep-alive\r\ncontent-length
SF::\x2025\r\n\r\n{\"errors\":\[\"Not\x20found\.\"\]}")%r(WWWOFFLEctrlstat
SF:,97,"HTTP/1\.1\x20404\x20Not\x20Found\r\nContent-Type:\x20application/j
SF:son;\x20charset=UTF-8\r\ncontent-length:\x2058\r\n\r\n{\"errors\":\[\"U
SF:nable\x20to\x20load\x20requested\x20file\x20/bad-request\.\"\]}");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port39803-TCP:V=7.99%I=7%D=8/25%Time=6A8DE477%P=x86_64-pc-linux-gnu%r(R
SF:PCCheck,ACF,"\0\0\n\xcf\xba\xdc\x0f\xfe\x01\xac\xed\0\x05sr\0Korg\.apac
SF:he\.flink\.shaded\.netty4\.io\.netty\.handler\.codec\.TooLongFrameExcep
SF:tion\xe4M\|\xb36\x8e\xac\(\x02\0\0xr\0Forg\.apache\.flink\.shaded\.nett
SF:y4\.io\.netty\.handler\.codec\.DecoderException`\x20\xa4Dm\x9d\xf1\xdc\
SF:x02\0\0xr\0Dorg\.apache\.flink\.shaded\.netty4\.io\.netty\.handler\.cod
SF:ec\.CodecException\xeb\xab\xe0\x82\xf5\x86\xb3\x87\x02\0\0xr\0\x1ajava\
SF:.lang\.RuntimeException\x9e_\x06G\n4\x83\xe5\x02\0\0xr\0\x13java\.lang\
SF:.Exception\xd0\xfd\x1f>\x1a;\x1c\xc4\x02\0\0xr\0\x13java\.lang\.Throwab
SF:le\xd5\xc65'9w\xb8\xcb\x03\0\x04L\0\x05causet\0\x15Ljava/lang/Throwable
SF:;L\0\rdetailMessaget\0\x12Ljava/lang/String;\[\0\nstackTracet\0\x1e\[Lj
SF:ava/lang/StackTraceElement;L\0\x14suppressedExceptionst\0\x10Ljava/util
SF:/List;xpq\0~\0\nt\0@Adjusted\x20frame\x20length\x20exceeds\x20214748364
SF:7:\x202147483688\x20-\x20discardedur\0\x1e\[Ljava\.lang\.StackTraceElem
SF:ent;\x02F\*<<\xfd\"9\x02\0\0xp\0\0\0\x16sr\0\x1bjava\.lang\.StackTraceE
SF:lementa\t\xc5\x9a&6\xdd\x85\x02\0\x08B\0\x06formatI\0\nlineNumberL\0\x0
SF:fclassLoaderNameq\0~\0\x07L\0\x0edeclaringClassq\0~\0\x07L\0\x08fileNam
SF:eq\0~\0\x07L\0\nmethodNameq\0~\0\x07L\0\nmoduleNameq\0~\0\x07L\0\rmodul
SF:eVersionq\0~\0\x07xp\x01\0\0\x02\x01t\0\x03appt\0Rorg\.apache\.flink\.s
SF:haded\.netty4\.io\.netty\.")%r(Kerberos,C60,"\0\0\x0c`\xba\xdc\x0f\xfe\
SF:x01\xac\xed\0\x05sr\0Forg\.apache\.flink\.shaded\.netty4\.io\.netty\.ha
SF:ndler\.codec\.DecoderException`\x20\xa4Dm\x9d\xf1\xdc\x02\0\0xr\0Dorg\.
SF:apache\.flink\.shaded\.netty4\.io\.netty\.handler\.codec\.CodecExceptio
SF:n\xeb\xab\xe0\x82\xf5\x86\xb3\x87\x02\0\0xr\0\x1ajava\.lang\.RuntimeExc
SF:eption\x9e_\x06G\n4\x83\xe5\x02\0\0xr\0\x13java\.lang\.Exception\xd0\xf
SF:d\x1f>\x1a;\x1c\xc4\x02\0\0xr\0\x13java\.lang\.Throwable\xd5\xc65'9w\xb
SF:8\xcb\x03\0\x04L\0\x05causet\0\x15Ljava/lang/Throwable;L\0\rdetailMessa
SF:get\0\x12Ljava/lang/String;\[\0\nstackTracet\0\x1e\[Ljava/lang/StackTra
SF:ceElement;L\0\x14suppressedExceptionst\0\x10Ljava/util/List;xpsr\0\x1fj
SF:ava\.lang\.IllegalStateException\xe6WU\xe6\x9aF\xf2H\x02\0\0xq\0~\0\x02
SF:q\0~\0\x0bt\0:Network\x20stream\x20corrupted:\x20received\x20incorrect\
SF:x20magic\x20number\.ur\0\x1e\[Ljava\.lang\.StackTraceElement;\x02F\*<<\
SF:xfd\"9\x02\0\0xp\0\0\0\x12sr\0\x1bjava\.lang\.StackTraceElementa\t\xc5\
SF:x9a&6\xdd\x85\x02\0\x08B\0\x06formatI\0\nlineNumberL\0\x0fclassLoaderNa
SF:meq\0~\0\x06L\0\x0edeclaringClassq\0~\0\x06L\0\x08fileNameq\0~\0\x06L\0
SF:\nmethodNameq\0~\0\x06L\0\nmoduleNameq\0~\0\x06L\0\rmoduleVersionq\0~\0
SF:\x06xp\x01\0\0\0\xdft\0\x03appt\0Jorg\.apache\.flink\.runtime\.io\.netw
SF:ork\.netty\.NettyMessage\$NettyMessageDecodert\0\x11NettyMe");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

- Apache Flink 1.11.0 has unauthenticated file read on metasploit
- Apache Spark has a rce cve on metasploit
- Obtain shell with metasploit, grab ssh key

```text
1   exploit/linux/local/cve_2022_0847_dirtypipe                         Yes                      The target appears to be vulnerable. Linux kernel version found: 5.15.0                                                                   
 2   exploit/linux/local/cve_2022_0995_watch_queue                       Yes                      The target appears to be vulnerable.                                                                                                      
 3   exploit/linux/local/cve_2023_0386_overlayfs_priv_esc                Yes                      The target appears to be vulnerable. Linux kernel version found: 5.15.0                                                                   
 4   exploit/linux/local/netfilter_nft_set_elem_init_privesc             Yes                      The target appears to be vulnerable.                                                                                                      
 5   exploit/linux/local/su_login                                        Yes                      The target appears to be vulnerable.                                                                                                      
 6   exploit/linux/local/ubuntu_needrestart_lpe                          Yes                      The target appears to be vulnerable. Vulnerable needrestart version 3.5.pre.5ubuntu2.1 detected on Ubuntu 22.04                           
 7   exploit/linux/persistence/bash_profile                              Yes                      The service is running, but could not be validated. Bash profile exists and is writable: /home/ipp/.bashrc                                
 8   exploit/linux/persistence/init_systemd                              Yes                      The target appears to be vulnerable. /tmp/ is writable and system is systemd based                                                        
 9   exploit/multi/persistence/cron                                      Yes                      The target appears to be vulnerable. Cron timing is valid, no cron.deny entries found
```

