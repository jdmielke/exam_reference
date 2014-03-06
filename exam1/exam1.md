### Threads and Processes
  * Per process items: Address space, Global variables, Open files, Child processes, Pending alarms, Signals and handlers
  * Per thread items: Program counter, Registers, Stack, State

#### Threads
* Kernel space:
  * Bad:
    * Thread operations use system calls (expensive)
  * Good:
    * Can use addtl. hardware
    * System call will only block individual threads
* User space:
  * Bad:
    * System calls block all threads
    * Can't use addtl. hardware
  * Good:
    * OS doesn't have to know about threads
    * Thread operations are *fast*

#### Memory Layout
|               |Top        |          |         |          |    Bottom|
|---------------|-----------|----------|---------|----------|----------|
|               | **Stack** | **Heap** | **BSS** | **Data** | **Text** |
| **Contains**  | Local vars| Dynamic (malloc)  |Uninitialized globals| Initialized globals|  code |
| **Grows**     | Down       |  Up     | N/A     | N/A      | N/A      |

### Deadlock
  * A set of processes is deadlocked if each process in the set is waiting for an event that only another process in the set can cause.

#### Four conditions:
  * Mutual exclusion, hold and wait, no preemption, and circular wait

#### Four Solutions:
  1. **Ostrich Algorithm** - Ignore the problem
  2. **Detection** - Look at currently held and currently needed resources
    * If there is a cycle in the current dependency graph, there is a deadlock
  3. **Avoidance** - Check for potential deadlocks before granting resources
    * Not practical - too much overhead
  4. **Prevention** - Remove one of the four deadlock conditions
    * *Attack mutual exclusion:* Allow > 1 process to access a resource (Printer spooling)
    * *Attack hold and wait:* Require process to request resources before starting (might not have enough resources to run)
    * *Attack no preemption:* takes resources that are currently being used, from process that are using them.
    * *Attack circular wait:* use a resource graph
  
Semaphores
  how to use
  implementation details
      
OS Level Code:
  POSIX
    mutexes, conditional waits, etc.
  Basic
    chmod, read, write, lseek, etc.
