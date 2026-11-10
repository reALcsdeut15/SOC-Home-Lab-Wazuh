# SOC Home Lab Timeline

[Back to README](README.md)

**Target Stack:** Wazuh SIEM, Kali Linux, Ubuntu Server, Windows with Sysmon

| Status | Meaning |
|---|---|
| ✅ | Complete |
| 🔄 | In progress |
| ⬜ | Planned |

---

## Stage 1: Build and Detect (Modules 1 to 30)

### Phase 1: Lab Setup, Agents, and First Detections (Modules 1 to 10) ✅

| Module | Focus | Status |
|---|---|---|
| 1 | Deploy the Wazuh server | ✅ |
| 2 | Deploy the Kali attacker VM | ✅ |
| 3 | First brute-force test | ✅ |
| 4 | Deploy the Ubuntu target VM with a static IP | ✅ |
| 5 | Install the Wazuh agent on Ubuntu | ✅ |
| 6 | SSH brute force with Hydra | ✅ |
| 7 | Custom rule for a successful login after brute force | ✅ |
| 8 | Install the Wazuh agent on Windows | ✅ |
| 9 | Network scan and brute-force detection | ✅ |
| 10 | Log review and agent visibility check | ✅ |

### Phase 2: File Integrity Monitoring, Hardening, and Windows Logging (Modules 11 to 20) ✅

| Module | Focus | Status |
|---|---|---|
| 11 | File integrity monitoring (FIM) | ✅ |
| 12 | Review FIM file size limits | ✅ |
| 13 | File tampering test | ✅ |
| 14 | Firewall setup with UFW | ✅ |
| 15 | Windows process creation auditing (Event ID 4688) | ✅ |
| 16 | Send Event ID 4688 to Wazuh | ✅ |
| 17 | Confirm 4688 events in Wazuh | ✅ |
| 18 | Custom rule for cmd.exe and PowerShell | ✅ |
| 19 | Test the shell detection rule | ✅ |
| 20 | Install Sysmon | ✅ |

### Phase 3: Sysmon and Detection Engineering (Modules 21 to 30) 🔄

| Module | Focus | Status |
|---|---|---|
| 21 | Send Sysmon logs to Wazuh | ✅ |
| 22 | Custom rule for discovery commands | ✅ |
| 23 | Test the discovery rule | ✅ |
| 24 | Trace a detection gap | ✅ |
| 25 | Fix overlapping rules 100002 and 100003 | 🔄 |
| 26 | Measure alert noise | ⬜ |
| 27 | Tune noisy rules | ⬜ |
| 28 | Document the system state: network diagram, IP table, agents, and custom rules | ⬜ |
| 29 | Review rule IDs and MITRE mappings | ⬜ |
| 30 | Phase review and VM snapshot backups | ⬜ |

---

## Stage 2: Expand and Simulate (Modules 31 to 60)

### Phase 4: Vulnerability Detection (Modules 31 to 40) ⬜
- Turn on Wazuh vulnerability detection for the Ubuntu and Windows agents.
- Review the CVEs it finds and rank them by severity.
- Patch at least one finding and confirm it clears from the dashboard.

### Phase 5: Attack Simulation and Detection (Modules 41 to 60) ⬜
- Write rules for privilege escalation, such as a user being added to the local Administrators group.
- Write rules for persistence, such as new scheduled tasks and new services.
- Run attack simulations from Kali and confirm each rule fires.
- Tune each new rule to reduce false positives.

---

## Stage 3: Respond and Report (Modules 61 to 90)

### Phase 6: Active Response (Modules 61 to 75) ⬜
- Set up Wazuh active response to block an attacking IP after a high-severity alert.
- Test it against the Kali brute-force attack.
- Add an allowlist so the response never blocks the Wazuh server or my own access.

### Phase 7: MITRE ATT&CK Coverage (Modules 76 to 85) ⬜
- Map every custom rule to its MITRE ATT&CK technique.
- Build a coverage table that shows which tactics the lab detects and where the gaps are.

### Phase 8: Final Documentation (Modules 86 to 90) ⬜
- Create an architecture diagram of the full lab.
- Finish all answers in [CONCEPTS.md](CONCEPTS.md).
- Write a project summary covering what I built, what I learned, and what I would do next.
