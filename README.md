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
- Line 19: Added `<time.h>` header file
- Line 238: Initialized random number generator for `proc.c`
- Line 280-284: Modified startup banner with custom message 
### proc.c

## Testing
