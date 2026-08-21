# Experiment 1: Installation of Windows Operating System

## Commands

```cmd
winver
systeminfo
hostname
diskpart
list disk
exit
slmgr /xpr
ipconfig /all
```

## Output

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
