
## Contents
    1.  User Space
    2.  Kernel Space
    3.  Virtual Memory
    4.  File System
    5.  Scheduling
    6.  Interrupt
        1. What is Interupt?
            An interrupt is a signal to the processor emitted by hardware or software indicating an event that needs immediate attention. 

            There are two types of interrupt: Software and Hardware.

            hareware interrupt (external interrupt) can be divided into two catagories:
            blockable interrupt and unblockable interrupt. 

            Blockable interrupt are interrupts that can be blocked, usually issues by not so important peripheral devices such as printer. Unblockable interrupts must be served by the operating system such as disk reading error. 

        2.  What happen during an interrupt operation?
            Whenever an interrupt occurs, the controller completes the execution of the current instruction and starts the execution of an Interrupt Service Routine (ISR) or Interrupt Handler. ISR tells the processor or controller what to do when the interrupt occurs. The interrupts can be either hardware interrupts or software interrupts.

            ![alt text](http://hi.csdn.net/attachment/200910/18/10307_1255838664t2Or.jpg "Interrupt catagory")

        3. How is interrupt implemented? 
            1. Upper half/bottom half
            2. tasklet

            Useful Links:

            [CPU interrupt mechanism](https://blog.csdn.net/qq_36894974/article/details/79172603)
            [Interrupts, Exceptions, and System Calls](http://www.cse.iitm.ac.in/~chester/courses/15o_os/slides/5_Interrupts.pdf)
    7.  System call
    8.  Interprocess communication
    9.  Mutiprocessing/Multithreading
    10. RTOS