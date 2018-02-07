# minix-random-scheduling
This project modifies the Minix startup banner and implements a randomized selection of processes to skew the priority scheduling. This should increase the amount of time it takes to boot by a noticeable amount.

## File Descriptions

### main.c
Location: `/usr/src/kernel/main.c`

This file contains the main program of Minix as well as its shutdown code. It initializes the system and starts the ball rolling by setting up the process table, interrupt vectors, and scheduling each task to run to initialize itself.
### proc.c
Location: `/usr/src/kernel/proc.c`

This file contains essentially all of the process and message handling. Together with "mpx.s" it forms the lowest layer of the Minix kernel. Minix uses a multi-priority round robin scheduler. Each process is placed in a priority queue and has an assigned CPU time allowance which is periodically decreased. 
## Changes

### main.c
- Line 238: Initialized random number generator for `proc.c`
- Line 280-284: Modified startup banner with custom message 
### proc.c
- Line 1313: Added check for processes with priority 4 or higher
- Line 1314: Modified `rand()` for specified range using the following formula: `rand() % (MAX + 1 - MIN) + MIN`
## Testing
To test my solution, I compared the time it took for a clean Minix image to reboot (~5.6s real time) and compared it to an image with the modifications added. Times were recorded using a mobile stopwatch app.

To further test the implementation of my solution, I could utilize the `fork()` system call from the previous lab. Using Minix's standard priority queue, PIDs should be printed in consecutive order. However, implementing the randomized priority queue should result in a random distribution of PIDs.
