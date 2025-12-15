# Rickdiculously – VulnHub Walkthrough

## 📌 Machine Information
- **Name:** Rickdiculously
- **OS:** Fedora 26 (Server Edition)
- **Category:** Linux Internals / Boot-Level CTF
- **Difficulty:** Medium
- **Objective:** Gain root access and collect all flags

---

## 🔍 Initial Recon (Misdirection)

### Network Discovery
```bash
ip a
nmap -sn 192.168.194.0/24
```
# Target IP identified:
```
192.168.194.4 / 192.168.194.6
```
# port scan 
```
nmap -sS -A -p- 192.168.194.4
```
**Result:**
All ports filtered. No usable network services.
➡️ This confirmed the machine is not intended for network/web exploitation.
# 🖥️ Boot Issue Analysis
On boot, the VM showed an EFI/GRUB menu instead of a login screen.
# Root Cause
* Rickdiculously is a legacy Linux VM
* VirtualBox had EFI + Secure Boot enabled
* Fedora failed to boot correctly
**Fix**
VirtualBox → Settings → System → Motherboard:

* Disable Enable EFI
* Disable Secure Boot
* Boot Order → Hard Disk first
