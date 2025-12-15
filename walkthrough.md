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
- **Root Cause**
* Rickdiculously is a legacy Linux VM
* VirtualBox had EFI + Secure Boot enabled
* Fedora failed to boot correctly

- **Fix**
  
> VirtualBox → Settings → System → Motherboard:

* Disable Enable EFI
* Disable Secure Boot
* Boot Order → Hard Disk first

# 🚫 Login Attempts (Intentional Failure) 
`After boot:`
```
Fedora 26 (Server Edition)
localhost login:
```
`Tried standard credentials:`
```
root / password
rick / rick
morty / morty
```
➡️ Result: Login always failed.

> Insight

* Console & Cockpit logins are intentionally blocked
* Web page showing root / password is misdirection
* Real entry point is boot-level access
# 🔓 Privilege Escalation via GRUB (Key Exploit)
**Step 1**: Enter GRUB Menu

* Reboot VM
* Press ESC / SHIFT repeatedly during boot

> GRUB menu appears:
```
Fedora (4.11.8-300.fc26.x86_64)
```
**Step 2**: Edit Boot Parameters
* Select first Fedora entry
* Press e
> Find the line starting with:
`
linux16 /vmlinuz-4.11.8-300.fc26.x86_64 ...
`
> Append before LANG=:
```
rd.break
```
**Final Example:**
> ... rhgb quiet rd.break LANG=en_AU.UTF-8
**Step 3**: Boot into Emergency Shell
```
Ctrl + X
```
* Ststem drops into:
` switch_root:/#
> ➡️ Root shell achieved without password
