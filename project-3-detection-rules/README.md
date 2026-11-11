# Project 3: Detection Engineering & Custom Rule Creation

## 📌 Objective
Develop and test custom detection logic for brute-force logon attempts on Windows endpoints. Translate generic threat activity into an industry-standard **Sigma Rule** (YAML format) and implement custom **Wazuh XML detection rules** to detect multi-attempt credential guessing in real time.

---

## 🛠️ Detection Engineering Workflow
1. **Log Metadata Identification:** Leverage key event fields (`Event ID 4625`, `LogonType 3`, `SubStatus 0xC000006A`).
2. **Sigma Rule Design:** Draft a platform-agnostic Sigma rule using standard YAML schema.
3. **SIEM Implementation:** Write custom Wazuh XML rules in `local_rules.xml` featuring threshold detection (frequency-based alerting).
4. **Validation:** Trigger simulated authentication failures to verify rule execution.

---

## 📄 Section 1: Standardized Sigma Rule (`win_brute_force_substatus.yml`)

```yaml
title: Potential Password Guessing via SMB/Network Logon Failure
id: a1b2c3d4-e5f6-7890-1234-56789abcdef0
status: experimental
description: Detects multiple Windows logon failures (Event ID 4625) with SubStatus 0xC000006A over a short time window via network logon (LogonType 3).
author: Kosolu Peter
references:
  - [https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4625](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4625)
logsource:
  product: windows
  service: security
detection:
  selection:
    EventID: 4625
    LogonType: 3
    SubStatus: '0xC000006A'
  timeframe: 1m
  condition: selection | count() >= 3
falsepositives:
  - Misconfigured batch scripts or service accounts utilizing outdated credentials over SMB.
level: high
tags:
  - attack.credential_access
  - attack.t1110.001
