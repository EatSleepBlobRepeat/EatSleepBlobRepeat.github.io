## StackOverFlow
Buffer overflow is an old and classic topic in the field of computer security.It is well known that the operation of computer programs depends on the function call stack.
A stack overflow is an attack that writes data in the stack that exceeds the length limit, thereby disrupting the operation of the program or even gaining control of the system.
This article will explain the technical details of stack overflow.

To implement stack overflow, two conditions need to be satisfied. First, the program must write data to the stack; second, the program does not limit the length of the written data. The first widely noticed "Morris worm" in history exploited the vulnerability of the C standard library's gets() function, which does not limit the length of input data, to achieve a stack overflow.

![Image](https://cdn.discordapp.com/attachments/818680057017925672/836958341783355442/180px-Morris_Worm.png)

Before we jump into how to implement an overflow attack, let's slightly refresh our knowledge of the function call stack.

A function call stack is a continuous area of memory used to store information about the running state of a function, including function parameters and local variables, while the program is running. It is called a "stack" because when a function call occurs, the state of the calling function (caller) is stored on the stack and the state of the called function (callee) is pressed into the top of the call stack; at the end of the function call, the state of the function (callee) at the top of the stack is popped out and the top of the stack is restored to the state of the calling function (caller). The function call stack grows in memory from a high address to a low address, so that the memory address corresponding to the top of the stack becomes smaller when the stack is pressed and larger when it is unstacked.

![Image](https://cdn.discordapp.com/attachments/818680057017925672/819758983044530186/unknown.png)

The function state involves three registers - esp, ebp and eip. esp is used to store the top address of the function call stack, which changes when the stack is pressed and unstacked. ebp is used to store the base address of the current function state, which remains unchanged while the function is running and can be used to index the location of function parameters or local variables. eip is used to store the address of the program instruction to be executed. The CPU reads and executes the instruction according to the contents of eip, which then points to the next adjacent instruction, and so on so that the program can execute the instruction continuously.
![Image](https://cdn.discordapp.com/attachments/818680057017925672/819760993256865822/v2-9125ba203edd2bab1308ad88db2ae197_720w.png)
