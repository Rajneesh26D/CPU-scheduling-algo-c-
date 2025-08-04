CPU-Scheduling-Simulator
A C++ implementation of various CPU scheduling algorithms, including First Come First Serve (FCFS), Round Robin (RR), Shortest Process Next (SPN), Shortest Remaining Time (SRT), Highest Response Ratio Next (HRRN), Feedback (FB), Feedback with Varying Quantum (FBV), and Aging.
Table of Contents

CPU-Scheduling-Simulator
Algorithms
First Come First Serve (FCFS)
Round Robin with Dynamic Quantum (RR)
Shortest Process Next (SPN)
Shortest Remaining Time (SRT)
Highest Response Ratio Next (HRRN)
Feedback (FB)
Feedback with Dynamic Quantum (FBV)
Aging


Setup Instructions
Input Specifications
Contributors



Algorithms
First Come First Serve (FCFS)

First Come First Serve (FCFS) schedules processes in the order they arrive. It’s straightforward but may cause delays if long processes arrive early, as it’s non-preemptive. Processes execute fully once started, making it suitable for batch systems where order matters but less ideal for systems with varied process lengths.

Round Robin with Dynamic Quantum (RR)

Round Robin (RR) with dynamic quantum allocates CPU time to processes in a time-sharing manner, with adjustable time slices (quantum). Shorter processes can receive smaller quanta, while longer ones get larger quanta, improving efficiency.

Processes are queued, and each gets a time slice to run. If the quantum expires, the process moves to the queue’s end, and the next process runs. Dynamic quanta reduce waiting times and prevent starvation by balancing CPU allocation across processes.


Shortest Process Next (SPN)

Shortest Process Next (SPN) prioritizes processes with the shortest burst time (total execution time). It’s non-preemptive, meaning a process runs to completion once started.

A queue holds processes sorted by burst time, with the shortest at the front. New arrivals are inserted based on their burst time. SPN minimizes average waiting time but may delay longer processes if short ones keep arriving.


Shortest Remaining Time (SRT)

Shortest Remaining Time (SRT) is a preemptive version of SPN, prioritizing processes with the least remaining execution time. If a new process with a shorter remaining time arrives, it can interrupt the current process.

The queue sorts processes by remaining time, updating as processes execute or new ones arrive. SRT reduces waiting times and adapts to dynamic burst times, making it effective when process durations are unpredictable.


Highest Response Ratio Next (HRRN)

Highest Response Ratio Next (HRRN) selects processes based on their response ratio, calculated as (waiting time + burst time) / burst time. It’s non-preemptive, so processes run to completion.

The queue sorts processes by response ratio, prioritizing those with longer waits relative to their burst time. HRRN balances fairness and efficiency, reducing waiting times when burst times vary or are unknown.


Feedback (FB)

Feedback (FB) assigns CPU time based on process priority, using multiple priority queues. Higher-priority processes run first, and completed processes move to a lower-priority queue.

This approach handles diverse workloads, ensuring high-priority tasks execute promptly while allowing lower-priority ones eventual access. It’s ideal for systems with mixed short and long processes.


Feedback with Dynamic Quantum (FBV)

Feedback with Dynamic Quantum (FBV) extends FB by assigning different time quanta to each priority queue. Higher-priority queues get larger quanta, optimizing CPU allocation for critical tasks while still serving lower-priority ones.

Aging

Aging prevents starvation in systems like Xinu, where the highest-priority process always runs, potentially blocking lower-priority ones. Xinu uses round-robin for equal-priority processes, but differing priorities can cause starvation.

Aging increments the priority of all ready processes by a fixed amount during each scheduling cycle, ensuring every process eventually becomes the highest priority. The scheduler:

Resets the current process’s priority to its initial value.
Increments priorities of all ready processes by 1.
Selects the highest-priority process from all eligible processes (ready list + current process).


The entire ready list is traversed each cycle to update priorities.


Setup Instructions

Clone the repository.
Install the g++ compiler and make:

sudo apt-get install g++ make


Compile the code using the make command.
Run the generated executable.

Input Specifications

Line 1: "trace" or "stats" to specify output mode.
Line 2: Comma-separated list of algorithms to analyze/visualize, with parameters if needed. Algorithms are numbered:
FCFS
RR (Round Robin, specify quantum, e.g., 2-4 for RR with quantum=4)
SPN
SRT
HRRN
FB-1 (Feedback, all queues with quantum=1)
FB-2i (Feedback, quantum=2^i)
Aging (specify quantum, e.g., 8-1 for Aging with quantum=1)


Line 3: Integer for the last simulation instant to display on the timeline.
Line 4: Integer for the number of processes to simulate.
Line 5 onward: Process descriptions, one per line. For algorithms 1–7, each line includes:
Process name (string)
Arrival time
Service time (burst time)


For Aging (algorithm 8), each line includes:
Process name (string)
Arrival time
Priority


Processes are sorted by arrival time. If arrival times are equal, lower-priority processes are assumed to arrive first.
Refer to the testcases for examples.
