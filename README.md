# Proxmox Virtual Lab Setup

## Overview
This document serves as a Standard Operating Procedure (SOP) for setting up a virtual lab using Proxmox. The environment consists of the following virtual machines (VMs):

- **Windows Server 2019** (Active Directory & Domain Controller)
- **Windows 10 Client** (Domain-joined workstation)
- **Kali Linux** (Penetration testing)
- **Metasploitable** (Vulnerable target machine)

This setup provides a controlled environment for security testing, network management, and system administration using **KVM** virtualization under Proxmox.

## Prerequisites
- A Proxmox VE installation (latest version recommended)
- At least **16GB RAM**, **4 CPU cores**, and **500GB storage**
- Access to Windows ISOs and Linux images
- Network connectivity (bridged or NAT, depending on your needs)

## Step 1: Install Proxmox VE
1. Download Proxmox VE from the [official site](https://www.proxmox.com/en/downloads).
2. Flash the ISO onto a USB drive using **Rufus** or **BalenaEtcher**.
3. Boot from the USB and follow the guided installation.
4. Assign a static IP address and configure the network settings.
5. Access the Proxmox Web UI via `https://<proxmox-ip>:8006/`.

## Step 2: Configure Storage
1. Navigate to **Datacenter > Storage**.
2. Add **LVM-Thin** or **Directory** storage as needed.
3. Upload ISOs to `local` storage.

## Step 3: Create Virtual Machines
### Windows Server 2019
1. **Create a new VM** > Assign a name.
2. **Select the Windows Server 2019 ISO**.
3. **Set CPU to 2 cores, RAM to 4GB**, and **disk size to 60GB**.
4. **Enable QEMU Guest Agent**.
5. **Use VirtIO drivers** for better performance.
6. Complete installation and configure **Active Directory** and **DNS**.

### Windows 10 Client
1. Follow the same steps as above with **2GB RAM** and **40GB disk**.
2. Join the Windows 10 client to the domain.

### Kali Linux
1. Use the latest **Kali ISO** and assign **2 cores, 2GB RAM**, and **40GB disk**.
2. Ensure **networking is enabled** for testing purposes.

### Metasploitable
1. Download the Metasploitable VM.
2. Convert the VMDK to QCOW2 using:
   ```bash
   qemu-img convert -O qcow2 metasploitable.vmdk metasploitable.qcow2
   ```
3. Create a VM in Proxmox and use the converted disk.

## Step 4: Network Configuration
1. Set up a **bridged network** for internet access.
2. Optionally, create an **isolated internal network** for testing.
3. Assign static IPs where necessary.

## Step 5: Snapshots & Backup
- Take snapshots before major changes.
- Set up automated backups using **Proxmox Backup Server**.

## Conclusion
This lab provides hands-on experience with **KVM-based virtualization**, **Active Directory**, **network security**, and **penetration testing**. You can expand this setup with additional machines and services based on your needs.

---

For more details or troubleshooting, refer to the [Proxmox Documentation](https://pve.proxmox.com/wiki/Main_Page).

