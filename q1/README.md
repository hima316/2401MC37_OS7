# Question 1: Kernel-Supported Multithreading in xv6

## Overview

xv6 natively manages isolated processes, where each process maintains its own page directory (`pgdir`) created via `fork()`. This assignment introduces kernel-supported multithreading, allowing multiple execution contexts (threads) to run concurrently while sharing the same virtual address space.

### System Call Implementation

1. **`clone(void (*fcn)(void *), void *arg, void *stack)`**
   - Allocates a process table entry using `allocproc()`.
   - Assigns the parent's page directory (`pgdir`) directly to the child thread rather than duplicating memory with `copyuvm()`.
   - Allocates a distinct kernel stack and configures the user trapframe to begin execution at `fcn(arg)` using the provided user stack pointer.

2. **`join(void **stack)`**
   - Suspends the calling thread using `sleep()` until a child thread terminates.
   - Cleans up thread state, reclaims the child's kernel stack, and returns the thread ID and user stack location for user-space deallocation.

3. **Lifecycle Management (`proc.c`, `exit()`, `wait()`)**
   - Modified `exit()` to ensure a exiting thread does not free the shared `pgdir` while sibling threads remain active. Memory deallocation is deferred until all threads within the process address space terminate.

---

## Verification (`threadtest.c`)

The test program validates memory sharing and race condition behavior:

- Spawns three concurrent threads using `clone()`.
- Each thread increments a shared global variable 100,000 times without synchronization primitives.
- Demonstrates race conditions in shared memory, yielding an un-synchronized final count less than 300,000.

---

## Compilation & Execution

```bash
make qemu
$ threadtest