## Boot Process :
The Boot Process is a sequence of steps a computer follows to start up and load the operating system into memory when you turn it on .

**1. BIOS:**
- Basic I/O system 
- First program that execute which is stored in the read-only-memory on the motherboard of the computer.
- Perform POST (Power on self test) verify the hardware components .
- Then check for the bootable device like: PAN Drive, HDD, etc.

Then handover control to the first sector of bootable device i.e; MBR

**2. MBR:**
- Master Boot Record
- Its size is 512 bytes, first sector of any bootable device contain the machine code instruction to boot the machine and having following info
  - Boot Loader (446 bytes)
  - Partition table (64 bytes)
  - Error checking (2 bytes)
- It will load the bootloader into memory and handover control to it. 

**3. GRUB:**
- Grand Unified Bootloader
- Load /boot/grub2/grub.conf at boot time.
- At this stage , user can see GUI asking for different OS or Kernels configured to boot.
- Main job is to load the Kernel and initrd/initramfs images into memory.
- Once load the kernel into memory , it passes control to it.

**4. KERNEL:**
- First kernel loaded into read-only-mode.
- Initrd/Initramfs get decompressed and then it load the temporary file system.
- Initrd then detect and load the drivers from temporary file system to actual filesystem.
- mount the other partition like LVM, RAID, etc and unmount itself.
- Once filesystem is mounted , kernel initialize the first process init/systemd.

**5. SystemD:**
- First service loaded with PID-1.
- Starts all required process /etc/systemd/system/default.target
- To bring the system to the run level (0-6).





## Questions From Boot Process.
1. What is GNU GRUB?</br>
   GRUB is a bootloader used in Linux systems.
- Its responsibilities are:
  - Load Linux kernel into memory
  - Load initramfs
  - Provide boot menu
  - Pass control to kernel

2. What is initramfs?</br>
initramfs is a temporary root filesystem loaded into RAM during boot.
- Purpose:
  - Load essential drivers/modules
  - Detect storage devices
  - Mount actual root filesystem
  - Help kernel complete booting

3. Difference Between BIOS and UEFI ? </br>
   | BIOS             | UEFI                     |
   | ---------------- | ------------------------ |
   | Older firmware   | Modern firmware          |
   | Uses MBR         | Uses GPT                 |
   | Slower           | Faster                   |
   | Limited features | Supports Secure Boot     |
   | Text interface   | Better graphical support |

4. What is systemd?</br>
   systemd is the init system and service manager in modern Linux distributions.</br>

**It:**
   - Starts services
   - Manages processes
   - Handles boot targets
   - Controls system startup/shutdown

5. How Do You Troubleshoot Boot Failure?</br>
1. Check error message on screen.
2. Boot using older kernel from GRUB.
3. Boot into rescue/emergency mode.
4. Check /etc/fstab entries.
5. Verify disk and filesystem.
6. Rebuild initramfs if corrupted.
7. Reinstall/recover GRUB if needed.
8. Check logs using journalctl and dmesg.