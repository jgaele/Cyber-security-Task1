# Cyber Security Internship – Task 1
## Scan Your Local Network for Open Ports

### 1. Objective

The objective of this task was to scan a local network to discover active devices and identify open ports. This exercise helped me understand network reconnaissance, exposed services, and the importance of securing network ports.

### 2. Tools Used

- **Nmap:** For network discovery and port scanning.
- **Npcap:** Installed to support packet capture and network scanning on Windows.
- **Windows PowerShell / Command Prompt:** For checking network configuration, listening ports, processes, and firewall settings.

### 3. Network Configuration

I used the Windows `ipconfig` command to identify my local network configuration.

| Setting | Result |
|---|---|
| IPv4 address | `192.168.8.186` |
| Subnet mask | `255.255.255.0` |
| Default gateway | `192.168.8.1` |
| Network range | `192.168.8.0/24` |

**[INSERT SCREENSHOT 1 HERE – Windows ipconfig output showing IPv4 address, subnet mask, and default gateway]**

### 4. Local Network Discovery

I used the following Nmap command to discover active devices on my local network:

```bash
nmap -sn 192.168.8.0/24
```

The scan checked 256 IP addresses and reported **11 active hosts**.

This helped identify devices connected to the local network. The discovered devices included the router, my laptop, and other network devices.

**[INSERT SCREENSHOT 2 HERE – Nmap host discovery scan showing 11 hosts up]**

### 5. Scanning My Laptop for Open Ports

I scanned my own laptop at `192.168.8.186` using:

```bash
nmap -sV 192.168.8.186
```

The scan identified the following open TCP ports:

| Port | Service identified | General purpose |
|---|---|---|
| 135 | MSRPC | Microsoft Remote Procedure Call |
| 139 | NetBIOS-SSN | Windows network communication |
| 445 | Microsoft-DS | Windows file and printer sharing |
| 5432 | PostgreSQL | PostgreSQL database service |
| 16992 | AMT SOAP HTTP | Provisionally identified as an Intel AMT-related service |

Port `995/tcp` was reported as closed in the scan.

**[INSERT SCREENSHOT 3 HERE – Nmap service scan showing the open and closed ports]**

### 6. Saving Scan Results

I saved the Nmap scan output into a text file using:

```bash
nmap -sV 192.168.8.186 -oN scan_results.txt
```

The output was saved as `scan_results.txt` for documentation and future reference.

**[INSERT SCREENSHOT 4 HERE – Command showing the scan saved successfully, or the opened scan_results.txt file]**

### 7. Checking Listening Ports and Processes

I used the following Windows command to identify listening network ports and their associated process IDs:

```cmd
netstat -ano | findstr LISTENING
```

The output included listening ports such as:

- 135
- 139
- 445
- 623
- 5040
- 5432
- 16992
- 27017

I then used the `tasklist` command to investigate selected process IDs. The checks identified `postgres.exe` for PID `8752` and `explorer.exe` for PID `11700`.

These checks helped me understand how network ports can be associated with running processes. Not every process-to-port association was conclusively verified.

**[INSERT SCREENSHOT 5 HERE – netstat output showing listening ports and PIDs]**

**[INSERT SCREENSHOT 6 HERE – tasklist output showing the process names and PIDs]**

### 8. Windows Firewall Checks

I used Windows PowerShell to check the firewall profiles:

```powershell
Get-NetFirewallProfile | Format-Table Name, Enabled, DefaultInboundAction, DefaultOutboundAction
```

I also checked enabled inbound firewall rules that allow incoming connections:

```powershell
Get-NetFirewallRule -Enabled True -Direction Inbound -Action Allow | Select-Object DisplayName, Profile, Enabled, Action | Format-Table -AutoSize
```

These commands were used to inspect the firewall configuration and allowed inbound rules. The exact output values have not been recorded in this report.

**[INSERT SCREENSHOT 7 HERE – Firewall profile command output]**

**[INSERT SCREENSHOT 8 HERE – Enabled inbound firewall rules output]**

### 9. Security Observations

The scan showed that my laptop had several open ports.

Open ports are not automatically vulnerabilities, because some are required for normal services. However, unnecessary or improperly configured services can increase security risks.

Some possible risks include:

- Unauthorized access to network services.
- Exposure of file-sharing services.
- Attempts to exploit vulnerable or outdated services.
- Unnecessary services increasing the device's attack surface.

It is important to keep services updated, disable services that are not required, and configure firewall rules to allow only necessary connections.

### 10. Conclusion

Through this task, I learned how to identify my local network range, discover active devices, scan my own laptop for open ports, identify services, and save scan results.

I also learned how to use Windows commands to inspect listening ports, processes, and firewall settings.

This practical exercise improved my understanding of basic network reconnaissance and the importance of monitoring and securing exposed network services.

### 11. Interview Questions and Answers

**1. What is an open port?**

An open port is a network communication endpoint where a service is listening and can potentially accept connections.

**2. What is a TCP SYN scan?**

A TCP SYN scan is a scanning method that sends SYN packets to determine whether TCP ports are open without completing a full TCP connection.

**3. What are the risks of open ports?**

Unnecessary or poorly secured open ports can expose services to unauthorized access and attacks.

**4. What is the difference between TCP and UDP scanning?**

TCP scanning checks TCP services and connection states, while UDP scanning checks UDP services, which do not use the TCP connection handshake.

**5. How can open ports be secured?**

By disabling unnecessary services, applying updates, configuring firewall rules, and limiting access to trusted devices.

**6. What is the role of a firewall?**

A firewall controls incoming and outgoing network traffic according to security rules.

**7. Why do attackers scan networks?**

They scan networks to identify active devices, open ports, and potentially vulnerable services.

**8. How does Wireshark complement Nmap?**

Nmap identifies hosts, ports, and services, while Wireshark can capture and inspect network traffic.

### 12. Project Evidence

The following screenshots should be included as evidence:

1. Windows network configuration (`ipconfig`).
2. Nmap local network discovery.
3. Nmap service and port scan.
4. Saved scan results.
5. Listening ports (`netstat`).
6. Process identification (`tasklist`).
7. Windows Firewall profile check.
8. Enabled inbound firewall rules.

### 13. Important Note

This report records the scan results and commands available from the completed exercise. Firewall output values and the exact results of the later verification scan should be added if available. No unverified firewall settings or scan results have been assumed.

**End of Report**
