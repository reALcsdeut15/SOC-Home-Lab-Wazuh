# Security Audit Assessment & Compliance Review: Botium Toys

### Project Overview
This project represents a completed **IT Security Audit Assessment** conducted as part of my cybersecurity certification training and preparation for the CompTIA Security+ certification.
**Scenario Context (Provided):** Background information on Botium Toys' assests, IT scope, and business goals.
**Completed Audit Work (My Contribution:** Evaluation and completion of the Controls Assessment Checklist, Regulatory Compliance Checklist, and Auditor Recommendations. 
---
## 1. Scenario Context & Background (Provided Data)

### Scope & Primary Goals
* **Scope:** Internal IT audit assessment covering user permissions, existing controls/procedures, and hardware/software assets in use.
* **Goals:** Align operations with the NIST Cybersecurity Framework, improve regulatory compliance, and strengthen system controls.
* **Scenario Risk Score:** **8 / 10** (High Risk) due to missing foundational technical controls and unaddressed regulatory standards.

### Assests Evaluated in Scenario
* **Employee Equipment:** End-user devices (desktops/laptops, smartphones), remote workstations, surveillance cameras, and peripherals
* **Internal Network:** Protected storage containing customer, vendor, and internal organizational data.
---
## 2. Controls Assessment Checklis (Completed Audit Work)

Below is the controls assessment I completed, evaluating Botium Toys' existing setup against administrative, technical, and physical security control standards.

|Control Name | Category | Type | Control Purpose | In Place? |
|:--- | :--- | :--- | :--- | :---: |
|**Least Privilege** | Administrative | Preventative | Reduce risk and overall impact of malicious insider or compromised accounts | **No** |
|**Disaster Recovery Plans** | Administrative | Corrective | Provide business continuity during major incidents | **No** |
|**Password Policies** | Administrative | Preventative | Reduce likelihood of account compromise through brute-force attacks | **No** | 
|**Separation of Duties** | Administrative | Prevantative | Reduce risk of single points of failure and internal fraud | **No** | 
|**Firewall** | Technical | Prevantative | Filter unwated or malicious traffic from entering the network | **Yes** | 
|**Intrusion Detection System (IDS)** | Technical | Detective | Detect and prevent anomalous traffic matching attack signatures | **No** | 
|**Backups** | Technical | Corrective | Restore/recover systems and data following an incident | **No** | 
|**Antivirus (AV) Software** | Technical | Corrective | Detect and quarantine known threats | **Yes** | 
|**Manual Monitoring / Legacy Systems** | Technical | Preventative | Identify and manage threats/vulnerabilities on legacy systems | **No** | 
|**Encryption** | Technical | Deterrent | Provide confidentiality for sensitive stored/transmitted data | **No** | 
|**Password Management Systems** | Technical | Preventative | Reduce password fatigue and unsafe password practices | **No** | 
|**Locks (Offices, Storefront, Warehouse)** | Physical | Preventative | Prevent unauthorized physical access to physical assets | **Yes** | 
|**CCTV Surveillance** | Physical | Detective | Monitor physical perimeters and assist post-incident investigations | **Yes** | 
|**Fire Detection & Prevention** | Physical | Preventative | Detect fires and protect physical hardware and inventory | **Yes** | 
---

## 3. Regulatory Compliance Checklist (Completed Audit Work)

Below is the compliance assessment I completed, determining whether Botium Toys currently adheres to the key regulatory frameworks.

###Payment Card Industry Data Security Standard (PCI DSS)
* [ ] **Authorized Access Only:** Only authorized users have access to customers' credit card information.
* [ ] **Secure Storage & Processing:** Credit car information is stored, accepted, processed, and transmitted in a secure environment.
* [ ] **Data Encryption:** Data encryption procedures are implemented across credit card touchpoints.
* [ ] **Password Policies:** Secure password management policies are adopted.

### General Data Protection Regulation (GDPR)
* [ ] **E.U. Data Privacy:** E.U. customers' data is kept private/secured.
* [x] **72-Hour Breach Notificaton:** A plan is in place to notify E.U. customers within 72 hours of a data breach.
* [ ] **Data Inventory & Classification:** Data is properly classified and inventoried.
* [ ] **Privacy Policies:** Privacy policies, procedures, and processes are enforced and documented.

### System and Organization Controls (SOC 1 / SOC 2)
* [ ] **User Access Policies:** User access policies are formally established.
* [ ] **Confidentiality:** Sensitive data (PII/SPII) is confidential/private.
* [ ] **Data Integrity:** Data integrity measures ensure data is consistent, complete, and validated.
* [x] **Data Availability:** Data is available to authorized individuals when needed.
---

## 4. Summary & Auditor Recommendations (Completed Audit Work)

Based on the completed controls and compliance assessment, the following recommendations were formulated to reduce risk exposureand improve Botium Toys' security posture. 
