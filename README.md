<h1 align="center">🛡️🔐 networkwalks-B082-week1-Cybersecurity Lab Setup</h1>

<p align="center">
  <b>Building a Kali  Linux penetration  Testing Lab </b>
</p>
 
--------------------------------------------
📖 Project Overview
--------------------------------------------
This project documents the design, deployment, and testing of a self-contained cybersecurity lab environment built for hands-on penetration testing practice. 

The lab was constructed using virtualization software to safely simulate a small network consisting of an attacker machine and one or more intentionally vulnerable target machines.


--------------------------------------------
🎯 Objectives
--------------------------------------------
-  The main objectives of this project are to:

    - Install and configure VirtualBox.
      
	- Install/import Kali Linux as a virtual machine.

    - Create a private NAT Network for the cybersecurity lab.

    - Configure network connectivity for Kali Linux.

    - Assign a consistent IP address to the Kali VM.

    - Verify network connectivity and DNS resolution.
	
   - Take a clean VM snapshot for recovery.
	
    - Document the complete setup process.
	
    - Prepare the environment for future cybersecurity projects.


--------------------------------------------
🏗️ Lab Architecture
--------------------------------------------
<img width="1346" height="616" alt="1-screenshot-title-image" src="https://github.com/user-attachments/assets/78fd8cd3-6c5f-4151-a2de-a646dbc36152" />

--------------------------------------------
⚙️ Lab Configuration
--------------------------------------------
| 🧩 Component | ⚙️ Configuration |
|:---|:---|
| 💻 **Host OS** | Windows 10 |
| 🧠 **Host RAM** | 8 GB |
| ⚡ **Processor** | Intel Core i7 |
| 🖥️ **Hypervisor** | VirtualBox 7.2 |
| 🐉 **Security OS** | Kali Linux 2026.2 |
| 🧠 **Kali RAM** | 2048 MB |
| 🌐 **Virtual Network** | NAT Network |
| 📡 **Network Address** | `10.0.0.0/24` |
| 🐧 **Kali IP Address** | `10.0.0.2/24` |
| 🔶 **Default Gateway** | `10.0.0.1` |
| 🌐 **DNS Server** | `8.8.8.8` |
| 🔮 **Future VM Range** | `10.0.0.3 – 10.0.0.99` |

--------------------------------------------
🪜 Lab Setup Procedure
--------------------------------------------
Step 1. Install 7-Zip
--------------------------------------------
7-Zip was installed to extract the Kali Linux virtual-machine package, which may be distributed as a `.7z` archive.

Tool: 7-Zip

--------------------------------------------
Step 2. Install VirtualBox
--------------------------------------------

VirtualBox was installed as the hypervisor.

--------------------------------------------
Step 3. Create the NAT Network
--------------------------------------------
A dedicated NAT Network was created in VirtualBox.

Configuration: Network Name: NatNetwork IPv4 Prefix: 10.0.0.0/24 DHCP: Enabled IPv6: Disabled

<img width="1911" height="1012" alt="NAT Set" src="https://github.com/user-attachments/assets/ec99c6ea-870e-4d4b-afb0-46948efe70e9" />
A NAT Network was selected because multiple virtual machines connected to the same NAT Network can communicate with one another while also having outbound network connectivity.

--------------------------------------------
Step 4. Import Kali Linux
--------------------------------------------
The Kali Linux virtual machine was downloaded from the official Kali Linux website and imported into VirtualBox.

The VM network adapter was configured as follows:

    Adapter 1
    Attached to: NAT Network
    Network:     NatNetwork
    Adapter Type: Intel PRO/1000 MT Desktop
    
The VM was allocated:

    RAM: 2048 MB

<img width="1277" height="796" alt="Kali Home" src="https://github.com/user-attachments/assets/e5677f1e-c39c-4101-aa18-b8aae182f64c" />

--------------------------------------------
Step 5. Configure the Kali Linux Network
--------------------------------------------
The Kali Linux network configuration was checked and configured with a consistent IPv4 address.

Example configuration:

    IP Address: 10.0.0.2
    Subnet Mask: 255.255.255.0
    Gateway: 10.0.0.1
    DNS: 8.8.8.8

A consistent IP address makes it easier to document the lab and reference the Kali machine in future exercises.

<img width="1272" height="791" alt="Wired c1" src="https://github.com/user-attachments/assets/bd2f75d5-e595-4447-8406-0d070768fa79" />

--------------------------------------------

Step 6. Create a Clean VM Snapshot
--------------------------------------------

After completing the initial configuration, a VirtualBox snapshot was created.


Example snapshot name:

    My Fresh Kali Linux 

<img width="1905" height="1020" alt="Snapshot" src="https://github.com/user-attachments/assets/879bba42-ceab-4a73-98b1-6f31bdb35554" />

The snapshot represents the clean baseline of the laboratory.

If a future exercise changes or damages the VM configuration, the machine can be restored to this baseline.

--------------------------------------------

🔎 Lab Verification
--------------------------------------------
| ✅ Test | 📱 Command | 🎯 Expected Result |
|---|---|---|
| 🌐 Check IP address | `ip a` | Correct Kali IP displayed |
| 🔌 Test gateway | `ping 10.0.0.1` | Successful replies |
| 🌍 Test Internet connectivity | `ping 8.8.8.8` | Successful replies |
| 🔎 Test DNS resolution | `nslookup networkwalks.com` | Domain resolves |
| 🧰 Verify Nmap | `nmap --version` | Nmap version displayed |
| 🔄 Verify snapshot | Restore snapshot and run `ip a` | Baseline configuration restored |

Example Results

    IP Address:
    10.0.0.2/24
    
    Gateway:
    10.0.0.1
    
    DNS:
    8.8.8.8

--------------------------------------------
🐞 Problems Encountered & Solutions
--------------------------------------------
Documenting problems is an important part of the project.

Problem 1. Internet Connectivity After Static IP Configuration
--------------------------------------------
After manually configuring the IPv4 settings, Internet connectivity may fail depending on the Kali/NetworkManager configuration.

One workaround used during this lab was:

    sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
The network connection was then restarted/rebooted and connectivity was tested again.


> **Important:** Network interface and connection names may vary.
> Check the actual connection name before running an `nmcli` command.

--------------------------------------------
Problem 2. VirtualBox VT-x / Virtualization Error
--------------------------------------------
The VM initially failed to start because hardware virtualization was disabled in the system firmware/BIOS.

The issue was resolved by:

1.	Restarting the computer.
2.	Entering BIOS/UEFI settings.
3.	Enabling Intel VT-x / hardware virtualization.
4.	Saving the configuration.
5.	Restarting the computer.
6.	Starting the Kali VM again.
	
  After enabling virtualization, the VM started successfully.

--------------------------------------------
💡 What I Learned
--------------------------------------------
Through this project, I learned how to create and configure a virtual environment for cybersecurity practice.

The most important concepts I learned include:

1. NAT vs NAT Network
A standard NAT configuration and a NAT Network serve different purposes.

A NAT Network allows multiple VMs connected to the same virtual network to communicate with one another while providing network address translation for external connectivity.

This makes it useful for building a multi-machine cybersecurity laboratory.

2. Virtual Machine Networking
I learned how VirtualBox virtual network adapters connect virtual machines to different types of networks and how network configuration affects communication between machines.

3. Static IP Configuration
I learned how to configure and verify IPv4 addressing, subnet masks, gateways, and DNS settings in Kali Linux.

4. VM Snapshots
I learned that a clean snapshot should be created before performing risky or experimental activities.

This provides a known-good recovery point for future cybersecurity exercises.

5. Documentation
I learned that documenting commands, configuration, screenshots, problems, and solutions is an important part of a professional cybersecurity project.

--------------------------------------------
🔐 Security & Ethical Use
--------------------------------------------
This laboratory is intended strictly for education purposes only.


--------------------------------------------
🔗 Tools & Resources
--------------------------------------------
- 7-Zip
- VirtualBox
- Kali Linux

--------------------------------------------
👤 Author
--------------------------------------------
###  Vijay Solanki
**Cybersecurity Intern B082**  


LinkedIn: https://www.linkedin.com/in/solanki-vijay/

--------------------------------------------
🛠️ Tools Explored
--------------------------------------------

As part of the cybersecurity lab setup, I visited and explored the official websites and documentation of different tools used for cybersecurity learning.

- 🕷️ **Burp Suite** – Explored web application security testing, HTTP/HTTPS traffic interception, and request analysis.
  
  <img width="1272" height="787" alt="Burp" src="https://github.com/user-attachments/assets/03434ff1-3020-4f1d-9fe0-ca9673388dbb" />
--------------------------------------------
- 🦈 **Wireshark** – Explored network packet capture and analysis.
  
  <img width="1272" height="796" alt="Wire" src="https://github.com/user-attachments/assets/9b867de0-ce22-4248-bb0e-cb0a52053f55" />


  --------------------------------------------
  
📌 Project Information
--------------------------------------------
| Program Name | Cybersecurity at Networkwalks |
|---|---|
| Week | 01 |
| Project | Cybersecurity & Pentesting Lab Setup |
| Repository | GitHub |


