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
### 🏗️Day 1: Deploying the Wazuh Server
- **Task:** Imported the Wazuh OVA into VirtualBox and confirmed the dashboard was reachable.
- **Status:** Complete ✅
- **Verification:**
* **Telemetry Verification:**
<img width="1009" height="579" alt="image" src="https://github.com/user-attachments/assets/73259352-121e-4c2d-bfe4-f90c330b8276" />

### 🪤Day 2: Deploying the Attacker VM
- **Task:** Deployed Kali Linux and connected it to the host-only network so it could reach the Wazuh server.
- **Status:** Complete ✅
- **Verification:**
* **Telemetry Verification:**
<img width="1067" height="753" alt="image" src="https://github.com/user-attachments/assets/b0a6c156-d4e8-44a9-a7e0-79973fef08fe" />

### 🪤Day 3: First Brute-Force Test
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

### 👀Day 5: Installing the Wazuh Agent on Ubuntu
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


### 🧠Day 7: Custom Rule for Successful Login After Brute Force
- **Task:** Wrote a custom rule in `local_rules.xml` that alerts when a successful login follows repeated failures. Mapped it to MITRE ATT&CK.
- **Status:** Complete ✅
- **Verification:**
* SIEM Alert Telemetry Verification:**
<img width="620" height="531" alt="image" src="https://github.com/user-attachments/assets/4eb7bc66-b505-48a0-8950-81271ba05271" />
<img width="1293" height="559" alt="image" src="https://github.com/user-attachments/assets/147b09b4-6346-49b6-a49d-ac94f0743ad1" />


### 📁Day 8: Wazuh Agent on a Windows Host
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


### 📁Day 10: Log Review and Agent Visibility Check
- **Task:** Reviewed 24 hours of events in Wazuh Discover to confirm logging from my attack tests.
- **Results:**
  - Found 181 events from the test activity.
  - Confirmed both `wazuh-server` and my Windows laptop (`Glory2Glory`) were sending logs.
- **Status:** Phase 1 Complete ✅

<img width="845" height="681" alt="image" src="https://github.com/user-attachments/assets/7d66b661-b528-41bb-8b4c-2e7d3ef4bc03" />


### 📂Day 11: File Integrity Monitoring (FIM)
- **Task:** Set up real-time file monitoring on the Ubuntu VM.
- **Steps:**
  - Edited `ossec.conf` to watch `/root/top_secret` with `realtime="yes"` and `report_changes="yes"`.
  - Created a test file, `leak.txt`, to simulate a sensitive file being dropped.
  - Found the FIM alert in Discover from the Ubuntu agent (192.168.56.120).
- **Status:** Complete ✅

<img width="1347" height="670" alt="image" src="https://github.com/user-attachments/assets/137063ed-3330-4aa1-85bc-d51f18dfcf5f" />


### 📁 Day 12: Advanced Core Ingestion Tuning & Capability Verification
* **Task:** Conduct optimization auditing inside the internal system options matrix to verify high-capacity forensic file digestion parameters.
* **Engineering Review & Validation:**
  * Audited the core system configuration layer definitions (`internal_options.conf`) to inspect the engines's text delta comparison cap limitations.
  * Verified that the core ingestion parameter `syscheck.file_max_size` is target-locked at its optimized performance threshold of **1024 MB (1 GB)**.
  * Validated that the underlying kernel hooks possess wide-open capability to compute cryptographic text difference mapping (diffs) across heavily monitored system folders.
* **Status:** Core Tuning & Capability Verification Complete ✅

<img width="636" height="768" alt="image" src="https://github.com/user-attachments/assets/a76b3a81-6312-4085-903e-64e993ad0de6" />


### 📂 Day 13: Live File-Tampering Simulation & Cryptographic Text Delta Extraction
* **Task:** Execute an active insider-threat simulation inside a guarded filesystem container to text real-time cryptographic text difference mapping (diffs).
* **Forensic Auditing & Detection Metrics:**
  * Appended a high-risk text line signature (`EXFILTRATION_TARGET=192.168.56.102`) into the restricted text document layer (`/root/top_secret/leak.txt`).
  * Validated that the underlying kernel-level file auditing engine successfully tracked the content alteration event natively.
  * Isolated the tracking payload inside the central SIEM console, verifying that the advanced **`syscheck.diff`** data field explicitly exposed the exact added string lines using cryptographic text delta map identifiers (`+`).
* **Status:** Phase 2 File Integrity Auditing Milestone Complete ✅
  
<img width="1282" height="630" alt="image" src="https://github.com/user-attachments/assets/16952bc5-c730-4238-98d5-186fbffb6992" />


### 📁 Day 14: Local Firewall Hardening & Network Access Control Baseline 
* **Task:** Implement host-based network segmentation parameters on the target endpoint node using the native Linux firewall utility.
* **Engineering Hardening Metrics:**
  * Audited the native firewall subsystem (**UFW**) to identify open baseline entry vectors.
  * Hardcoded explicit rule matrices to permit traffic exclusively from the centralized SIEM core manager (`192.168.56.101`) and the tactical attacker framework (`192.168.56.102`)
  * Explicitly locked down the main transport entry channel (**Port 22/TCP**) to enforce strict administrative access routes.
  * Triggered system-wide perimeter activation, verifying that the default policy automatically drops unauthorized incoming communication attempts on startup.
* **Status:** Local Firewall Baseline Complete ✅

<img width="544" height="139" alt="image" src="https://github.com/user-attachments/assets/67343acc-6d92-4284-b691-d7d046f29e3a" />

<img width="789" height="768" alt="image" src="https://github.com/user-attachments/assets/ddceca82-c45b-429f-9435-afc59a6a5f4c" />


### 📂 Day 15: Advanced Windows Auditing Policies & Process Tracking Activation
* **Task:** Configure host-system kernel logging enhancements to capture granular background application telemetry.
* **Engineering Review & Validation:**
  * Navigated the Advanced Audit Policy Configuration console (`secpol.msc`) to isolate host tracking vectors.
  * Activated explicit **Success** and **Failure** security auditing matrices under the **Detailed Tracking** sub-category.
  * Enabled system-wide tracking for **Audit Process Creation (Event ID 4688)** to ingest real-time background application execution chains.
  * Executed an administrative group policy force-refresh (`gpupdate /force`) to cleanly mount the updated security schemas into active workstation memory.
* **Status:** Advanced Windows Audit Baseline Complete ✅

<img width="911" height="636" alt="image" src="https://github.com/user-attachments/assets/4253645b-c578-44e8-8156-5ec6d27c0718" />

<img width="612" height="512" alt="image" src="https://github.com/user-attachments/assets/cdac9317-b33d-4ff6-8824-26d7c51edde6" />

### 📁 Day 16: Custom Wazuh Agent Telemetry Routing & XML Hooking
* **Task:** Modify host-level endpoint detection parameters to route advanced kernel event channels over the virtual switch infrastructure.
* **Engineering Review & Validation:**
  * Executed a workspace sandbox migration to bypass host-directory folder permission protections on `ossec.conf`.
  * Injected a targeted XML data collection block configured explicitly for the **Security** event channel.
  * Hardcoded an explicit query filter (`Event[System[EventID=4688]]`) to selectively harvest process creation event streams while minimizing telemetry noise.
  * Recycled the background **Wazuh Agent** system service daemon, verifying a clean initialization and stead runtime state.
 * **Status:** Telemetry Routing Complete & Active Channel Established ✅

<img width="948" height="655" alt="image" src="https://github.com/user-attachments/assets/3779a182-2138-4939-9175-746bc1829c70" />


### 📂 Day 17: Live Attack Simulation & SIEM Detection Validation
* **Task:** Execute tactical exploitation simulations from the Kali Linux testing suite and validate real-time ingestion pipelines.
* **Engineering Review & Forensic Analysis:**
  * Initialized the centralized security manager core and booted the **Kali Linux Attack Cockpit** onto the host network range.
  * Executed live network and application-layer discovery simulations targeting the local host environment boundaries.
  * Audited the **Wazuh Discover Cockpit** using targeted indexing queries (`data.win.system.eventID: "4688"`).
  * Validated complete telemetry ingestion loops, verifying that the SIEM successfully parsed kernel-level process creation event blocks generated during the attack loop.
 * **Status:** Attack Simulation & Pipeline Validation Successful ✅

<img width="1191" height="735" alt="image" src="https://github.com/user-attachments/assets/a146b1dd-6c72-4eb4-8b85-4647ff0c32c1" />

<img width="929" height="609" alt="image" src="https://github.com/user-attachments/assets/a30dd330-09e3-47a7-b65b-786ec65183f1" />


### 📁 Day 18: Custom SIEM Detection Rules & XML Correlation Logic
* **Task:** Engineer a custom correlation rule matrix inside the centralized SIEM manager to escalate raw event streams into high-severity security.
* **Engineering Design & Logic Controls:**
  * Opened the master rule configuration definitions panel (`local_rules.xml`) within the centralized SIEM manager environment.
  * Authored a custom correlation block (`rule id="10002"`) assigning a **High-Severity Tier (Level 12)** to flag critical workstation activities.
  * Built nested conditional filters utilizing regular expression (Regex) pattern matchers (`cmd.exe|powershell.exe`) targeted directly at incoming **Windows Event ID 4688** (Process Creation) logs.
  * Appended standardized industry tags mapped straight to the **MITRE ATT&CK Framework (T1059.001)** for native alignment with corporate threat matrices.
  * Executed a live manager service compilation cycle, validating structural integrity and establishing an active detection baseline.
 * **Status:** Custom SIEM Logic Complete & Active Detection Profile Established ✅

<img width="1145" height="630" alt="image" src="https://github.com/user-attachments/assets/d6e2fba6-411a-4ab0-bcc1-a520a7fd9249" />


### 📂 Day 19: Custom Rule Validation & High-Severity Threat Triggering
* **Task:** Validate custom SIEM rule logic constraints by executing a simulated local privilege escalation attack chain.
* **Engineering Review & Forensic Analysis:**
  * Initialized an administrative local shell execution loop (`cmd.exe`) on the workstation layer to trigger host process parameters.
  * Verified active endpoint log forwarding loops, harvesting over 30 distinct real-time hits matching custom classification parameters.
  * Audited the centralized SIEM telemetry panels using explicit filtering queries (`rule.id: "100002"`).
  * Validated that the correlation engine successfully intercepted the raw event data, automatically escalating the behavior into a **High-Security Level 12 Alarm Event**.
 * **Status:** Threat Detection Rule Validated & Operational ✅

<img width="1138" height="634" alt="image" src="https://github.com/user-attachments/assets/c9040f71-f412-42bf-86f0-e63bebb73fe6" />

<img width="1143" height="637" alt="image" src="https://github.com/user-attachments/assets/f2971de6-1b34-4661-a925-41b62ec40b93" />


### 📁 Day 20: Advanced Endpoint Instrumentation & Microsoft Sysmon Deployment
* **Task:** Deploy low-level kernel auditing engines on the host endpoint to eliminate advanced structural logging blind spots.
* **Engineering Review & Forensic Blueprint:**
  * Provisioned the official **Microsoft Sysmon (System Monitor)** low-level kernel driver framework directly onto the workstation architecture.
  * Authored a customized XML configuration template targeting high-fidelity data collection parameters across **Event ID 1** (Granular Process Creation with Hash Captures) and **Event 3** (Network Socket Connections).
  * Resolved nested XML tag validation constraints natively within the system root directory schemas.
  * Successfully initialized the `SysmonDrv` kernel filter layer and engaged the background system service daemon.
  * Reclaimed local hardware storage blocks by purging unneeded offline asset virtual disk drives.
 * **Status:** Advanced Instrumentation Complete & Structural Phase 2 Finalized ✅

<img width="1126" height="360" alt="image" src="https://github.com/user-attachments/assets/a26d9560-e689-4868-aae1-c983ecac0507" />


### 📂 Day 21: Forensic Telemetry Ingestion & Sysmon Pipeline Validation
* **Task:** Route advanced Windows kernel logging channels into the centralized SIEM array and validate parsed data schemas.
* **Engineering Review & Operational Troubleshooting:**
  * Audited the local agent daemon runtime logs (`ossec.log`) using native administrative shortcuts to diagnose endpoint mapping disconnects.
  * Corrected telemetry gaps by manually modifying the active agent configuration file (`ossec.conf`) via root system arrays.
  * Injected an independent event collection block mapping the operational channel: `Microsoft-Windows-Sysmon/Operational`.
  * Recycled the background data collector engine (`WazuhSvc`) and synchronized the centralized manager core.
  * Successfully verified data intake loops inside the SOC cockpit, parsing over 20 real-time high-fidelity forensic data records.
 * **Status:** Telemetry Routing Complete & Phase 3 Baseline Active ✅

<img width="1254" height="653" alt="image" src="https://github.com/user-attachments/assets/4b5ac539-a754-4956-92eb-4eecce0d66c4" />

<img width="977" height="531" alt="image" src="https://github.com/user-attachments/assets/84110cb7-b98c-496b-81cc-f1bbe05dd3ca" />


### 📁 Day 22: Advanced Sysmon Rule Engineering & Behavioral Correlation
* **Task:** Engineer a custom correlation ruleset inside the centralized SIEM manager to parse Sysmon streams and isolate post-exploitation tactics.
* **Engineering Design & Analytics Architecture:**
  * Opened the master rule configuration definitions panel (`local_rules.xml`) within the centralized SIEM manager workspace.
  * Authored an advanced behavioral correlation block (`rule id="100003"`) assigning a **High-Severity Tier (Level 12)** to isolate high-fidelity threat markers.
  * Configured structural logic filters (`if_sid>61600</if_sid>`) to hook natively into the incoming Microsoft Sysmon data highway.
  * Built nested regular expression (Regex) pattern matches (`whoami.exe|net.exe|ipconfig.exe`) targeted directly at the `win.eventdata.image` field to detect host footprinting loops.
  * Standardized data tracking parameters by explicitly mapping the profile straight to the **MITRE ATT&CK Matrix (T1082 - System Information Discovery)**.
  * Executed a live manager service compilation cycle, validating syntax and establishing an active behavioral detection baseline.
 * **Status:** Advanced Sysmon Threat Logic Active & Operational ✅

<img width="1247" height="652" alt="image" src="https://github.com/user-attachments/assets/81a5947d-f8ff-45fd-b31c-4d22fc5ac453" />


### 📂 Day 23: Live Behavior Validation & Threat Detection Correlation Pipeline
* **Task:** Validate custom security correlation rulesets natively inside the centralized SIEM dashboard using live post-exploitation footprinting attack simulations.
* **Engineering Review & Forensic Triage:**
  * Executed live endpoint reconnaissance commands (`whoami`, `ipconfig`, `net user`) inside an administrative shell on the target workstation.
  * Conducted deep visual field auditing on un-correlated background logs to identify variations in the native Windows Event Channel decoder schema.
  * Corrected correlation boundaries by mapping filters directly to the verified `win.eventdata.newProcessName` field layout.
  * Recompiled the core custom rule file (`local_rules.xml`) and successfully synchronized the centralized engine manager.
  * Validated live data capture loops, escalating raw security events into active, high-visibility Level-12 behavioral alert.
* **Status:** Threat Detection Pipeline Validated & Phase 3 Core Operational ✅

<img width="1308" height="672" alt="image" src="https://github.com/user-attachments/assets/c72447fa-5b9d-4c52-bc42-6e39e87dd2f6" />

