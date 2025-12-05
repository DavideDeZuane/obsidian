
**Tags**: #kernel
Status: #child 

---
# Introduction

One of the main tasks of the Kernel is *process management*.
This because the goal of the Operating System is provide an efficient and controlled **execution environment** in which process can be:

- **Created and Terminated**: we'll discuss the management of a process's life cycle.
- **Scheduled**: to manage the coexistence of multiple processes.
- **Synchronized**: to coordinate concurrent access to resources and prevent race conditions or deadlocks.

The kernel exists precisely to hide the complexity of the hardware system and provide processes with a standardized and secure environment, so that they can perform their tasks (*application logic*) without worrying about directly controlling the machine.

# Timeline of the Evolution of the Process Concept 

Let's take a look at some history and how we arrived at the concept of process as we understand it today. Some references:
- [Wikipedia](https://en.wikipedia.org/wiki/Timeline_of_computing_1950%E2%80%931979)
- [Computer History Museum](https://www.computerhistory.org/timeline/1950/)

## The 1950 s
- *Computer type*: first generation mainframe, programmed via punched cards.
- *Execution model*: `single-program execution`, only one program in memory at a time. Programs were loaded directly into memory and executed from start to finish without interruption.
- *Kernel*: absent. The hardware executed the program directly without any abstraction and no mechanism for interrupting or suspending execution.

>No conceptual distinction between **program** (code) and **execution** (state). 
>They were a single entity.

## Early 1960 s
- *Computer type*: more advanced mainframes with first forms of I/O automation.
- *Execution model*: `batch processing`, programs (jobs) executed sequentially in an automated manner. Still sequential execution: one job in the CPU at a time.
- *Kernel*: emergence of the **control monitor** (`proto-kernel`). Which manages job loading, starting, and termination. Still no management of execution contexts or complex interrupts.

>The distinction between job description and program code begins to emerge.

## Mid 1960 s
- *Computer type*: Systems with **interrupt support**, basic protection mechanisms, and more advanced memory management.
- *Execution model*: `Multiprogramming`, multiple jobs reside in memory simultaneously. Now the system can suspend a job waiting for I/O and execute another. Emergence of the `execution context` concept (savable state).
- *Kernel*: now has a more complex role. Interrupt handling, saving/restoring job state. Introduction of job tables, precursor of Process Control Block (PCB).

>**Interleaved concurrency**: multiple jobs progress alternately, not simultaneously. Preemption only occurs due to I/O, not time slicing.

## The 1970 s
- *Computer type*: `Multiuser` systems with multiple connected terminals.
- *Execution model*: `Time-sharing` with preemption via timers. Each process gets a CPU time slice in this way Real-time user interaction is supported.
- *Kernel*: Emergence of the modern kernel: preemptive scheduler, dual mode, IPC, fully structured PCB. Kernel becomes the central manager of execution contexts and system resources.

>Now we have **True concurrency**, time-based and kernel-managed. Multiple processes “active” simultaneously, thanks to fast context switching. **Clear distinction between program and process**: a program is static code, while a process is an active execution context with its own state, memory, and resources.




# Tasks Details

Vediamo nel dettaglio quelli che sono i task per poter gestire i processi