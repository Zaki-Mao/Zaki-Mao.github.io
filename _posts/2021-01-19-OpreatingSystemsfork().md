---
layout: post
title: Getpid()函数和fork()函数的解释
subtitle: CO003 Operating System Basic Process Management leture note
date: 2021-01-19
author: Zaki
header-img: img/home-bg-o.jpg
catalog: true
tags:
     - Operating System
     - C
     - Computer Science
     - Computer 
---

# getpid()函数

Each process is given an unique ID number, and is called the <strong>process ID</strong>, or the PID.

The system call, getpid(), prints the PID of the calling process.

创建任何进程时，它都有一个唯一的ID，称为其进程ID。 该函数返回调用函数的进程ID。

#### code example

      #include <stdio.h>
      #include <sys/types.h>
      #include <unistd.h>
 
       int main(void)
     {
	     //variable to store calling function's process id
	     pid_t process_id;
	     //variable to store parent function's process id
	     pid_t p_process_id;
 
	     //getpid() - will return process id of calling function
	     process_id = getpid();
	     //getppid() - will return process id of parent function
	     p_process_id = getppid();
 
	     //printing the process ids
	     printf("The process id: %d\n",process_id);
	     printf("The process id of parent function: %d\n",p_process_id);
 
	     return 0;
      }

值得注意的是，getppid()函数表示返回父函数的进程id。

注意： pid_t是进程ID的类型，它是数据类型的无符号整数类型。

头文件注意：

stdio.h - it is used for printf() function.

stdio.h-用于printf()函数。

sys/types.h - it is used for pid_t type, that is the data type of the variables which are using to store the process ids.

sys / types.h-用于pid_t类型，即用于存储进程ID的变量的数据类型。

unistd.h - it is used for getpid() and getppid() functions.

unistd.h-用于getpid()和getppid()函数。

# fork() 函数

To create a process, we use the system call fork().

fork（）函数通过系统调用创建一个与原来进程几乎完全相同的进程，也就是两个进程可以做完全相同的事。如下图所示。

![](https://tva1.sinaimg.cn/large/008eGmZEgy1gmu46bvm8uj30p80btwft.jpg )

#### code example

     #include <unistd.h>  
     #include <stdio.h>   
     int main ()   
     {   
     pid_t result; //result表示fork函数返回的值  
     int count=0;  
     result=fork();   
     if (result < 0)   
        printf("error in fork!");   
     else if (result == 0) {  
        printf("i am the child process, my process id is %d/n",getpid());   
        printf("我是子进程/n");
        count++;  
     }  
     else {  
        printf("i am the parent process, my process id is %d/n",getpid());   
        printf("我是父进程/n");  
        count++;  
     }  
     printf("统计结果是: %d/n",count);  
     return 0;  
     }  

运行结果是：

      i am the child process, my process id is 5574
 
      我是子进程
 
 统计结果是: 1
 
      i am the parent process, my process id is 5573
 
      我是父进程

 统计结果是: 1
 
在语句result=fork()之前，只有一个进程在执行这段代码，但在这条语句之后，就变成两个进程在执行了，这两个进程的几乎完全相同。

<strong>fork调用的一个奇妙之处就是它仅仅被调用一次，却能够返回两次，它可能有三种不同的返回值：</strong>

    1）在父进程中，fork返回新创建子进程的进程ID；
    
    2）在子进程中，fork返回0；
    
    3）如果出现错误，fork返回一个负值；
    
Both the parent and the child processes execute the same programcode after fork().

The child process is not starting its execution from the beginning of the program code.

The child process starts its execution after the location that fork() is called.

在fork函数执行完毕后，如果创建新进程成功，则出现两个进程，一个是子进程，一个是父进程。在子进程中，fork函数返回0，在父进程中，fork返回新创建子进程的进程ID。我们可以通过fork返回的值来判断当前进程是子进程还是父进程。

<strong>其实就相当于链表，进程形成了链表，父进程的result指向子进程的进程id,因为子进程没有子进程，所以其result为0。</strong>






