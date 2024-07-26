# Active Directory Lab

## Overview
This project simulates a corporate network environment using VirtualBox, where a Windows Server 2019 machine acts as a Domain Controller (DC) and DHCP server, and a Windows 10 machine acts as a client. The goal is to replicate a typical Active Directory setup, using PowerShell ISE script to auto create 100 different users.

## Components
- **VirtualBox**: The virtualization platform used to create and manage virtual machines.
- **Windows Server 2019 ISO**: The server operating system for the Domain Controller.
- **Windows 10 ISO**: The client operating system.

## Network Configuration

### Domain Controller (Server19)
- **NIC 1 (INTERNET)**: Connected to the home router to get internet access via DHCP.
- **NIC 2 (Internal)**: Connected to the internal virtual network with the following settings:
  - IP: `172.16.0.1`
  - Subnet Mask: `255.255.255.0`
  - Gateway: `<empty>`
  - DNS: `127.0.0.1` (loopback address to the DC)

### Client1 (Win10)
- **NIC (Internal)**: Connected to the internal virtual network to get its configuration from the DC via DHCP.

## Services Configuration

- **Active Directory Domain Services (AD DS)**
  - Domain: `mydomain.com`

- **Routing and Remote Access Service (RAS) / Network Address Translation (NAT)**
  - External Network: `INTERNET`
  - Internal Network: `Internal`

- **DHCP Server**
  - Scope Range: `172.16.0.100-200`
  - Subnet Mask: `255.255.255.0`
  - Gateway: `172.16.0.1`
  - DNS Server: `172.16.0.1`

## Steps to Reproduce

1. **Set up VirtualBox and Install ISOs**
   - Download and install VirtualBox.
   - Obtain Windows Server 2019 and Windows 10 ISOs.
   - Create a new virtual machine for Windows Server 2019 and another for Windows 10.

2. **Configure the Domain Controller**
   - Install Windows Server 2019 on the first VM.
   - Set up two network interfaces: one for internet access and one for internal communication.
   - Assign the internal NIC a static IP address of `172.16.0.1`.
   - Install and configure Active Directory Domain Services (AD DS).
   - Set up and configure the DHCP server with the specified scope.
   - Configure RAS/NAT to allow internal clients to access the internet if needed.

3. **Configure the Client Machine**
   - Install Windows 10 on the second VM.
   - Connect the client machine's NIC to the internal network.
   - Ensure it receives its IP address and network configuration from the DHCP server on the DC.
   - Join the client machine to the domain `mydomain.com`.

4. **Testing and Verification**
   - Verify that the Windows 10 client can join the domain and log in with domain credentials.
   - Confirm that the client receives the correct IP configuration from the DHCP server.
   - Test network connectivity between the client and the server.
   - Optionally, test internet connectivity if NAT is configured.

## Conclusion
This setup successfully simulates a corporate environment with a centralized domain controller and DHCP server using VirtualBox. This configuration is ideal for learning and testing Active Directory, DHCP, and network management in a controlled virtual environment.

---

Feel free to customize further based on your specific setup or any unique challenges you faced.
