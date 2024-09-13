# Network Reconnaissance Using Nmap and Wireshark

**Overview:**  
This project showcases how I conducted network reconnaissance using **Nmap** and **Wireshark** to map network structures, identify open ports, and detect potential vulnerabilities. The goal was to simulate a network discovery and vulnerability assessment process while learning the importance of thorough reconnaissance in a penetration test.

---

## Project Steps

### **1. Setting Up the Environment**

For this reconnaissance task, I utilized **Kali Linux** as my penetration testing environment. Kali Linux comes with built-in tools such as **Nmap** and **Wireshark**, making it ideal for network reconnaissance activities.

- **Kali Linux Setup:**
  - Installed Kali Linux on VirtualBox, ensuring network adapters were in **Bridged Mode** to interact with my network.
  - Set up both tools (Nmap and Wireshark) in the terminal and GUI environments.

**Tools Used:**
- **Nmap**: A versatile network mapping and scanning tool for discovering hosts and services.
- **Wireshark**: A powerful packet analyzer for capturing and inspecting network traffic.

---

### **2. Initial Network Discovery (Nmap)**

The first step was to identify all devices (hosts) on my network by performing a **ping sweep** using Nmap.

**Steps:**

1. **Ping Sweep:**
   I used Nmap to conduct a simple ping sweep of my local network to discover live hosts:
   ```bash
   nmap -sn 192.168.1.0/24
   ```
   - `-sn`: Performs a ping scan, disabling port scanning.
   - `192.168.1.0/24`: Specifies the subnet to scan.

**Result:**  
Nmap returned a list of live hosts on the network, along with their IP addresses, indicating which devices were currently active. 

2. **Host Discovery Output:**
   The scan revealed multiple live devices, including routers, printers, and computers, displaying their IP and MAC addresses.

**Sample Output:**
```bash
Nmap scan report for 192.168.1.1
Host is up (0.0040s latency).
MAC Address: 00:11:22:33:44:55 (Router)

Nmap scan report for 192.168.1.10
Host is up (0.0060s latency).
MAC Address: 66:77:88:99:AA:BB (Computer)
```

---

### **3. Detailed Port Scanning (Nmap)**

Once I had identified the live hosts on my network, I moved on to perform a **detailed port scan** to see what services were running and which ports were open.

**Steps:**

1. **Scan for Open Ports:**
   I targeted a specific IP address to scan for open ports using the following Nmap command:
   ```bash
   nmap -p 1-65535 192.168.1.10
   ```
   - `-p 1-65535`: Scans all 65,535 ports on the target device.

2. **Service Version Detection:**
   After finding open ports, I used Nmap’s version detection feature to gather more detailed information about the services running:
   ```bash
   nmap -sV 192.168.1.10
   ```
   - `-sV`: Attempts to determine the version of the services running on open ports.

**Result:**  
The scan returned a list of open ports, services running on those ports, and the service versions. This helped identify whether any of the services were outdated or vulnerable.

**Sample Output:**
```bash
PORT     STATE SERVICE     VERSION
22/tcp   open  ssh         OpenSSH 7.4p1
80/tcp   open  http        Apache httpd 2.4.29
443/tcp  open  https       Apache httpd 2.4.29
```

---

### **4. Network Traffic Capture (Wireshark)**

After identifying open ports and services, I used **Wireshark** to capture network traffic and inspect the data packets traveling across my network. This step helped me understand the kind of data being transmitted and if there were any unencrypted or suspicious packets.

**Steps:**

1. **Open Wireshark:**
   I launched Wireshark and selected my network interface (e.g., `eth0` or `wlan0`) to start capturing traffic.

2. **Start Capture:**
   I started capturing packets on my local network by selecting the interface and clicking the **Start Capture** button.

3. **Analyze Packets:**
   Once packets were captured, I applied filters in Wireshark to focus on specific types of traffic. For example, filtering **HTTP traffic** to see unencrypted requests:
   ```bash
   http
   ```
   I could also filter for **DNS traffic**:
   ```bash
   dns
   ```

**Result:**  
Wireshark provided a detailed view of the network packets, including the source and destination IP addresses, protocols in use (e.g., TCP, HTTP, DNS), and the actual data being transmitted.

**Sample Screenshot:**

![Wireshark Capture](https://upload.wikimedia.org/wikipedia/commons/thumb/7/7b/Wireshark_screenshot.png/800px-Wireshark_screenshot.png)

4. **Saving the Capture:**
   After capturing and analyzing traffic for a set period, I saved the capture file for future analysis and reporting:
   - **File → Save As** to save the capture as a `.pcap` file.

---

### **5. Vulnerability Detection (Nmap Scripting Engine)**

To further investigate, I used **Nmap’s Scripting Engine (NSE)** to detect vulnerabilities in the services I had discovered.

**Steps:**

1. **Vulnerability Scan:**
   I ran the vulnerability detection scripts provided by Nmap to check for known issues:
   ```bash
   nmap --script vuln 192.168.1.10
   ```
   This script automatically checks for various vulnerabilities based on the services running on the target.

2. **Specific Vulnerability Checks:**
   I focused on specific scripts to test particular services. For example, testing for **SMB vulnerabilities** (e.g., EternalBlue):
   ```bash
   nmap --script smb-vuln-ms17-010 192.168.1.10
   ```

**Result:**  
The Nmap scan revealed potential vulnerabilities in some services, such as outdated versions of software that could be exploited.

---

### **6. Documentation and Reporting**

After gathering all the information from Nmap and Wireshark, I created a detailed report that documented my findings. This report included:
- **Host Information**: List of active hosts and open ports.
- **Service Details**: Description of services and versions detected.
- **Vulnerability Findings**: Vulnerabilities discovered during the scan.
- **Traffic Analysis**: Summary of network traffic captured by Wireshark, including any suspicious or unencrypted data packets.

I structured the report to include remediation recommendations, such as updating vulnerable services or enforcing encrypted communication protocols like HTTPS.

---

## **Tools Used:**

- **Nmap**: Network scanning and vulnerability detection tool.
- **Wireshark**: Network packet capture and analysis tool.
- **Kali Linux**: The operating system used for penetration testing.

---

## **Lessons Learned:**

This project enhanced my understanding of network reconnaissance and how attackers might gather information about a network before launching an attack. Key takeaways include:
- The importance of conducting thorough network scans to identify weak points.
- How open ports and vulnerable services can provide entry points for attackers.
- The value of network traffic analysis in detecting suspicious activity and improving security posture.

---

This README serves as documentation of my network reconnaissance project using Nmap and Wireshark. Through this exercise, I gained practical experience in mapping networks, detecting vulnerabilities, and analyzing network traffic to assess the security of my network.
