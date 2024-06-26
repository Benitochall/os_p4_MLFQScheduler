# os_p4_MLFQScheduler

This project implements a multi-queue feedback scheduler for the xv6 operating system. The scheduler uses CPU usage as a measure of fairness and every tick chooses the process with the highest priority to run. I have also implemented a `nice()` system call that can lower the priority of a process.

## Implementation

I created a `pschedinfo` struct to keep track of information on the scheduler, including:
- Whether there is a process in the process table
- The priority of each process
- The `nice` value of each process, which can yield the process
- The PID of each process
- The number of ticks the process has spent running on the CPU

I then added instance variables to the individual process structure to keep track of the `nice` value, priority, ticks, and whether it is running, etc.

In the scheduler method of `proc.c`, I modified the scheduler to recalculate the instance variables of each process every 100 ticks. This modifies the priority of each process. Then I loop through all processes to find the lowest priority process, calling `switchuvm(lowpriority)` to run the lowest priority process. When this process finishes or is kicked off, I recalculate the time it spent on the CPU.

## System Calls

- `nice(int n)` - Sets and then returns the current nice value for the current process.
- `getschedstate(pscedinfo *sched)` - Updates the scheduler with the information for each running process in the process table.

## Usage

This is all system level. See PDFs for results.
