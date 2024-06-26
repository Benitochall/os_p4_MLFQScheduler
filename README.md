# os_p4_MLFQScheduler
This project implements a multi-queue feedback scheduler for the xv6 opperating system. The scheduler uses cpu usage as a measure of fairness and every tick chosses the process with the highest proiority will be run. I have also implmented a nice() system call that can lower the priority of the process. 

## Implementation
I created a pschedinfo struct to keep track of info on the scheduler like
- Wheather there is a process in the process table
- the priority of each process
- the `nice` value of each process which just yeilds the process
- the PID of each process
- the number of ticks the process has spent running on the CPU
I then added instance variables to the individual process structure to keep track of the nice, priority, ticks, if it is running etc.
In the scheduler method of proc.c I modified the scheduler to recalculate the instace variables of each process every 100 ticks. This modifies the priority or each process. Then I loop through all process to find the lowest priority calling switchuvm(lowpriority) to run the lowest priority process. When this process finishes or is kicked off I recalclate the time it spent on the CPU.


## System calls
nice(int n) - sets and then returns the current nice value for the current process 
getschedstate( pscedinfo * sched) - updates the scheduler with the info for each running process in the ptable. 

## Usage
This is all system level, see pdfs for results. 
