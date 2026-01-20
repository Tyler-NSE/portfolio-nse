---
layout: default
---

# PfSense Installation in VMWare Workstation

Description.

- [Prerequisites](#prerequisites)
- [Steps to install pfSense on VMWare](#steps-to-install-pfsense-on-vmware)
- [Configure VMware workstation network for pfSense](#configure-vmware-workstation-network-for-pfsense)
- [Create PfSense Virtual machine](#create-pfsense-virtual-machine)
- [Setup the pfSense VM hard disk](#setup-th-pfsense-vm-hard-disk)
- [Assign the VM resources](#assign-the-vm-resources)
- [PfSense installation](#pfesnse-installation)
- [Setup the client machine](#setup-the-client-machine)
- [pfSense initial setup](#pfsense-initial-setup)
- [Install VMware tools in pfSense](#install-vmware-tools-in-pfsense)
- [Access the internet on Pfsense LAN side](#access-the-internet-on-pfsense-lan-side)

## Prerequisites

* You need to have VMware workstation pro.

I am using VMware workstation 17 and have a guide to install [here](/projects/lab_setup_instructions/vmware_workstation_setup.html).

* PfSense ISO image.

You can download the Pfsense image from [here](https://www.pfsense.org/download/), make sure you choose AMD64, DVD image(iso) installer.

## Steps to install pfSense on VMware

### Configure VMware workstation network for pfSense

We require two interfaces for pfSense, one for the WAN and the other for the LAN, for the WAN interfaces you need to have internet access. And the LAN side will act as a gateway for the LAN users. We need to configure these two interfaces on the VMware workstation first.

WAN- We will be using the Bridge interface, which will bring the PfSense firewall WAN side to be part of the local network. Your local router will assign an IP address on the WAN side. There are times the bridge interface may not work well, and you can follow the guide here to troubleshoot the problem. As a workaround, you could use the NAT interface if the bridge interface doesn’t work.

LAN- For the LAN interface we will be using the host-only adapter and select VMnet1. By default, the VMnet1 will act as DHCP server for the Virtual machine. You need to disable the DHCP service on the VMnet1 first.

Open VMware Workstation and click on Edit > Virtual Network editor. In the Virtual Network Editor click on Change settings.

Note: You need to have admin rights, in order to change the settings.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/edit-vne.PNG)

Here is my virtual adapter configuration; we will configure VMnet1 for the LAN as the second adapter. As you can see, I have the DHCP configuration disabled on this adapter, and it is acting as the host-only adapter, meaning it will allow the VM to talk internally in a Private network.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/vne-host-only.PNG)

### Create PfSense Virtual machine

We are now going to create the pfSense firewall VM, so Click on File and new virtual machine.

In the New virtual machine wizard choose Typical.

In the installer disk file image, choose the PfSense image that you have downloaded earlier and click on Next.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/new_vm_wiz_disk-image.PNG)

Name the virtual machine. Leave as default or choose the location to install VM files by selecting "Browse", selecting the directory, and clicking OK. Click on Next.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/name_vm.PNG)

### Setup the pfSense VM hard disk

Configure the Hard Disk as the default value 20GB and choose split virtual disk into multiple files and click on Next.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/virtual_disk.PNG)

### Assign the VM resources

Before you click on next, you need to click on the customize hardware option here.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/cust_hardware.PNG)

First change the default RAM size to 2048MB.

CPU – 2

Note: The PfSense VM will work just fine with 1024MB memory and 1CPU as well.

I configure the RAM and the CPU next lets go ahead and add the Network interfaces.

Connect two network interfaces that you configured earlier.

The first interface is already configured as NAT by default, we will change it to use it as a bridge interface that connects to the WAN, and I will add the second interface for the LAN.

#### Attach the WAN interface

Select the network interface that is configured as NAT, and change it to Bridge interface.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/add_wan.PNG)

#### Attach the LAN interface

Attach the LAN interface by clicking Add. The Add Hardware wizard now open.

Choose network adapter and Finish.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/add_lan_adapter.PNG)

For Network adapter two (LAN), I can choose a Host-only adapter which is by default configured as VMnet1 adapter and we have validated that in step1.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/add_lan_host-only.PNG)

Make sure you check the option which says, Power on this Virtual machine after creation. Click on Finish on the New virtual machine wizard.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/power-on_after_creation.PNG)

### PfSense installation

The pfsense installation now will begin. You can accept the copyright notice.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/accept-copyright.PNG)

Click on Install on the pfSense installer welcome screen.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/install_pfsense.PNG)

Select WAN interface and click OK. Leave network operation mode as default and select OK.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/select_wan.PNG)

Select LAN interface and click OK. Leave network operation mode as default and select OK.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/select_lan.PNG)

Note: Can find MAC of the interface under advanced settings in the network adapter settings of the VM.

Confirm interface Assign and continue.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/confirm_int_assign.PNG)

No active subscription for this lab, select Install CE

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/install-ce.PNG)

In the file system type and partitioning scheme step, leave defaults and select on OK to continue.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/disk_select.PNG)

Select OK for ZFS Virtual Device configuration to set to Stripe.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/zfs_vd.PNG)

Select OK for disk seection of previously configured 20G disk.

Select yes to destroy disk current contents.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/destroy_ok.PNG)

Select version of pfSense to install and select OK; I chose 2.8.0, as it is the current stable version recommended.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/version_to_install.PNG)

After few seconds the installation will now be completed, and you may select OK to continue. Go ahead and reboot the firewall.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/reboot.PNG)

After the reboot, you will be presented with the below screen, as you can see below the WAN interface got the DHCP IP address from my local network 192.168.2.24/24 and the LAN is configured with the default IP 192.168.1.1.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/after_reboot.PNG)

Let me ping the internet to see, whether I can reach the internet or not, so type the key 7 and enter the IP address that wanted to ping.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/ping_1.PNG)

And we can reach the internet VIA the WAN interface.

I personally like to manually configure the LAN side and will update the IP to 192.168.105.2. The .1 is usually assigned to the VNIC on your device created when you add the network in VMWare network editor.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/VNIC-LAN.PNG)

This can be done by selecting option 2 "Set interfaces IP address, Select available LAN interface, Select "n" for configuring via DHCP, Enter desired IP address.

Enter subnet mask, which is 24 is CIDR notation. Select enter for LAN, Select n to not configure IPv6 (unless desired), Select enter for no IPv6 address, and enable DHCP since it was disabled in the Virtual Network Editor for the LAN network.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/Assign-lan-ip.PNG)

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/assign-lan-ip_2.PNG)

Enter range for DHCP to assign; I chose 192.168.105.201-254.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/dhcp_range-lan.PNG)

### Setup the client machine

I have a Windows 10 test machine configured in VMware workstation using steps [here](/projects/lab_setup_instructions/Win10_setup.html); I will be using it as a client machine to test the end user connectivity on the PfSense LAN side.

Remember we have configured PfSense LAN side interface as Host-only network, go to the client operating system in VMware workstation and right-click on it and click on settings, add client VM to be part of Host-only network.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/lan_host_adapter.PNG)

Once the LAN side of the PfSense connected to the client operating systems, it should start getting IP addresses from the PfSense DHCP server on the LAN.

As you can see, the Windows 10 machine got the IP address 192.168.105.201

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/lan_host_ip.PNG)

### pfSense initial setup

As we have the IP address on both the Centos and the Linux mint, you now should be able to access the pfSense web GUI from either of the machine by typing the URL for your pfSense LAN IP. For me that would be https://192.168.105.2 

You would get a security warning, ignore that and click on continue.

You will be prompted to enter the credentials; the username is admin and the password is pfsense and click on Sign in.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/pfsense_login.PNG)

You will be taken to the initial setup wizard, since this is going to be the lab, I would choose the default options and eventually on the step 6 I would set the password for the web GUI.

Once reloaded you will be able to see the message Congratulations! pfSense is now configured. Click on Finish.

### Install VMware tools in pfSense

When you are using the any operating system on VMware workstation, it is recomeded that you install VMware tools to get best performance.  It is no different for the pfsense.

Click on system and package manager.

In the package manager, click on Available packages and search for VMware.

You should be able to see Open-VM-Tools appeared, click on Install.

When you get a prompt click on confirm under package installer.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/pfsense_vm-tools.PNG)

You will get a message that says, VMware tools package was successfully installed.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/pfsense_vm-tools2.PNG)

### Access the internet on Pfsense LAN side

Let’s try to access the internet on the machine that is connected to the pfSense LAN side.

To test the internet connectivity, I am going to ping the google DNS IP 8.8.8.8.

As you can see, I can reach the internet, and if you try to do a traceroute it shows the internet is via the pfSense firewall.

![Branching](https://nse-portfolio.github.io/assets/img/pfsense_install/lan_host_ping.PNG)



[Back](/projects/home_lab.html)