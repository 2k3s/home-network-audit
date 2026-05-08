# Finding: UPnP enabled on router

**Date:** 2026-05-08  
**Device:** 192.168.1.1 (Cisco-Linksys E4200 Router)  
**Severity:** Low–Medium  
**Status:** ⚠️ To review

## Description

nmap detected the router's UPnP service running on port 49152. UPnP (Universal
Plug and Play) allows devices on the network to automatically open ports through
the router without user confirmation. While convenient, it is a known attack
vector — malicious software can abuse UPnP to expose internal services to the
internet without the user's knowledge.

## Evidence

nmap output:
```
PORT      STATE SERVICE VERSION
49152/tcp open  upnp    Cisco-Linksys E4200 WAP upnpd (UPnP 1.0)
```

## Recommended fix

1. Log in to the router admin panel at `http://192.168.1.1`
2. Navigate to **Administration** or **Advanced Settings**
3. Find the **UPnP** setting and disable it
4. Save and reboot the router

## Notes

Disabling UPnP may affect some applications that rely on automatic port forwarding
(e.g. some games, torrent clients, video calling apps). If something stops working
after disabling it, manual port forwarding rules can be set up as a safer alternative.
