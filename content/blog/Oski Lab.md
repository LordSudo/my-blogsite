---
title: "CyberDefenders: Oski Lab"
date: 2025-04-19T22:00:47+05:30
draft: false
params:
  slug: ""
layout: "post"
tags: ["Threat Intel" , "CyberDefenders"]
authors: ["Lordsudo"]
---
## Prologue — Into the Shadows

In the endless chess game between defenders and adversaries, sharpening one's edge is a ritual as old as the hunt itself. Seeking to refresh my threat intelligence tradecraft, I turned to CyberDefenders, a playground for digital detectives, and selected a case that promised just the right dose of malice: Oski. [Access it from here](https://cyberdefenders.org/blueteam-ctf-challenges/oski/)

Beneath its name lay the fragments of a malicious campaign, waiting to be pieced together — a puzzle designed to challenge both observation and deduction. What began as an exercise would soon unravel into a tale of compromise, command, and control.

## Scenario - The Baited Invoice

The accountant at the company received an email titled "Urgent New Order" from a client late in the afternoon. When he attempted to access the attached invoice, he discovered it contained false order information. Subsequently, the SIEM solution generated an alert regarding downloading a potentially malicious file. Upon initial investigation, it was found that the PPT file might be responsible for this download. Could you please conduct a detailed examination of this file?

## The Hunt — Tracing the Malicious Trail

The investigation began not with a smoking gun, but with something far more subtle: an MD5 hash. Often overlooked, these digital fingerprints are the first breadcrumb in reconstructing a threat actor's trail.

    Provided Artifact:
    MD5 Hash: 12c1842c3ccafe7408c23ebf292ee3d9

No executable, no email attachment — just this solitary signature. The task was clear: identify the file, uncover its purpose, and trace the path from compromise to command.

### Stage 1 — Initial Recon: The VirusTotal Verdict

The first step was to feed the hash into the threat intelligence oracle — VirusTotal.
Within moments, the silence was broken. Multiple engines had reached a consensus: the file associated with this hash was flagged as malicious.

![VTResults](https://gist.github.com/user-attachments/assets/79aaa6d3-eacd-41ff-a260-49455b3f62b9)

But knowing that it was malicious wasn’t enough — the true power of VirusTotal lies in the historical context.
I delved into the file’s recorded history to uncover its timeline of exposure:

    When it first surfaced.

    When it began making rounds in the wild.

![VTHistory](https://gist.github.com/user-attachments/assets/ae2908be-9ad5-4814-810a-41bbead82ed7)

This timeline not only provided clues about the malware's age but also hinted at the spread of the campaign.

Armed with this background, I moved to Basic Properties, where VirusTotal unmasked the file's true nature: a Windows 32-bit executable.

![VTbasicinfo](https://gist.github.com/user-attachments/assets/c77d51ca-24c1-4f15-b3f1-4a8d5f66b7eb)

The innocent façade dropped. The attachment wasn’t an invoice, but a carefully crafted binary, waiting for its moment to strike.
### Stage 2 — Unmasking Connections: The Relations Tab

Next, I examined the Relations tab — a crucial map of the malware's behavior in the wild.

Here, the plot deepened. VirusTotal recorded the sample reaching out to an external host, specifically making two intriguing HTTP requests:

    A POST request to a PHP endpoint.

    A GET request to download a DLL.

![VTRelations](https://gist.github.com/user-attachments/assets/d15ffe14-7291-4d14-b0df-1b8caa7dca64)

The structure of these requests suggested classic staged infection behavior:
first establish contact with a Command and Control (C2) server, then retrieve further payloads.
The DLL's name — sqlite3.dll — was a clever disguise, masquerading as a legitimate library to evade suspicion.

At this point, the signature was clear: this wasn’t just a rogue executable — it was part of a larger ecosystem of compromise.
### Stage 3 — Behavior Under the Microscope: Any.Run Sandbox Analysis

To validate these findings and observe the malware in action, I moved to Any.Run, a dynamic sandbox environment.
Within moments of execution, the malware began revealing its true colors.

![Anyrun](https://gist.github.com/user-attachments/assets/c58d203e-5bd6-49d1-8cc0-5d8047ae0cef)

The HTTP request logs confirmed the prior suspicion — an unmistakable pattern:

    POST request to:
    http://171.22.28.221/5c06c05b7b34e8e6.php
    — likely serving as an infection beacon or initial handshake.

    GET request to:
    http://171.22.28.221/9e226a84ec50246d/sqlite3.dll
    — fetching the secondary payload, masked as a legitimate DLL.

![httprequests](https://gist.github.com/user-attachments/assets/ead65c93-68ec-4462-a94a-2f4423bdacb1)

This sequence — beaconing, followed by payload delivery — aligned perfectly with known behaviors of droppers and loaders, which often operate in this two-step fashion to bypass static detection and deliver their real malicious logic in stages.
### Stage 4 — Process Behavior: Unveiling the Attack Chain

Beyond network communication, the malware’s behavior on the local machine told an equally chilling story.

Upon execution, the sample — disguised as VPN.exe — launched a new instance of cmd.exe. That process, in turn, executed timeout.exe, forming a predictable but telling process chain:

vpn.exe → cmd.exe → timeout.exe

![processtree](https://gist.github.com/user-attachments/assets/f531494d-913a-410c-b752-47aa7c3795b7)

The command issued by cmd.exe was even more revealing:

"C:\Windows\system32\cmd.exe" /c timeout /t 5 & del /f /q "C:\Users\admin\AppData\Local\Temp\VPN.exe" & del "C:\ProgramData\*.dll"" & exit

A clear sequence:

    Delay Execution: timeout /t 5
    A stall tactic, likely designed to give any network operations or in-memory payload execution time to complete.

    Self-Deletion: del /f /q "VPN.exe"
    Once its purpose was served, the dropper erased itself to cover its tracks.

    Payload Clean-Up: del "C:\ProgramData\*.dll""
    A final sweep to remove any downloaded .dll files — evidence, payloads, or both.
    Interestingly, the syntax error (*.dll"") hinted at a rushed or imperfect script on the attacker’s part.

### Stage 5 — Timeline & Techniques: The MITRE Mapping

Peering into the process timeline offered even more clarity on the malware’s objectives.
The executable’s behavior aligned with classic info-stealer patterns: scanning browsers, local files, and active sessions for credentials and other sensitive artifacts.

![processtimeline](https://gist.github.com/user-attachments/assets/7c78725d-2932-4a41-8c5d-dcadc0b92b0a)

The timeline also offered an automatic MITRE ATT&CK mapping, helping align observed behaviors with known adversarial techniques.
From initial access, to credential access, to defense evasion — the campaign was structured like a carefully rehearsed play.
### Stage 6 — Attribution: Unmasking Stealc

Finally, after correlating the observed behavior, network indicators, and payload structure, the malware’s identity was confirmed: a variant of Stealc.

![malwconf](https://gist.github.com/user-attachments/assets/7fa25508-463d-4d97-b39e-5afc356913c0)

Stealc is a seasoned player in the info-stealing ecosystem, specializing in:

    Harvesting browser-stored passwords.

    Exfiltrating sensitive session data.

    System reconnaissance and fingerprinting.

    Payload staging and modular expansion.

    Employing RC4 encryption to protect stolen data and configuration blobs.

The presence of RC4 encryption was verified during the malware’s configuration analysis — a signature tactic to ensure both data confidentiality during exfiltration and to hinder reverse engineering.

## The Questions

Q1. Determining the creation time of the malware can provide insights into its origin. What was the time of malware creation?

The creation time was identified during the VirusTotal History tab analysis, where the sample's metadata revealed its origin timestamp.

    💡 Answer: 2022-09-28 17:40

Q2. Identifying the command and control (C2) server that the malware communicates with can help trace back to the attacker. Which C2 server does the malware in the PPT file communicate with?

This was observed during the HTTP request inspection inside Any.Run, where the sample initiated communication with its C2 infrastructure.

    💡 Answer: http://171.22.28.221/5c06c05b7b34e8e6.php

Q3. Identifying the initial actions of the malware post-infection can provide insights into its primary objectives. What is the first library that the malware requests post-infection?

Captured during the HTTP request analysis in Any.Run, the first external resource the malware attempted to fetch was a .dll file.

    💡 Answer: sqlite3.dll

Q4. Upon examining the malware, it appears to utilize the RC4 key for decrypting a base64 string. What specific RC4 key does this malware use?

Extracted during the malware configuration analysis (malconf) phase, where the encryption key was hardcoded in the binary.

    💡 Answer: 5329514621441247975720749009

Q5. Identifying an adversary's techniques can aid in understanding their methods and devising countermeasures. Which MITRE ATT&CK technique are they employing to steal a user's password?

This mapping was confirmed during the process timeline analysis via Any.Run, which correlated to MITRE ATT&CK technique ID.

    💡 Answer: T1555

Q6. Malware may delete files left behind by the actions of their intrusion activity. Which directory or path does the malware target for deletion?

Found within the process command-line parameters for cmd.exe, revealing the targeted path during the deletion phase.

    💡 Answer: C:\ProgramData

Q7. Understanding the malware's behavior post-data exfiltration can give insights into its evasion techniques. After successfully exfiltrating the user's data, how many seconds does it take for the malware to self-delete?

This was clearly visible in the execution command sequence via timeout /t 5, observed during the process analysis.

    💡 Answer: 5


## Aftermath — Lessons from the Oski Hunt

The "Oski" case was a sharp reminder of the quiet sophistication behind even seemingly simple malware campaigns.

What began as a humble investigation — a single MD5 hash — unfolded into the anatomy of a staged attack:
a malicious executable concealed behind a forged invoice, designed to blend into the daily noise of corporate life. Once executed, the malware reached out to its Command & Control server, fetched its secondary payload, harvested credentials, and, like a seasoned thief, cleaned up its traces before anyone could notice.

The behavioral evidence, supported by process trees, HTTP communications, and self-deletion routines, painted a clear profile: this was the handiwork of Stealc — an infostealer built for modular exfiltration, anti-forensics, and quiet persistence.

But beyond the technical findings, the exercise underscored something far more important:

    Malware doesn't need to be loud to be effective. It needs only to be precise, and patient.

The Oski lab served as a perfect example of why defenders must trace the smallest of footprints, and why proactive threat intelligence — from hash analysis to sandboxing — is the only true shield in a world where attackers erase their tracks as fast as they make them.

---

    The hunt is over for now — but the shadows are always waiting to shift once more.
    Until the next analysis...

