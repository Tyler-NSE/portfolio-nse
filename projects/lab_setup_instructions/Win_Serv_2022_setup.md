---
layout: default
---

## Download Windows Server 2022 ISO
-----------------------------------

Windows server 2022 ISO can be downloaded [here](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022). When downloading, you can insert any information you want in the form but it does require a valid email.

Choose the 64 bit ISO edition.

![Branching](https://gt-legend.github.io/assets/img/win_serv-2022/iso_download.PNG)

## Create the Windows Server 2022 Virtual Machine
-------------------------------------------------

#### 1. Open VMware Workstation 17 Pro

* Launch VMware Workstation after installation.

#### 2. Create a New Virtual Machine

* Click on "Create a New Virtual Machine."

* Choose between the Typical (recommended) or Custom configuration. For beginners, Typical is usually the easiest option.

#### 3. Select the Installation Media

* Choose "Installer disc image file (iso)" and browse to the location where you saved your Windows Server 2022 ISO file.

![Branching](https://gt-legend.github.io/assets/img/win_serv-2022/disk_image.PNG)

#### 4. Easy Install Information

* No product key is needed for now, as this is a demo version. Enter a username and password (if desired). Click Next.

![Branching](https://gt-legend.github.io/assets/img/win_serv-2022/product_key.PNG)

#### 5. Name the Virtual Machine

* Give your VM a name and choose the location for storing the VM files. Ensure that you have enough local disk space available.

![Branching](https://gt-legend.github.io/assets/img/win_serv-2022/name_vm.PNG)

#### 6. Specify Disk Capacity

* Enter the maximum disk capacity. It is recommended to allocate at least 60 GB to accommodate the operating system and applications. Choose whether to store the virtual disk as a single file or split it into multiple files. Single files generally perform better.

![Branching](https://gt-legend.github.io/assets/img/win_serv-2022/disk_cap.PNG)

#### 7. Customize Hardware (Optional)

* Click on Customize Hardware to allocate resources such as RAM, CPU cores, and network preferences.

* Memory: For Windows Server 2022, at least 2 GB is required. I went with 4GB for better performance.

* Processors: Allocate at least 2 cores for a smoother experience.

* Network Adapter: Set it based on your network configuration. I set to VMnet1, as this is my host only network for my lab servers.

#### 8. Finish Configuration

* Once configured, click Close, then Finish to create your virtual machine.

### Installing Windows Server 2022
----------------------------------

#### 1. Power On the VM

* Select your newly created VM from the library and click on Power on this virtual machine.

Note: I ran into a bug when powering on for the first time I booted the VM. I had to power down the VM, remove the floppy drive, and power back on. Error I got was ""Windows Cannot Find the Microsoft Software License Terms".

#### 2. Run the Installation

* The VM will boot from the Windows Server 2022 ISO. Follow the on-screen instructions to initiate the installation process.

* I chose the standard desktop version to include the GUI interface, as well as the customer installation.

* At Customize sessings prompt, enter a password for the built in administrator account and click Finish.

![Branching](https://gt-legend.github.io/assets/img/win_serv-2022/custom_settings.PNG)

#### 3. Start Windows Setup

* * *

[Back](/projects/home_lab.html)