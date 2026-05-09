# Home Network Audit

A beginner networking project to map and secure my home network using nmap.

## Tools used
- nmap 7.80
- Windows PowerShell (admin)
- MySQL 8.0

## What I did
- Scanned my local network (`192.168.1.0/24`) to discover all active devices
- Identified open ports and running services on each device
- Found and remediated a MySQL misconfiguration exposing the database to the local network
- Verified the fix using `netstat`

## Findings summary

| Device | IP | Issue | Status |
|---|---|---|---|
| Cisco-Linksys E4200 Router | 192.168.1.1 | UPnP enabled on port 49152 | ⚠️ To review |
| Windows PC | 192.168.1.8 | MySQL bound to 0.0.0.0:3306 | ✅ Fixed |
| Google Pixel 7 Pro | 192.168.1.2 | Randomized MAC, unidentified | ✅ Identified |

See the [`findings/`](./findings/) folder for detailed writeups on each issue.

## Network map

See [`network-map.md`](./network-map.md) for the full device inventory.

## What I learned
- How to use nmap for host discovery and service detection (`-sn`, `-O`, `-sV`)
- The difference between open, filtered, and closed ports
- How to read and interpret nmap output
- What randomized MAC addresses are and why devices use them
- How MySQL's `bind-address` setting works and why exposing it to `0.0.0.0` is a risk
- How to use `netstat` to verify what services are listening on which interfaces
- How Windows service management works (`net stop/start`, `sc.exe`)

## Commands reference

```bash
# Discover all live hosts (ping scan)
nmap -sn 192.168.1.0/24

# Full scan with OS and service detection, save to file
nmap -O -sV 192.168.1.0/24 -oN network-audit.txt

# Check what's listening on a specific port
netstat -an | findstr 3306

# Find a service name in Windows
sc.exe query type= all | findstr -i mysql

# Restart a service
net stop MySQL80
net start MySQL80
```

## Next steps
- [ ] Disable UPnP on the router
- [ ] Identify the unknown device at 192.168.1.2 via router admin panel
- [ ] Lock down MySQL X Protocol port 33060 with `mysqlx-bind-address = 127.0.0.1`
- [ ] Verify router admin panel is using a strong, non-default password
