## RAID
RAID is a technology that combine multiple physical storage devices into a single logical unit to improve the performance, provide redundancy and both.

**RAID-0: (Stripping) (2 Disk Required)**</br>
- Performance increase
- How it works:- Data is split across multiple drivers
- Advantage:- High read and write speed
- Disadvantage:- No Redundancy. If one disk fails, all data lose.

**RAID-1: (mirroring) (2 Disk Required)**</br>
- Performance is slow compare to RAID-0
- How it works:- Same data will be store in both disk.
- Advantage:- If 1 disk failed we can recover the data from another disk.
- Disadvantage:- If two disk fail we cannot recover the data.

**RAID-5: (Striping+Parity)**
- Performance:- Reading and writing is very fast so its provide high performance.
- How it Works:- It is used stripping and Parity .
- Advantage :- If one disk is failed we can recover the data using remaining disk and parity.
- Disadvantage:- If two disk fails we can not recover the data.

