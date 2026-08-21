# Experiment 1: Installation of Windows Operating System

## Ex. No: 1

### Aim
To install the Windows Operating System on a computer using bootable installation media and verify its successful operation.

### Procedure

#### Step 1: Create Bootable Installation Media
1. Download the Windows ISO image from the official Microsoft website.
2. Insert a USB flash drive (minimum 8 GB capacity).
3. Use a bootable media creation tool (such as Windows Media Creation Tool or Rufus) to create a bootable USB.

#### Step 2: Configure Boot Settings
1. Insert the bootable USB drive into the target computer.
2. Restart the system and press the designated function key (`F2`, `F12`, `DEL`, or `ESC`) to enter BIOS/UEFI setup.
3. Set the USB drive as the primary (first) boot device in boot options.
4. Save settings (`F10`) and restart the computer.

#### Step 3: Install Windows
1. Boot the computer from the USB drive.
2. Select language, time/currency format, and keyboard input method. Click **Next**.
3. Click **Install Now**.
4. Enter the product key if available (or click "I don't have a product key" to activate later).
5. Accept the license terms and click **Next**.
6. Select **Custom: Install Windows only (advanced)**.
7. Select or create the primary partition for installation.
8. Click **Next** to start the installation process.

#### Step 4: Initial Configuration
1. Wait for installation, file copying, feature installation, and automatic system restarts to complete.
2. Configure region and keyboard settings.
3. Create a primary user account name and password.
4. Configure privacy settings and network connectivity options.

#### Step 5: Verification
1. Log in to the newly installed Windows environment.
2. Open Windows Command Prompt (`cmd`) or PowerShell.
3. Execute system verification commands to check OS build, hardware details, and network configurations.

---

### Commands Used for Verification

#### 1. Display Windows Version
```cmd
winver
```

#### 2. Display Detailed System Information
```cmd
systeminfo
```

#### 3. Display Computer Hostname
```cmd
hostname
```

#### 4. Display Disk Information
```cmd
diskpart
list disk
exit
```

#### 5. Check Windows Activation Status
```cmd
slmgr /xpr
```

#### 6. Display IP and Network Configuration
```cmd
ipconfig /all
```

---

### Sample Verification Output

```text
C:\Users\Student> hostname
DESKTOP-OSLAB01

C:\Users\Student> winver
[System Dialog: Microsoft Windows 11 / Version 22H2 (OS Build 22621.1778)]

C:\Users\Student> systeminfo

Host Name:                 DESKTOP-OSLAB01
OS Name:                   Microsoft Windows 11 Pro
OS Version:                10.0.22621 N/A Build 22621
OS Manufacturer:           Microsoft Corporation
OS Configuration:          Standalone Workstation
OS Build Type:             Multiprocessor Free
Registered Owner:          Student
System Type:               x64-based PC
Processor(s):              1 Processor(s) Installed.
                           [01]: Intel64 Family 6 Model 158 Stepping 10 GenuineIntel ~3000 Mhz
Total Physical Memory:     8,192 MB
Available Physical Memory: 5,420 MB
Network Card(s):           1 NIC(s) Installed.
                           [01]: Realtek PCIe GbE Family Controller

C:\Users\Student> diskpart
Microsoft DiskPart version 10.0.22621.1

DISKPART> list disk

  Disk ###  Status         Size     Free     Dyn  Gpt
  --------  -------------  -------  -------  ---  ---
  Disk 0    Online          238 GB      0 B        *

DISKPART> exit

C:\Users\Student> slmgr /xpr
[System Dialog: Windows(R), Professional edition: The machine is permanently activated.]

C:\Users\Student> ipconfig /all

Windows IP Configuration

   Host Name . . . . . . . . . . . . : DESKTOP-OSLAB01
   Primary Dns Suffix . . . . . . . : 
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No

Ethernet adapter Ethernet:

   Connection-specific DNS Suffix  . : localdomain
   IPv4 Address. . . . . . . . . . . : 192.168.1.105(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.1.1
```

---

### Inference
- The Windows Operating System was successfully installed using bootable USB installation media.
- System configuration settings were completed successfully.
- The installed operating system was verified using native Windows command-line utilities.
- Hardware, disk partitions, and network configurations were detected correctly by the operating system.

### Result
Thus, the Windows Operating System was successfully installed and configured on the computer. The installation was verified using system commands, and the system was found to be functioning properly.
