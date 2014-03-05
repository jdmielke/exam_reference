### Threads and Processes

Per process items: Address space, Global variables, Open files, Child processes, Pending alarms, Signals and signal handlers, Accounting information
Per thread items: Program counter, Registers, Stack, State
  
    location
  Threads
    Implementation details for user space vs kernal space

#### Memory Layout

|               |Top        |          |         |          |    Bottom|
|---------------|-----------|----------|---------|----------|----------|
|               | **Stack** | **Heap** | **BSS** | **Data** | **Text** |
| **Contains**  | Local vars, function params | Dynamic vars (malloc) | Uninitialized static/global vars | initialized static/global vars | program code |
| **Grows**     | Down       |  Up     | N/A     | N/A      | N/A      |



Mutex
  When, where, why
  
Stack
    ???
    
### Deadlock
  will lock, or not to lock?

  *Definition*: A set of processes is deadlocked if each process in the set is waiting for an event that only another process in the set can cause.

#### Four conditions:

  1. Mutual exclusion
  2. Hold and wait condition
  3. No preemption condition
  4. Circular wait condition
  
Semaphores
  how to use
  implementation details
      
OS Level Code:
  POSIX
    mutexes, conditional waits, etc.
  Basic
    chmod, read, write, lseek, etc.
