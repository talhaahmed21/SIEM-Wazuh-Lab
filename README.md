# SIEM & Threat Detection Lab: Wazuh Deployment

## 🎯 Objective
The goal of this project was to build a functional Security Operations Center (SOC) home lab to gain hands-on experience with deploying a SIEM, configuring endpoint agents, and creating real-time security alerts. This lab allowed me to move beyond basic endpoint administration and dive into centralized log aggregation and investigative threat hunting.

## 💻 Environment & Technologies
* **Hypervisor:** Oracle VirtualBox
* **SIEM / EDR:** Wazuh (Open-Source)
* **Servers:** Ubuntu Linux (Wazuh Manager), Windows Server (Active Directory Domain Controller)
* **Endpoints:** Windows 10 Client
* **Networking:** pfSense Firewall (Internal Network routing)

## 🛠️ Step 1: Deploying the SIEM Command Center
I spun up a headless Ubuntu Server VM and installed the Wazuh Manager. This required managing Linux system resources carefully to ensure the Wazuh Indexer (database) had enough memory and storage to handle log ingestion without crashing.

[INSERT SCREENSHOT HERE: A picture of your Ubuntu terminal showing the successful Wazuh installation, or the initial Wazuh dashboard login screen]

## 🔗 Step 2: Connecting the Endpoints
To monitor my environment, I needed to deploy the Wazuh Agent to a domain-joined Windows 10 virtual machine. 

* **The Challenge:** Because the Windows 10 machine was behind a pfSense firewall on an internal network and bound to Active Directory, it could not resolve external DNS to download the agent.
* **The Solution:** Instead of breaking the Active Directory trust by manually changing the client's DNS, I configured DNS Forwarders on the Windows Server (Domain Controller) to securely route internet requests. Once connectivity was established, I deployed the agent via PowerShell.

[INSERT SCREENSHOT HERE: A picture of your Wazuh Dashboard showing the "Win10-Endpoint" with a green "Active" status]

## 🚨 Step 3: File Integrity Monitoring (FIM)
With the SIEM ingesting standard Windows event logs, I configured a custom rule to actively monitor a highly sensitive folder (`C:\TopSecret`) for any unauthorized changes. 

I modified the Wazuh agent's `ossec.conf` XML file to track the directory in real-time. To test the trap, I simulated an attack by modifying existing files and dropping new files into the directory.

[INSERT SCREENSHOT HERE: A picture of the Wazuh FIM Dashboard showing the donut charts of added/modified files]

[INSERT SCREENSHOT HERE: A picture of the specific FIM Events log showing the exact file you changed (e.g., passwords.txt) and the timestamp]

## 🧠 What I Learned
Building this lab from scratch was an incredible exercise in system administration and security engineering. I gained practical experience in:
* Troubleshooting Linux storage and repairing corrupted package managers (`dpkg`).
* Understanding how Active Directory DNS routing interacts with internal virtual networks.
* Writing XML configurations to create targeted security alerts.
* Reading and analyzing SIEM dashboards to track simulated threat activity.
