# SOC Home Lab Concepts

These are questions from each module of my lab, answered in my own words.
I use this file to practice for interviews and to explain what I learned.

[Back to README](README.md)

---

## Phase 1: Lab Setup, Agents, and First Detections

### Module 1: Deploying the Wazuh Server
**Q: What is a SIEM, and what problem does it solve?**

My answer: A SIEM stands for Security Information and Event Management. It collects logs from many computers and puts them in one place. It checks those logs against rules and raises an alert when something looks suspicious. Without a SIEM, an analyst would have to check each computer's logs one at a time, and attacks could be missed or have a delayed response. In my lab, Wazuh is my SIEM. It collects logs from my Ubuntu VM and my Windows laptop, and it raised level 10 alerts when I ran a brute-force attack from Kali.

**Q: What are the three main parts of Wazuh, and what does each one do?**

My answer: The three main parts are the server, the indexer, and the dashboard. The server receives logs from the agents, checks them against rules, and creates alerts. The indexer stores the alerts so they can be searched quickly. The dashboard is the web page where I search, filter, and review alerts. Agents are a fourth piece. They are installed on each computer being monitored and send logs to the server. In my lab, all three main parts run on one VM from the Wazuh OVA.

### Module 2: Deploying the Attacker VM
**Q: Why did I put the attacker VM on a host-only network instead of a bridged network?**

My answer: I put the attacker VM on a host-only network instead of a bridged network to keep the attacks off my real home network. With bridged networking, Kali would join my home Wi-Fi like any other device, so a scan or brute force could hit my phone, TV, or sister's laptop. Scanning devices that I don't own or have permission to test can also be illegal. In my lab, Wazuh, Ubuntu, and Kali share the host-only network and its address range `192.168.56.0/24`.

**Q: What is the difference between host-only, NAT, and bridged networking?**

My answer: A host-only network is a private network that can only be reached by the host and other VMs on the same network. It has no internet access. With NAT, the VM shares the host's address. It can reach out to the internet through the host, but other devices can't reach it directly unless port forwarding is set up. With bridged networking, the VM joins the home network like any other device and gets its own IP address from the router. Every device on the home network can reach it. In my lab, my Ubuntu VM was on the host-only network with no internet, so I used a VirtualBox shared folder to move the Wazuh agent onto it.

### Module 3: First Brute-Force Test
**Q: What is a brute-force attack, and what evidence does it leave in the logs?**

My answer:

**Q: Why does a SIEM alert on many failed logins instead of just one?**

My answer:

### Module 4: Deploying the Ubuntu Target VM
**Q: Why does a server need a static IP address?**

My answer:

**Q: What could go wrong in monitoring if a host's IP address changed?**

My answer:

### Module 5: Installing the Wazuh Agent on Ubuntu
**Q: What does a Wazuh agent do?**

My answer:

**Q: How does the agent prove to the manager that it is allowed to send logs?**

My answer:

### Module 6: SSH Brute-Force with Hydra
**Q: Where does Linux record SSH login attempts?**

My answer:

**Q: What are three ways to protect a server from SSH brute-force attacks?**

My answer:

### Module 7: Custom Rule for Successful Login After Brute Force
**Q: Why is a successful login after many failures more serious than the failures alone?**

My answer:

**Q: What is a correlation rule?**

My answer:

**Q: What is MITRE ATT&CK, and why map alerts to it?**

My answer:

### Module 8: Wazuh Agent on a Windows Host
**Q: How is collecting logs from Windows different from collecting logs from Linux?**

My answer:

### Module 9: Network Scan and Brute-Force Detection
**Q: What does an Nmap scan tell an attacker?**

My answer:

**Q: What is the difference between red team and blue team work?**

My answer:

### Module 10: Log Review and Agent Visibility Check
**Q: What is the difference between an event and an alert?**

My answer:

**Q: How do you confirm an agent is healthy and sending logs?**

My answer:

---

## Phase 2: File Integrity Monitoring, Hardening, and Windows Logging

### Module 11: File Integrity Monitoring (FIM)
**Q: What is file integrity monitoring, and why does it matter?**

My answer:

**Q: What is the difference between real-time monitoring and scheduled scans?**

My answer:

**Q: What does `report_changes` add, and what is a risk of turning it on?**

My answer:

### Module 12: Reviewing FIM File Size Limits
**Q: Why would a SIEM limit the size of files it tracks changes on?**

My answer:

### Module 13: File Tampering Test
**Q: What is an insider threat?**

My answer:

**Q: How does a file diff help during an investigation?**

My answer:

### Module 14: Firewall Setup with UFW
**Q: What does "default deny" mean, and why is it a best practice?**

My answer:

**Q: What is the difference between a host firewall and a network firewall?**

My answer:

**Q: What is the principle of least privilege, and how did I apply it here?**

My answer:

### Module 15: Windows Process Creation Auditing
**Q: What is Event ID 4688?**

My answer:

**Q: Why isn't process creation auditing turned on by default?**

My answer:

### Module 16: Sending Event ID 4688 to Wazuh
**Q: Why filter logs at the agent instead of sending everything to the SIEM?**

My answer:

**Q: What is the risk of filtering out too much?**

My answer:

### Module 17: Confirming 4688 Events in Wazuh
**Q: How do you check that a log pipeline works from start to finish?**

My answer:

### Module 18: Custom Rule for cmd.exe and PowerShell
**Q: Why do security teams watch Command Prompt and PowerShell closely?**

My answer:

**Q: How do you decide what severity level to give a rule?**

My answer:

### Module 19: Testing the Shell Detection Rule
**Q: What is a false positive?**

My answer:

**Q: What is alert fatigue, and how can a noisy rule cause it?**

My answer:

### Module 20: Installing Sysmon
**Q: What does Sysmon add that built-in Windows logging does not?**

My answer:

**Q: Why are file hashes useful in an investigation?**

My answer:

---

## Phase 3: Sysmon and Detection Engineering

### Module 21: Sending Sysmon Logs to Wazuh
**Q: Walk me through how you troubleshot missing logs.**

My answer:

### Module 22: Custom Rule for Discovery Commands
**Q: What are discovery commands, and why do attackers run them after getting access?**

My answer:

**Q: What does `if_sid` do in a Wazuh rule?**

My answer:

### Module 23: Testing and Fixing the Discovery Rule
**Q: Why must a rule's field name match the log data exactly?**

My answer:

### Module 24: Tracing a Detection Gap
**Q: What is a parent process, and why does it matter in an investigation?**

My answer:

**Q: How did the order of my rules cause a detection gap?**

My answer:

**Q: Tell me about a time you troubleshot a problem. What did you find, and how did you fix it?**

My answer:
