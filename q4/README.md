# Question 4: Priority-Based Preemptive CPU Scheduler with Aging

**Student Name:** Hima Sai Chandana  
**Roll Number:** 2401MC37  
**Course Code:** MA3105 Lab 7  

---

## Overview

Replaces xv6's default Round-Robin scheduler with a priority-based preemptive CPU scheduler containing an anti-starvation aging mechanism.

### Implemented Functionality:
1. **Priority Tracking**:
   - Adds a `priority` attribute ($1$ to $20$, where $1$ is highest priority) to `struct proc` with a default value of $10$.
2. **System Calls**:
   - `set_priority(pid, priority)`: Updates a process's priority level dynamically.
   - `get_priority(pid)`: Retrieves the active priority level of a process.
3. **Scheduler Logic (`proc.c`)**:
   - Selects the `RUNNABLE` process with the lowest priority number, breaking ties in Round-Robin order.
4. **Aging Mechanism**:
   - Tracks process wait-ticks. If a `RUNNABLE` process waits longer than 30 ticks, its priority value is decremented by 1 (increasing its relative priority) to prevent starvation.

---

## User Verification Program
- **`priotest.c`**:
  - Spawns 4 concurrent CPU-bound processes with distinct priorities.
  - Confirms higher priority tasks complete faster while low priority tasks complete eventually through aging.

---

## Compilation & Execution

```bash
make qemu
$ priotest