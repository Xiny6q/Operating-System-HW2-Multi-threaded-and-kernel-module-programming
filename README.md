Download link :https://programming.engineering/product/operating-system-hw2-multi-threaded-and-kernel-module-programming/

# Operating-System-HW2-Multi-threaded-and-kernel-module-programming
Operating System HW2 Multi-threaded and kernel module programming
Objectives

Multi-threaded Program

Take advantage of multi-core systems

Load sharing

Linux Kernel Module

Understand how to write a kernel module

Understand how to provide read/write operations of proc files to users


Requirement – Kernel Module

You have to write a kernel module named My_proc

The kernel module has to create a proc file with pathname /proc/thread_info during its initialization/loading

You have to implement file operations of the proc file

User threads will write their thread ids to the proc file. When a user thread writes its id, the kernel module should record the thread id, get the thread execution time and context switch count of the thread.

*Note: thread execution time can be obtained from utime, and context switch count

nvcsw + nivcsw, where utime, nvcsw and nivcsw are fields of a task structure.

When the proc file is read, the thread relationships and the above timing information of all the recorded threads should be output to the reader.

Refer to Reference 4 for kernel module programming!


Requirement – Multi-threaded Program

You need to write a multithreaded program to perform matrix multiplication.

The program starts with a single main/parent thread, which is responsible for creating multiple worker threads.

Each worker thread should perform a part of the matrix multiplication job.

Each worker thread should write its thread ID to the proc file right before its termination. (May cause race condition, slide 7 and 8 shows description of race condition)

After completing the matrix multiplication, the main thread has to read the proc file and print the following resulting information on the console (Slide 10 shows an example) .

Main/parent thread ID

Each worker/child thread ID and execution time and context switch times.

After completing the matrix multiplication, the program also has to save the result of the matrix multiplication (i.e. the result matrix) to a file named as result.txt.


Requirement – Multi-threaded Program

You should hand in a report. In the report,

You have to explain how you dispatch works to the worker threads.

For example : by row dispatch or by element dispatch

You are given four test cases. For each test case, you have to plot the matrix multiplication execution time with the following worker thread numbers.

Worker thread number: 1,2,3,4,8,16,24,32

You have to summarize the four charts you plot.

For example :

What happen if the number of threads is less than the number of cores. Why ?

What happen if the number of threads is greater than the number of cores. Why ?

Anything else you observe


Requirement – Multi-threaded Program

8. The executable and parameters of your multithread program:

./MT_matrix [number of worker threads] [file name of input matrix1] [file name of input matrix2]

The VM memory should be set to 4 GB, and the VM cores should be set to 4 cores.

Steps to set your VM memory and cores are shown in Slide 16.

If you can’t set your VM memory and cores as requested, you should set them as large as possible.


Race condition

A race condition is an undesirable situation that occurs when two or more threads can access shared resources and they try to change it at the same time.

Assume that two threads each increment the value of a global integer variable named count by 1.

In ideal case , we hope the value of count variable is 2.

Each thread has its own registers.

Split increment the value by 1 into three steps.


Critical section

Parts of the multithreaded program where the shared resource is accessed by more than one thread need to be protected.

This protected section cannot be entered by more than one thread at a time.

You can use pthread_mutex_lock(pthread_mutex_t *mutex) and

pthread_mutex_unlock(pthread_mutex_t *mutex) to protect critical section.

In the requirement of multi-threaded program, the fourth requirement mentioned that each worker thread should write its thread ID to the proc file right before its termination.

The fourth requirement may cause race condition because more than one worker thread write to the proc file at the same time.

You can use mutex lock to guard write operation to ensure kernel module can correctly record the  required information. 8

Input/Output Matrix Format

You are given four test cases. Each test case contains two input matrix files.

In a matrix file, the first line indicates the row and column of the matrix.

1 <= element value <= 1000

The output matrix format is the same as input matrix format.


An Example Display Format of the Output

Output format : PID : [PID number]

[\t] ThreadID : [TID number] time : [utime](ms) context switch times : [Context switches]

Context switches = nvcsw + nivcsw.

The resolution of time is millisecond.


An Example Format of Charts in the Report

Chart format:

Chart title : Elapsed time with different number of worker threads

X-axis title : number of worker threads

Y-axis title : Elapsed time (s)


T1

pthread_create()

Elapsed time

matrix_multiplication

＝

T2–T1

pthread_join()

T2


The resolution of elapsed time is second.


Precautions

You should implement hw2 with C language.

You will get files from hw2 github classroom.

You can modify makefile as you want.

Make sure your makefile can compile your codes and create the executable file.

The executable file name should be : MT_matrix.

The kernel module name should be : My_proc.

Make sure your codes can be compiled and run in the DEMO environment introduced in the HW0 slide.


GitHub classroom

Github classroom :

Click here to start your assignment.

Test Cases :

Click here to download test cases.

Due Date :

2022/11/25 (Fri. ) 23:59:59 (以 github 上傳時間為準)


Grading

For the multi-threaded part, TA will do some tests to check whether the result is correct.

Be sure to partition the matrix multiplication job to all the worker thread(s). TA will check your program !

For the kernel module part, TA will vary the number of worker threads to check whether you can obtain correct information from the proc file.

You need to explain to TA how you implement your multi-threaded program and kernel module.

If you cannot explain smoothly, you will not get scored.


Reference

Matrix multiplication

pthreads(7) – Linux manual page

Task_struct

The Linux Kernel Module Programming Guide

The /proc Filesystem


How to set VM memory sizes and core numbers


1. Click Settings



2. Click System



3. Set Base Memory to 4GB



4. Set Processors to 4 CPUs

5. Click OK !


19
