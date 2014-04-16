### Running Process States
 * Running | Ready | Blocked

#### Scheduling | Minimize: response time and switch overhead | Maximize: throughput and CPU utilization | Be fair
 * **(FCFS)** Non-preemptive | Schedule first in queue | Pro: Easy to implement | Con: Slow for mix of short/long jobs
 * **(SJF)** Non-preemptive | As the name says, schedule shortest job in queue to run | Pro: Easy to implement
 * **(SRTN)** Preemptive | SJF with preemption | Cons: Can starve long jobs if many short jobs enter queue
 * **(RR)** Cycle through queue | Too Small Quantum: High context switch overhead | Too Large Quantum: Bad response times
 * **(Priority-(Prio)** Preemptive/Non | Jobs w/ top prio first | Issues: Starve lower prio | Sol: Decrease prio over time
 * **(Multiple Queues - Static)** Prime example of priority scheduling | Starvation solution: Time slice between queues
 * **(Multiple Queues - Dynamic)** Lower prio if after 1 quantum | Pro: Reduce switches for long jobs
 * **(Lottery)** Give out "tickets" based on priority | Winner gets a quantum of run time | Pro: Probabilistic guarantees
 * **(Real-Time)** Provide time guarantees | Soft: Can reschedule (mp3) | Hard: Is lost if missed (Air-traffic controller)
 * **Exponential Averaging** guess = a(new_data) + (1 - a)(previous_guess), where a is weight given to new data

### Algorithm Goals | Impossible to satisfy all at the same time
 * **Turnaround time (Part of Latency)** Total time between submission of a process and its completion
 * **Response time (Part of Latency)** Amount of time it takes from when a request was submitted until gives a response
 * **Throughput** Total number of processes that complete their execution per time unit
 * **Waiting time** The time the process remains in the ready queue

### Virtual Memory | Each process own set of addresses that the program generates at run time
 * **Goals** Proctect processes from others | Protect OS from user processes | Provide efficient management of storage
 * **Advantages** Program can be larger than physical memory and run faster as long as pages are in memory
 * **Structuring** Paging: fixed-size pages (intneral frag) | Segmentation: variable-size segs (external frag) | Hybrid
 * **_TODO_** **Generate Physical Address** 

### Memory Management Unit (MMU) Maps address space onto physical memory and 2ndary | Page faults if not in memory

### Page Table | Mappings of virtual addresses to physical addresses
 * **Uniqueness** Virtual addresses are unique to accessing process | Physical addresses are unique to hardware
 * **_TODO_** Determine parameters (size, offset, page size, etc.)
 * **Types** | Page Table: Most popular | TLB: Improves performance | Inverted: Large address spaces

### TLB | Stores a cache of recently used mappings | Improves virtual address translation speed

### Translation Process | Search TLB | If TLB Miss: Search Page Table | If Page Fault: Load from disk

### Memory Management | First fit: **_TODO_** | Best fit: **_TODO_** | Worst fit: **_TODO_**

### Page Replacement Algos
 * FIFO
 * NRU
 * Second Chance
 * Clock
 * LRU

### Working Set
 * Calculate


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
