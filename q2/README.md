# Question 2: Process & Thread Synchronization using Semaphores

## Overview

To solve the race conditions observed in Question 1, counting semaphores are implemented inside the xv6 kernel using built-in `sleep()` and `wakeup()` primitives.

### Implemented Functionality:
1. **Kernel Semaphore Storage**:
   - Maintains an array of 10 counting semaphores in kernel space protected by a spinlock.
2. **System Calls**:
   - `sem_init(sem_id, value)`: Initializes a kernel semaphore with a given value.
   - `sem_wait(sem_id)`: Decrements the semaphore value; blocks the process if the count falls below 0.
   - `sem_signal(sem_id)`: Increments the semaphore value and awakens waiting processes.

---

## Test Programs

1. **`synctest.c`**:
   - Protects the global counter increments using `sem_wait()` and `sem_signal()`.
   - Verifies that the final synchronized counter reaches exactly **300,000**.

2. **Producer-Consumer Implementation**:
   - Manages a fixed-size buffer (capacity 5) using `mutex`, `empty`, and `full` semaphores.
   - Logs concurrent production and consumption without buffer overflows or underflows.

---

## Compilation & Execution

```bash
make qemu
$ synctest