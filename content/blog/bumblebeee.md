---
title: "HTB Sherlocks:Bumblebee Draft"
date: 2024-01-01T09:09:47+05:30
draft: true
params:
  slug: "sherlocks-bumblebee"
layout: "post"
tags: ["Sherlocks", "HTB"]
authors: ["Lordsudo"]
---
![banner](https://gist.github.com/user-attachments/assets/9a9b528d-89c0-47ba-af23-7715f0369989)

-----

# 🐝 HTB Sherlocks: Bumblebee — A Tale of Deceit and Digital Breadcrumbs

---

## 🕯️ Prologue — When Curiosity Meets Intrusion

The line between guest and intruder is often thinner than most organizations realize. When the Forela security team flagged an unusual login from within their guest WiFi range, the true extent of the breach was still unknown.

The scenario was simple: a contractor, fleeting network access, and stolen admin credentials. But the story buried beneath the logs was anything but ordinary.

Armed with a database dump and access logs, I stepped into the trail — and began to unravel the adversary's plan.

---

## 🗺️ Scenario — The Contractor’s Little Game

> "An external contractor has accessed the internal forum here at Forela via the Guest WiFi and they appear to have stolen credentials for the administrative user! We have attached some logs from the forum and a full database dump in sqlite3 format to help you in your investigation."

---

## 🧠 The Hunt — Following the Stinger

---

### 🗃️ Phase 1 — Identifying the Intruder

The investigation began at the source: the `phpbb_users` table. A quick glance at the user list revealed something that stood out — a user whose email didn’t match the organization’s typical domain.

- **Username:** `apoole1`  
- **Email Address:** `apoole1@contractor.net`

The adversary had set their trap under the guise of a legitimate user.

![Screenshot: User Enumeration in phpbb_users](<path_to_screenshot_here>)

---

### 🌍 Phase 2 — Tracing the Origin

The `user_ip` field told the story of how the account came to life.  
The address pointed to a machine on the guest network.

- **User IP:** `10.10.0.78`

![Screenshot: IP address from phpbb_users](<path_to_screenshot_here>)

---

### 💡 Phase 3 — Uncovering the Malicious Post

In the `phpbb_posts` table, **Post ID 9** stood out like a corpse in the open.

The post contained an embedded form, cleverly disguised but malicious in intent. Its true purpose? To hijack the `phpbb_token` and silently exfiltrate it to an external URL.

- **Exfiltration URI:** `http://10.10.0.78/update.php`

![Screenshot: Post Content from phpbb_posts](<path_to_screenshot_here>)

---

### 🗂️ Phase 4 — Confirming the Breach

The `phpbb_log` table revealed the decisive moment: a successful login to the admin account.

- **Login Time:** `26/04/2023 10:53:12 UTC`

![Screenshot: Admin Login Entry from phpbb_log](<path_to_screenshot_here>)

---

### 🔓 Phase 5 — Exposing the Stolen Secrets

The hunt didn’t end with the login — the attacker wasn’t just interested in forum access.  
In the `phpbb_config` table, a far more dangerous discovery waited.

- **LDAP Password:** `Passw0rd1`

![Screenshot: LDAP Password in phpbb_config](<path_to_screenshot_here>)

---

### 🧾 Phase 6 — Profiling the Admin’s Browser

Turning to the `access.log`, I matched the admin login request to its corresponding user-agent string.

- **User-Agent:**  
`Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/112.0.0.0 Safari/537.36`

![Screenshot: Access Log Matching the Admin Login](<path_to_screenshot_here>)

---

### 🧑‍💻 Phase 7 — Privilege Escalation: The Final Sting

Not content with mere access, the contractor secured long-term control by escalating privileges. The logs captured the exact moment they joined the Administrator group.

- **Privilege Escalation Time:** `26/04/2023 10:53:51 UTC`

![Screenshot: Log Entry Showing Group Modification](<path_to_screenshot_here>)

---

### 💾 Phase 8 — The Data Heist

The final piece of the puzzle lay in the download logs: a database backup exfiltrated without raising a single alert.

- **Download Time:** `26/04/2023 11:01:38 UTC`  
- **Backup File Size:** `34707 bytes`

![Screenshot: Access Log Showing Backup Download](<path_to_screenshot_here>)

---

## ☠️ Aftermath — The Sting Behind the Bee

The "Bumblebee" challenge is more than a simple log analysis exercise. It’s a full-fledged story of insider exploitation, lateral movement, credential theft, and digital misdirection.

From planting a poisoned post to quietly vanishing with sensitive data, the attacker showcased an almost mechanical understanding of how defenders overlook the familiar.

> 💡 **Lesson:**  
In modern security breaches, attackers no longer need to break down doors — they slip through the windows users leave open.

The devil isn’t in the payload. The devil is in the details.

---

> *Until the next hunt... the shadows remain patient.*  
> — **L0rd$ud0** 🖤
