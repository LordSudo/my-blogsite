---
title: "CyberDefenders: 3CX Supply Chain Attack"
date: 2025-04-24T00:02:35+05:30
draft: false
params:
  slug: ""
layout: "post"
tags: ["Threat Intel" , "CyberDefenders"]
authors: ["Lordsudo"]
---

## **Prologue: The Quiet Before the Storm**

In the quietest moments of routine operations, danger often stirs. A trusted software update, something so mundane, becomes the entry point for a dark and malicious force. The **3CX Supply Chain Attack**—an incident where trust was manipulated, and a seemingly harmless software update became a weapon of digital warfare. Prepare yourself, for the tale is one of hidden danger, covert movements, and the eerie calm before a storm. Let’s walk through this, step by step, through the veil of deceit and into the truth that lies beneath.

---

## **Scenario**

A large multinational corporation heavily relies on the 3CX software for phone communication, making it a critical component of their business operations. After a recent update to the 3CX Desktop App, antivirus alerts flag sporadic instances of the software being wiped from some workstations while others remain unaffected. Dismissing this as a false positive, the IT team overlooks the alerts, only to notice degraded performance and strange network traffic to unknown servers. Employees report issues with the 3CX app, and the IT security team identifies unusual communication patterns linked to recent software updates.

As the threat intelligence analyst, it's your responsibility to examine this possible supply chain attack. Your objectives are to uncover how the attackers compromised the 3CX app, identify the potential threat actor involved, and assess the overall extent of the incident.

---

## **What is a Supply Chain Attack?**

A **supply chain attack** is a cunning strategy where an adversary strikes not directly at a target, but instead at the trusted services or software the target relies on. They manipulate or compromise the trusted entities—often software updates, code repositories, or even hardware supply chains. In the case of the **3CX** breach, the attackers exploited the very update mechanism of a trusted app, turning it into a Trojan horse.

The attack is subtle, hidden beneath the veil of trust that companies place in their tools. The victim doesn’t even see the strike coming, and by the time they realize it, the damage is done. Trust is shattered, and the network is compromised. This is the power of a well-executed **supply chain attack**.

---

## **Who is 3CX?**

**3CX** is a key player in the world of unified communications. They provide software that integrates voice, video, and messaging into a single platform. The **3CX Desktop App** is used by businesses globally for their internal and external communication. It’s trusted by thousands of organizations to maintain seamless communication channels. But what happens when trust is betrayed? What happens when a tool designed to enhance security is turned against you?

---

## **Unraveling the Attack: The Analysis**

The **attack** began as a whisper. Users began to notice strange anomalies after updating their **3CX Desktop App**. The IT teams couldn’t make sense of it. But the breach was more sophisticated than anyone realized. Enter **Mandiant**—the knights who would sift through the wreckage and expose the truth.

Upon digging deeper, **Mandiant** discovered that the malicious code had been inserted during the **update process** of the **3CX Desktop App**. This wasn't just a simple vulnerability; it was a full-scale operation. **UNC4736**, a notorious North Korean hacker group, was the mastermind behind this attack. The group had gained access to **3CX’s infrastructure** and used their trusted update process as a delivery system for the malware.

---

## **Details from 3CX’s Official Site**

The **3CX** team, now aware of the breach, published an **official statement** [3CX Supply Chain Attack Details](https://www.3cx.com/blog/news/security-incident-updates/), outlining the incident. They provided a timeline of the attack, starting from the first user complaints to the eventual discovery of the malicious code. Versions of the **3CX Desktop App** prior to **18.12.416** were identified as vulnerable.

This update, initially intended to improve the software, instead opened a backdoor to thousands of organizations using the app. The **3CX** team’s swift action and transparency were crucial in halting the breach, but the damage was already done.

---

## **The Mandiant Findings: Unveiling the Malice**

The attack was not an isolated incident. **Mandiant**, the cybersecurity experts summoned by **3CX**, conducted a deep analysis that would unearth the hidden origins of the **3CX Supply Chain Attack**. Their findings revealed a carefully orchestrated chain of events—one that demonstrated the full scope of the attackers' sophistication.

According to **Mandiant**, the **initial compromise vector** of **3CX's network** stemmed from **malicious software downloaded from the Trading Technologies website**. This would become the key starting point in a series of cascading events. A **software supply chain attack**, where the very tools meant to enable business operations were weaponized, led to the infection of 3CX’s software. 

The victim in this case? **3CX Desktop App 18.12.416 and earlier versions**. These legitimate versions were **trojanized**—meaning they were embedded with **malicious code**. Upon installation, this trojanized software deployed a **downloader** named **SUDDENICON**, which quietly communicated with **command-and-control (C2) servers**. These servers, which were hidden in **encrypted icon files** hosted on **GitHub**, were a key aspect of the attack. 

The malware would then **decrypt the C2 servers**, enabling further downloads from the attackers. One such malicious payload was a **third-stage** malware known as **ICONICSTEALER**, a sophisticated **dataminer** that stealthily exfiltrated browser information and other sensitive data.

The attackers themselves were traced back to **UNC4736**, a **North Korean** cyber-espionage group. This group, part of a **nexus of activity** linked to **North Korea**, had carefully crafted this attack to infiltrate trusted companies worldwide. 

As the investigation unfolded, Mandiant's report would go on to highlight that this was not just one isolated breach—this was a **supply chain attack** that had its roots in another **software supply chain attack**. A chilling realization that the tools we trust can often be the very channels through which our systems are breached.

For more detailed information, you can read the full Mandiant report here: [Mandiant's Report on 3CX Supply Chain Compromise](https://cloud.google.com/blog/topics/threat-intelligence/3cx-software-supply-chain-compromise).

![AttackFlowChart](https://gist.github.com/user-attachments/assets/45307f91-9236-4301-9072-c1c91f92866b)
---

## **The Connection to Trading Technologies**

As Mandiant uncovered, the **initial compromise** that led to the 3CX supply chain attack originated from a trusted source—**Trading Technologies**, a provider of trading software. The malicious software, which was later found to be infected, was downloaded from their website, setting the stage for the supply chain attack on **3CX**.

According to Mandiant, the **Trading Technologies** website served as the **malicious entry point** for the attack, where the compromised software was hosted. This connection revealed a **deep supply chain vulnerability**, showcasing how an attack could propagate from one trusted entity to another, causing a ripple effect that affected 3CX's operations and beyond.


In total, this event marks an alarming trend of how **supply chain attacks** can unfold—starting with one trusted entity, spreading through legitimate channels, and ultimately compromising significant targets like 3CX.

For further reading on this, refer to the original [Mandiant Blog Post](https://cloud.google.com/blog/topics/threat-intelligence/3cx-software-supply-chain-compromise).

---

As the investigation continued, Mandiant traced the **initial intrusion vector** back to a compromised software package distributed via an earlier software supply chain attack. This attack began with a **tampered installer** for **X_TRADER**, a software package provided by **Trading Technologies**. 

Mandiant determined that the attack unfolded through a **complex loading process** that eventually led to the deployment of **VEILEDSIGNAL**, a **multi-stage modular backdoor**, alongside its various modules. The malware was cleverly designed to infiltrate and spread through **3CX’s network**, eventually reaching a server used for **software development**, where it corrupted a legitimate **3CX installer application**.

#### **How it Happened**
The **X_TRADER** software was not being actively used, yet it could still be downloaded from the **Trading Technologies** website as late as **2022**. Hackers infiltrated this software, signed it with the same digital signature as the legitimate software (set to expire in **October 2022**), and infected it with malicious code.

Once installed on a **3CX employee’s system**, this compromised installer allowed the attackers to **spread their access** across 3CX’s infrastructure, including critical servers. 

The attack was multi-faceted:

1. **Downloader and Command & Control (C2) Servers**: The compromised software contained a downloader that received **encrypted icon files** from **GitHub**, which in turn decrypted **C2 servers**. These servers were used to retrieve further payloads, including the **IconicStealer** dataminer capable of stealing browser information.

2. **Lateral Movement**: The attackers made use of **Fast Reverse Proxy**, a publicly available tool, to move laterally through the **3CX network**, increasing their control.

3. **SIGFLIP and DAVESHELL**: These tools were used to decrypt malicious code that was loaded into the system's memory. Specifically, **SIGFLIP** used an **RC4 stream cipher** to decrypt bad programs and find other malicious modules such as **DAVESHELL**.

4. **Compromising the 3CX Build Environment**: At some point, the attackers successfully compromised the **3CX build environment**, allowing them to tamper with the software development process itself. This move allowed them to inject further malicious code into the production software used by 3CX customers.

In short, the attack was multi-layered and sophisticated, involving several stages of exploitation, encryption, and lateral movement.

For more details on this phase, refer to the [Mandiant Blog](https://cloud.google.com/blog/topics/threat-intelligence/3cx-software-supply-chain-compromise).

This was the beginning of a more complex web of intrusions that impacted both **Trading Technologies** and **3CX**, resulting in the eventual compromise of 3CX’s legitimate software that spread to their customers.

For more details, refer to the article from [Wired](https://www.wired.com/story/3cx-supply-chain-attack-times-two/) and [Kratikal](https://kratikal.com/blog/an-overview-of-3cx-supply-chain-attack/#When_it_all_started).


---
## **Breaking Down the Attack**

Now that we've analyzed the scenario and gathered key insights from Mandiant and other sources, let's break down the individual components of the attack.

---

#### **The Downloader: `SUDDENICON`**

The malware triage analysis of **3CXDesktopApp installer MSI** reveals a fascinating and dangerous multi-step attack. Upon installation, the malicious software waits **seven days** before fetching additional payloads from **GitHub** and establishing **Command and Control (C2)** communication. Two files, **ffmpeg.dll** and **d3dcompiler_47.dll**, were dropped onto the system, with the latter containing the backdoor **SUDDENICON**.

Both of these libraries are commonly used and seem innocuous at first glance, but in this case, they were **backdoored**. It’s critical to understand that these files' names alone shouldn't trigger alarms. The real danger lies in their malicious modification. 

- **SUDDENICON** is a key part of the attack, running a downloader that fetches further malicious payloads. 
- **ffmpeg.dll** and **d3dcompiler_47.dll** are legitimate files, which have been compromised in this case.
  
For more details, refer to the [Elastic Security Blog](https://www.elastic.co/security-labs/elastic-users-protected-from-suddenicon-supply-chain-attack).

---

#### **The Payload: `ICONICSTEALER`**

The **ICONICSTEALER** malware is a **C/C++ data miner** that specifically targets **browser information**. Its function is to collect sensitive data from the victim’s system, particularly focusing on **browser history** and **application configuration data**.

This payload was deployed in the **third stage** of the 3CX attack and continues to be an active player in information theft.

- According to **Mandiant**, ICONICSTEALER is capable of pilfering sensitive data, making it a critical component in the attack sequence.
- More information on this infostealer can be found on [Malpedia](https://malpedia.caad.fkie.fraunhofer.de/details/win.iconic_stealer).

---

#### **UNC4736: The North Korean Threat Actor**

The attack has been traced back to **UNC4736**, a North Korean state-sponsored cybercrime group. **UNC4736** is known for its involvement in **supply chain attacks**, targeting software chains like **3CX** and **X_TRADER**. Their malware arsenal includes strains like **TAXHAUL**, **Coldcat**, and **VEILEDSIGNAL**.

These malware families have been used to target **Windows** and **macOS** systems, specifically focusing on **cryptocurrency** and **fintech** sectors. 

For further details, refer to the [Malpedia page on UNC4736](https://malpedia.caad.fkie.fraunhofer.de/actor/unc4736).

---

#### **IOCs (Indicators of Compromise)**

Key indicators from the attack help identify compromised files and malware signatures:

- **3CXDesktopApp-18.12.416.msi**
- **3CXDesktopApp.exe**
- **ffmpeg.dll**
- **d3dcompiler_47.dll**

These files are key signatures and can be used to trace the activity in affected systems. For more information on these indicators, refer to the [Zscaler Blog](https://www.zscaler.com/blogs/security-research/3cx-supply-chain-attack-campaign#affected-3cx-versions).

---

#### **Infection Chain**

Below is the general flow of the attack from initial compromise to data exfiltration.
![Infection Chain](https://gist.github.com/user-attachments/assets/a6dad5b1-6cca-4388-a67f-82c8508f01fc)
---

#### **Lateral Movement**

In the **3CX supply chain compromise**, lateral movement was facilitated by several malware families. These helped the attackers expand their foothold within the environment, allowing them to **communicate with C2 servers** and execute additional payloads.

Here are some of the key malware families used:

- **TaxHaul**: Upon execution, this malware decrypts a shellcode payload and persists via **DLL search-order hijacking**.
- **Coldcat**: A downloader that also establishes communication with **C2 infrastructure**.
- **PoolRat**: Used on **macOS systems** to collect system information and execute commands.
- **IconicStealer**: The third stage of the attack, serving as a data miner.

This lateral movement helped the attackers maintain persistence and further infiltrate the network.

For further details on the lateral movement, refer to the [DarkTrace Blog](https://www.darktrace.com/blog/3cx-supply-chain-compromise-how-darktrace-uncovered-a-smooth-operator).

---

#### **MITRE ATT&CK Framework**

The following MITRE ATT&CK tactics and techniques were identified during the analysis of this attack:

- **Resource Development**
    - T1588: Obtain Capabilities
    - T1588.004: Digital Certificates
    - T1608: Stage Capabilities
    - T1608.003: Install Digital Certificate
- **Initial Access**
    - T1190: Exploit Public-Facing Application
    - T1195: Supply Chain Compromise
    - T1195.002: Compromise Software Supply Chain
- **Persistence**
    - T1574: Hijack Execution Flow
    - T1574.002: DLL Side-Loading
- **Privilege Escalation**
    - T1055: Process Injection
    - T1574: Hijack Execution Flow
    - T1574.002: DLL Side-Loading
- **Command and Control**
    - T1071: Application Layer Protocol
    - T1071.001: Web Protocols
    - T1071.004: DNS
    - T1105: Ingress Tool Transfer
    - T1573: Encrypted Channel

For further analysis, refer to the [DarkTrace Blog](https://www.darktrace.com/blog/3cx-supply-chain-compromise-how-darktrace-uncovered-a-smooth-operator).

---

#### **Affected Versions**

The following versions of the **3CX Electron Windows App** and **Mac App** were affected by the attack:

- **Windows Versions**
    - 18.12.416
    - 18.12.407
- **Mac Versions**
    - 18.11.1213
    - 18.12.402
    - 18.12.407
    - 18.12.416

For more details, refer to the [Zscaler Blog](https://www.zscaler.com/blogs/security-research/3cx-supply-chain-attack-campaign#affected-3cx-versions).

---

#### **VirusTotal Analysis**

I uploaded the **3CXDesktopApp installer MSI** to **[VirusTotal](https://www.virustotal.com/gui/file/59e1edf4d82fae4978e97512b0331b7eb21dd4b838b850ba46794d9c7a2c0983/relations)** and conducted a thorough analysis. Here's a breakdown of the results:

1. **History**: 
![VTHistory](https://gist.github.com/user-attachments/assets/485bf6ea-36bd-4814-9485-989d44ffd060)
2. **Basic Info**: 
![VTBasicInfo](https://gist.github.com/user-attachments/assets/9e8f3292-f2ca-405a-a9dd-a49c852ce131)

Additionally, the **Community tab** led me to a report by **FileScan.io**, which can be accessed [here](https://www.filescan.io/reports/59e1edf4d82fae4978e97512b0331b7eb21dd4b838b850ba46794d9c7a2c0983/9ff36d46-d90b-40b6-a708-ba9e2ddcbdec/overview).

---

This breakdown outlines the critical components of the attack, from the initial compromise vector to the various tools used by the attackers. It also highlights the stages of the malware infection, lateral movement, and persistence techniques employed by the adversaries. Understanding these steps is crucial for mitigating similar attacks in the future.

---
### The Questions

**Q1. Understanding the scope of the attack and identifying which versions exhibit malicious behavior is crucial for making informed decisions if these compromised versions are present in the organization. How many versions of 3CX running on Windows have been flagged as malware?**

The analysis from **Zscaler** identified two specific versions of the **3CX DesktopApp** for Windows that were flagged as malicious.

    💡 Answer: 2 

**Q2. Determining the age of the malware can help assess the extent of the compromise and track the evolution of malware families and variants. What's the UTC creation time of the `.msi` malware?**

The creation time of the **`.msi`** malware was identified using the **VirusTotal** analysis.

    💡 Answer: 2023-03-13 06:33 

**Q3. Executable files (`.exe`) are frequently used as primary or secondary malware payloads, while dynamic link libraries (`.dll`) often load malicious code or enhance malware functionality. Analyzing files deposited by the Microsoft Software Installer (`.msi`) is crucial for identifying malicious files and investigating their full potential. Which malicious DLLs were dropped by the `.msi` file?**

According to the **Zscaler IOCs**, the **`.msi`** file dropped the following malicious **DLLs**:

    💡 Answer: ffmpeg.dll, d3dcompiler_47.dll

**Q4. Recognizing the persistence techniques used in this incident is essential for current mitigation strategies and future defense improvements. What is the MITRE Technique ID employed by the `.msi` files to load the malicious DLL?**

The MITRE ATT&CK technique **T1574**, which corresponds to **Hijack Execution Flow** and **DLL Side-Loading**, was used to load the malicious DLLs in this incident.

    💡 Answer: T1574

**Q5. Recognizing the malware type (`threat category`) is essential to your investigation, as it can offer valuable insight into the possible malicious actions you'll be examining. What is the threat category of the two malicious DLLs?**

Upon analyzing the hash of the **DLLs** in **VirusTotal**, the two malicious files were categorized as **Trojan** malware.

    💡 Answer: Trojan

**Q6. As a threat intelligence analyst conducting dynamic analysis, it's vital to understand how malware can evade detection in virtualized environments or analysis systems. This knowledge will help you effectively mitigate or address these evasive tactics. What is the MITRE ID for the virtualization/sandbox evasion techniques used by the two malicious DLLs?**

The **MITRE ID** for the **virtualization/sandbox evasion** techniques used by the two malicious **DLLs** is **T1497**.

    💡 Answer: T1497 (From VT of DLL under behavior)

**Q7. When conducting malware analysis and reverse engineering, understanding anti-analysis techniques is vital to avoid wasting time. Which hypervisor is targeted by the anti-analysis techniques in the `ffmpeg.dll` file?**

The **ffmpeg.dll** file employs anti-analysis techniques targeting the **VMware** hypervisor, as observed in the **VirusTotal behavior** analysis.

    💡 Answer: VMWare

**Q8. Identifying the cryptographic method used in malware is crucial for understanding the techniques employed to bypass defense mechanisms and execute its functions fully. What encryption algorithm is used by the `ffmpeg.dll` file?**

The **ffmpeg.dll** file uses the **RC4 encryption algorithm** to encrypt and obfuscate its payloads.

    💡 Answer: RC4

**Q9. As an analyst, you've recognized some TTPs involved in the incident, but identifying the APT group responsible will help you search for their usual TTPs and uncover other potential malicious activities. Which group is responsible for this attack?**

The **Lazarus Group**, a notorious North Korean state-sponsored APT, is responsible for this attack, as indicated by the nature of the attack and the tools used.

    💡 Answer: Lazarus

## **Conclusion: The Price of Trust**

The **3CX Supply Chain Attack** serves as a stark reminder that the greatest threats often come from within the systems we trust most. The attackers didn’t break into **3CX** directly—they infiltrated the supply chain, striking at the very heart of trust in software updates.

The lesson here is clear: **zero trust** is no longer optional. We must question every update, verify every file, and scrutinize every connection. In the world of cybersecurity, trust is a fragile thing. Once broken, it leaves behind not just data, but entire organizations vulnerable to the deepest kinds of betrayal.

---


    The trail has gone cold for now, but the echo of these breaches lingers in the silence. As always, the attackers remain patient, watching, and waiting for the next opening.

    Until the next breach...
