---
title: Simplified-Operating-System 
date: 2019-02-19 15:20:35 
tags:
---
# CS350 Operating Systems 

# 1 Implement Kernel Synchronization Primitives

The OS/161 kernel includes four types of synchronization primitives: spinlocks, semaphores, locks,and condition variables. Spinlocks and semaphores are alreadyimplemented. Locks and condition variables are implement by myself.

## 1.1 Implement Locks
Your first task is to implement locks. The interface for the lock structure is defined in kern/include/synch.h.Stubcodeisprovidedinkern/threads/synch.c.Youcanusetheimplementation of semaphores as a model, butdo not build your lock implementation on top of semaphores or you will be penalized. In other words, your lock implementation should not usesemcreate(), P(),V()or any of the other functions from the semaphore interface.
Locks are used throughout the OS/161 kernel. You will need properly functioning locks for this and futureassignments to ensure that the kernel’s threads are properlysynchronized. Becauseofthis,implementing locks correctly though not difficult is the most important part of this assignment.Make sure that you get locks working before moving on to the other parts of the assignment.


## 1.2 Implement Condition Variables

The second task is to implement condition variables for OS/161. The interface for the cv structure is defined inkern/include/synch.hand stub code is provided in kern/thread/synch.c.Eachconditionvariable is intended to work with a lock: condition variables are onlyusedfrom within the critical section that is protected by the lock

## 1.3 Testing Locks and Condition Variables

The filekern/test/synchtest.cimplements a simple test case for locks, and another for condition variables.
You can run the lock test from the kernel menu by issuing thesy2command, e.g,:

```
%sys161kernel"sy2;q"
```
Similarly, thesy3command will run the condition variable test. If the lock testreports“Locktestdone”
without reporting any failure messages, it has succeeded. The output from the condition variable test should be self-explanatory.
Testing synchronization primitives like locks and condition variables is difficult. Bothsy2andsy are subject to false positives. In other words, an incorrectlock or condition variable implementation may pass these tests. However, if your implementationfailsatest,thereisdefinitelyaproblem. Sincethe


synchronization tests are not perfect, we may use code inspection - in addition to testing - to evaluate your lock and condition variable implementations.
Although you are free to implement locks however you want,you should not modify any of the kernel’s test programs,i.e.,donotmodifyanyofthefilesinkern/test. Furthermore, you should not make any changes to the way that the tests are invoked, e.g., donotchange“sy2”to“sy2a”.

# 2 Solve a Synchronization Problem

For this part of the assignment, you are expected to implementasolutiontoasynchronizationproblem called the “trafficintersection”problem.Thesynchronization primitives that you may use in your solution aresemaphores, locks, and condition variables.Youarefreetousewhicheverofthesesynchronization primitives you choose, however you like. However, you must not directly use any “lower-level”
methods of synchronization,suchaswaitchannelsorspinlocks.

The TrafficIntersectionProblem

In the trafficintersectionproblem,vehiclesaretryingtopass through an intersection of two roads, one north/south, the other east/west, without colliding. Eachvehicle arrives at the intersection from one of four directions (north, south, east, or west), called it’sorigin. It is trying to pass through the intersection and exit in some direction other than its origin, called it’sdestination.
In OS/161, each arriving vehicle is simulated by a thread, and the intersection is a critical section.
Each vehicle (thread) enters the intersection (critical section) and eventually leaves. The vehicle simulation is implemented in the filekern/synchprobs/traffic.c.Youarefreetoinspectthecodeinthisfileto understand the simulation. However,you may not change this file in any way.
The vehicle simulation works by creating a fixed number of concurrent threads. Each thread simulates a sequence of vehicles attempting to pass through the intersection. In a loop, each thread generates a random vehicle (randomly choosing an origin and destination for thevehicle)andthenentersandleavesthecritical section to simulate the vehicle passing through the intersection. Threads then sleep for a configurable period of time before generating another random vehicle and repeating the process. Each thread simulates one vehicle at a time. However, since there are multiple concurrent threads, there may be multiple vehicles attempting to enter the critical section (intersection) concurrently.
Your job is to synchronize the vehicles so that they do not collide in the intersection. Informally, it is OK for more than one vehicle to be in the intersection at the same time as long as their paths will not result in a collision. For example, it is OK for a vehicle thatis traveling from north to south to share the intersection with another vehicle that is traveling from south to north, but not with one that is traveling from east to west. For the purposes of this assignment, we’vecodified a specific set of conditions under which vehicles can safely share the intersection (critical section). If two vehicles,VaandVb, are in the intersection simultaneously, thenat least oneof the following must be true:

- VaandVbentered the intersection from the same direction, i.e.,Va.origin=Vb.origin,or
- VaandVbare going in opposite directions, i.e.,Va.origin=Vb.destinationandVa.destination=
    Vb.origin,or
- VaandVbhave different destinations, and at least one of them is makingarightturn,e.g.,Vais right-turning from north to west, andVbis going from south to north.

Note that it is possible for more than two vehicles to be in theintersection at the same time, as long asall pairsof vehicles satisfy one of the above conditions.
These conditions are less flexible than what is allowed at some real road intersections. For example,
the conditions above do not allow cars traveling in oppositedirections to make left turns concurrently.
Nonetheless, for the purposes of this assignment, these somewhat simplified conditions will serve as our definition of correctness.
It is up to you to determine exactly how to synchronize the vehicles - there are many ways to satisfy the synchronization requirements. OS/161 includes a simpledefaultsolution(inthefiletrafficsynch.c,


see Section 2.1) which uses a single semaphore to ensure thatonly one vehicle at a time can enter the intersection. This is a correct solution - it trivially satisfies all of the conditions above. However, it is not anefficientsolution because it misses opportunities to let more than onevehicleusetheintersectionatthe same time when the synchronization rules permit it. For thisassignment, we are looking for solutions that are correct, fair, and efficient.

## 2.1 Implementing Your Solution

In the directorykern/synchprobs,thereisafilecalledtrafficsynch.c.Yoursolutiontothe“traffic intersection” problem should be implemented entirely in this file.
Thetrafficsynch.cfile contains four functions, which are invoked by the trafficsimulation program:

- intersectionbeforeentry:calledbyavehiclesimulationbeforeavehicleenterstheintersection.
- intersectionafterentry:calledbyavehiclesimulationafteravehicleleavestheintersection
- intersectionsyncinit:calledonlyonce,beforeanyvehiclestrytoentertheintersection
- intersectionsynccleanup:calledonlyonce,attheendofthesimulation.

trafficsynch.cincludes a simple default implementation of these functions. It uses a single semaphore to ensure that only one vehicle at a time will enter the intersection. For this assignment, you shouldre-
implement these functions to produce a solution that is correct, fair,and efficient. In particular, you should use theintersectionbeforeentryfunction to make vehicles wait before entering the intersec-
tion, so that the synchronization requirements are not violated. To do this, your implementation of intersectionbeforeentryshould cause that vehicle (thread) toblockuntil it is OK for it to proceed into the intersection without violating the synchronization rules. In other words,intersectionbeforeentry should not return until it is OK for the vehicle to enter the intersection, since the vehicle will enter the intersection onceintersectionbeforeentryreturns.

# 3 CodeReview

## 3.1 kern/syscall

This directory contains the files that are responsible for loading and running user-level programs, as well as basic and stub implementations of a few system call handlers.

procsyscalls.c:This file is intended to hold the handlers for process-relatedsystemcalls,includingthe calls that you are implementing for this assignment. Currently, it contains a partial implementation of ahandlerforexit()and stub handlers forgetpid()andwaitpid().

runprogram.c:This file contains the implementation of the kernel’srunprogramcommand, which can be invoked from the kernel menu. Therunprogramcommand is used to launch the first process run by the kernel. Typically, this process will be the ancestor of all other processes in the system.

## 3.2 kern/arch/mips/

This directory contains machine-specific code for basic kernel functions, such as handling system calls,
exceptions and interrupts, context switches, and virtual memory.

locore/trap.c:This file contains the functionmipstrap(),whichisthefirstkernelCfunctionthatis called after an exception, system call, or interrupt returnscontroltothekernel. (mipstrap()gets called by the assembly language exception handler.)

syscall/syscall.c:This file contains the system call dispatcher function, calledsyscall().Thisfunction,
which is invoked bymipstrap()determines which kind of system call has occured, and calls the appropriate handler for that type of system call. As providedtoyou,syscall()will properly invoke the handlers for a few system calls. However, you will need tomodify this function to invoke your handler forfork().Inthisfile,youwillalsofindastubfunctioncalledenterforkedprocess().This is intended to be the function that is used to cause a newly-forked process to switch to user-mode for the first time. When you implemententerforkedprocess(),youwillwanttocallmipsusermode()
(fromlocore/trap.c)toactuallycausetheswitchfromkernelmodetousermode.

## 3.3 kern/include

Thekern/includedirectory contains the include files that the kernel needs. Thekernsubdirectory contains include files that are visible not only to the operating systemitself,butalsotouser-levelprograms.(Think about why it’s named “kern” and where the files end up when installed.)

## 3.4 kern/vm

Thekern/vmdirectory contains the machine-independent part of the kernel’s virtual memory implementa-
tion. Although you do not need to modify the virtual memory implementation for this assignment, some functions implemented here are relevant to the assignment.


copyinout.c:This file contains functions, such ascopyin()andcopyoutfor moving data between kernel space and user space. See the partial implementations of thehandlers for thewrite()andwaitpid()
system calls for examples of how these functions can be used.

## 3.5 Inuser

Theuserdirectory contains all of the user level applications, whichcanbeusedtotestOS/161. Don’tforget that the user level applications are built and installed separately from the kernel. All of the user programs can be built by runningbmakeand thenbmake installin the top-level diretory (os161-1.99).

# 2ImplementationRequirements

All code changes for this assignment should be enclosed in#if OPTA2statements. For example:

```
#if OPT_A
// code you created or modified for ASST2 goes here
#else
// old (pre-A2) version of the code goes here,
// and is ignored by the compiler when you compile ASST
// the ‘‘else’’ part is optional and can be left
// out if you are just inserting new code for ASST
#endif /* OPT_A2 */
```
For this to work, you must add#include "opt-A2.h"at the top of any file for which you make changes for this assignment.
If in Assignment 1 you wrapped any new code with#if OPTA1,itwillalso be included in your build when you compile for Assignment 2.
For this assignment, you are expected to implement the following OS/161 system calls:

- fork
- getpid
- waitpid
- exit

forkenables multiprogramming and makes OS/161 much more useful. exitandwaitpidare closely related to each other, since exitallows the terminating process to specify an exit status code, andwaitpid allows another process to obtain that code. You are not required to implement theWAITANY,WAITMYPGRP,
WNOHANG,andWUNTRACEDflags forwaitpid()-seekern/include/kern/wait.h.
To help get you started, there is a partially-implemented handler for exitalready in place, as well as stub implementatations of handlers forgetpidandwaitpid.Youwillneedtocompletetheimplementations of these handlers, and also create and implement a handler forfork.Thereisaman(manual)pagefor each OS/161 system call. These manual pages describe the expected behaviour of the system calls. The system call man pages are located in the OS/161 source tree underos161-1.99/man/syscall.Theyare also available on-line through the course web page.
Your system call implementations should correctly and gracefully handle error conditions, and properly return the error codes as described on the man pages. This is because application programs, including those used to test your kernel for this assignment, depend on the behaviour of the system calls as specified in the man pages. Under no circumstances should an incorrect system call parameter cause your kernel to crash.
Integer codes for system calls are listed inkern/include/kern/syscall.h.Thefileuser/include/unistd.h contains the user-level function prototypes for OS/161 system calls. These describe how a system call is made from within a user-level application. The filekern/include/syscall.hcontains the kernel’s prototypes for its internal system call handling functions. You will find prototypes for the handlers forwaitpid, exitand getpidthere. Don’t forget to add a prototype for your newfork()handler function to this file.


## 4.1 Process IDs

APID,orprocessID,isauniquenumberthatidentifiesaprocess. You should carefully review the manual pages forfork, exit,andwaitpidto understand how PIDs are expected to work.
For the purposes of this assignment, you should ensure that aprocess can usewaitpidto obtain the exit status of any of its children, and that a process may not usewaitpidto obtain the exit status of any other processes. In the terminology used on thewaitpidmanual page, you should assume that a process is
“interested” in its children, but is not interested in any other processes.

## 4.2 Silence is Golden

Your final, submitted kernel should not produce any output other than the normal boot and shutdown messages and the kernel menu prompt. We enourage you to use theDEBUGmechanism to generate kernel debugging output while you are testing your work, but make sure that all such debugging messages are turned offin the version of the kernel that you submit.
If your kernel produces lots of spurious output, it is more difficult for us to review the output produced by the user-level programs that we test with. If your kernel produces output other than the normal boot and shutdown messages, your assignment may be penalized.

# 5 CodeReview

This section gives a brief overview of some parts of the kernelthatarerelevanttothenewAssignment2b requirements.

## 5.1 kern/syscall

This directory contains the files that are responsible for loading and running user-level programs, as well as basic and stub implementations of a few system call handlers.

loadelf.c:This file contains the functions responsible for loading an ELF executable from the filesystem into an address space. (ELF is the name of the executable format produced by cs350-gcc.)

procsyscalls.c:This file is intended to hold the handlers for process-relatedsystemcalls,includingthe handler forexecv,whichyouareimplementingforthisassignment.

runprogram.c:This file contains the implementation of the kernel’srunprogramcommand, which can be invoked from the kernel menu. Therunprogramcommand is used to launch the first process run by the kernel. Typically, this process will be the ancestor of all other processes in the system. Studying therunprogramfunction should give you some ideas on how to implementexecv.Thinkabouthow runprogram’s task is similar toexecv’s, and how it is different.

## 5.2 kern/arch/mips/

This directory contains machine-specific code for basic kernel functions, such as handling system calls,
exceptions and interrupts, context switches, and virtual memory.

syscall/syscall.c:This file contains the system call dispatcher function, calledsyscall().Aswas described in Assignment 2a, you will need to modify this function to invoke your handler forexecv().

locore/trap.c:In this file, in addition to the kernel exception handler, youwill find the functionenternewprocess,
which should be useful for your implementation ofexecv.

vm/dumbvm.c:This file contains the machine-specific part of OS/161’s verysimple implementation of virtual address spaces.

## 5.3 kern/vm

Thekern/vmdirectory contains the machine-independent part of the kernel’s virtual memory implementa-
tion.

copyinout.c:This file contains functions, such ascopyinandcopyoutfor moving data between kernel space and user space.


## 5.4 kern/include

vfs.h:This file describes the VFS interface, which the kernel uses toopenandclosefiles,e.g.,program executable files. See therunprogramfunction for an example of how to use the VFS interface.

vnode.h:Opening a file using the VFS interface results in avnodeobject representing the open file. The vnodeobject can be used to read data from and write data to the open file. vnode.hdescribes the vnodeinterface. Seeloadelf.cfor an example of code that usesvnodeoperations to read data from afile.

uio.h:This file describes theuiointerface. The kernel usesuiostructures to describe a data transfer between a file and memory, between memory and a file, or betweentwo locations in memory. vnode operations, such asVOPREAD,expectuiostructures as parameters.


## 5.5 execv

Theexecvsystem call replaces the address space of the calling processwithanewaddressspacecontaining anewprogram. Aftertheexecvsystem call, the process starts executing the new program, starting with itsmainfunction.
Be sure to review the manual page for theexecvsystem call, which describes howexecvis expected to behave. The system call man pages are located in the OS/161 source tree underos161-1.99/man/syscall.
They are also available on-line through the course web page.
The second parameter toexecvis an array of pointers to arguments (parameters). The idea isthat execvpasses these parameters to the new application program, which can access them using theargcand argvparameters to itsmainfunction. As discussed in Section 3, you should first getexecvworking without worrying about passing these arguments properly. Onceexecvis working without argument passing, you can then focus on getting argument passing working.


## 5.6 Argument Passing

Theexecvmanual page specifies how the second parameter (the argumentarray) must be set up. Make sure you understand this before proceeding.
Argument passing means taking the arguments that are passedtoexecvand making them available to the new program that will start running in the process that does theexecv.Todothis,yourkernelwillneed to retrieve these arguments from the address space of the original program (before destroying its address spaces) and then set up a properly structured argument arrayin the address space of the new program before it starts running. You will need to decide where in the new address space to place the arguments.
In addition to passing arguments to new programs throughexecv,yourkernelisalsoexpectedtobe able to pass arguments to the very first program that runs, i.e., to the program that is launched in response to the “p” (runprogram) kernel command. This is similar to passing arguments throughexecv,exceptfor the fact that the arguments are coming directly from the kernel (which reads them from its command line)
rather than from the program that is making theexecvcall. Therefore, once you have argument passing working forexecv,itshouldberelativelysimpletogetargumentpassingworking forrunprogram.

# 6 Strategy

We cannot test yourexecvimplementation unless the system calls from Assignment 2a (fork,waitpid,
exit)areimplementedandworkingproperly.Therefore,thereislittle point in working onexecvuntil the Assignment 2a system calls are done. If you did not finish the Assignment 2a system calls, get them finished first. When we test your Assignment 2b, we will alsore-test the Assignment 2a system calls, and part of the Assignment 2b marks will be awarded based on that re-testing.
When you are ready to start working onexecv,youshouldstartbygettingexecvto workwithout worryingaboutargumentpassing. There are someexecvtests that do not require argument passing - make sure that yourexecvwill pass those tests before you start on argument passing, which is the most challenging part of the assignment. Once you have anexecvthat works without argument passing,submityourkernel.
If you get argument passing working, you can submit a revisedversion. If you do not, you will at least be able to get the marks for the partially working version ofexecvthat you submitted before you started on argument passing.
Finally, you should work on argument passing. Argument passing forrunprogramis very similar to argument passing forexecv,soifyoucangetargumentpassingworkingforone,youshouldbeabletoget it working for the other.

# 7 CodeReview

##7.1 Inkern/vm

This directory is intended to hold machine-independent parts of the virtual memory implementation.

- kmalloc.c:Thisfilecontainsimplementationsofkmallocandkfree,tosupportdynamicmemory
    allocation for the kernel.
- uw-vmstats.c:containscodefortrackingstatisticsrelatedtothevirtual memory system. Not used
    for this assignment.
- copyinout.c:containscodeforcopyingdatabetweenapplicationsandthekernel.

##7.2 Inkern/syscall

loadelf.c:This file contains the functions responsible for loading an ELF executable from the filesystem into virtual memory space. You should already be familiar with this file from Assignment 2.

Inkern/include

addrspace.h:Defines the addrspace interface. You may need to make changeshere, at least to define an appropriate addrspace structure.

vm.h:Some VM-related definitions, including prototypes for somekey functions, such asvmfault(the TLB miss handler) andallockpages(used, among other places, inkmalloc).

##7.3 Inkern/arch/mips/vm

dumbvm.c:This file contains the implementation of the dumbvm virtual memory system, including the implementation of theaddrspacefunctions andvmfault,whichisthekernel’shandlerfunctionfor exceptions related to virtual memory. It also includes somevery simple functions (e.g.,allockpages)
for physical memory management.

ram.c:This file includes functions that the kernel uses to manage physical memory (RAM) while the kernel is booting up, before the VM system has been initialized. Since your VM system will essentially be taking over management of physical memory, you need to understand how these functions work.

##7.4 Inkern/arch/mips/include

tlb.h:This file defines the prototypes for the kernel’s functions formanagingtheTLB(suchastlbwrite),
as well as definitions of the fields in each TLB entry.

vm.h:This file defines some macros and constants (such as the page size) related to address translation on the MIPS. Note that thisvm.his different from thevm.hinkern/include.


# 8 ImplementationRequirements

## 8.1 Handling a Full TLB

Currently, the dumbvm system will panic and crash if the TLB fills up with valid entries. Change this so that the kernel will not panic in this situation. If kernel needs to add a new entry to the TLB and the TLB is full, the kernel should simply overwrite one of the existing entries with the new entry. A simple way to do this is to use thetlbrandomfunction to allow the hardware to choose a random entry to be overwritten.
Thevmfaultfunction is responsible for managing the TLB, so you should beabletoimplementthis part of the assignment with some small changes to that function.
You should get this part of the assignment finished first and test that it works correctly, because many of the test programs used for the other parts of the assignmentwillnotworkproperlyifthekernelpanics when the TLB fills up.

## 8.2 Read-Only Text Segment

In the dumbvm system, all three address space segments (text,data,andstack)arebothreadableand writable by the application. For this assignment, you shouldchangethissothateachapplication’stext segment isread-only.YourkernelshouldsetupTLBentriessothatanyattemptbyanapplicationtomodify its text section will cause the MIPS MMU to generate a read-only memory exception (VMFAULTREADONLY).
If such an exception occurs, your kernel should terminate theprocessthatattemptedtomodifyitstext segment. Your kernel shouldnotcrash.
Get this part of the assignment finished and tested before moving on to physical memory management.

## 8.3 Physical-Memory Management

The dumbvm virtual memory system has two severe limitationsin the way it manages physical memory.
First, it assumes that each segment will be allocated contiguously in physical memory. Second, it never re-uses physical memory. That is, when a process exits, the physical memory that was used to hold that process’s address space does not become available for use byother processes. As a result, the kernel will quickly run out of physical memory.
Your objective in this assignment is to remove both of these limitations. In particular:

- It should be possible for the pages in process’ address spacestobeplacedintoanyfree frame of
    physical memory. That is, the kernel should no longer requirethataddressspacesegmentsbestored
    contiguously in physical memory.
- When a process terminates, the physical frames that were usedtoholditspagesshouldbefreed,and
    should become available for use by other processes.

To implement these changes, your kernel will need some way ofkeeping track of where each page in each process’s virtual address space is located, and some way of keeping track of which frames of physical memory are free, and which are in use.
The kernel uses physical memory both to hold its own data structures and to hold the address spaces of user processes. The kernel useskmallocandkfreeto dynamically allocate space for new kernel data structures. kmallocandkfree,inturn,callallockpagesandfreekpagesto allocate or free physical memory as necessary. When you change the way the kernel’s physical memory management works to satisfy the requirements above,you must also ensure thatkmallocandkfreecontinue to work properly.
In addition, you should ensure that any physical pages freedbykfree(when it callsfreekpages)become free and available for re-use by the kernel. This will requireyoutoimplementfreekpages,whichcurrently


does nothing. Note that there is no need for you to modify the implementations of kmallocandkfree themselves. Instead, you should modifiy the functions (allockpagesandfreekpages)thatkmallocand kfreeuse to allocate and free physical memory.
Finally, note that when the kernel is booting—and before yourVM system has been initialized—the kernel will allocate memory for its data structures. OS/161 has a simple physical-memory allocation mechanism (in arch/mips/mips/ram.c)whichwillsupporttheseearlymemoryallocations.WhenyouinitializeyourVM system, you will need to make sure that it is aware that some parts of physical memory are already being used by the kernel, so that it does not mistakenly allocate that physical memory for some other purpose.
Your VM system is not required to re-use any parts of physicalmemory that are allocated to the kernel before your VM system is initialized—though it is allowed to doso,providedthekernelfreesupthespace.
Once your VM system has been initialized during the boot process, all subsequent physical-memory requests
(viaallockpagesandfreekpages)fromthekernelshouldbehandledbyyourVMsystem.



