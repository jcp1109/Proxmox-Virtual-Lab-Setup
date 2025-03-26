# Proxmox-Virtual-Lab-Setup
This lab provides hands-on experience with KVM-based virtualization, Active Directory, network security, and penetration testing. You can expand this setup with additional machines and services based on your needs.

Overview

This document serves as a Standard Operating Procedure (SOP) for setting up a virtual lab using Proxmox. The environment consists of the following virtual machines (VMs):

Windows Server 2019 (Active Directory & Domain Controller)

Windows 10 Client (Domain-joined workstation)

Kali Linux (Penetration testing)

Metasploitable (Vulnerable target machine)

This setup provides a controlled environment for security testing, network management, and system administration using KVM virtualization under Proxmox.

Prerequisites

A Proxmox VE installation (latest version recommended)

At least 16GB RAM, 4 CPU cores, and 500GB storage

Access to Windows ISOs and Linux images

Network connectivity (bridged or NAT, depending on your needs)

Step 1: Install Proxmox VE

Download Proxmox VE from the official site.

Flash the ISO onto a USB drive using Rufus or BalenaEtcher.

Boot from the USB and follow the guided installation.

Assign a static IP address and configure the network settings.

Access the Proxmox Web UI via https://<proxmox-ip>:8006/.

Step 2: Configure Storage

Navigate to Datacenter > Storage.

Add LVM-Thin or Directory storage as needed.

Upload ISOs to local storage.

Step 3: Create Virtual Machines

Windows Server 2019

Create a new VM > Assign a name.

Select the Windows Server 2019 ISO.

Set CPU to 2 cores, RAM to 4GB, and disk size to 60GB.

Enable QEMU Guest Agent.

Use VirtIO drivers for better performance.

Complete installation and configure Active Directory and DNS.

Windows 10 Client

Follow the same steps as above with 2GB RAM and 40GB disk.

Join the Windows 10 client to the domain.

Kali Linux

Use the latest Kali ISO and assign 2 cores, 2GB RAM, and 40GB disk.

Ensure networking is enabled for testing purposes.

Metasploitable

Download the Metasploitable VM.

Convert the VMDK to QCOW2 using:

qemu-img convert -O qcow2 metasploitable.vmdk metasploitable.qcow2

Create a VM in Proxmox and use the converted disk.

Step 4: Network Configuration

Set up a bridged network for internet access.

Optionally, create an isolated internal network for testing.

Assign static IPs where necessary.

Step 5: Snapshots & Backup

Take snapshots before major changes.

Set up automated backups using Proxmox Backup Server.
