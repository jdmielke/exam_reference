 * **Running Process States:** Running | Ready | Blocked
 * **Scheduling:** Minimize: response time and switch overhead | Maximize: throughput and CPU utilization | Be fair
    * **_FCFS_** Non-preemptive | Schedule first in queue | **Pro** Easy to implement | **Con** Slow for mix of short/long jobs
    * **_SJF_** Non-preemptive | As the name says, schedule shortest job in queue to run | **Pro** Easy to implement
    * **_SRTN_** Preemptive | SJF with preemption | **Cons** Can starve long jobs if many short jobs enter queue
    * **_RR_** Cycle through queue | **Too Small Quantum** High context switch overhead | **Too Large Quantum** Bad response times
    * **_Priority-(Prio)_** Preemptive/Non | Jobs w/ top prio first | **Issues** Starve lower prio | **Sol** Decrease prio over time
    * **_Multiple Queues - Static_** Prime example of priority scheduling | **Starvation solution** Time slice between queues
    * **_Multiple Queues - Dynamic_** Lower prio if after 1 quantum | **Pro** Reduce switches for long jobs
    * **_Lottery_** Give out "tickets" based on priority | Winner gets a quantum of run time | **Pro** Probabilistic guarantees
    * **_Real-Time_** Provide time guarantees | **Soft** Can reschedule (mp3) | **Hard** Is lost if missed (Air-traffic controller)
    * **_Exponential Averaging_** guess = a(new_data) + (1 - a)(previous_guess), where a is weight given to new data
 * **Algorithm Goals:** Impossible to satisfy all at the same time
    * **_Turnaround_** *t<sub>end</sub> - t<sub>queued</sub>* **_Response_** *t<sub>response</sub> - t<sub>queued</sub>* **_Waiting_** *t<sub>start</sub> - t<sub>queued</sub>* **_Throughput_** *completed per t<sub>unit</sub>*
 * **Virtual Memory** Each process own set of addresses that the program generates at run time
    * **_Goals_** Protect processes from others | Protect OS from user processes | Provide efficient management of storage
    * **_Advantages_** Program can be larger than physical memory and run faster as long as pages are in memory
    * **_Structuring_** **Paging** fixed-size pages (_internal frag_) | **Segmentation** variable-size segs (_external frag_) | Hybrid
    * **_TODO_** **_Generate Physical Address_** 
 * **Memory Management Unit (MMU):** Maps address space onto physical memory and 2ndary | Page faults if not in memory
 * **Page Table:** Mappings of virtual addresses to physical addresses | **_Conversions_** 1 KB = 2<sup>10</sup> bytes | 1 MB = 2<sup>20</sup> bytes
    * **_Uniqueness_** *Virtual addresses* are unique to accessing process | *Physical addresses* are unique to hardware
    * **_TODO_** Determine parameters (size, offset, page size, etc.)
    * **_Page Size_** e.g. Given 32-bit space, 8KB pages, 4 bytes/entry: 2<sup>32</sup>(space)/2<sup>13</sup>(pages) = 2<sup>19</sup> entries * 2<sup>2</sup>(entry) = 2<sup>21</sup> bytes
    * **_Types_** | **Page Table** Popular | **TLB** Performance | **Inverted** Large AS | **Multi Level** Large AS, bad page access time
    * **_Location_** **Registers** <sub>Fast trans, small tables, expensive switching </sub> | <sub>**Memory** Slow trans, large tables, pointer for location and size, quick switching</sub>
    * **_vfork()_** Parent AS not copied | Parent AS given to child | Parent suspended until child returns AS | Child does exec
    * **_Copy on Write_** Processes given pointer to same resource | When changed, a local copy is then made to use
 * **TLB** Associative Register | Small cache of recently used mappings | Improves translation speed
    * **_Average Access Time_** = $2m + \epsilon - \alpha m$, where $\alpha$ = TLB hit ratio, $m$ = memory access time in ms and $\epsilon$ = TLB search time in ms
 * **Translation Process:** Search TLB | If TLB Miss: Search Page Table | If Page Fault: Load from disk
 * **Memory Management:** First fit: **_TODO_** | Best fit: **_TODO_** | Worst fit: **_TODO_**
 * **Page Replacement Algos:**
    * **_FIFO_** Easy to implement | Not a good policy
    * **_NRU_** _Classes_: _0_:R=0,M=0 _1_:R=0,M=1 _2_:R=1,M=0 _3_:R=1,M=1 | Remove random from lowest class | R cleared periodically
    * **_Second Chance_** FIFO ordering | If R=0, evict | If R=1, move to end of list and set R=0
    * **_Clock_** Similar to 2nd Chance | Circular list,no overhead of moving, just reset R | Can be used with NRU, reset R & M
    * **_LRU_** Replace page unused for longest time | Locality of Reference: Pages used in near past will be used in near future
    * **_Implementations_** List: Moving overhead | Time of Access: Searching overhead
    * **_NFU_** Each page access, counter incremented | Randomly evict page with lowest counter
    * **_Aging_** NFU combined with LRU | Accounts for time and frequency by shifting to the right and adding one to MSB
    * **_Optimal_** Evict page used furthest in the future
 * **Page Frame Allocation: Global:** All processes complete for pages | **Local** Equal or Proportional allocation
    * **_Thrasing_** A program causing page faults every few instructions
    * **_Working Set of a Process_** Reduces thrashing | Set of references pages in the last k memory references
 * **Files: Permissions:** rwx(**user**)rwx(**groups**)rwx(**others**)
    * **_Opening_** int open(const char *pathname, int flags, mode t mode); | returns file descriptor | Use dup to open same file
    * **_Flags_** *read only* (O_RDONLY), *write only* (O_WRONLY), *read and write* (O_RDWR)
    * **_Reading_** ssize t read(int fildes, void *buf, size t count); | returns # of bytes transferred | 0 for end | -1 for error
    * **_Writing_** ssize t write(int fildes, const void *buf, size t count); | returns # of bytes transferred | -1 for error
    * **_filedes_** *standard input* (0), *standard output* (1), *standard error output* (2)
    * **_Seeking_** off t lseek(int fildes, off t offset, int whence); | returns updated value of file pointer relative to beg
    * **_whence_** *offset* (SEEK_SET), *current + offset* (SEEK_CUR), *size of file* (SEEK_END) 
 * **Block Placement Schemes:**
    * **_Cont Alloc_** Sequential alloc | *Pros* fast read, easy tracking, #1 for read-only | *Cons* frags with dels, file growth expensive
    * **_Linked List_** *Pro* Sequential access is fast | *Con* Random access is slow
    * **_TODO_** **_FAT_** One entry per physical disk block | Can be in main memory
    * **_TODO_** **_UNIX Version_** 
 * **_TODO_** **Shared Files:**
 * **_TODO_** **Buffer Caches:** Read disk into memory until no longer needed
    * **_Write-back Cache_** Write to cache and return; write to disk is done later | Most efficient
    * **_Write-through Cache_** Write to cache, schedule a write to disk and return | Most reliable
    * **_Exceptional Cases_** Write to cache, do a synchronous (blocking) write to disk, and return
    * **_Replacement Algos_**
 * **_TODO_** **Disk Scheduling:**

 * **Sample code:**

```c
int main() {
    write(1, buf, sizeof(buf));
}
```
