# Finding: Unidentified device on network

**Date:** 2026-05-08  
**Device:** 192.168.1.2  
**Severity:** Low  
**Status:** ✅ Identified

## Description

nmap detected an active host at 192.168.1.2 with a locally administered MAC address
(`2E:CC:3D:61:12:CD`). A locally administered MAC (identifiable by the `2` at the
start) indicates the device is using MAC address randomization — a privacy feature
common in modern phones, tablets, and laptops. Because of this, the MAC prefix
cannot be used to identify the manufacturer.

nmap was unable to determine the OS or hostname.

## Evidence

nmap output:

```
Nmap scan report for 192.168.1.2
Host is up (0.039s latency).
PORT  STATE    SERVICE VERSION
7/tcp filtered echo
MAC Address: 2E:CC:3D:61:12:CD (Unknown)
Too many fingerprints match this host to give specific OS details
```

### Resolution

Device identified as a Google Pixel 7 Pro. MAC randomization is enabled by

default on Android, which is why the MAC prefix was unrecognizable. No further

action needed.

## Recommended investigation

1. Log in to the router admin panel at `http://192.168.1.1`
2. Navigate to the connected devices or DHCP client list
3. Look for the entry at 192.168.1.2 — the router may show a hostname or device name
4. Cross-reference with known devices in the house (phones, tablets, smart TVs, IoT)

## Notes

MAC randomization is normal and not itself a security concern. The device is only
flagged here because it could not be identified. Once identified, this finding can
be closed.

