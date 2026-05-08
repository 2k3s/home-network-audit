# Network map

**Scan date:** 2026-05-08  
**Subnet:** 192.168.1.0/24  
**Active hosts found:** 3 / 256

## Device inventory

| IP | MAC address | Hostname | Device type | Open ports | Notes |
|---|---|---|---|---|---|
| 192.168.1.1 | D0:DB:B7:95:3E:8D | NL20.Home | Cisco-Linksys E4200 Router | 80, 49152 | Admin panel on :80, UPnP on :49152 |
| 192.168.1.2 | 2E:CC:3D:61:12:CD | — | Unknown | 7 (filtered) | Randomized MAC — likely phone or IoT device |
| 192.168.1.8 | — | — | Windows PC (self) | 135, 139, 445, 3306 | Machine scan was run from |

## Port reference

| Port | Service | Device | Notes |
|---|---|---|---|
| 80 | HTTP | Router | Admin web interface |
| 135 | RPC | Windows PC | Normal Windows process |
| 139 | NetBIOS | Windows PC | Windows file sharing |
| 445 | SMB | Windows PC | Windows file sharing |
| 3306 | MySQL | Windows PC | Was exposed — now fixed |
| 49152 | UPnP | Router | Security risk — review |

## Filtered ports on router

These ports are blocked by the router's firewall (filtered = firewall present, not just closed):

| Port | Service |
|---|---|
| 21 | FTP |
| 22 | SSH |
| 23 | Telnet |
| 139 | NetBIOS |
| 443 | HTTPS |
| 445 | SMB |
