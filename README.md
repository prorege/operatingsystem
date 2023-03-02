# operatingsystem

## Introduction

- What Programs do?
1. fetch 2. decode 3. execute 4. update

- Virtualization   
   The primary way the OS does this is through a general technique that we call virtualization. That is, the OS takes a physical resource (such as the processor, or memory, or a disk) and transforms it into a more general, powerful, and easy-to-use virtual form of itself. Thus, we sometimes refer to the operating system as a virtual machine.

- Resource manager   
Because virtualization allows many programs to run (thus sharing the CPU), and many programs to concurrently access their own instructions and data (thus sharing memory), and many programs to access devices (thus sharing disks and so forth), the OS is sometimes known as a ***resource manager***. Each of the CPU, memory, and disk is a resource of the system; it is thus the operating system’s role to manage those resources, doing so efficiently or fairly or indeed with many other possible
goals in mind. To understand the role of the OS a little bit better, let’s take a look at some examples.

[운영체제 개요 : 기록하는 프로그래밍 공간 참고](https://programming-workspace.tistory.com/26)

### CPU Virtualization

```C

#include <stdio.h>
#include <stdlib.h>
#include <sys/time.h>
#include <assert.h>
#include "common.h>

int main(int argc, char *argv[])
{ 
  if(argc != 2) {
    fprintf(stderr, "usage: cpu <string>\n");
    exit(1);
  }
  char*str = argv[1];
  while(1){
    spin(1);
    printf("%s\n", str);
  }
  return 0;
}
```

You might also notice that the ability to run multiple programs at once raises all sorts of new questions. For example, if two programs want to run at a particular time, which should run? This question is answered by a ***policy*** of the OS; policies are used in many different places within an OS to answer these types of questions, and thus we will study them as we learn about the basic mechanisms that operating systems implement(such as the ability to run multiple programs at once). Hence the role of the OS as a resource manager



### Memory Virtualization


```C
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>
#include "common.h"
int
main(int argc, char *argv[])
{
int *p = malloc(sizeof(int)); // a1
 assert(p != NULL);
 printf("(%d) address pointed to by p: %p\n",
 getpid(), p); // a2
 *p = 0; // a3
 while (1) {
    Spin(1);
    *p = *p + 1;
    printf("(%d) p: %d\n", getpid(), *p); // a4
 }
 return 0;
```
```
prompt> ./mem
(2134) address pointed to by p: 0x200000
(2134) p: 1
(2134) p: 2
(2134) p: 3
(2134) p: 4
(2134) p: 5
ˆC

c 2008–20, ARPACI-DUSSEAU
THREE
EASY
PIECES
6 INTRODUCTION TO OPERATING SYSTEMS
prompt> ./mem &; ./mem &
[1] 24113
[2] 24114
(24113) address pointed to by p: 0x200000
(24114) address pointed to by p: 0x200000
(24113) p: 1
(24114) p: 1
(24114) p: 2
(24113) p: 2
(24113) p: 3
(24114) p: 3
(24113) p: 4
(24114) p: 4
...

```
Indeed, that is exactly what is happening here as the OS is virtualizing memory. Each process accesses its own private virtual address space (sometimes just called its address space), which the OS somehow maps onto the physical memory of the machine. A memory reference within one running program does not affect the address space of other processes (or the OS itself); as far as the running program is concerned, it has physical memory all to itself. The reality, however, is that physical memory is
a shared resource, managed by the operating system. Exactly how all of this is accomplished is also the subject of the first part of this book, on the topic of virtualization.


### Concurrency

 The problems of concurrency arose first within the operating
system itself; as you can see in the examples above on virtualization, the
OS is juggling many things at once, first running one process, then another, and so forth. As it turns out, doing so leads to some deep and
interesting problems.

```C
#include <stdio.h>
#include <stdlib.h>
#include "common.h"
#include "common_threads.h"

volatile int counter = 0;
int loops;
 void *worker(void *arg) {
   int i;
   for (i = 0; i < loops; i++) {
   counter++;
   }
   return NULL;
 }

 int main(int argc, char *argv[]) {
   if (argc != 2) {
     fprintf(stderr, "usage: threads <value>\n");
     exit(1);
   }
   loops = atoi(argv[1]);
   pthread_t p1, p2;
   printf("Initial value : %d\n", counter);

   Pthread_create(&p1, NULL, worker, NULL);
   Pthread_create(&p2, NULL, worker, NULL);
   Pthread_join(p1, NULL);
   Pthread_join(p2, NULL);
   printf("Final value : %d\n", counter);
 return 0;

```
As it turns out, the reason for these odd and unusual outcomes relate to how instructions are executed, which is one at a time. Unfortunately, a key part of the program above, where the shared counter is incremented, takes three instructions: one to load the value of the counter from memory into a register, one to increment it, and one to store it back into memory. Because these three instructions do not execute atomically (all at once), strange things can happen. It is this problem of concurrency that we will address in great detail in the second part of this book.


### Persistence

The software in the operating system that usually manages the disk is called the file system; it is thus responsible for storing any files the user creates in a reliable and efficient manner on the disks of the system.      


Unlike the abstractions provided by the OS for the CPU and memory, the OS does not create a private, virtualized disk for each application. Rather, it is assumed that often times, users will want to share information that is in files.

### Design Goals








