# SOC Home Lab (Wazuh)

### Project Status: Phase 3, Detection Engineering with Sysmon

## Project Objective
Build a working Security Operations Center (SOC) lab with open-source tools.
I simulate attacks, collect logs in a central SIEM, and write custom rules
to detect them.

▶ **View the complete engineering milestones here:** [Download Full 30-60-90 Day Timeline PDF](soc_homelab_30_60_90_timeline.pdf)


## 🛠️ Tooling Stack
* **Virtualization Engine:** Oracle VirtualBox
* **SIEM Engine:** Wazuh OVA Appliance v4.14.7
* **Threat Generator:** Kali Linux (x86 architecture)

---

## 📈Milestone Logs
### 🏗️ Day 1: Deploying the Wazuh Server
- **Task:** Imported the Wazuh OVA into VirtualBox and confirmed the dashboard was reachable.
- **Status:** Complete ✅
- **Verification:**
* **Telemetry Verification:**
<img width="1009" height="579" alt="image" src="https://github.com/user-attachments/assets/73259352-121e-4c2d-bfe4-f90c330b8276" />

### 🪤 Day 2: Deploying the Attacker VM
- **Task:** Deployed Kali Linux and connected it to the host-only network so it could reach the Wazuh server.
- **Status:** Complete ✅
- **Verification:**
* **Telemetry Verification:**
<img width="1067" height="753" alt="image" src="https://github.com/user-attachments/assets/b0a6c156-d4e8-44a9-a7e0-79973fef08fe" />

### 🪤 Day 3: First Brute-Force Test
- **Task:** Ran a brute-force attack from Kali and confirmed Wazuh generated alerts.
- **Status:** Complete ✅
- **Verification:**
* **Telemetry Verification
<img width="1048" height="532" alt="image" src="https://github.com/user-attachments/assets/ffcb3c7f-dadf-4177-8558-d92927e435fc" />

### 🖥️ Day 4: Deploying the Ubuntu Target VM
- **Task:** Deployed an Ubuntu Server VM and set a static IP address so it keeps the same address after reboots.
- **Status:** Complete ✅
- **Verification:**
* **Telemetry Verification:**
<img width="1360" height="766" alt="image" src="https://github.com/user-attachments/assets/59b9942c-bd43-4159-b781-51b1d15dff37" />

### 👀 Day 5: Installing the Wazuh Agent on Ubuntu
- **Task:** Used a VirtualBox shared folder to move the Wazuh agent package onto the Ubuntu VM, since it had no internet access. Installed the agent and connected it to the Wazuh server.
- **Status:** Complete ✅
- **Verification:**
* **Telemetry Verification:**
<img width="1359" height="676" alt="image" src="https://github.com/user-attachments/assets/ac7cf235-cd89-45bb-b15f-c9b1c6b9936e" />
<img width="1355" height="606" alt="image" src="https://github.com/user-attachments/assets/5851b76a-5a35-4643-8935-d5cdd3c3f802" />

### ⚔️Day 6: SSH Brute-Force with Hydra
- **Task:** Used Hydra on Kali to brute force SSH on the Ubuntu VM, then reviewed the high-severity alerts in the Wazuh dashboard.
- **Status:** Complete ✅
- **Verification:**
* **SIEM Telemetry Verification:**
<img width="676" height="634" alt="image" src="https://github.com/user-attachments/assets/4920f428-d563-47c1-bfcf-4eb9f9f3504c" />
<img width="1354" height="671" alt="image" src="https://github.com/user-attachments/assets/3c27e5c6-28f6-4f99-9fcf-ea8b647f6d9a" />


### 🧠 Day 7: Custom Rule for Successful Login After Brute Force
- **Task:** Wrote a custom rule in `local_rules.xml` that alerts when a successful login follows repeated failures. Mapped it to MITRE ATT&CK.
- **Status:** Complete ✅
- **Verification:**
* SIEM Alert Telemetry Verification:**
<img width="620" height="531" alt="image" src="https://github.com/user-attachments/assets/4eb7bc66-b505-48a0-8950-81271ba05271" />
<img width="1293" height="559" alt="image" src="https://github.com/user-attachments/assets/147b09b4-6346-49b6-a49d-ac94f0743ad1" />


### 📁 Day 8: Wazuh Agent on a Windows Host
- **Task:** Installed the Wazuh agent on my Windows laptop and connected it to the Wazuh server at 192.168.56.101 over the host-only network.
- **Status:** Complete ✅
- **Verification:**
* **SIEM Telemetry Verification:**
<img width="1347" height="593" alt="image" src="https://github.com/user-attachments/assets/a677e7b8-7503-4000-b329-b27e36b4601c" />
<img width="1331" height="659" alt="image" src="https://github.com/user-attachments/assets/88704bf8-c92c-4a60-91d3-c771d259f67b" />


### 📂Day 9: Network Scan and Brute-Force Detection

**Attack**
- Used Nmap to find active hosts on the host-only network (`192.168.56.0/24`).
- Built a small custom password list.
- Used Hydra to brute force SSH on the Ubuntu target (`192.168.56.120`).

**Detection**
- The Wazuh agent on Ubuntu collected the failed login events.
- The agent sent them to the Wazuh server (`192.168.56.101`).
- Confirmed Level 10+ alerts on the dashboard.

<img width="1206" height="359" alt="image" src="https://github.com/user-attachments/assets/a5ebbabe-c9fa-40e7-9b6f-4a4f099ae4eb" />

<img width="1345" height="670" alt="image" src="https://github.com/user-attachments/assets/ff7c50ac-ee58-418a-9b36-27a0a451c186" />


### 📁 Day 10: Log Review and Agent Visibility Check
- **Task:** Reviewed 24 hours of events in Wazuh Discover to confirm logging from my attack tests.
- **Results:**
  - Found 181 events from the test activity.
  - Confirmed both `wazuh-server` and my Windows laptop (`Glory2Glory`) were sending logs.
- **Status:** Phase 1 Complete ✅

<img width="845" height="681" alt="image" src="https://github.com/user-attachments/assets/7d66b661-b528-41bb-8b4c-2e7d3ef4bc03" />


### 📂 Day 11: File Integrity Monitoring (FIM)
- **Task:** Set up real-time file monitoring on the Ubuntu VM.
- **Steps:**
  - Edited `ossec.conf` to watch `/root/top_secret` with `realtime="yes"` and `report_changes="yes"`.
  - Created a test file, `leak.txt`, to simulate a sensitive file being dropped.
  - Found the FIM alert in Discover from the Ubuntu agent (192.168.56.120).
- **Status:** Complete ✅

<img width="1347" height="670" alt="image" src="https://github.com/user-attachments/assets/137063ed-3330-4aa1-85bc-d51f18dfcf5f" />


### 📁 Day 12: Reviewing FIM File Size Limits
- **Task:** Reviewed `internal_options.conf` to understand the file size limits for FIM change reporting.
- **Findings:**
  - Confirmed `syscheck.file_max_size` is set to 1024 MB.
  - This means Wazuh can report changes on files in my monitored folders up to that size.
- **Status:** Complete ✅

<img width="636" height="768" alt="image" src="https://github.com/user-attachments/assets/a76b3a81-6312-4085-903e-64e993ad0de6" />


### 📂 Day 13: File Tampering Test
- **Task:** Simulated an insider changing a protected file to test FIM change reporting.
- **Steps:**
  - Added the line `EXFILTRATION_TARGET=192.168.56.102` to `/root/top_secret/leak.txt`.
  - Wazuh detected the change.
  - The `syscheck.diff` field in the alert showed the exact line added, marked with `+`.
- **Status:** Phase 2 FIM Testing Complete ✅
  
<img width="1282" height="630" alt="image" src="https://github.com/user-attachments/assets/16952bc5-c730-4238-98d5-186fbffb6992" />


### 📁 Day 14: Firewall Setup with UFW
- **Task:** Configured UFW on the Ubuntu VM to limit which systems can connect.
- **Steps:**
  - Reviewed which ports were open.
  - Allowed traffic only from the Wazuh server (`192.168.56.101`) and Kali (`192.168.56.102`). Kali stays allowed so I can keep running attack tests.
  - Restricted SSH (port 22/TCP) to those addresses.
  - Enabled UFW and confirmed the default policy denies other incoming traffic.
- **Status:** Complete ✅

<img width="544" height="139" alt="image" src="https://github.com/user-attachments/assets/67343acc-6d92-4284-b691-d7d046f29e3a" />

<img width="789" height="768" alt="image" src="https://github.com/user-attachments/assets/ddceca82-c45b-429f-9435-afc59a6a5f4c" />


### 📂 Day 15: Windows Process Creation Auditing
- **Task:** Turned on Windows auditing for process creation.
- **Steps:**
  - Opened `secpol.msc` and went to Advanced Audit Policy Configuration, then Detailed Tracking.
  - Enabled Success and Failure auditing for Audit Process Creation (Event ID 4688).
  - Ran `gpupdate /force` to apply the change.
- **Status:** Complete ✅

<img width="911" height="636" alt="image" src="https://github.com/user-attachments/assets/4253645b-c578-44e8-8156-5ec6d27c0718" />

<img width="612" height="512" alt="image" src="https://github.com/user-attachments/assets/cdac9317-b33d-4ff6-8824-26d7c51edde6" />

### 📁 Day 16: Sending Event ID 4688 to Wazuh
- **Task:** Configured the Windows Wazuh agent to forward process creation events.
- **Steps:**
  - `ossec.conf` is protected under Program Files, so I copied it out, edited it, and copied it back with admin rights.
  - Added a `localfile` block for the Security event log with the query `Event[System[EventID=4688]]` to collect only process creation events.
  - Restarted the Wazuh agent service and confirmed it started cleanly.
- **Status:** Complete ✅

<img width="948" height="655" alt="image" src="https://github.com/user-attachments/assets/3779a182-2138-4939-9175-746bc1829c70" />


### 📂 Day 17: Confirming 4688 Events in Wazuh
- **Task:** Confirmed process creation events from Windows were reaching Wazuh.
- **Steps:**
  - Started the Wazuh server and Kali.
  - Ran test activity, then searched Discover with `data.win.system.eventID: "4688"`.
  - Confirmed Wazuh parsed the 4688 events.
- **Status:** Complete ✅

<img width="1191" height="735" alt="image" src="https://github.com/user-attachments/assets/a146b1dd-6c72-4eb4-8b85-4647ff0c32c1" />

<img width="929" height="609" alt="image" src="https://github.com/user-attachments/assets/a30dd330-09e3-47a7-b65b-786ec65183f1" />


### 📁 Day 18: Custom Rule for cmd.exe and PowerShell
- **Task:** Wrote a custom Wazuh rule to flag command shell launches.
- **Rule details:**
  - Added rule `100002` to `local_rules.xml` at Level 12.
  - Matches Event ID 4688 when the process is `cmd.exe` or `powershell.exe`, using regex.
  - Mapped to MITRE ATT&CK T1059.001 (PowerShell) and T1059.003 (Windows Command Shell).
  - Restarted the Wazuh manager and confirmed the rule loaded without errors.
- **Status:** Complete ✅

<img width="1145" height="630" alt="image" src="https://github.com/user-attachments/assets/d6e2fba6-411a-4ab0-bcc1-a520a7fd9249" />


### 📂 Day 19: Testing the Shell Detection Rule
- **Task:** Tested rule 100002 by opening an admin command prompt.
- **Results:**
  - Opened `cmd.exe` as administrator on the Windows laptop.
  - Searched Discover with `rule.id: "100002"` and found 30+ matching alerts.
  - Confirmed the events were raised to Level 12.
- **Note:** This rule fires on every shell launch, so in a real environment it would be noisy. Next step would be tuning it.
- **Status:** Complete ✅

<img width="1138" height="634" alt="image" src="https://github.com/user-attachments/assets/c9040f71-f412-42bf-86f0-e63bebb73fe6" />

<img width="1143" height="637" alt="image" src="https://github.com/user-attachments/assets/f2971de6-1b34-4661-a925-41b62ec40b93" />


### 📁 Day 20: Installing Sysmon
- **Task:** Installed Microsoft Sysmon on the Windows laptop for more detailed logging than built-in Windows auditing.
- **Steps:**
  - Wrote a Sysmon config to log Event ID 1 (process creation with file hashes) and Event ID 3 (network connections).
  - Fixed XML errors in the config file.
  - Installed Sysmon and confirmed the driver and service were running.
  - Deleted unused VM disks to free up storage.
- **Status:** Phase 2 Complete ✅

<img width="1126" height="360" alt="image" src="https://github.com/user-attachments/assets/a26d9560-e689-4868-aae1-c983ecac0507" />


### 📂 Day 21: Sending Sysmon Logs to Wazuh
- **Task:** Forwarded Sysmon events to Wazuh and confirmed they were parsed.
- **Troubleshooting:**
  - Checked the agent log (`ossec.log`) and found Sysmon events weren't being collected.
  - Added a `localfile` block in `ossec.conf` for `Microsoft-Windows-Sysmon/Operational`.
  - Restarted the agent (`WazuhSvc`).
  - Confirmed 20+ Sysmon events in Discover.
- **Status:** Complete ✅

<img width="1254" height="653" alt="image" src="https://github.com/user-attachments/assets/4b5ac539-a754-4956-92eb-4eecce0d66c4" />

<img width="977" height="531" alt="image" src="https://github.com/user-attachments/assets/84110cb7-b98c-496b-81cc-f1bbe05dd3ca" />


### 📁 Day 22: Custom Rule for Discovery Commands
- **Task:** Wrote a rule to detect common reconnaissance commands an attacker runs after getting access.
- **Rule details:**
  - Added rule `100003` to `local_rules.xml` at Level 12.
  - Built on Sysmon events using `<if_sid>61600</if_sid>`.
  - Matches `whoami.exe`, `net.exe`, or `ipconfig.exe` in the `win.eventdata.image` field.
  - Mapped to MITRE ATT&CK: T1033 (whoami), T1016 (ipconfig), and T1087 (net user).
  - Restarted the manager and confirmed the rule loaded.
- **Status:** Complete ✅

<img width="1247" height="652" alt="image" src="https://github.com/user-attachments/assets/81a5947d-f8ff-45fd-b31c-4d22fc5ac453" />


### 📂 Day 23: Testing and Fixing the Discovery Rule
- **Task:** Tested rule 100003 with live commands and fixed it when it didn't fire.
- **Steps:**
  - Ran `whoami`, `ipconfig`, and `net user` in an admin shell.
  - The rule didn't fire at first. I compared the raw events and found the process name was in `win.eventdata.newProcessName`, not `image`.
  - Updated the rule to use that field and restarted the manager.
  - Confirmed Level 12 alerts for the commands.
- **Status:** Phase 3 Detection Working ✅

<img width="1308" height="672" alt="image" src="https://github.com/user-attachments/assets/c72447fa-5b9d-4c52-bc42-6e39e87dd2f6" />


### 📂 Day 24: Tracing a Detection Gap
- **Task:** Found out why rule 100003 caught only 1 of 3 recon commands on Day 23.
- **Steps:**
  - Ran `whoami`, `ifconfig /all`, and `net user` from an admin command prompt.
  - Expanded each alert in Wazuh Discover and compared the process fields.
- **Findings:**

| Command | New Process | Parent Process | Rule That Fired |
|---|---|---|---|
| whoami | whwoami.exe | cmd.exe | 100002 |
| ipconfig | ipconfig.exe | cmd.exe | 100002 |
| net user | net.exe | cmd.exe | 100002 | 
| (automatic) | net1.exe | net.exe | 100003 |

  - Rule 100002 matched `cmd.exe` in the parent process field, so it fired on every program started from a command prompt.
  - Rule 100002 sits above rule 100003, and Wazuh uses the first matching rule. Rule 100003 only caught net1.exe because its parent is net.exe.
  - Rule 100002 had fired 70 times, which shows how noisy it was.
- **Next:** Narrow rule 100002 and fix rule 100003 on Day 25.
- **Status:** Complete ✅

<img width="656" height="623" alt="unnamed" src="https://github.com/user-attachments/assets/302e517e-a35d-42b3-8b4c-eda663ca5ef6" />

<img width="658" height="613" alt="unnamed" src="https://github.com/user-attachments/assets/0015daaa-ddc0-4e9f-81db-9fc00cc32385" />

<img width="660" height="613" alt="unnamed" src="https://github.com/user-attachments/assets/7cfd542b-d682-42d7-879c-5386e7d9680f" />

<img width="1317" height="648" alt="unnamed" src="https://github.com/user-attachments/assets/6f6a6448-c735-4ef4-b37e-572d2b902a7a" />

