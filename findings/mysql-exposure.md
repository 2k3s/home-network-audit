# Finding: MySQL exposed to local network

**Date:** 2026-05-08  
**Device:** 192.168.1.8 (Windows PC)  
**Severity:** Medium  
**Status:** ✅ Fixed

## Description

During a routine nmap scan, port 3306 (MySQL) was found listening on `0.0.0.0`,
meaning any device on the local network could attempt a connection to the database.
This was discovered on the same machine the scan was run from.

## Evidence

nmap output:
```
PORT     STATE SERVICE    VERSION
3306/tcp open  tcpwrapped
```

netstat output before fix:
```
TCP    0.0.0.0:3306    0.0.0.0:0    LISTENING
```

## Fix

Located the MySQL config file at:
```
C:\ProgramData\MySQL\MySQL Server 8.0\my.ini
```

Added the following line under the `[mysqld]` section:
```ini
[mysqld]
bind-address = 127.0.0.1
```

Restarted the MySQL service:
```
net stop MySQL80
net start MySQL80
```

## Verification

netstat output after fix:
```
TCP    127.0.0.1:3306    0.0.0.0:0    LISTENING
```

Port 3306 is now only accessible from localhost. No external or LAN connections possible.

## Follow-up

MySQL X Protocol port 33060 is still bound to `0.0.0.0`. Lower severity than 3306
but can be locked down by adding to `my.ini`:
```ini
mysqlx-bind-address = 127.0.0.1
```
