---
title: "networkind"
date: 2024-11-30 10:00:00 +0000
categories: [Web Development, Deployment]
tags: [deployment]
toc: true
---



Here’s a **Linux-only command table** for exploring networking properties comprehensively:

---

| **Purpose**                  | **Command**                                   | **Details Shown**                                                                 |
|------------------------------|-----------------------------------------------|-----------------------------------------------------------------------------------|
| **List network interfaces**  | `ip addr`                                     | Interface names, IP addresses (IPv4/IPv6), MAC addresses, and status (UP/DOWN).  |
|                              | `ip link show`                                | MAC address, interface state, and MTU (Maximum Transmission Unit).               |
|                              | `ifconfig`                                    | Legacy command for IP, MAC, and interface state.                                 |
| **Check IP configuration**   | `ip addr show`                                | IP addresses, subnet mask, and interface details.                                |
|                              | `nmcli device show`                           | Detailed network configuration (IP, DNS, etc.) for each device.                  |
| **View routing table**       | `ip route`                                    | Routes, gateways, and default gateway.                                           |
|                              | `route -n`                                    | Legacy command to see routing table with numeric IPs.                            |
| **Check DNS settings**       | `cat /etc/resolv.conf`                        | DNS server IPs used for name resolution.                                         |
|                              | `nmcli dev show | grep DNS`                   | DNS server details for active connections.                                       |
| **View active connections**  | `netstat -tuln`                               | Open TCP/UDP connections, listening ports.                                       |
|                              | `ss -tuln`                                    | Similar to `netstat` but more modern.                                            |
| **Ping/connectivity test**   | `ping <hostname or IP>`                       | Tests connectivity to a host (IP or domain name).                                |
|                              | `traceroute <hostname or IP>`                 | Shows the path packets take to reach a host.                                     |
| **Check wireless networks**  | `iwconfig`                                    | Details about wireless interfaces (SSID, frequency, signal strength).            |
|                              | `nmcli dev wifi list`                         | Lists available Wi-Fi networks.                                                 |
| **View MAC address**         | `ip link show`                                | Hardware (MAC) addresses for interfaces.                                         |
|                              | `cat /sys/class/net/<interface>/address`      | MAC address of a specific interface.                                             |
| **View devices on network**  | `arp -a`                                      | ARP table with IP and MAC addresses of devices on the same network.              |
|                              | `ip neigh`                                    | Neighbor table showing reachable hosts.                                          |
| **Monitor network usage**    | `iftop`                                       | Real-time bandwidth usage per connection.                                        |
|                              | `nload`                                       | Real-time incoming and outgoing bandwidth usage.                                 |
| **Check firewall status**    | `sudo ufw status`                             | Firewall rules and status.                                                       |
|                              | `sudo iptables -L`                            | Detailed firewall rules.                                                         |
| **View all network events**  | `dmesg | grep -i net`                         | Logs related to network hardware and drivers.                                    |
|                              | `journalctl -u NetworkManager`                | Logs related to the NetworkManager service.                                      |
| **Test network speed**       | `speedtest-cli`                               | Internet speed test (requires installation of `speedtest-cli`).                  |
| **View network interfaces hardware** | `ethtool <interface>`                      | Hardware properties and statistics for an interface.                             |
| **Inspect wireless details** | `iwlist <interface> scanning`                 | Detailed scan of wireless networks (SSID, frequency, signal strength, etc.).     |

---

### **Essential Installation Commands (Optional)**
Some tools like `iftop`, `nload`, and `speedtest-cli` may need installation:

- **Install `iftop`**:
  ```bash
  sudo apt install iftop
  ```

- **Install `nload`**:
  ```bash
  sudo apt install nload
  ```

- **Install `speedtest-cli`**:
  ```bash
  sudo apt install speedtest-cli
  ```

---

### **How to Use This Table**
1. Start with **`ip addr`** to see all active network interfaces and their IPs.
2. Use **`ip route`** to understand routing (default gateway).
3. Check active connections with **`netstat`** or **`ss`**.
4. Dive deeper into wireless or DNS settings with **`iwconfig`**, **`nmcli`**, or **`cat /etc/resolv.conf`**.
5. Test connectivity with **`ping`** and speed with **`speedtest-cli`**.

Let me know if you need help interpreting any of these commands!
