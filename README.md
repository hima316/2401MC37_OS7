# Assignment 7: Kernel Multithreading, Semaphores, Deadlock Analysis, and Priority Scheduling in xv6

## Overview

### Question 1: User-Level & Kernel-Supported Threads (`threadtest.c`)
Implements kernel-supported multithreading in xv6 by introducing `clone()` and `join()` system calls. The `clone()` system call creates a thread that shares the parent's address space (`pgdir`) while executing on a dedicated user-space stack. The test program `threadtest.c` spawns three concurrent threads that increment a shared global counter 100,000 times each to demonstrate address space sharing and race conditions.

### Question 2: Synchronization using Counting Semaphores (`synctest.c`)
Implements counting semaphores within the xv6 kernel using `sleep()` and `wakeup()` primitives along with `sem_init()`, `sem_wait()`, and `sem_signal()` system calls. The test program `synctest.c` uses these semaphores to eliminate the race condition from Question 1 (ensuring a final counter value of 300,000) and solves the Bounded-Buffer Producer-Consumer problem.

### Question 3: Deadlock Detection & Banker's Algorithm (`deadlock.c`)
Simulates resource allocation matrices (`Allocation`, `Max`, `Available`, `Need`) in user space. Implements the Banker's Algorithm for **deadlock avoidance** and a matrix-based **deadlock detection** algorithm to identify processes in circular wait. Additionally, it simulates a physical circular wait in xv6 using inter-process communication via pipes.

### Question 4: Priority-Based Preemptive CPU Scheduler (`priotest.c`)
Replaces xv6's default Round-Robin scheduler with a priority-based preemptive scheduler (Priority 1 = highest, Priority 20 = lowest). Adds `set_priority()` and `get_priority()` system calls, updates `proc.c` to schedule the executable task with the lowest priority value, and implements an aging mechanism (increasing process priority after 30 wait ticks) to prevent starvation. The test program `priotest.c` validates execution ordering and aging dynamics.