# SIEM & Threat Detection Lab: Wazuh Deployment

## Objective
The goal of this project was to build a functional Security Operations Center (SOC) home lab to gain hands-on experience with deploying a SIEM, configuring endpoint agents, and creating real-time security alerts. This lab allowed me to move beyond basic endpoint administration and dive into centralized log aggregation and investigative threat hunting.

## Environment & Technologies
* **Hypervisor:** Oracle VirtualBox
* **SIEM / EDR:** Wazuh 
* **Servers:** Ubuntu Linux, Windows Server 
* **Endpoints:** Windows 10 Client
* **Networking:** pfSense Firewall 

## Step 1: Deploying the SIEM Command Center
I spun up a headless Ubuntu Server VM and installed the Wazuh Manager. This required managing Linux system resources carefully to ensure the Wazuh Indexer (database) had enough memory and storage to handle log ingestion without crashing.

## Step 2: Connecting the Endpoints
To monitor my environment, I needed to deploy the Wazuh Agent to a domain-joined Windows 10 virtual machine. 

<img width="1019" height="638" alt="Screenshot 2026-05-07 050615" src="https://github.com/user-attachments/assets/fa11ade7-036c-428c-9372-2e174ee86f3a" />

*Wazuh dashboard confirming the Windows 10 endpoint is actively communicating with the SIEM manager.*

## Step 3: File Integrity Monitoring (FIM)
With the SIEM ingesting standard Windows event logs, I configured a custom rule to actively monitor a specific folder for any unauthorized changes. 

I modified the Wazuh agent's `ossec.conf` XML file to track the directory in real-time. To test the trap, I simulated an attack by modifying existing files and dropping new files into the directory.

<img width="1020" height="641" alt="Screenshot 2026-05-07 050220" src="https://github.com/user-attachments/assets/34489771-f913-4bc6-89f5-6ea059274cc0" />

*FIM module dashboard displaying real-time alerts for added and modified files within the monitored directory.*


<img width="1019" height="637" alt="event-fmi" src="https://github.com/user-attachments/assets/d83c6c44-afd2-4790-92f2-2ab795a726d2" />

*Detailed event logs showing the specific files altered and the exact timestamps of the unauthorized modifications.*

## What I Learned
Building this lab from scratch was an incredible exercise in system administration and security engineering. I gained practical experience in:
* Troubleshooting Linux storage constraints and repairing corrupted package managers (`dpkg`).
* Understanding how Active Directory DNS routing interacts with internal virtual networks and client machines.
* Writing XML configurations to create targeted security alerts.
* Reading and analyzing SIEM dashboards to track simulated threat activity.
