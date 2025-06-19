# Penetration Test Lab: Kali Linux, Metasploitable 2, and Windows VM

This project documents a penetration testing lab I set up using:
- 🐱 Kali Linux (Attacker)
- 💣 Metasploitable 2 (Target)
- 🪟 Windows 10 VM (Target)

## 🛠️ Lab Setup

- **Kali Linux** as the attacking machine
- **Metasploitable 2** running vulnerable services
- **Windows 10** for testing client-side attacks and vulnerabilities
- **Virtualization:** VirtualBox 
- **Network Setup**: Host-only adapter (isolated lab environment)
  
![Screenshot (282)](https://github.com/user-attachments/assets/d3da1f22-0793-4cfb-9feb-ab1f03acbd5c)

## 🧰 Tools Used

- `Nmap` – Port scanning and OS detection
- `Metasploit Framework` – Exploitation and enumeration
- `Enum4linux` – SMB enumeration
- `Netcat` – Shell access
- `msfvenom` – Payload generation
- `FTP` / `Telnet` – Protocol testing

## 📋 Test Phases

### 1. Executive Summary
A penetration test was conducted against a Metasploitable 2 and Windows 10 VM. Using tools like Nmap and Metasploit, several vulnerabilities were identified, with successful root-level exploitation of the Linux system via vsftpd 2.3.4. Recommendations include port hardening, access control, and regular vulnerability scanning.

---

### 2. 🗺️ Plan and Scope

| Machine | Role      | OS             |
|---------|-----------|----------------|
| Kali    | Attacker  | Kali Rolling   |
| Meta    | Target    | Metasploitable 2 |
| Win10   | Target    | Windows 10     |

- **Scope**: Limit testing to Metasploitable and Windows 10 within host-only network.
- **Tools**: Nmap, Metasploit, FTP brute force, vulnerability scanners.

---

### 3. 🔎 Scanning and Enumeration

```bash
nmap -sS -sV -O 192.168.56.101
```

- Identified open ports on Metasploitable: 21 (FTP), 22 (SSH), 80 (HTTP), etc.

- Windows VM appeared with all ports filtered.

- Used Metasploit to probe HTTP services and identify FTP vulnerabilities.

- Discovered vulnerable FTP service: vsftpd 2.3.4
  
![Screenshot (283)](https://github.com/user-attachments/assets/416a3747-d362-4074-a81f-d2b43a20d19c)
![Screenshot (285)](https://github.com/user-attachments/assets/8370f191-0df4-4789-9ea9-870cf374fb24)
![Screenshot (286)](https://github.com/user-attachments/assets/f2c2e45b-094a-4e4f-8208-5e0f790938e3)

### 4. 🛠️ Vulnerability Assessment

 -Identified multiple services on Metasploitable with known exploits.

- Selected FTP service `(vsftpd 2.3.4)` for exploitation due to publicly available and reliable Metasploit module.

### 5. 🎯 Exploitation (Establishing Access)

```bash
msfconsole
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOSTS 192.168.56.101
run
```
- Successfully gained root shell access to the Linux target via vsftpd backdoor.

- Verified full system control from the attacking Kali machine.
- 
![Screenshot (287)](https://github.com/user-attachments/assets/efc44a1e-9645-405c-8849-425d8e726f8f)
### 6. 🔒 Maintaining Access
- Maintained root access using reverse shells.

- Simulated persistence techniques:

- Install rootkits

- Schedule cron jobs

- Add malicious SSH keys

### 7. 🛡️ Recommendations
### Linux (Metasploitable):

- Disable unused services (e.g., FTP)

- Apply latest security patches

- Enable firewall rules to limit access

### Windows 10:

- Enable all OS updates

- Configure Windows Defender properly

- Monitor logs and access attempts

### 8. 🧠 Final Reflection
This penetration test lab helped reinforce:

- Real-world enumeration and exploitation workflows
  
- Metasploit use in practical engagements
  
- Defensive security understanding through post-exploit reflection
  
# Next Steps:

- Learn client-side attacks
  
- Perform privilege escalation on Windows targets
  
- Explore web application vulnerabilities

### 🧾 References

- Mastering Metasploit - Packtpub

- SI110 Cyber-Attack Phases – USNA

- Information Security Stack Exchange
- 
