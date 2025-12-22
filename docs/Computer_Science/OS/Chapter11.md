---
statistics: True
comments: true
---

# Chapter 11 | File System Implementation

Tmpfs, a temporary file system in memory, fast but not persistent

一种基于内存的临时文件系统，速度非常快，但数据不会持久保存（重启后数据丢失）。常用于存放临时文件，比如 /tmp 目录。

Squashfs, a read-only compressed file system supporting fast access

一种只读的压缩文件系统，支持快速访问。常用于嵌入式系统、LiveCD 等场景，节省存储空间。

Ext4, the main Linux journaling file system, reliable

Linux 下主流的日志型文件系统，具有高可靠性和较好的性能。支持大文件、日志记录（防止数据丢失）。

Ceph, an open source distributed and scalable file system

一个开源的分布式、可扩展文件系统，适合大规模存储集群。支持高可用性和弹性扩展。

FAT, simple and robust file system widely used for compatibility

文件分配表（File Allocation Table），一种简单、健壮且兼容性极强的文件系统。广泛用于U盘、SD卡等移动存储设备。

- Why so many file systems?
- File system is still one of the most active areas of OS research!

为什么有这么多文件系统？

不同的应用场景、性能需求、兼容性要求等，导致需要不同类型的文件系统。

---

## File-System Structure

File structure（文件结构）

- Logical storage unit
- Collection of related information

文件是逻辑存储单元，是相关信息的集合。

File system resides on secondary storage (disks)

文件系统通常存放在二级存储设备（如磁盘）上。

File system is composed of many layers

文件系统由多个层次组成，每一层负责不同的功能。

**Layered File System**

![img](./assets/11-1.png)

1. 应用程序/用户接口层

作用：为用户和应用程序提供访问文件的接口，如 `open`、`read`、`write`、`close` 等系统调用。

例子：你在命令行输入 `cat file.txt`，或用 Python 的 `open()` 读写文件，都是通过这一层。

2. 逻辑文件系统层

作用：管理文件的元数据（如文件名、权限、目录结构），实现文件的命名空间、访问控制、目录操作等。

例子：决定 `/home/user/file.txt` 这个路径如何映射到具体的文件对象。

3. 文件组织模块

作用：负责文件的逻辑结构与物理结构之间的映射，比如文件如何分块存储、如何分配和释放空间。

例子：决定文件内容分布在哪些磁盘块上，如何查找和分配空闲块。

4. 基本文件系统层

作用：提供对物理块的基本读写操作，管理缓存、调度磁盘 I/O 请求。

例子：实现“读第 100 号磁盘块”或“写入第 200 号磁盘块”这样的操作。

5. I/O 控制层

作用：负责与设备驱动程序交互，发出具体的硬件操作命令（如启动磁盘读写、检测设备状态）。

例子：把“读第 100 号块”的请求转化为磁盘控制器能理解的命令。

6. 设备层

作用：实际的物理存储设备，如硬盘、SSD、U盘等。

例子：真正存储数据的硬件部分。

---

## Data Structures Used to Implement FS

Disk structures

这些结构永久存储在磁盘上，即使关机也不会丢失，是文件系统的核心元数据。

- Boot control block (per volume)
- Volume control block per volume (superblock in Unix)
- Directory structure per file system
- Per-file FCB (inode in Unix)

1. Boot control block（引导控制块）

- 每个卷（volume）有一个。
- 作用：包含启动操作系统所需的信息（如引导程序），通常位于磁盘的最前面。

2. Volume control block（卷控制块）

- 每个卷有一个，在 Unix 中叫 superblock（超级块）。
- 作用：记录整个文件系统的全局信息，如总块数、空闲块数、inode 数量、文件系统类型等。

3. Directory structure（目录结构）

- 每个文件系统有一套目录结构。
- 作用：保存文件和目录的层次关系、文件名到 inode/FCB 的映射。
- 例子：`/home/user/` 目录下有哪些文件和子目录。

4. Per-file FCB（文件控制块）

- FCB（File Control Block），在 Unix 中叫 inode。
- 作用：记录单个文件的元数据，如文件大小、所有者、权限、数据块指针、时间戳等。

In-memory structures (see fig)

这些结构只存在于内存中，用于加速文件系统操作，提高效率，关机后会丢失。

- In-memory mount table about each mounted volume
- Directory cache for recently accessed directories
- System-wide open-file table
- Per-process open-file table

1. In-memory mount table（内存中的挂载表）

- 记录当前系统已挂载的所有卷的信息（如挂载点、文件系统类型等）。
- 作用：让操作系统知道哪些文件系统已经挂载到哪些目录。

2. Directory cache（目录缓存）

- 缓存最近访问过的目录信息。
- 作用：加快目录查找速度，减少磁盘访问次数。

3. System-wide open-file table（系统级打开文件表）

- 记录系统中所有进程当前打开的文件信息（如文件指针、引用计数等）。
- 作用：实现文件共享、管理文件的全局状态。

4. Per-process open-file table（每个进程的打开文件表）

- 每个进程有自己的打开文件表，记录该进程打开的文件及其状态（如读写指针、访问模式等）。
- 作用：支持多进程独立访问文件。

---

### A Typical File control Block

**File control block** – storage structure consisting of information about a file

FCB 是文件系统用来描述和管理单个文件的核心数据结构。

![img](./assets/11-2.png)

1. file permissions: 记录谁可以对该文件进行读、写、执行等操作。
2. file dates (create, access, write): 文件时间戳：创建、访问、修改。
3. file owner, group, ACL: 文件所有者、所属组、访问控制列表。
4. file size: 文件大小（以字节为单位）。
5.  file data blocks or pointers to file data blocks（文件数据块或指向数据块的指针）: 记录文件实际内容存放在磁盘上的位置。可能直接存储数据块编号，也可能是指向数据块的指针（如 inode 结构中的直接、间接块指针）。

!!! info "NOTICE"
    FCB 里面是不存储文件名的，文件名存储在目录结构中，并通过目录项与 FCB 关联。

    为什么？因为一个文件可能有多个名字（硬链接），如果把文件名存储在 FCB 里，会导致数据冗余和一致性问题。

---

### In-Memory File System Structures

The following figure illustrates the necessary file system structures provided by the operating systems.

- Figure 12-3(a) refers to **opening** a file.
- Figure 12-3(b) refers to **reading** a file.

![img](./assets/11-3.png)

(a) 打开文件（open）

1. 用户空间（user space）用户进程发出 `open(file name)` 请求，想要打开一个文件。
2. 内核内存（kernel memory）

- 操作系统在内存中维护目录结构（directory structure），用于查找文件名对应的文件。
- 目录结构会指向磁盘上的实际目录结构和文件控制块（file-control block, FCB/inode）。

3. 外存（secondary storage）

- 目录结构和文件控制块实际存储在磁盘上，内存中只缓存部分信息以加速访问。
- 打开文件时，系统会把相关目录项和文件控制块信息加载到内存。

(b) 读取文件（read）

1. 用户空间（user space）用户进程发出 `read(index)` 请求，想要读取文件内容。
2. 内核内存（kernel memory）

- 每个进程有自己的打开文件表（per-process open-file table），记录该进程打开的文件及其状态（如读写指针）。
- 系统还有一个系统级打开文件表（system-wide open-file table），记录所有进程当前打开的文件信息，实现文件共享和全局管理。
- 进程的打开文件表通过索引（index）指向系统级打开文件表。

3. 外存（secondary storage）系统级打开文件表会指向磁盘上的文件控制块（file-control block），文件控制块再指向实际的数据块（data blocks），即文件内容所在的磁盘位置。

---

## Virtual File Systems

Virtual File Systems (VFS) provide an object-oriented way of implementing file systems. VFS is NOT a disk file system!

**VFS（虚拟文件系统）**是一种“面向对象”的文件系统实现方式。它不是实际存储数据的磁盘文件系统，而是一个“中间层”或“抽象层”，为不同类型的文件系统（如 ext4、FAT、NFS 等）提供统一的接口和管理机制。

VFS allows the same system call interface (the API) to be used for different types of file systems.

VFS 让操作系统可以用同一套系统调用接口（API）（如 open、read、write、close）来访问不同类型的文件系统。用户和应用程序不需要关心底层文件系统的具体实现，只需调用统一的 API。

The API is to the VFS interface, rather than any specific type of file system.

应用程序和用户通过 API 访问的是 VFS 接口，而不是某个具体的文件系统（比如 ext4 或 FAT）。VFS 负责把这些通用的 API 请求“翻译”并分发到对应的底层文件系统驱动。

Defines a network-wide unique structure called **vnode**.

VFS 定义了一种叫做 vnode（虚拟节点）的结构。vnode 是对“文件”或“目录”的统一抽象，无论底层是本地磁盘文件、远程网络文件，还是其他类型的文件系统，VFS 都用 vnode 来表示和管理它们。vnode 使得跨网络、跨文件系统的操作变得统一和透明。

**Schematic View of Virtual File System**

![img](./assets/11-4.png)

---

### In-Memory VFS objects

The four primary object types of VFS:

- superblock object: a specific mounted filesystem，对应(但不是)磁盘文件系统的文件系统超级块或控制块。
- inode object: a specific file, 对应(但不是)磁盘文件系统的文件控制块
- dentry object: an individual directory entry
- file object: an open file as associated with a process, 只要文件一直打开，这个对象就一直存在于内存。

---

## Directory Implementation

**Linear list** of file names with pointer to the data blocks.

目录用一个线性表（数组或链表）来存储所有文件名及其对应的数据块指针。

- simple to program
- time-consuming to execute

**简单易实现**：只需顺序存储文件名和指针，编程简单。

**查找慢**：每次查找文件时，都要从头到尾顺序遍历整个列表，效率低，尤其是目录项很多时。

**Hash Table** – linear list with hash data structure.

在原有线性表的基础上，增加了哈希数据结构，通过哈希函数将文件名映射到哈希表中的位置。

- decreases directory search time
- **collisions** – situations where two file names hash to the same location
- fixed size – can use chained-overflow hash table
- Or rehashing to another larger hash table

**查找快**：大大减少了查找时间，通常接近常数时间（O(1)）。

**冲突**（collisions）：不同文件名可能被哈希到同一个位置，需要解决冲突（如链式哈希、开放定址等）。

**固定大小**：哈希表通常有固定大小，目录项过多时可能需要扩容（rehashing）。

---

## Allocation Methods

An allocation method refers to how disk blocks are allocated for files:

- Contiguous allocation 连续分配
- Linked allocation 链接分配
- Indexed allocation 索引分配

---

### Contiguous Allocation

Each file occupies a set of contiguous blocks on the disk

每个文件在磁盘上占据一组连续的块。只需记录起始块号和长度（块数），即可定位整个文件。

Simple – only starting location (block #) and length (number of blocks) are required

**实现简单**：只需两个参数（起始位置和长度）。

Random access supported

**支持随机访问**：可以直接通过偏移量定位到文件的任意位置，访问速度快。

Wasteful of space (dynamic storage-allocation problem)

**空间利用率低**：容易产生“外部碎片”，即磁盘上有很多小的空闲块，但无法满足大文件的连续分配需求。

Files cannot grow

**文件不能动态增长**：如果文件需要扩展，后面空间可能已被其他文件占用，导致扩展困难。

Mapping from logical to physical

![img](./assets/11-5.png)

- LA：逻辑地址（文件内部的字节编号，从0开始）
- 512：每个磁盘块的大小（单位：字节），这里假设每块512字节
- Q：逻辑块号（文件内第几个块，从0开始）
- R：块内偏移（逻辑地址在块内的字节偏移）

![img](./assets/11-6.png)

---

#### Extent-Based Systems

Many newer file systems use a modified contiguous allocation scheme

现代文件系统对连续分配做了改进，采用区段（extent）分配。

Extent-based file systems allocate disk blocks in **extents**

一个extent是若干连续磁盘块的集合。

An **extent** is a contiguous block of disks

一个文件可以由多个extent组成，每个extent仍是连续的。

- Extents are allocated for file allocation 文件可以动态增长，只需为新数据分配新的extent。
- A file consists of one or more extents. 文件由一个或多个extent组成。

---

### Linked Allocation

Each file is a linked list of disk blocks: blocks may be scattered anywhere on the disk.

每个文件在磁盘上由一系列分散的磁盘块组成，这些块通过指针串联成一个链表。

![img](./assets/11-7.png)

每个磁盘块除了存放数据外，还存放一个指向下一个块的指针。只需记录文件的起始块号，就可以通过指针依次找到文件的所有数据块。

Simple – need only starting address

**实现简单**：只需记录起始地址，后续块通过指针串联。

Free-space management system – no waste of space

**空间利用率高**：磁盘空间不会产生外部碎片，空闲块可以灵活利用。

**No random access, poor reliability**

**不支持随机访问**：要访问文件的第n个块，必须从头顺序遍历n次，效率低。

**可靠性差**：如果某个块的指针损坏，后续数据就无法访问，链断了。

**指针占用空间**：每个块都要存储指针，会占用一部分存储空间。

Mapping

![img](./assets/11-8.png)

![img](./assets/11-9.png)

File-allocation table (FAT) – disk-space allocation used by MS-DOS and OS/2.

FAT 是一种特殊的链接分配实现方式，广泛用于 MS-DOS、Windows 的 FAT12/16/32 文件系统，以及U盘、SD卡等。

文件分配表（FAT）是一个数组，每个元素对应一个磁盘块，存储该块的“下一个块号”。

文件的目录项只需记录起始块号，后续块号通过查表依次获得。

![img](./assets/11-10.png)

FAT 表较大时，需常驻内存，占用空间。

随机访问效率较低，需要多次查表。

---