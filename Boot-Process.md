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
