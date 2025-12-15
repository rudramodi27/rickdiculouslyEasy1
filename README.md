# rickdiculouslyEasy1 - Vulnhub

## 📌 Overview
This repository documents my solution approach for the **Rickdiculously** VulnHub machine.

The machine focuses on **Linux internals and boot-level exploitation** rather than traditional network or web-based attacks.  
Standard enumeration and login attempts are intentionally misleading, and the correct approach involves understanding the Linux boot process and GRUB configuration.

---

## 🧠 Key Skills Demonstrated
- Linux boot process analysis
- GRUB boot parameter manipulation
- `rd.break` based privilege escalation
- initramfs & filesystem mounting
- Root access without valid credentials
- Flag enumeration and analysis

---

## 🚩 Flags
All intended flags were successfully identified and extracted from the system, including:
- Root directory flag
- FTP service flag
- Web/password directory flag
- User (Summer) ASCII-art flag

---

## 📄 Walkthrough
A **detailed, step-by-step walkthrough** is maintained separately .



*(The walkthrough includes exact commands, reasoning, and screenshots where applicable.)*

---

## ⚠️ Disclaimer
This repository is for **educational purposes only**.  
The walkthrough is intended to demonstrate learning outcomes related to Linux internals and CTF-style problem solving.

---

## 📜 License
This project is licensed under the **MIT License**.
