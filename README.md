# Running Ubuntu24.04 in a GitHub Codespace
To run an Ubuntu-based environment in a GitHub Codespace using a Dev Container. This guide walks you through setting up your repository with the necessary configuration files so that every time you start a Codespace, you’ll be booted into an Ubuntu container.

## Setting Up a Codespace in GitHub to run Ubuntu 24.04
Follow the steps below to set up a GitHub Codespace. Codespaces offer a cloud-based development environment that makes it easy to get started without any local setup.

## Step 1: Fork this repository to your github account. 
1. Clone [this repository](https://github.com/dipaish/ubuntu24.04/) to your own GitHub account by clicking the "Fork" button in the top right corner of the repository page.

## Step 2: Create a Codespace

1. Go back to your repository's **main** page.
2. Click the **"Code"** button (usually located near the top right).
3. Select **"Create codespace on main"**.
4. Wait for a few moments while your Codespace environment is being set up.

## Start working on the Firewall Tasks 
After the codespace starts, read the following and do as instrcuted:  

# What is firewall?

- **Firewall**: A security tool (hardware or software) that monitors and controls network traffic based on set rules.
- **Purpose**: Acts as a barrier between trusted internal networks and untrusted external networks.
- **Key Functions**:
  - **Traffic Filtering**: Allows or blocks data based on IP, ports, and protocols.
  - **Access Control**: Restricts access to applications, services, or devices.
  - **Threat Prevention**: Detects and blocks malicious content.

**Firewalls are essential for protecting networks from unauthorized access and cyber threats.**


# Firewall Rules: Default, Allow, and Deny Policies

### Default, Allow, and Deny Explained

- **Default**: The initial rule that applies to all network traffic unless there is a specific rule (allow or deny) in place. This **default policy** is like the firewall's overall stance toward any traffic it doesn't explicitly recognize. Firewalls typically use one of two default policies:
  - **Default Deny**: Blocks all traffic unless explicitly allowed. This is the more secure option, as only predefined safe traffic is permitted.
  - **Default Allow**: Permits all traffic unless explicitly denied. This is less secure, as all traffic is permitted unless specified otherwise.

- **Allow**: Rules that permit specific traffic through the firewall. For example, allowing incoming SSH traffic on port 22 for remote access.

- **Deny**: Rules that block specific traffic. Useful for restricting access to certain ports or IP addresses or preventing unauthorized access.

# Types of Firewalls

1. **Network Firewalls**
   - **Function**: Operate at the network layer, filtering traffic between networks.
   - **Placement**: Typically placed at the edge of a network, between the internal network and the internet.
   - **Examples**: 
     - **Cisco ASA**: A hardware firewall with extensive features for managing large network environments.
     - **pfSense**: An open-source firewall with capabilities for network-level filtering.
   - **Usage**: Blocks or permits traffic based on IP addresses, ports, and protocols.
   - **Example Rule**: In pfSense, allow inbound HTTPS traffic on port 443 but block all traffic from untrusted IP ranges.

2. **Host-Based Firewalls**
   - **Function**: Installed on individual computers or devices, providing protection at the endpoint level.
   - **Placement**: Installed on each device or server.
   - **Examples**:
     - **UFW (Uncomplicated Firewall)**: Commonly used on Ubuntu for managing rules on a per-host basis.
     - **Windows Defender Firewall**: Provides host-based firewalling for Windows operating systems.
   - **Usage**: Controls inbound and outbound traffic per host, often configured for personal computers or specific servers in a network.
   - **Example Rule**: In UFW, allow SSH access only from a local network by running `sudo ufw allow from 192.168.1.0/24 to any port 22`.

3. **Application Firewalls**
   - **Function**: Operate at the application layer, filtering traffic based on application data and user requests.
   - **Placement**: Between the user and the application or directly integrated with the application.
   - **Examples**:
     - **ModSecurity**: An open-source Web Application Firewall (WAF) often used with Apache and Nginx servers.
     - **Cloudflare WAF**: A cloud-based WAF that protects web applications from attacks like SQL injection and XSS.
   - **Usage**: Inspects application-layer data to detect and block suspicious behavior related to specific applications.
   - **Example Rule**: In ModSecurity, block HTTP requests containing SQL injection patterns (e.g., `SELECT * FROM`) to protect a web application.

4. **Next-Generation Firewalls (NGFWs)**
   - **Function**: Combine traditional firewall functionality with advanced features like deep packet inspection, intrusion prevention, and application awareness.
   - **Placement**: At strategic points in the network, like entry/exit points or between critical internal network segments.
   - **Examples**:
     - **Cisco Firepower**: An NGFW with advanced security features, including intrusion prevention and deep packet inspection.
     - **Fortinet FortiGate**: Offers application awareness and control, deep packet inspection, and integrated threat intelligence.
   - **Usage**: Enhances traditional firewall capabilities with threat intelligence, deep inspection, and complex application-level analysis, making them ideal for sophisticated environments.
   - **Example Rule**: In FortiGate, allow only known applications, such as email clients, to access the internet while blocking all unidentified applications.

# Firewall Placement in a Network

- **Perimeter (Network Edge)**: Protects the entire network from external threats. This is usually the first line of defense, filtering incoming and outgoing traffic.

- **Internal Segmentation**: Placed within a network to separate and protect sensitive areas from less secure ones. This setup is ideal for controlling lateral movement within the network.

- **Endpoints (Devices)**: Host-based firewalls on individual devices ensure that each device can only interact with trusted sources, adding security layers to specific servers or workstations.

# UFW (Uncomplicated Firewall)

UFW is a command-line tool for managing a firewall on Ubuntu and other Debian-based Linux systems. It simplifies the configuration and management of iptables, making it easier to set up rules for network traffic. With UFW, users can easily allow or deny access to specific ports and services, enhancing security.

## Common Ports for Server Applications

Refer to [this guide on TCP and UDP ports](https://www.examcollection.com/certification-training/network-plus-overview-of-common-tcp-and-udp-default-ports.html) for more details. Here are some typical ports:

- **22** - SSH
- **25** - SMTP
- **53** - DNS
- **80** - HTTP
- **443** - HTTPS
- **3306** - MySQL

## Installing UFW on Ubuntu

To install **UFW** (Uncomplicated Firewall) on Ubuntu, use the following command:

***Note: remove sudo from command line it if says not recognized in the codespace***

```bash
sudo apt update
sudo apt install ufw -y
```

## Check UFW Status:
```bash
sudo ufw status
```
## Enable UFW
```bash
sudo ufw enable
```
## Disable UFW:
```bash
sudo ufw disable
```
UFW Command Syntax
The basic syntax for allowing a port through UFW:
sudo ufw allow <port>/<optional: protocol>

Allow DNS (port 53) for both TCP and UDP
sudo ufw allow 53
sudo ufw allow 53/tcp
sudo ufw allow 53/udp


## Allow Connections

### To allow a specific port (e.g., SSH on port 22)
```bash
sudo ufw allow 22
```

### Listing Available Applications
```bash
sudo ufw app list
```

### To allow a specific service (e.g., OpenSSH):
```bash
sudo ufw allow OpenSSH
```

### To allow a range of ports (e.g., 5000-6000)
```bash
sudo ufw allow 5000:6000/tcp
```
### To allow from a specific IP (e.g., 192.168.1.10)
```bash
sudo ufw allow from 192.168.1.10
```
### To allow access to a port only from a specific IP (e.g., 192.168.1.10 on port 22)
```bash
sudo ufw allow from 192.168.1.10 to any port 22
sudo ufw allow from 203.0.113.103 proto tcp to any port 22

```
### Allow HTTP and HTTPS (for web traffic):
```bash
sudo ufw allow 80
sudo ufw allow 443
```
### Allow SSH (for remote access):
```bash
sudo ufw allow 22
```

## Deny Connections
### To block a specific port (e.g., 80)
```bash
sudo ufw deny 80
```
### To deny from a specific IP
```bash
sudo ufw deny from 192.168.1.10
```


### To block all IPs from 192.168.1.10 to 192.168.1.20 (Subnet)
```bash
sudo ufw deny from 192.168.1.10/29

sudo ufw allow from 203.0.113.0/24 proto tcp to any port 22

```

### To block outgoing SMTP (port 25) to prevent mail sending:
```bash
sudo ufw deny out 25
```



## Delete a Rule
### List numbered rules
```bash
sudo ufw status numbered
```
### Delete a rule by number (e.g., rule #3)
```bash
sudo ufw delete 3
```

### Deleting All UFW Rules at Once

The command below will:
- Delete all active UFW rules.
- Disable UFW.
- Reset UFW settings to their defaults.

```bash
sudo ufw reset
```

## Set Default Policies
### Set UFW to deny all incoming connections by default
```bash
sudo ufw default deny incoming
```
### Set UFW to allow all outgoing connections by default
```bash
sudo ufw default allow outgoing
```
