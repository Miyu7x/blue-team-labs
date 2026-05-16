---
title: Splunk IT
module: Investigations
path: BTL1
platform: BTLO
tags: [splunk, spl, phishing, persistence, credential-dumping, lateral-movement, btl1]
status: in-progress
date: 2026-05-15
date_completed:
---

*Write-up by [Miyu7x](https://github.com/Miyu7x) | TryHackMe: [Miyu7](https://tryhackme.com/p/Miyu7) | BTLO: [Miyu7x](https://blueteamlabs.online/public/user/Miyu7x)*

---

## Scenario

One of the employees clicked on a malicious link and got the endpoint compromised. After executing malicious files and getting a foothold, the attacker compromised the AD by dumping sensitive information.

**Platform:** Splunk (local instance)
**Credentials:** admin:changeme
**Timeframe:** All Time

---

## Investigation Notes

> Use this section for freeform notes, SPL queries that worked, rabbit holes, and timeline reconstruction. Think out loud here before locking in answers below.

```
[ scratch space ]
```

---

## Q1 -- Phishing Email IP (3 pts)

**Question:** Did one of the employees inform you about a recent phishing email they received named "Invoice" during the investigation? Can you locate the IP address from which the file was downloaded?

**Format:** `X.X.X.X:Port`

<!-- Q: What Splunk source or index would contain evidence of a file download tied to a phishing document named "Invoice"? -->
<!-- Q: What SPL fields are most useful for isolating a file download event -- think URL, filename, source IP? -->
<!-- Q: Why is the port significant here, and what common ports might an attacker use to serve a malicious file? -->

**SPL Query Used:**
```spl

```

**Methodology:**


**Answer:**

---

## Q2 -- Malicious Payload Path (3 pts)

**Question:** What is the file that was downloaded after the malicious document was opened? Provide the complete path where the file was downloaded and saved.

**Format:** `C:\path\to\file.ext`

<!-- Q: What log sources capture file creation events on a Windows endpoint -- think Sysmon Event IDs? -->
<!-- Q: After a phishing doc executes, what directories are commonly used as drop zones for second-stage payloads? -->
<!-- Q: How would you correlate the timing of the Invoice document opening with a subsequent file creation event in Splunk? -->

**SPL Query Used:**
```spl

```

**Methodology:**


**Answer:**

---

## Q3 -- C2 Download URL (3 pts)

**Question:** What is the URL from which additional files were being downloaded?

**Format:** `http://something:something/file.ext`

<!-- Q: What Splunk fields or log sources would capture outbound HTTP requests from the compromised host? -->
<!-- Q: How does C2 staging typically look in network logs -- what patterns distinguish it from normal web traffic? -->
<!-- Q: What SPL functions help you extract or reconstruct a full URL from raw log data? -->

**SPL Query Used:**
```spl

```

**Methodology:**


**Answer:**

---

## Q4 -- Compromised Domain User (2 pts)

**Question:** Which domain user seemed to be compromised?

**Format:** `Username`

<!-- Q: What Windows Event IDs are associated with logon events, and which fields identify the account being used? -->
<!-- Q: How would you distinguish a compromised domain account from normal user activity in Splunk -- what behavioral signals stand out? -->
<!-- Q: If the attacker moved laterally using stolen credentials, where in the logs would that domain username appear? -->

**SPL Query Used:**
```spl

```

**Methodology:**


**Answer:**

---

## Q5 -- Persistence Program (2 pts)

**Question:** Could you check if there were any persistent actions detected? Name the program utilized.

**Format:** `filename.ext`

<!-- Q: What are the most common persistence mechanisms on Windows -- registry run keys, scheduled tasks, services, startup folders? -->
<!-- Q: Which Sysmon Event IDs or Windows Event IDs surface new process creation or registry modification events tied to persistence? -->
<!-- Q: What SPL search strategy would you use to hunt for newly created executables or processes that survive across reboots? -->

**SPL Query Used:**
```spl

```

**Methodology:**


**Answer:**

---

## Q6 -- Persistence Task Name (3 pts)

**Question:** What is the name of the task employed for maintaining persistence?

**Format:** `Task Name`

<!-- Q: What Windows Event ID logs scheduled task creation, and what fields contain the task name? -->
<!-- Q: How does a scheduled task created by an attacker typically differ from legitimate system tasks -- what naming patterns or paths are suspicious? -->
<!-- Q: How would you correlate this task with the compromised user account or the payload dropped in Q2? -->

**SPL Query Used:**
```spl

```

**Methodology:**


**Answer:**

---

## Q7 -- Reconnaissance Script (3 pts)

**Question:** What famous script, commonly used by attackers, was dropped as an additional file to facilitate internal reconnaissance and enumeration?

**Format:** `filename.ext`

<!-- Q: What are the most well-known attacker reconnaissance scripts used in Windows environments -- think PowerShell-based tools? -->
<!-- Q: What log sources or Event IDs would capture a script being written to disk or executed on the endpoint? -->
<!-- Q: How does PowerShell script block logging (Event ID 4104) help surface attacker tooling in Splunk? -->

**SPL Query Used:**
```spl

```

**Methodology:**


**Answer:**

---

## Q8 -- Credential Extraction File (3 pts)

**Question:** What additional file was deployed by the attacker to extract credentials?

**Format:** `filename.ext`

<!-- Q: What tools are commonly used to extract credentials from Windows memory or the SAM database -- think both native and third-party? -->
<!-- Q: What Sysmon events or process creation logs would reveal a credential-harvesting tool being dropped and executed? -->
<!-- Q: How would you search for known credential dumping tool names in Splunk across process, file, and network events? -->

**SPL Query Used:**
```spl

```

**Methodology:**


**Answer:**

---

## Q9 -- Credential Dumping Technique (3 pts)

**Question:** What technique for credential dumping, similar to a known method often used in domain controller environments, was employed by the attacker?

**Format:** `xxxxxx`

<!-- Q: What is the most well-known credential dumping technique targeting domain controllers -- think NTDS and VSS? -->
<!-- Q: How does this technique differ from dumping LSASS memory, and what artifacts does it leave behind in logs? -->
<!-- Q: What MITRE ATT&CK technique ID maps to this method, and how does that help you search Splunk for evidence? -->

**SPL Query Used:**
```spl

```

**Methodology:**


**Answer:**

---

## IOCs

| Type | Value |
|------|-------|
| IP:Port | |
| File path | |
| Download URL | |
| Domain user | |
| Persistence binary | |
| Scheduled task | |
| Recon script | |
| Cred tool | |
| Dump technique | |

---

## MITRE ATT&CK Mapping

| Technique ID | Name | Evidence |
|--------------|------|----------|
| | | |

---

## Key Takeaways

<!-- What did this investigation teach you about attacker TTPs, Splunk hunting, or log analysis? -->
