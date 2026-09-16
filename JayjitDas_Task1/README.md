# OASIS INFOBYTE - Security Analyst Internship

## Task 1: Basic Network Scanning with Nmap

### Project Information

Internship        : OASIS Infobyte – Security Analyst
Task              : Task 1 – Basic Network Scanning with Nmap
Target System     : Metasploitable Virtual Machine
Target IP Address : 192.168.56.101
Scanner System    : Kali Linux
Scanning Tool     : Nmap 7.99
Environment       : Controlled Local Virtual Machine Lab
---
## 1. Objective
The objective of this task is to perform basic network reconnaissance and identify open ports and running services on an authorized virtual machine using Nmap.

The assessment includes:
- Basic port scanning
- Service and version detection
- Operating-system detection attempt
- Identification of exposed services
- Basic security-risk analysis
- Security recommendations

The scan was performed against a Metasploitable virtual machine in a controlled local laboratory environment.
---
## 2. What is Nmap?

Nmap (Network Mapper) is a network scanning and security auditing tool.

It can be used to:
- Discover hosts on a network
- Identify open ports
- Detect running services
- Determine service versions
- Attempt operating-system detection
- Help assess a system's network attack surface

Nmap is commonly used by network administrators, penetration testers, and security professionals.
---

## 3. Why Network Scanning Matters

Network scanning helps security professionals understand which services are exposed on a system.

An open port may indicate a running network service. If a service is unnecessary, incorrectly configured, outdated, or insufficiently protected, it may increase the system's attack surface.

Network scanning can therefore help identify services that require:

- Access restrictions
- Configuration changes
- Security updates
- Monitoring
- Removal or disabling
---
## 4. Lab Environment

The assessment was performed using a local virtual machine laboratory.

### Scanner

- Kali Linux

### Target

- Metasploitable VM
- IP address: `192.168.56.101`

### Network

The target was accessed through the local virtual-machine laboratory network.

Only the authorized Metasploitable VM was scanned.

---

## 5. Installing Nmap

Nmap can be installed on Kali Linux using:

```bash
sudo apt update
sudo apt install nmap -y

Verify the installation:  nmap --version
The scan was performed using Nmap 7.99.

6. Basic Nmap Scan
Command:- nmap 192.168.56.101

Purpose

The basic scan identifies accessible TCP ports on the target.

Recorded Open Ports

21/tcp   open  ftp
22/tcp   open  ssh
23/tcp   open  telnet
25/tcp   open  smtp
53/tcp   open  domain
80/tcp   open  http
111/tcp  open  rpcbind
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
512/tcp  open  exec
513/tcp  open  login
514/tcp  open  shell

The basic scan identified 12 open TCP ports in the recorded result.

7. Service and Version Detection
Command:-  nmap -sV 192.168.56.101

The -sV option attempts to identify the services and their versions running on open ports.

Results
Port	Service	Version
21	FTP	vsftpd 2.3.4
22	SSH	OpenSSH 4.7p1
23	Telnet	Linux telnetd
25	SMTP	Postfix smtpd
53	DNS	ISC BIND 9.4.2
80	HTTP	Apache httpd 2.2.8
111	RPCbind	2
139	NetBIOS/SMB	Samba smbd 3.X - 4.X
445	SMB	Samba smbd 3.X - 4.X
512	exec	netkit-rsh rexecd
513	login	rlogind
514	shell	Netkit rshd
1099	Java RMI	GNU Classpath grmiregistry
1524	Bindshell	Metasploitable root shell
2049	NFS	2-4
2121	FTP	ProFTPD 1.3.1
3306	MySQL	MySQL 5.0.51a-3ubuntu5
5432	PostgreSQL	PostgreSQL 8.3.0 - 8.3.7
5900	VNC	Protocol 3.3
6000	X11	Access denied
6667	IRC	UnrealIRCd
8009	AJP13	Apache JServ Protocol v1.3

The service-version scan identified 22 open TCP ports.

8. Operating System Detection
Command :- sudo nmap -O 192.168.56.101

The -O option attempts to identify the operating system of the target.

Recorded Result

The scan showed the target as reachable and displayed the following open services:

21/tcp   open  ftp
22/tcp   open  ssh
23/tcp   open  telnet
25/tcp   open  smtp
53/tcp   open  domain
80/tcp   open  http
111/tcp  open  rpcbind
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
512/tcp  open  exec
513/tcp  open  login
514/tcp  open  shell

The recorded output did not provide a confirmed operating-system fingerprint.

Therefore, no specific operating system identification is claimed from the -O result.

9. Security Observations
FTP - Port 21

FTP does not provide encryption for normal authentication and data transfer.

Risk: Credentials and data may be exposed to network interception.

Recommendation: Use SFTP or appropriately secured FTPS. Disable unnecessary FTP access.

SSH - Port 22

SSH provides encrypted remote administration.

Risk: An exposed SSH service can be targeted through credential attacks or vulnerabilities in outdated software.

Recommendation: Use strong authentication, restrict access where possible, and keep the software updated.

Telnet - Port 23

Telnet provides remote terminal access without modern encryption.

Risk: Credentials and session information may be exposed.

Recommendation: Disable Telnet and use SSH instead.

SMTP - Port 25

Postfix provides SMTP services.

Risk: Incorrect configuration may allow unauthorized mail relay or abuse.

Recommendation: Configure relay restrictions and appropriate access controls.

DNS - Port 53

BIND provides DNS services.

Risk: Incorrect configuration may expose information or permit unauthorized queries or zone transfers.

Recommendation: Restrict DNS access and review zone-transfer settings.

HTTP - Port 80

Apache provides web services.

Risk: HTTP does not encrypt communication.

Recommendation: Use HTTPS where sensitive communication is required and keep the web server updated.

RPCbind - Port 111

RPCbind provides information about RPC services.

Risk: An exposed RPCbind service can increase the attack surface.

Recommendation: Disable unnecessary RPC services and restrict access.

SMB - Ports 139 and 445

Samba provides network file-sharing services.

Risk: Improperly secured SMB services may expose files, shares, or system information.

Recommendation: Restrict SMB access and disable unnecessary legacy protocols.

Legacy Remote Services - Ports 512, 513 and 514

These ports provide legacy remote-access services such as rexecd, rlogind, and rshd.

Risk: These services are insecure compared with modern encrypted administration.

Recommendation: Disable these services and use SSH instead.

Java RMI - Port 1099

Java RMI provides remote Java application communication.

Risk: An exposed RMI service can increase the attack surface.

Recommendation: Restrict access to trusted systems and disable the service when unnecessary.

Bindshell - Port 1524

Nmap identified this service as:

Metasploitable root shell

Risk: A network-accessible root shell represents a critical security risk because it can provide privileged access.

Recommendation: This service should not be exposed on a production system. It should be disabled or removed.

Note: This service is intentionally present in the Metasploitable training environment.

NFS - Port 2049

NFS provides network file-sharing functionality.

Risk: Incorrect export permissions may expose files or allow unauthorized access.

Recommendation: Restrict NFS exports to authorized hosts.

FTP - Port 2121

ProFTPD 1.3.1 is running on port 2121.

Risk: A second FTP service increases the attack surface, and traditional FTP is not encrypted.

Recommendation: Disable unnecessary FTP services and use secure file-transfer mechanisms.

MySQL - Port 3306

MySQL is directly accessible over the network.

Risk: Direct database exposure increases the attack surface.

Recommendation: Restrict database access to authorized systems.

PostgreSQL - Port 5432

PostgreSQL is network accessible.

Risk: Direct database exposure increases the attack surface.

Recommendation: Restrict access to trusted systems and use strong authentication.

VNC - Port 5900

VNC provides remote graphical access.

Risk: An exposed VNC service can be targeted for unauthorized remote access.

Recommendation: Restrict VNC access to trusted systems.

X11 - Port 6000

Nmap reported:

access denied

Risk: Network-exposed X11 can increase the attack surface.

Recommendation: Restrict or disable network X11 access when not required.

IRC - Port 6667

UnrealIRCd is exposed.

Risk: An unnecessary or outdated IRC service increases the attack surface.

Recommendation: Disable it when not required and keep it updated.

AJP13 - Port 8009

Apache JServ Protocol is exposed.

Risk: An unnecessarily exposed AJP service can increase the application-server attack surface.

Recommendation: Restrict AJP access to trusted systems and disable it when not required.

10. Overall Findings :-

      The service-version scan identified 22 open TCP ports.

      The target exposes a large number of services, including:

FTP
SSH
Telnet
SMTP
DNS
HTTP
RPC
SMB
NFS
MySQL
PostgreSQL
VNC
X11
IRC
Java RMI
AJP13

Several services are legacy services or use older software versions that should be reviewed and updated.

The most significant finding identified by the scan was:

1524/tcp open bindshell Metasploitable root shell

This represents a critical security concern because a network-accessible root shell can provide privileged access.

11. Key Recommendations:-

 1 Disable unnecessary services.
 2 Replace Telnet with SSH.
 3 Disable legacy rsh/rlogin services.
 4 Restrict SMB access.
 5 Secure or disable unnecessary FTP services.
 6 Restrict database services to authorized hosts.
 7 Restrict RPC and NFS services.
 8 Secure VNC and X11 access.
 9 Review Java RMI exposure.
10 Restrict AJP13 access.
11 Apply appropriate security updates.
12 Use strong authentication.
13 Configure firewall controls.
14 Monitor exposed services.
15 Reduce the overall network attack surface.

12. Screenshots:-

    Screenshots of the Nmap scans are included in the screenshots/ directory.

Recommended screenshots:

screenshots/
├── basic-scan.png
├── service-version-scan.png
└── os-detection-scan.png

The screenshots demonstrate the commands and terminal output used during the assessment.

13. Ethical Use:-

This scan was performed only against an authorized Metasploitable virtual machine in a controlled local laboratory environment.

Target:

192.168.56.101

The target was intentionally configured for security training and testing.

Nmap should only be used against systems for which the tester has explicit authorization.

External, third-party, or production systems should not be scanned without appropriate permission.

14. Project Files :-

SecurityAnalyst-Beginner-Task1-BasicNetworkScanning/
│
├── screenshots/
│   ├── basic-scan.png
│   ├── service-version-scan.png
│   └── os-detection-scan.png
│
├── nmap_scan_results.txt
└── README.md
nmap_scan_results.txt

Contains the detailed Nmap scan results, service/version information, OS detection result, security observations, and recommendations.

screenshots/

Contains screenshots of the Nmap commands and terminal output.

README.md

Contains the project documentation, methodology, findings, and ethical-use information.

15. Conclusion:-


The Nmap assessment successfully identified exposed network services on the Metasploitable target.

The basic scan identified open ports, while the -sV scan provided service and version information.

The -O scan attempted operating-system detection but did not provide a confirmed OS fingerprint in the recorded output.

The assessment demonstrates how network scanning can identify a system's attack surface and highlight services requiring security review.

The findings should be interpreted within the context of the intentionally vulnerable Metasploitable training environment.

Disclaimer

This project was performed for authorized educational and security-training purposes in a controlled virtual-machine laboratory.

Do not use Nmap to scan systems or networks without explicit authorization.


### final Task 1 folder
```text
OIBSIP
└── SecurityAnalyst-Beginner-Task1-BasicNetworkScanning
    ├── screenshots
    │   ├── basic-scan.png
    │   ├── service-version-scan.png
    │   └── os-detection-scan.png
    ├── nmap_scan_results.txt
    └── README.md

1. BASIC NMAP SCAN
------------------------------------------------------------
Command: nmap 192.168.56.101

Output:
┌──(panther㉿kali)-[~]
└─$ nmap 192.168.56.101   
Starting Nmap 7.99 ( https://nmap.org ) at 2026-09-07 02:31 +0530
Nmap scan report for 192.168.56.101
Host is up (0.0083s latency).
Not shown: 977 filtered tcp ports (no-response)
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
23/tcp   open  telnet
25/tcp   open  smtp
53/tcp   open  domain
80/tcp   open  http
111/tcp  open  rpcbind
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
512/tcp  open  exec


  