# Firewall Setup and Management Using UFW
## Objective
The Firewall Configuration Project is aimed at setting up a secure network environment by configuring a firewall on an Ubuntu system using UFW. Key tasks include installing and enabling UFW, creating and managing firewall rules for services, ports, and IP ranges, and testing the firewall setup to ensure proper functionality. Additional tasks involve enabling logging for monitoring purposes, applying advanced configurations such as default policies. This exercise demonstrates fundamental network security practices and emphasizes the importance of firewalls in protecting systems from unauthorized access and cyber threats.
## Skills Learned
- Learned to install and enable UFW on an Ubuntu system to manage and secure network traffic effectively.
- configuring firewall rules to allow or block traffic for specific ports, services (e.g., SSH, HTTP), and IP addresses.
- Understood the importance of firewalls in protecting systems from unauthorized access and potential cyber threats.
- Used tools like nmap to scan for open ports and validate that the configured firewall rules are working as intended.
- Developed skills to identify and resolve issues in firewall configurations, such as misconfigured or conflicting rules.
- Explored advanced UFW options, including logging, setting default policies, and using application profiles for streamlined management.
- Enabled logging to monitor network activity and detect suspicious or unauthorized access attempts.
## Tools Used
- Linux Operating System (Ubuntu): The target system where UFW was installed and firewall rules were configured for network security.
- UFW (Uncomplicated Firewall): Configured on Ubuntu to manage and secure inbound and outbound network traffic through customizable firewall rules.
- Network Scanning Tool (nmap): Used for scanning the network to check open ports and verify the effectiveness of the firewall rules.
## Steps
#### 1.Update the System
- update the system's package list and install the latest security updates:
```bash
  sudo apt update && sudo apt upgrade -y
```
![image](https://github.com/user-attachments/assets/3a87a910-ba6f-404f-889b-cbd349a05b39)

#### 2.Install UFW (Uncomplicated Firewall)
- Installing the UFW firewall
```bash
  sudo apt install ufw
```
![image](https://github.com/user-attachments/assets/c4e9a9f8-ef02-4e2d-b45f-91482d813e2c)

#### 3.Enable the UFW firewall 
- To activate the firewall and begin enforcing rules
```bash
  sudo ufw enable
```
![image](https://github.com/user-attachments/assets/e49c4a58-fcd4-4999-91ee-a8cfe9a0e225)

####  4.Allow SSH Connection
- Before adding other rules, ensure that you can access your system remotely. Allow SSH traffic:
```bash
  sudo ufw allow ssh
```
![image](https://github.com/user-attachments/assets/74bfd68a-fe4b-43e7-b011-c672104a194f)

- This allows incoming traffic on the default SSH port (22).
```bash
  sudo ufw allow 22/tcp
```
![image](https://github.com/user-attachments/assets/cfcdcc13-64e3-420d-95bb-aafdf1c8b19c)

#### 5.Allow Specific Services and Ports
- Allow HTTP and HTTPS (used for web traffic):
```bash
  sudo ufw allow http
```
```bash
  sudo ufw allow https
```
![image](https://github.com/user-attachments/assets/28ffa8b9-fb89-45fa-9d70-1eaa72ff8d2b)

- Or specify the port numbers:
```bash
  sudo ufw allow 80/tcp
```
```bash
  sudo ufw allow 443/tcp
```
![image](https://github.com/user-attachments/assets/d01bdede-5427-41b0-8398-a7cdaf2223e2)

- Allow a Custom Port (e.g., an application running on port 8080):
```bash
  sudo ufw allow 8080/tcp
```

- Allow a Range of Ports (e.g., for applications requiring multiple ports):
```bash
  sudo ufw allow 1000:2000/tcp
```
![image](https://github.com/user-attachments/assets/5f64ef2c-62b8-4a43-bec5-0608b9c5eaaa)

- Allow Traffic from a Specific IP Address:
```bash
  sudo ufw allow from 10.0.2.11
```
![image](https://github.com/user-attachments/assets/ba05bdfd-12c1-4ba8-852b-122bc8180213)

- Allow Traffic from a Subnet (e.g., for a local network):
```bash
  sudo ufw allow from 10.0.2.0/24
```
![image](https://github.com/user-attachments/assets/30a5275d-caca-4744-8f23-71db9e617f8d)

#### 6.Deny Specific Services and Ports
- By default, UFW blocks incoming traffic unless explicitly allowed. However, you can explicitly deny certain traffic:
- Deny a Port:
```bash
  sudo ufw deny 23/tcp
```
![image](https://github.com/user-attachments/assets/9d9de408-bacb-42ef-a177-18059a112fd6)

- Deny Traffic from a Specific IP:
```bash
  sudo ufw deny from 203.0.113.0
```
![image](https://github.com/user-attachments/assets/b0cd4b16-6d6c-4750-9cc0-45cf6ba27f8f)

####  7.View UFW Status and Rules
- To see the active rules and firewall status, which displays all configured rules along with their status (e.g., allowed or denied).
```bash
  sudo ufw status verbose
```
![image](https://github.com/user-attachments/assets/a437b4d0-2984-4f3f-8424-166f7d55bffc)

#### 8.Delete UFW Rules
- i. First, list rules with numbers:
```bash
  sudo ufw status numbered
```
![image](https://github.com/user-attachments/assets/4651dde2-fde4-4535-8cb0-6893f5cd5c56)

- Delete a rule using its number (e.g., rule 2):
```bash
  sudo ufw delete 2
```
![image](https://github.com/user-attachments/assets/40f258b2-b02e-4f22-802d-402b7b8948d0)
- ii. By Rule Specification:
```bash
  sudo ufw delete allow 8888/tcp
```
![image](https://github.com/user-attachments/assets/8b38cb0a-c2d8-4fb1-81b1-a74ba9694131)

#### 9.Advanced Configuration
- Enable Logging: Monitor UFW activity for troubleshooting or security audits:
```bash
  sudo ufw logging on
```
![image](https://github.com/user-attachments/assets/2f988b81-834f-4a20-8c70-eefe008e7c02)

##### Set Default Policies
- Deny all incoming traffic:
```bash
  sudo ufw default deny incoming
```
- Allow all outgoing traffic:
```bash
  sudo ufw default allow outgoing
```
![image](https://github.com/user-attachments/assets/9be9df09-e0cd-441d-bd48-5f5d5158b86c)

- Use Application Profiles: List predefined profiles for common applications:
```bash
  sudo ufw app list
```
![image](https://github.com/user-attachments/assets/8a59a655-4c17-4a68-af1b-e9aa337c799a)

- Allow traffic for a specific application (e.g., Nginx):
```bash
  sudo ufw allow 'CUPS'
```
![image](https://github.com/user-attachments/assets/1964bb57-e8c9-44b4-9400-b68bff4f1fa0)

#### Testing the Firewall
- Check Open Ports: Use a tool like nmap from Kali OS (another machine to scan your system)
```bash
  nmap -v -A 127.0.0.1
```
![image](https://github.com/user-attachments/assets/55c8b514-afcf-4bd3-a52c-7c7034b04ca1)

## Conclusion 

This project provided hands-on experience in configuring a firewall using UFW on Ubuntu. Key outcomes include securing network traffic, managing rules for services and ports, and validating configurations using tools like nmap. The setup strengthens the system’s security, highlighting the importance of firewalls as a first line of defense against cyber threats.
