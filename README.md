# xv6 Lottery Scheduler and System Calls

A modified version of the xv6 operating system kernel implementing a lottery-based CPU scheduler, custom system calls, process metadata tracking, and a custom `ps` userspace utility.

This project focused on operating systems concepts including process scheduling, kernel-level programming, system calls, process control blocks, and CPU time allocation.

---

## Features

- Custom lottery scheduler implementation
- Dynamic CPU ticket allocation per process
- Custom kernel-level system calls
- Process color attributes stored in PCB
- Randomized process scheduling
- Userspace `ps` utility
- Process statistics tracking
- Parent-to-child ticket inheritance
- CPU tick accounting

---

## Technologies Used

- C
- xv6 Operating System
- QEMU
- Linux
- Git/GitHub

---

## System Calls Implemented

### `setTickets(int tickets)`

Allows a process to dynamically change the number of scheduling tickets assigned to it.

- Ticket range: `1–256`
- Higher ticket count increases CPU scheduling probability
- Child processes inherit parent ticket count

---

### `setColor(enum COLOR)`

Stores a color attribute inside the process control block (PCB).

Supported colors:
- RED
- ORANGE
- YELLOW
- GREEN
- BLUE
- INDIGO
- VIOLET

---

### `getpinfo(struct pstat *)`

Returns process information from the kernel to userspace, including:
- process name
- PID
- process state
- ticket count
- CPU ticks accumulated
- process color

---

## Lottery Scheduler

The default xv6 scheduler was modified to use a lottery scheduling algorithm.

### How it works

- Each process receives one or more tickets
- A pseudo-random number generator selects the winning ticket
- Processes with more tickets receive a larger share of CPU time
- Scheduling fairness is determined probabilistically over time

This project required modifying:
- `proc.c`
- `proc.h`
- scheduler control flow
- process creation logic

---

## Userspace `ps` Utility

A custom `ps` command was implemented to display process information.

Example output:

```text
NAME    PID     STATUS      COLOR    TICKETS
init    1       SLEEPING    RED      10
sh      2       SLEEPING    ORANGE   2
test    4       SLEEPING    RED      4
ps      6       RUNNING     INDIGO   1
```

---

## Concepts Learned

This project strengthened understanding of:

- Operating system scheduling
- Kernel development
- System calls
- Process management
- Process control blocks (PCB)
- Context switching
- Randomized scheduling algorithms
- User/kernel space communication

---

## Building the Kernel

```bash
source source_me.sh
make
```

---

## Running xv6

```bash
make qemu
```

---

## Exiting xv6

```bash
ctrl-a x
```

---

## Future Improvements

- Priority-based scheduling
- Multi-level feedback queue scheduler
- Improved randomness algorithms
- Additional scheduler benchmarking
- Process visualization tools

---

## Author

Muhammad Zahid
