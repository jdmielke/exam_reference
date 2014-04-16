### Running Process States

#### Scheduling
 * FCFS
 * SFJ
 * SRTN
 * RR
 * Priority Lottery

### Algorithm Goals
 * Response time
 * Throughput

### Address Space

### Virtual Address
 * Generate a physical address

### Page Table
 * Store the mapping between virtual addresses and physical addresses.
  * Virtual addresses are unique to accessing process
  * Physical addresses are unique to hardware
 * Determine parameters (size, offset, page size, etc.)

### Page Replacement
 * FIFO
 * NRU
 * Second Chance
 * Clock
 * LRU

### Working Set
 * Calculate

### TLB
 * Improves virtual address translation speed

### File Descriptors
 * Opening
 * Reading/Writing
 * Seeking

### Block Placement Schemes
 * Contiguous Allocation
 * Linked List
 * FAT
 * UNIX Version

### Shared Files

### Buffer Caches
 * Read disk into memory until no longer needed
 * Writing
  * Write-back Cache: Write to cache and return; write to disk is done later
   * Most efficient
  * Write-through Cache: Write to cache, schedule a write to disk and return
   * Most reliable
  * Exceptional Cases: Write to cache, do a synchronous (blocking) write to disk, and return
 * Replacement Algos

### Disk Scheduling

### Sample code:

```c
int main() {
    write(1, buf, sizeof(buf));
}
```
