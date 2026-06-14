# CPU Scheduling Simulator

A time-driven CPU scheduling simulator written in C, built as part of COMP 3500
(Introduction to Operating Systems) at Auburn University.

This project demonstrates three classic CPU scheduling algorithms and computes
performance metrics for each. It was written from scratch in C using separate
compilation and a custom Makefile.

---

## What This Does

Operating systems must decide which process gets access to the CPU at any given
moment. This simulator models that decision-making process millisecond by
millisecond, using three different strategies, and measures how well each one
performs.

---

## Scheduling Algorithms

**FCFS — First Come First Serve**
Processes run in the order they arrive. Simple and fair in principle, but a long
process can block everything behind it.

**RR — Round Robin**
Each process gets a fixed time slice (the "quantum"). When its slice expires it
goes to the back of the line, giving every process a regular turn. Good for
responsiveness.

**SRTF — Shortest Remaining Time First**
At every millisecond, whichever process has the least time left runs next. A
newly arrived short process can immediately displace whatever is currently
running. Optimal for minimizing average waiting time, but requires knowing burst
times in advance.

---

## Performance Metrics

After each simulation the program reports:

- **Average waiting time** — how long processes spent ready but not running
- **Average response time** — how long until each process first got the CPU
- **Average turnaround time** — total time from arrival to completion
- **Overall CPU usage** — percentage of time the CPU was busy

---

## Project Structure

| File | Description |
|---|---|
| `scheduler.h` | Shared header: task struct definition and function prototypes |
| `scheduler.c` | Main entry point: argument parsing, file loading, algorithm dispatch, statistics |
| `fcfs.c` | FCFS algorithm implementation |
| `rr.c` | Round Robin algorithm implementation |
| `srtf.c` | SRTF algorithm implementation |
| `Makefile` | Builds the project with a single `make` command |
| `task.list` | Sample input file used for testing |

> Note: This project was built around three helper files (open.c, read.c,
> print.c) provided by the course instructor, Professor Xiao Qin at Auburn
> University. Those files handle file I/O and are not included in this
> repository. The scheduling logic, header design, Makefile, and statistics
> calculation are my own work.

---

## How to Compile

This project requires gcc and make on a Linux system.

```bash
make
```

To clean and rebuild:

```bash
make clean
make
```

---

## How to Run

```bash
./scheduler task_list_file [FCFS|RR|SRTF] [time_quantum]
```

**Examples:**

```bash
./scheduler task.list FCFS
./scheduler task.list SRTF
./scheduler task.list RR 4
```

---

## Sample Input
| PID | Arrival Time | Burst Time |
|-----|-------------|------------|
| 1   | 0           | 10         |
| 2   | 0           | 9          |
| 3   | 3           | 5          |
| 4   | 7           | 4          |
| 5   | 10          | 6          |
| 6   | 10          | 7          |

Each line contains: `pid  arrival_time  burst_time`

---

## Sample Output (FCFS)
Scheduling Policy: FCFS

There are 6 tasks loaded from "task.list". Press any key to continue ...
| Time | Event                        |
|------|------------------------------|
| 0    | process 1 is running         |
| 1    | process 1 is running         |
| 2    | process 1 is running         |
| 3    | process 1 is running         |
| 4    | process 1 is running         |
| 5    | process 1 is running         |
| 6    | process 1 is running         |
| 7    | process 1 is running         |
| 8    | process 1 is running         |
| 9    | process 1 is running         |
| 10   | process 1 is finished...     |
| 10   | process 2 is running         |
| 11   | process 2 is running         |
| 12   | process 2 is running         |
| 13   | process 2 is running         |
| 14   | process 2 is running         |
| 15   | process 2 is running         |
| 16   | process 2 is running         |
| 17   | process 2 is running         |
| 18   | process 2 is running         |
| 19   | process 2 is finished...     |
| 19   | process 3 is running         |
| 20   | process 3 is running         |
| 21   | process 3 is running         |
| 22   | process 3 is running         |
| 23   | process 3 is running         |
| 24   | process 3 is finished...     |
| 24   | process 4 is running         |
| 25   | process 4 is running         |
| 26   | process 4 is running         |
| 27   | process 4 is running         |
| 28   | process 4 is finished...     |
| 28   | process 5 is running         |
| 29   | process 5 is running         |
| 30   | process 5 is running         |
| 31   | process 5 is running         |
| 32   | process 5 is running         |
| 33   | process 5 is running         |
| 34   | process 5 is finished...     |
| 34   | process 6 is running         |
| 35   | process 6 is running         |
| 36   | process 6 is running         |
| 37   | process 6 is running         |
| 38   | process 6 is running         |
| 39   | process 6 is running         |
| 40   | process 6 is running         |
| 41   | process 6 is finished...     |
| 41   | All processes finish ...      |
Average waiting time:   14.17
Average response time:  14.17
Average turnaround time: 21.00
Overall CPU usage:      100.00%

---

## Skills Demonstrated

- Systems programming in C
- Algorithm implementation (FCFS, RR, SRTF)
- Separate compilation and Makefile construction
- Time-driven simulation design
- Performance metric calculation
