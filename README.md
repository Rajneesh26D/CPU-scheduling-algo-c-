# CPU-Scheduling-Algorithms
A C++ implementation of multiple CPU scheduling algorithms, including First Come First Serve (FCFS), Round Robin (RR), Shortest Job First (SJF), Shortest Remaining Time First (SRTF), Highest Response Ratio First (HRRF), Multi-Level Feedback (MLF), Multi-Level Feedback with Variable Quantum (MLFV), and Priority Aging

## Table of Contents
  - [Scheduling Algorithms](#scheduling-algorithms)
    - [First Come First Serve (FCFS)](#first-come-first-serve-fcfs)
    - [Round Robin with Adjustable Quantum (RR)](#round-robin-with-adjustable-quantum-rr)
    - [Shortest Job First (SJF)](#shortest-job-first-sjf)
    - [Shortest Remaining Time First (SRTF)](#shortest-remaining-time-first-srtf)
    - [Highest Response Ratio First (HRRF)](#highest-response-ratio-first-hrrf)
    - [Multi-Level Feedback (MLF)](#multi-level-feedback-mlf)
    - [Multi-Level Feedback with Variable Quantum (MLFV)](#multi-level-feedback-with-variable-quantum-mlfv)
    - [Priority Aging](#priority-aging)
  - [Setup Guide](#setup-guide)
  - [Input Structure](#input-structure)

## Scheduling Algorithms

### First Come First Serve (FCFS)
- FCFS schedules processes based on their arrival order. It’s a non-preemptive algorithm, meaning a process runs until it completes. While simple, it may lead to inefficiencies if early-arriving processes have long execution times, delaying others. It’s best suited for systems prioritizing sequential processing.

### Round Robin with varying time quantum (RR)
- Round Robin (RR) with adjustable quantum uses time-sharing to allocate CPU time. The quantum (time slice) varies based on process needs, allowing shorter processes to use smaller slices and longer ones larger slices.
- Processes are queued, and each executes for its assigned quantum. If the quantum expires, the process moves to the queue’s end, and the next process runs. Adjustable quanta enhance efficiency by reducing wait times and preventing process starvation

### Shortest Job First (SJF)
- Shortest Job First (SJF) is a non-preemptive algorithm that selects the process with the shortest total execution time (burst time). Processes are queued and sorted by burst time, with the shortest at the front.
- SJF minimizes average waiting time by prioritizing quick tasks but may delay longer processes if short ones arrive frequently. It’s effective when minimizing wait times is critical.

### Shortest Remaining Time First (SRTF)
- Shortest Remaining Time First (SRTF) is a preemptive version of SJF, prioritizing the process with the least remaining execution time. New processes with shorter remaining times can interrupt the current process
- The queue dynamically sorts by remaining time, adapting to new arrivals or execution progress. SRTF optimizes wait times and is suitable for systems with unpredictable process durations

### Highest Response Ratio First (HRRF)
- Highest Response Ratio First (HRRF) is a non-preemptive algorithm that prioritizes processes based on their response ratio, calculated as (waiting time + burst time) / burst time. The highest ratio determines the next process to run.
- HRRF balances fairness by favoring processes that have waited longer relative to their burst time. It’s effective for reducing wait times in systems with variable or unknown process durations.

### Multi-Level Feedback (MLF)
- Multi-Level Feedback (MLF) uses multiple priority queues to manage processes. Higher-priority processes execute first, and upon completion, they move to a lower-priority queue.
- MLF efficiently handles diverse workloads, ensuring critical tasks run promptly while allowing less urgent processes eventual CPU access. It’s ideal for systems with mixed process types.

### Multi-Level Feedback with Variable Quantum (MLFV)
- MLFV extends MLF by assigning different time quanta to each priority queue. Higher-priority queues receive larger quanta, optimizing CPU time for critical tasks while still serving lower-priority ones.

### Priority Aging
- Priority Aging addresses starvation in systems where high-priority processes monopolize CPU time, leaving lower-priority ones unserved. In systems like Xinu, where the highest-priority process always runs (with round-robin for equal priorities), lower-priority processes can starve

- Aging increments the priority of all ready processes by a fixed value during each scheduling cycle, ensuring every process eventually gains top priority. The scheduler:
    - Resets the current process’s priority to its initial value.
    - Increases the priority of all ready processes by 1.
    - Selects the highest-priority process from the ready list and current process.

- The scheduler scans the entire ready list each cycle to update priorities.

## Setup Guide
1- Clone the repository

2- Install g++ compiler and make
```bash
sudo apt-get install g++ make
```
3- Compile the code using `make` command

4- Run the executable file

## Input Format
- Line 1: "trace" or "stats"
- Line 2: a comma-separated list telling which CPU scheduling policies to be analyzed/visualized along with
their parameters, if applicable. Each algorithm is represented by a number as listed in the
introduction section and as shown in the attached testcases.
Round Robin and Aging have a parameter specifying the quantum q to be used. Therefore, a policy
entered as 2-4 means Round Robin with q=4. Also, policy 8-1 means Aging with q=1.
 1. FCFS (First Come First Serve)
 2. RR (Round Robin)
 3. SPN (Shortest Process Next)
 4. SRT (Shortest Remaining Time)
 5. HRRN (Highest Response Ratio Next)
 6. FB-1, (Feedback where all queues have q=1)
 7. FB-2i, (Feedback where q= 2i)
 8. Aging
- Line 3: An integer specifying the last instant to be used in your simulation and to be shown on the timeline.
- Line 4: An integer specifying the number of processes to be simulated.
- Line 5: Start of description of processes. Each process is to be described on a separate line. For algorithms 1 through 7, each process is described using a comma-separated list specifying:

    1- String specifying a process name\
    2- Arrival Time\
    3- Service Time

- **Note:** For Aging algorithm (algorithm 8), each process is described using a comma-separated list specifying:

    1- String specifying a process name\
    2- Arrival Time\
    3- Priority
- Processes are assumed to be sorted based on the arrival time. If two processes have the same arrival time, then the one with the lower priority is assumed to arrive first.
> Check the attached [testcases](https://github.com/Rajneesh26D/CPU-scheduling-algo-c-/tree/main/testcases) for more details.
