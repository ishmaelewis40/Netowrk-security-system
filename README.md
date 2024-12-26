# Home Network Security System using Virtualization

## Project Overview

This project's goal is to provide a simulated home network environment for learning and practicing network security fundamentals. It entails creating virtual computers, configuring firewalls, monitoring network traffic, and detecting potential vulnerabilities. This project provides a secure and controlled environment for testing security tools and procedures without interfering with a live network.

## Table of Contents

-   [Project Overview](#project-overview)
-   [Table of Contents](#table-of-contents)
-   [Goals](#goals)
-   [Project Setup](#project-setup)
    -   [Virtualization Environment](#virtualization-environment)
    -   [Virtual Network Configuration](#virtual-network-configuration)
    -   [Virtual Machines](#virtual-machines)
-   [Security Measures Implemented](#security-measures-implemented)
    -   [Firewall Configuration (UFW/iptables)](#firewall-configuration-ufwiptables)
    -   [Network Traffic Monitoring (tcpdump/Wireshark)](#network-traffic-monitoring-tcpdumpwireshark)
    -   [Vulnerability Scanning (Nmap/OpenVAS)](#vulnerability-scanning-nmapopenvas)
-   [Tools Used](#tools-used)
-   [Findings and Analysis](#findings-and-analysis)
-   [Challenges and Lessons Learned](#challenges-and-lessons-learned)
-   [Future Improvements](#future-improvements)
-   [Contributing](#contributing)
-   [License](#license)

## Goals

* Create a virtual home network environment using Oracle Virtual Box.
* Set up a firewall to safeguard the network against unauthorised access.
* Check network traffic for any unusual activities.
* Determine potential vulnerabilities in the virtual network.
* Gain practical experience with network security tools and strategies.

## Project Setup

### Virtualization Environment

*   **Software:** [VirtualBox](https://www.virtualbox.org/) 
*   **Host OS:** Kali Linux(Monitoring VM & attacker VM)/ Windows 10(user VM)
*   **Configuration:** Each machine was given 10GB of RAM. each machine operated on 4 cores and 50gb of disk space.

### Virtual Network Configuration

*   **Network Type:** The netowrk type used was a bridged network for each machine 
*   **IP Addressing Scheme:** IP addresses for each machine: 192.168.0.71 (Monitoring VM), 192.168.0.1 (user VM), 192.168.0.222 (attacker VM)
*   **Gateway/Router:** The Monitoring VM was used as the Gateway/Router
### Virtual Machines

| VM Name            | Operating System | Purpose                                   | IP Address      |
| ------------------ | ---------------- | ----------------------------------------- | --------------- |
| Monitoring VM      | Kali Linux       | Firewall, Network Monitoring, Vulnerability Scanning | 192.168.0.72     |
| Attacker VM        | Kali Linux/Metasploitable | Simulating Attacks                         | 192.168.0.222    |
| User VM (Windows) | Windows 10/Server | Target System                             | 192.168.0.1    |

## Security Measures Implemented

### Firewall Configuration (UFW)

*   **Rules Implemented:** 
    *   `sudo ufw deny from 192.168.0.222 to 192.168.0.1`
    *   `sudo ufw deny from 192.168.0.222`
  
*   **Rationale:**
*   The rule to deny all traffic from the attacker VM to the Users VM was the first rule to be established. This would ensure that that User VM was protected from any port scanning techniques from the attacker.
*   The second rule was to deny all traffic from the attackers VM this was positioned second so there was no clashes and prevented the rule to protect the user machine from being executed. This rule is set so the attacker cannot scan any ports on the Monitoring VM.

### Network Traffic Monitoring (tcpdump/Wireshark)

*   **Monitoring Techniques:** Wireshark was used to capture all the traffic that was connected to the network. Wireshark monitored all ingoing and outgoing traffic and was used to detect any unusual activity.
*   **Filters Used:** filters used in wireshark: ip.dst == 192.168.0.1 && tcp.flags.syn == 1 

### Vulnerability Scanning (Nmap/OpenVAS)

*   **Scans Performed:**  The scans performed were a TCP-SYN scan, a version detection scan and an OS detection scan, UDP Scan
*   **Scan Results:** [image](https://github.com/user-attachments/assets/f3c49822-40cf-4cfa-bbb8-f02d71f904fd) This image indicates all the open ports that were found and vulnerabilities before firewall rules had ben implimented.


## Tools Used

*   VirtualBox 
*   Kali Linux
*   Windows 10
*   UFW 
*   Wireshark
*   Nmap

## Findings and Analysis


*   "Nmap identified filtered ports 22,23 (SSH) and 80 (HTTP) on the Windows VM."
*   "Wireshark captured a TCP three-way handshake between the attacker and Windows VMs, indicating a successful connection attempt before the firewall rule was implemented."
*   "OpenVAS reported a critical vulnerability related to SMB signing on the Windows VM."
*   "The firewall rule successfully blocked all ICMP (ping) requests from the attacker VM to the Windows VM." ]

## Challenges and Lessons Learned

 I had learnt during this project that using UFW or iptables as a firewall alone isnt enough, In some cases the hacker was able to establish a connection with the user VM before the fire wall could detect or block the hackers ip address, also a weakness in the firewall would be that if the hacker used a VPN it would mean that they could gain access again and they may be able to use more advanced techniques the next time.

It is better to use an IDS or IPS to ensure an extra layer of protection. 
All VM's in the network should use a bridged connection instead of NAT. This is because a NAT connection creates a separate network from the other machines which makes using wireshark for network monitoring redundant. 
Wireshark is able to pick up TCP SYN scans on the network even when then the firewall isnt able to, using an extra layer of protection would be advisable as you cannot constantly watch network traffic at all times of the day.

## Future Improvements

*   Implement an Intrusion Prevention System (IPS) like Snort, Suricata or Azure.
*   Set up a honeypot to attract and capture attacker activity.
*   Explore more advanced firewall configurations and techniques.
*   Create an environment that a hacker will use more advanced techniques to break into the network.
*   Automate vulnerability scanning and reporting.








Remember to replace the bracketed placeholders with your actual project details. This template should give you a solid foundation for your project documentation.
