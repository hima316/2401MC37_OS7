# Question 3: Deadlock Detection & Banker's Algorithm

## Overview

This program simulates multi-resource allocation and deadlock management in xv6 user space.

### Implemented Functionality:
1. **Deadlock Detection Algorithm**:
   - Evaluates `Allocation`, `Request`, and `Available` matrices to detect processes in a circular wait state.
2. **Banker's Safety Algorithm (`is_safe_state`)**:
   - Checks if allocating requested resources maintains a safe execution sequence.
3. **Circular Wait Simulation**:
   - Demonstrates IPC deadlock using two processes waiting on cross-dependent read/write pipe descriptors.

---

## User Test Program

- **`deadlock.c`**:
  - Tests three resource allocation scenarios:
  1. A safe state matrix configuration.
    2. A deadlocked matrix configuration.
    3. An unsafe state transition resulting from a specific resource request.

---

## Compilation & Execution

```bash
make qemu
$ deadlock