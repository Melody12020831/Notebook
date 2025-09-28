---
statistics: True
comments: true
---

# Chapter 2 | Operating-System Structures

## Operating System Services

One set of operating-system services provides functions that are helpful to the **user** :

- **User interface** - Almost all operating systems have a user interface (UI) 提供用户界面（UI），包括命令行界面（CLI）和图形用户界面（GUI），方便用户与计算机交互。
- **Program execution** - The system must be able to load a program into memory and to run that program, end execution, either normally or abnormally (indicating error) 把程序装载到内存中并运行，程序运行结束后能正常或异常（出错）终止。
- **I/O operations** - A running program may require I/O, which may involve a file or an I/O device.
- **File-system manipulation** - The file system is of particular interest. Obviously, programs need to read and write files and directories, create and delete them, search them, list file Information, permission management.
- **Communications** – Processes may exchange information, on the same computer or between computers over a network. 进程之间需要交换信息。
- **Error detection** – OS needs to be constantly aware of possible errors

Another set of OS functions exists for ensuring the efficient operation of the system itself via **resource sharing** :

- **Resource allocation** - When multiple users or multiple jobs running concurrently, resources must be allocated to each of them 合理分配CPU、内存、I/O设备等资源。
- **Accounting** - To keep track of which users use how much and what kinds of computer resources 为资源管理、计费或优化提供依据。
- **Protection and security** - The owners of information stored in a multiuser or networked computer system may want to control use of that information, concurrent processes should not interfere with each other 信息的所有者希望控制信息的使用权限。操作系统要防止进程间互相干扰，保护数据和资源的安全。

---

## User Operating System Interface

### CLl

CLI allows **direct command** entry

- Sometimes implemented in **kernel**, sometimes by **systems program**
- Sometimes **multiple flavors** implemented – shells
- Primarily **fetches a command** from user and executes it

---

### GUI

**User-friendly** desktop metaphor interface

- Usually mouse, keyboard, and monitor
- Icons represent files, programs, actions, etc
- Various mouse buttons over objects in the interface cause various actions (provide information, options, execute function, open directory (known as a folder))

Many systems now include both CLI and GUI interfaces

---

## System Calls

Programming interface to the services provided by the OS

系统调用是操作系统为程序提供服务的编程接口。

Typically written in a high-level language (C or C++)

Mostly accessed by programs via a high-level Application Program Interface (API) rather than direct system call use

大多数情况下，程序通过高级 API **间接**访问系统调用。

Three most common APIs are **Win32 API** for Windows, **POSIX API** for POSIX- based systems (including virtually all versions of UNIX, Linux, and Mac OS X), and **Java API** for the Java virtual machine (JVM)

System call sequence to **copy** the contents of one file to another file

![img](./assets/2-1.png)

---

### System Call Implementation

Typically, a **number** associated with each system call

- System-call interface maintains a table indexed according to these numbers

每个系统调用都有一个**编号**，系统调用接口维护一个表，通过编号查找对应的系统调用。

The system call interface **invokes** intended system call in OS kernel and **returns status** of the system call and any return values

系统调用接口负责在内核中调用目标系统调用，并返回状态和结果。

The caller needs to know nothing about how the system call is implemented

调用者（程序员）无需关心系统调用的具体实现，只需遵循API规范，理解调用结果即可。

- Just needs to obey API and understand what OS will do as a result call
- Most details of OS interface hidden from programmer by API

![img](./assets/2-2.png)

![img](./assets/2-3.png)

---

### System Call Parameter Passing

Three general methods used to pass parameters to the OS

1. Simplest: pass the parameters in **registers**

    - In some cases, may be more parameters than registers
    - 最简单的方法，直接把参数放在CPU寄存器中。如果参数太多，寄存器不够用时不适用。

2. Parameters stored in a **block**, or table, in memory, and **address of block passed** as a parameter in a register

    - 把所有参数存放在内存中的一个块（或表）里，然后把这个块的地址作为参数传递。适合参数数量或长度不定的情况。
    - This approach taken by Linux and Solaris

3. Parameters placed, or pushed, onto the **stack** by the program and popped off the stack by the operating system

    - 程序把参数压入栈中，操作系统从栈中弹出参数。

**Block** and **stack** methods **do not limit the number** or length of parameters being passed

==Parameter Passing via Table==

![img](./assets/2-4.png)

---

## Types of System Calls

Process control、File management、Device management、Information maintenance (e.g. time, date)、Communications、Protection

![img](./assets/2-5.png)

---

## System Programs

System programs provide a convenient environment for program development and execution. They can be divided into:

- File manipulation
- Status information
- File modification
- Programming language support
- Program loading and execution
- Communications
- Application programs

Provide a convenient environment for program development and execution

**File management** - Create, delete, copy, rename, print, dump, list, and generally manipulate files and directories

**Status information**

- Some **ask the system for info** - date, time, amount of available memory, disk space, number of users
- Others provide **detailed performance**, logging, and debugging information
- Typically, these programs format and print the output to the terminal or other output devices
- Some systems implement a registry - used to store and retrieve configuration information

**File modification**

- **Text editors** to create and modify files
- **Special commands** to search contents of files or perform transformations of the text

**Programming-language support** - Compilers, assemblers, debuggers and interpreters sometimes provided

**Program loading and execution** - Absolute loaders, relocatable loaders, linkage editors, and overlay-loaders, debugging systems for higher-level and machine language

**Communications** - Provide the mechanism for creating virtual connections among processes, users, and computer systems

---

## Operating System Design and Implementation

Start by defining **goals** and **specifications**

Affected by choice of **hardware**, **type of system**

User goals and System goals

- User goals – operating system should be **convenient** to use, easy to learn, reliable, safe, and fast
- System goals – operating system should be **easy to design**, implement, and maintain, as well as flexible, reliable, error-free, and efficient

---

1. **Policy**: What will be done? 策略（确定具体做什么事）
2. **Mechanism**: How to do it? 机制（定义做事方式）

!!! tip

    === "课上的举例"

    policy like c file

    mechanism like PC

    === "🌰"

    机制：实现了“分配和回收内存块”的基本操作。

    策略：可以选择首次适应、最佳适应、最差适应等不同分配算法。

    好处：更换分配策略时，内存管理机制无需大改。

The separation of policy from mechanism is a very important principle, it allows maximum flexibility if policy decisions are to be changed later

---

## Simple Structure

以 MS-DOS 为例，说明早期操作系统的结构特点：

MS-DOS – written to provide the most functionality **in the least space**

- Not divided into modules
- Although MS-DOS has some structure, its interfaces and levels of functionality are **not well separated**

---

### MS-DOS Layer Structure

![img](./assets/2-6.png)

虽然图中有层次，但实际上各层之间的界限并不严格。比如，应用程序可以直接调用MS-DOS设备驱动，甚至直接访问ROM BIOS驱动，而不一定非要通过上层的resident system program。

各部分之间耦合度高，接口不统一，导致系统难以维护和扩展。

应用程序可以直接操作底层硬件，容易导致系统崩溃或安全隐患。

---

### Layered Approach

The operating system is divided into a number of layers (**levels**), each built on top of lower layers. The bottom layer (layer 0), is the hardware; the highest (layer N) is the user interface.

With **modularity**, layers are selected such that each uses functions (operations) and services of only lower-level layers

---

### Layered Operating System

操作系统被划分为若干层，每一层只依赖于它下方的那一层。

![img](./assets/2-7.png)

---

## UNIX

UNIX – limited by hardware functionality, the original UNIX operating system had limited structuring. The UNIX OS consists of two separable parts

- System programs
- The kernel

    - Consists of everything below the system-call interface and above the physical hardware
    - Provides the file system, CPU scheduling, memory management, and other operating-system functions; a large number of functions for one level

UNIX结构分为**系统程序**和**内核**两大部分。

---

### UNIX System Structure

![img](./assets/2-8.png)

- 用户空间（the users）: 最上层是用户，包括所有使用计算机的人。
- 系统程序（shells and commands, compilers and interpreters, system libraries）
- 系统调用接口（system-call interface to the kernel） : 这是应用程序和内核之间的桥梁。用户程序通过系统调用接口请求内核服务（如文件操作、进程管理等）。
- 内核（Kernel）: 内核是UNIX操作系统的核心，负责所有底层资源管理和硬件控制。信号与终端处理、字符I/O系统、终端驱动、文件系统、交换、块I/O系统、磁盘和磁带驱动、CPU调度、页面置换、请求分页、虚拟内存。
- 内核与硬件接口（kernel interface to the hardware）: 这是内核与底层硬件之间的接口，内核通过它来控制和管理硬件设备。
- 硬件控制器和设备（terminal controllers, device controllers, memory controllers）

---

## Microkernel System Structure

Moves as much from the kernel into “**user**” space

微内核只保留**最基本、最核心**的功能在内核态（kernel mode），如进程间通信（IPC）、内存管理、CPU调度等。

Communication takes place between **user modules** using **message passing**

Benefits:

- Easier to **extend** a microkernel. **增加**或修改系统服务时，只需更改用户态模块，不影响内核。
- Easier to **port** the operating system to new architectures. 内核代码少，**移植**到新硬件平台更**容易**。
- More **reliable** (less code is running in kernel mode). 大部分操作系统代码在用户态运行，内核态代码少，**出错影响范围小**。
- More **secure**. 内核态代码少，攻击面小，**安全性高**。

Detriments:

- **Performance overhead** of user space to kernel space communication. 用户态和内核态之间频繁消息传递，导致**性能下降**。

---

### Architecture of A Typical Microkernel

![img](./assets/2-9.png)

---

### Mac OS X Structure

![img](./assets/2-10.png)

更详细地展示了Darwin内核环境的内部结构。

1. application environments and common services（应用环境与通用服务）提供给应用程序的运行环境和常用服务。
2. BSD层。BSD是Berkeley Software Distribution的缩写，这一层提供了类Unix的系统接口，包括进程管理、文件系统、网络协议栈等，是macOS兼容Unix标准的关键部分。
3. Mach内核。Mach是一个微内核，负责最底层的任务，如进程/线程管理、内存管理、进程间通信（IPC）等。BSD层运行在Mach之上，利用Mach提供的底层机制实现更高层的操作系统功能。

---

### Mac OS Structure

![img](./assets/2-11.png)

每一层都为上层提供服务和接口，应用程序可以直接调用上层或部分底层框架的功能。

1. applications（应用程序）用户直接使用的各种应用软件
2. user experience（用户体验层）提供图形界面、窗口管理、动画、系统交互等用户可见的体验功能。
3. application frameworks（应用框架）为应用开发者提供的各种API和框架。
4. core frameworks（核心框架）提供更底层的系统服务。
5. kernel environment (Darwin)（内核环境）最底层，是macOS的内核。它负责硬件管理、进程调度、内存管理、驱动支持等所有底层功能。

---

## Modules

Most modern operating systems implement **kernel modules**

它将操作系统的各个核心功能划分为**独立的模块**（module），每个模块负责不同的功能。这些模块可以**根据需要被动态加载**或卸载到内核中。

- Uses **object-oriented** approach. 类似于面向对象中的“对象”，职责单一，接口明确。
- Each core component is **separate**. 核心组件分离。
- Each talks to the others over **known interfaces**. Modules call each other instead of message passing. 已知接口通信。
- Each is loadable as needed within the kernel. 按需加载。

Overall, similar to layers but more flexible

模块化结构类似于==分层结构==，但更加灵活。分层结构层次固定，模块化结构可以**动态组合和扩展**。

==微内核==将大部分服务移到用户态，通过消息传递通信，安全性高但性能有损耗。模块化内核则大部分模块仍在内核态，直接调用接口，**性能更高**。

---

### Solaris Modular Approach

![img](./assets/2-12.png)

---

## Other Structures

![img](./assets/2-13.png)

Unikernel: statically linked with the OS code needed.

Good for cloud service, APP boots in tens of milliseconds

Unikernel/Library OS结构的核心思想：应用、库和内核紧密集成，按需裁剪，极致精简，适合云原生和高安全性场景。

---