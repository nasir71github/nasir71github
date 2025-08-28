# 🖥️ Cybersecurity Home Lab  

## 🎯 Title & Objective  
**VirtualBox-Based Cybersecurity Lab Setup**  
The objective of this project was to design and configure a personal cybersecurity home lab in a safe, isolated environment. The lab demonstrates how to set up multiple virtual machines with proper network segmentation, **static IP addressing**, and a dual-network setup where Kali Linux has both **Host-Only** (for lab traffic) and **NAT** (for internet access). This provides a stable foundation for security research and training.  


---

## 🛠️ Tools + Technologies  

- **Virtualization Platform**: Oracle VirtualBox  
- **Virtual Machines**:  
  - Kali Linux (security tools)  
  - Metasploitable 2 (vulnerable Linux server)  
  - bWAPP (buggy web application)  
  - Windows 10 (standard workstation simulation)  
  - **Networking**: VirtualBox **Host-Only Adapter** with manually assigned **static IP addresses** for all VMs.  
     - Kali Linux additionally uses a **NAT adapter** (`10.0.3.15`) to provide safe internet access for tools like BurpSuite, while other machines remain isolated on the Host-Only network.  

---

## 🔎 High-Level Methodology  

| Step | Description | Notes | Example Commands / Configurations |  
|------|-------------|-------|-----------------------------------|  
| **1. Virtualization Environment Setup** | Installed and configured Oracle VirtualBox on the host system. Established a dedicated **Host-Only Network** to ensure isolated communication between virtual machines without exposing them to the internet. | Applied virtualization and networking configuration knowledge | *VirtualBox Manager → File → Host Network Manager → Create Host-Only Network* |  
| **2. Virtual Machine Provisioning** | Deployed Kali Linux, Metasploitable 2, bWAPP, and Windows 10 as guest virtual machines. Allocated system resources (CPU, memory, and storage) proportionate to host machine capacity. | Resource allocation was adjusted to balance performance and stability | *VM Settings → System → Base Memory / Processors* |  
| **3. Internal Network Configuration** | Disabled DHCP in VirtualBox Host Network Manager and manually assigned **static IP addresses** to each VM within the `192.168.56.0/24` subnet. | Prevented IP conflicts and ensured predictable addressing | **Linux (Kali):**  ```sudo nano /etc/network/interfaces``` <br> ```iface eth0 inet static``` <br> ```address 192.168.56.101``` <br> ```netmask 255.255.255.0``` <br> ```gateway 192.168.56.1``` |  
| **4. External Network Connectivity** | Configured a secondary **NAT adapter** for Kali Linux to provide internet access for tools such as Burp Suite, while maintaining internal isolation for other VMs. | Dual-adapter setup preserved lab security and internet availability | ```ip route``` <br> Example output: <br> ```default via 10.0.3.2 dev eth1 proto dhcp src 10.0.3.15 metric 100``` |  
| **5. Verification & Testing** | Validated connectivity across systems using `ping`, `ifconfig`, and `ipconfig`. Confirmed both intra-VM communication and Kali’s internet accessibility. | Ensured operational stability and correct configuration | ```ping 192.168.56.102``` <br> ```ping google.com``` |  


---

## 📊 Network & IP Configuration  

| Virtual Machine  | Role / Purpose              | Static IP Address | Network Mode       | Notes |  
|------------------|-----------------------------|------------------|--------------------|-------|  
| Kali Linux       | Attacker / Security Tools   | `192.168.56.101` (Host-Only) <br> `10.0.3.15` (NAT) | Host-Only + NAT    | <img src="../../assets/images/Kali IP.png" alt="IP address snippet" height="100" /> |  
| Metasploitable 2 | Vulnerable Linux Target     | `192.168.56.102` | Host-Only          | <img src="../../assets/images/metasploit IP.jpg" alt="IP address snippet" height="100" /> |  
| bWAPP            | Vulnerable Web Application  | `192.168.56.103` | Host-Only          | <img src="../../assets/images/bwapp IP.jpg" alt="IP address snippet" height="100" /> |  
| Windows 10       | User Workstation Simulation | `192.168.56.104` | Host-Only          | <img src="../../assets/images/windows IP.png" alt="IP address snippet" height="100" /> |  

---

**Verification Steps**:  
- Configured static IPs manually on each VM.  
- Confirmed all machines are on the same subnet (`192.168.56.0/24`).  
- Tested connectivity between machines using `ping`.  
- Verified Kali Linux’s additional NAT adapter (`10.0.3.15`) provides internet access (e.g., updating packages, testing BurpSuite).  


---
# 🧠 Learning & Reflection  

- **Learning Journey**:  
  - Configuring static IPs gave me more control and stability compared to dynamic allocation. Each machine retained its address across reboots, which made management easier.  
  - Setting up a dual-adapter environment (Host-Only + NAT) allowed me to keep lab traffic isolated while still giving Kali internet access for updates and tools like BurpSuite.  

- **Challenges Faced**:  
  - Initially setting correct subnet masks and gateways for consistency.  
  - Conflict between DHCP/NetworkManager and static IP configuration (had to restart the Kali machine for changes to reflect).  
  - Misconfigured routing: Host-Only adapter added a default gateway, which caused internet traffic issues until I removed it and let only NAT handle the gateway.
  - By default, Windows Firewall blocks ICMP Echo Requests, which caused one-way ping issues,(Kali → Windows failed, Windows → Kali worked). This was solved by enabling the **ICMP Echo Request (Inbound)** rule in Windows Defender Firewall.  
 

- **Key Takeaway**:  
  - Static IP assignment is more reliable for multi-VM labs since it simplifies repeatability, documentation, and troubleshooting.  
  - Always ensure **only one default gateway (via NAT)** for internet, while Host-Only remains strictly for internal lab traffic.
  - The Windows ping failure showed me that sometimes connectivity issues can come from host firewalls that block traffic. In Windows, the **File and Printer Sharing (Echo Request – ICMPv4-In)** rule must be enabled to allow ping responses, **unless it is within a controlled lab environment, it is best to keep firewalls enabled for security**.  


---
📂 **Note**: All images associated with this lab setup can be found [here](../../assets/images/).  
 
---
This documentation highlights my ability to design and configure a multi-VM lab environment with **static IP networking**, an essential foundation for more advanced cybersecurity practice.  

---
