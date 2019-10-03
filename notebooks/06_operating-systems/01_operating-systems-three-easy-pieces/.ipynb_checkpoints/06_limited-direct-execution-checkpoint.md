# Mechanism: Limited Direct Execution

- attaining performance while maitaining control

## PRoblem #1 Restricted Operations

- time sharing
- without limits on running programs the OS wouldn't be in control of anything and thus would be "just a library"!

### mores of execution

- user mode: applications donot have full access to hardware resources
- kernel mode: OS has access to full resources of the machine

### protected control transfer

- special instructions to trap into the kernel and return-from-trap back to user-mode programs are also provided
- also instructions that allow the OS to tell the hardware where the trap table resides in memory

- user program when it wishes to to perform some kind of privilleged operation, such as reading from disk, makes a **systemcall** provided by virtually all modern OS

### executing systemcall

- to execute a systemcall, a program must execute a special `trap` instruction
- trap instruction jumps into kernel and raises privilege level to kernel mode
- once in kernel mode the system can now perform whatvever privilleged operations are needed (if allowed) and do the required work for the calling process
- when finished the OS calls a special `return-from-trap` instruction, which returns into the calling user program, simultaneously reducing the privilege level back to user mode

### Systemcall vs a regualr procedure call

- how does the trap know which code to run inside OS when a systemcall is made
- the calling usermode program can't specify the memory address of systemcall procedure (as it when making a regular prodecure call); doing so will enable the programs to jump anywhere into kernel
- so kernel must control what code executes upon a trap
- kernel does so by setting a **trap table** at boot time
- when machine boots up, it does so in privileged mode (kernel mode). so it is free to configure system hardware
- during bootup OS tells the hardware what code to run some exceptionals events occur (for example hard-disk interupt, keyboard interupt)
- OS informs the hardware of the locations of these **trap handlers**
