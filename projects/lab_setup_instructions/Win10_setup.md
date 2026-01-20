---
layout: default
---

# Windows 10 Test Machine in VMWare Workstation

* * *

This guide is for installing a Windows 10 machine in VMware Workstation.

## Quick Links
--------------------------------------

- [Prerequisites](#prerequisites)
- [Steps to install Windows 10 on VMware](#steps-to-install-windows-10-on-vmware)
- [Setting up VMWare Workstation](#setting-up-vmware-workstation)
- [Installing Windows](#installing-windows)
- [Post Installation Configuration](#post-installation-configuration)


## Prerequisites
-------------------------------------

* You need to have VMware workstation pro.

I am using VMware workstation 17 and have a guide to install [here](/projects/lab_setup_instructions/vmware_workstation_setup.html).

* Windows 10 ISO image.

You can download the Windows 10 image from [here](https://www.microsoft.com/en-us/software-download/windows10), make sure you choose AMD64, DVD image(iso) installer.

## Steps to install Windows 10 on VMWare
-------------------------------------

### Setting Up VMware Workstation
-------------------------------------

#### 1. Open VMware Workstation 17 Pro

* Launch VMware Workstation after installation.

#### 2. Create a New Virtual Machine

* Click on "Create a New Virtual Machine."

* Choose between the Typical (recommended) or Custom configuration. For beginners, Typical is usually the easiest option.

#### 3. Select the Installation Media

* Choose "Installer disc image file (iso)" and browse to the location where you saved your Windows 10 ISO file.

#### 4. Select a Guest Operating System

* Choose Microsoft Windows as the guest operating system and select Windows 10 from the version dropdown. Click Next.

#### 5. Name the Virtual Machine

* Give your VM a name and choose the location for storing the VM files. Ensure that you have enough local disk space available.

#### 6. Specify Disk Capacity

* Enter the maximum disk capacity. It is recommended to allocate at least 64 GB to accommodate the operating system and applications. Choose whether to store the virtual disk as a single file or split it into multiple files. Single files generally perform better.

#### 7. Customize Hardware (Optional)

* Click on Customize Hardware to allocate resources such as RAM, CPU cores, and network preferences.

* Memory: For Windows 10, at least 4 GB is required. However, if your host allows, allocate 8 GB or more for better performance.

* Processors: Allocate at least 2 cores for a smoother experience.

* Network Adapter: Set it to NAT or Bridged based on your network configuration.

* Ensure that the "Accelerate 3D graphics" option is enabled for graphic-intensive applications.

* If TPM is required, you can add a Trusted Platform Module through the hardware settings.

#### 8. Finish Configuration

* Once configured, click Close, then Finish to create your virtual machine.

### Installing Windows
-------------------------------------

#### 1. Power On the VM

* Select your newly created VM from the library and click on Power on this virtual machine.

Note: There is a bug and you will need to press any key quickly or it will time out. This is documented [here](https://community.broadcom.com/vmware-cloud-foundation/communities/community-home/digestviewer/viewthread?MessageKey=c1905a94-129f-404f-8bb0-31e144a21f7f&CommunityKey=fb707ac3-9412-4fad-b7af-018f5da56d9f). There is also option to open the .VMX file of your virtual machine in Notepad (or similar) and add or change firmware="efi" to firmware="bios" and Save the .VMX file.

#### 2. Run the Installation

* The VM will boot from the Windows 10 ISO. Follow the on-screen instructions to initiate the installation process.

* Choose your language, time, and keyboard preferences, then click Next.

#### 3. Start Windows Setup

* Click on Install Now.

* If prompted, enter your Windows 10 product key. You can skip this step if you want to enter the key later.

#### 4. Select the Operating System

* Accept the license terms and click next.

* Choose the "Custom: Install Windows only (advanced)" option. This will allow you to select where to install Windows 10.

#### 5. Partitioning

You can create new partitions or select the unallocated space and click Next. The installer will create the necessary partitions and begin installing Windows 10.

#### 6. Installation Process

The installation will take some time and may restart your virtual machine several times. At this point, let the process run its course.

#### 7. Setting Up Windows 10

* Once installed, you’ll be greeted with the setup screen. Follow the prompts, including selecting a region and connecting to a network.

* If you selected to use a Microsoft account, enter your details, or create a local account if preferred.

* Set up privacy settings, such as location tracking, diagnostics, etc.

#### 8. Finalizing Installation

* Wait for the setup to complete, and you’ll be directed to the Windows 10 desktop.

### Post Installation Configuration

Once you’re on the Windows 10 desktop, there are several configurations you might want to consider:

#### 1. Install VMware Tools

VMware Tools improves performance and usability. To install it:

* In the VMware menu at the top, go to VM > Install VMware Tools.

* This will mount the VMware Tools ISO in the VM. Open File Explorer and locate the mounted disk.

* Run setup.exe and follow the on-screen instructions to install VMware Tools.

* Restart the VM once VMware Tools is successfully installed.

#### 2. Adjust Display Settings

* After installing VMware Tools, you can adjust the display resolution to match your screen better.

* Right-click on the desktop, select Display settings, and define the recommended resolution.

#### 3. Network Configuration

* Ensure that your network settings are functioning correctly. Test connectivity by browsing the web.

* Adjust network settings in VMware if necessary, depending on whether you prefer Bridged, NAT, or Host-only networking.

#### 4. Backup Your Virtual Machine

* To avoid losing your setup, consider creating a backup of the virtual machine. You can copy the entire VM folder or take snapshots in VMware Workstation.

#### 5. Install Updates

* Open Settings > Windows Update, and check for updates to ensure you have the latest security patches and features.

* * *

[Back](/projects/home_lab.html)