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
    * **_Turnaround_** *t$_{end}$ - t$_{queued}$* **_Response_** *t$_{response}$ - t$_{queued}$* **_Waiting_** *t$_{start}$ - t$_{queued}$* **_Throughput_** *completed per t$_{unit}$*
 * **Virtual Memory** Each process has own AS at run time | **_Goals:_** Protection and Management
    * **_Advantages_** Program can be larger than physical memory and run faster as long as pages are in memory
    * **_Structuring_** **Paging** fixed-size pages (_internal frag_) | **Segmentation** variable-size segs (_external frag_) | Hybrid
 * **Memory Management Unit (MMU):** Maps address space onto physical memory and 2ndary | Page faults if not in memory
 * **Page Table:** Mappings of virtual addresses to physical addresses | **_Conversions_** 1 KB = 2$^{10}$ bytes | 1 MB = 2$^{20}$ bytes
    * **_Uniqueness_** *Virtual addresses* are unique to accessing process | *Physical addresses* are unique to hardware
    * **_Page Size_** e.g. Given 32-bit space, 8KB pages, 4 bytes/entry: 2$^{32}$(addresses)/2$^{13}$(pages) = 2$^{19}$ entries * 2$^2$(entry) = 2$^{21}$ bytes
    * **_Translation Process:_** Find virtual page frame and virtual page offset | Map to physical page frame | Add Add offset to physical location in referenced physical page frame
    * *e.g.* 4KB pages, virtual address 5000: virtual page frame = $\frac{5000}{2^{12}} = 1$ | virtual page offset = $5000\bmod 2^{12}$ = 904 | Mapped to frame 2(e.g.) | Frame 2 holds location 4(e.g.) | Location = $2^2 \times 2^{12}$
    * *e.g.* With 48-bit VA and 32-bit PA, how many entries if pages are 8 KB? | $\frac{2^{48}}{2^{13}} = 2^{35}$ entries
    * *e.g.* 32-bit v_address using 2-level page table. VA is split into a 9-bit top field and 11-bit 2nd field. Find page size and page entries | Page size = $\frac{2^{32}}{2^{20}} = 2^{12} = 4KB$ | Entries = $2^{20}$
    * **_Types_** | **Page Table** Popular | **TLB** Performance | **Inverted** Large AS | **Multi Level** Large AS, bad page access time
    * **_Location_** **Registers** Fast trans, small tables, expensive switch | **Memory** Slow trans, large tables, pointer for location & size, quick switch
    * **_Copy on Write_** Processes given pointer to same resource | When changed, a local copy is then made to use
 * **TLB** Associative Register | Small cache of recently used mappings | Improves translation speed
    * **_Average Access Time_** = $2m + \epsilon - \alpha m$, where $\alpha$ = TLB hit ratio, $m$ = memory access time in ms and $\epsilon$ = TLB search time in ms
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
    * **_Working Set of a Process_** Reduces thrashing | Set of referenced pages in the last k memory references
    * *e.g.* Find k-references at $t = 6$ with $k = 3$ | t: 0 1 2 3 4 5 6 7 8 9 and page #: 1 1 2 2 1 3 1 1 4 5 | $w(3, 6) = \{1,3\} |w(3,6)| = 2$
 * **Files: Permissions:** rwx(**user**)rwx(**groups**)rwx(**others**)
    * **_Opening_** Ret file descrip**_Reading_** Ret # bytes read | **_Writing_** Returns # of bytes written | **_Seeking_** Returns new file pointer
    * **_whence_** *offset* (SEEK_SET), *current + offset* (SEEK_CUR), *size of file* (SEEK_END) 
 * **Block Placement Schemes:**
    * **_Cont Alloc_** Sequential alloc | *Pros* fast read, easy tracking, #1 for read-only | *Cons* frags with dels, file growth expensive
    * **_Linked List_** *Pro* Sequential access is fast | *Con* Random access is slow
    * **_FAT_** One entry per physical disk block | Can be in main memory | Simple and robust
    * **_UNIX Version inodes_** i-nodes | owner & group | timestamps | size |  Direct blocks | Single indirect | Double indirect | Triple indirect
    * *e.g.* System has 1 KB blocks and 4-bytes addresses. What is max file size? | entires = $\frac{2^{10}}{2^2} = 2^8$ | direct = 10 ptrs, single = 256 ptrs, double = 256$^2$ ptrs and triple = 256$^3$ ptrs which sum to 16.06 GB
 * **Shared Files:** **_Hard Links:_** Both files point to same inode | **_Symbolic Links:_** Files point to different inodes
    * **
 * **Buffer Caches:** Disk keeps reading sectors ahead of requested sector and saves to buffer cache, in case the OS requests them later
    * **_Write-back Cache_** Write to cache and return; write to disk is done later | Most efficient
    * **_Write-through Cache_** Write to cache, schedule a write to disk and return | Most reliable
    * **_Exceptional Cases_** Write to cache, do a synchronous (blocking) write to disk, and return
    * **_Replacement Algos_** LRU | Sorted listed by time of use
 * **Disk Scheduling:** **_Goals:_** Trade-off between throughput and response time
    * **_FCFS_** **Pro:** Quick response time | **Cons:** No regard for throughput and head may move almost randomly across disk surface
    * **_SSTF_** Closest to current head position | **Pro:** Minimized head movement time | **Con:** Starvation of far reads
    * **_SCAN_** Sweep from outer to inner and back | Selects those that are in path | Lower movement time that FCFS | Fairer than SSTF
    * **_LOOK_** SCAN but will change direction if no waiting requests beyond current cylinder
    * **_C-SCAN_** SCAN but from innter to outer and back to inner without satisfying any requests
    * **_Page Replacement e.g._** Which page will be replaced by: a) NRU = 2b) FIFO = 3 c) LRU = 1 d) 2nd Chance = 2 Given:
\begin{table}[h]
\begin{tabular}{c c c c c}
Page & Loaded & Last ref. & R & M \\
0 & 126 & 280 & 1 & 0 \\
1 & 230 & 265 & 0 & 1 \\
2 & 140 & 270 & 0 & 0 \\
3 & 110 & 285 & 1 & 1 \\
\end{tabular}
\end{table}
    
