# SOC-Home-Lab-Wazuh
### 🚀 Project Status: Building Virtual Network Infrastructure on HP Host
## 🎯 Project Objective
The purpose of this deployment is to engineer a functional **Security Operations Center (SOC) environment** using open-source tools. This environment validates defensive endpoint monitoring controls by simulating cyber attacks and establishing centralized logging and analysis. 

▶ **View the complete engineering milestones here:** [Download Full 30-60-90 Day Timeline PDF](soc_homelab_30_60_90_timeline.pdf)
### ▶ 📂 Additional Completed Portfolio Assignments **[CompTIA Security+ Audit & Compliance Assessment](https://github.com/realCsdeut15/SOC-Home-Lab-Wazuh/tree/Conduct-A-Security-Audit)** — Complete controls assessment checklist, regulatory compliance evaluation (PCI DSS/GDPR), and remediation report[cite: 4, 5].


## 🛠️ Tooling Stack
* **Virtualization Engine:** Oracle VirtualBox
* **SIEM Engine:** Wazuh OVA Appliance v4.14.7
* **Threat Generator:** Kali Linux (x86 architecture)

---

## 📈Milestone Logs
### 🏗️Day 1: Provisioning the Security Brain
* **Task:** Import and configure the central Wazuh SIEM engine
* **Status:** Complete ✅
* **Telemetry Verification:**
<img width="1009" height="579" alt="image" src="https://github.com/user-attachments/assets/73259352-121e-4c2d-bfe4-f90c330b8276" />

### 🪤Day 2: Setting the Log Trap
* **Task:** Deploy the attacker node and establish virtual network routing connectivity.
* **Status:** Complete ✅
* **Telemetry Verification:**
<img width="1067" height="753" alt="image" src="https://github.com/user-attachments/assets/b0a6c156-d4e8-44a9-a7e0-79973fef08fe" />

### 🪤Day 3: Simulating the Attack Vector 
* **Task:** Execute a brute-force attack from Kali Linux and verify SIEM alert generation thresholds.
* **Status:** Complete ✅
* **Telemetry Verification
<img width="1048" height="532" alt="image" src="https://github.com/user-attachments/assets/ffcb3c7f-dadf-4177-8558-d92927e435fc" />

### 🖥️Day 4: Provisioning the Target Client Asset
* **Task:** Deploy an independent Ubuntu Server endpoint node and hardcode permanent network routing layouts.
* **Status:** Complete ✅
* **Telemetry Verification:**
<img width="1360" height="766" alt="image" src="https://github.com/user-attachments/assets/59b9942c-bd43-4159-b781-51b1d15dff37" />

### 👀Day 5: Injecting the Monitoring Daemon
* **Task:** Establish an offline shared-folder bridge to manually deploy and configure Wazuh endpoint agent daemon on the target node.
* **Status:** Complete ✅
* **Telemetry Verification:**
<img width="1359" height="676" alt="image" src="https://github.com/user-attachments/assets/ac7cf235-cd89-45bb-b15f-c9b1c6b9936e" />
<img width="1355" height="606" alt="image" src="https://github.com/user-attachments/assets/5851b76a-5a35-4643-8935-d5cdd3c3f802" />

### ⚔️Day 6: Threat Simulation & SIEM Alert Generation
* **Task:** Execute an automated SSH brute-force attack from the Kali Attacker node using Hydra, and analyze the ingested high-severity alerts on the Wazuh Dashboard.
* **Status:** Complete ✅
* **SIEM Telemetry Verification:**
<img width="676" height="634" alt="image" src="https://github.com/user-attachments/assets/4920f428-d563-47c1-bfcf-4eb9f9f3504c" />
<img width="1354" height="671" alt="image" src="https://github.com/user-attachments/assets/3c27e5c6-28f6-4f99-9fcf-ea8b647f6d9a" />




