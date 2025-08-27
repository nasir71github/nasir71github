# 🖥️ Cybersecurity Home Lab  

## 🎯 Title & Objective  
**VirtualBox-Based Cybersecurity Lab Setup**  
The objective of this project was to design and configure a personal cybersecurity home lab in a safe, isolated environment. The lab demonstrates how to set up multiple virtual machines with proper network segmentation and **static IP addressing**, providing a stable foundation for security research and training.  

---

## 🛠️ Tools + Technologies  

- **Virtualization Platform**: Oracle VirtualBox  
- **Virtual Machines**:  
  - Kali Linux (security tools)  
  - Metasploitable 2 (vulnerable Linux server)  
  - bWAPP (buggy web application running on a LAMP stack)  
  - Windows 10 (standard workstation simulation)  
- **Networking**: VirtualBox **Host-Only Adapter** with manually assigned **static IP addresses**  

---

## 🔎 High-Level Methodology  

| Step | Description | Notes |  
|------|-------------|-------|  
| **1. Virtualization Setup** | Installed and configured VirtualBox on the host machine. Created a **Host-Only Network** to ensure traffic is isolated from the internet while allowing inter-VM communication. | VirtualBox networking knowledge applied |  
| **2. VM Deployment** | Installed Kali Linux, Metasploitable 2, bWAPP, and Windows 10 as guest virtual machines. Configured system resources (CPU, RAM, storage) based on host capacity. | Adjusted resources based on host performance |  
| **3. Static IP Configuration** | Disabled DHCP for the host-only adapter. Assigned **static IP addresses** to each VM within the subnet `192.168.56.0/24`. Verified communication across all systems using `ping`, `ipconfig`, and `ifconfig`. | Ensured consistency and avoided IP conflicts |  

---

## 📊 Network & IP Configuration  

| Virtual Machine  | Role / Purpose              | Static IP Address | Network Mode       | Notes |  
|------------------|-----------------------------|------------------|--------------------|-------|  
| Kali Linux       | Attacker / Security Tools   | `192.168.56.101` (Host-Only) <br> `10.0.3.15` (NAT) | Host-Only + NAT    | <img src="../../assets/images/Kali IP.png" alt="IP address snippet" height="100" /> |  
| Metasploitable 2 | Vulnerable Linux Target     | `192.168.56.102` | Host-Only          | <img src="../../assets/images/metasploit IP.jpg" alt="IP address snippet" height="100" /> |  
| bWAPP            | Vulnerable Web Application  | `192.168.56.103` | Host-Only          | <img src="../../assets/images/bwapp IP.jpg" alt="IP address snippet" height="100" /> |  
| Windows 10       | User Workstation Simulation | `192.168.56.104` | Host-Only          | <img src="../../assets/images/windows IP.png" alt="IP address snippet" height="100" /> |  


**Verification Steps**:  
- Configured static IPs manually on each VM.  
- Confirmed all machines are on the same subnet (`192.168.56.0/24`).  
- Tested connectivity between machines using `ping`.  

---
# 🧠 Learning & Reflection  

- **Learning Journey**:  
  - Configuring static IPs gave me more control and stability compared to dynamic allocation. Each machine retained its address across reboots, which made management easier.  
  - Setting up a dual-adapter environment (Host-Only + NAT) allowed me to keep lab traffic isolated while still giving Kali internet access for updates and tools like BurpSuite.  

- **Challenges Faced**:  
  - Initially setting correct subnet masks and gateways for consistency.  
  - Conflict between DHCP/NetworkManager and static IP configuration (had to restart the Kali machine for changes to reflect).  
  - Misconfigured routing: Host-Only adapter added a default gateway, which caused internet traffic issues until I removed it and let only NAT handle the gateway.  

- **Key Takeaway**:  
  - Static IP assignment is more reliable for multi-VM labs since it simplifies repeatability, documentation, and troubleshooting.  
  - Always ensure **only one default gateway (via NAT)** for internet, while Host-Only remains strictly for internal lab traffic.  

---
You can find all the images for this project here
 
---
This documentation highlights my ability to design and configure a multi-VM lab environment with **static IP networking**, an essential foundation for more advanced cybersecurity practice.  

---
