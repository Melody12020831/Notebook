---
statistics: True
comments: true
---

# Ch2 | Memory Hierarchy Design

Basics of Memory Hierarchies:

大多数已经在[CO📖](https://melody12020831.github.io/Notebook/Computer_Science/CO/Chapter%205/)当中提及过，因此这里不再赘述。

To gain insights into the causes of high miss rates, which can inspire better cache designs, the three Cs model sorts all misses into three simple categories:

为了深入理解造成高缺失率的原因，从而更好地设计缓存，"3C"模型将所有这些缺失情景分为以下3个简单的类别。

- **Compulsory miss** ：对数据块的第一次访问肯定不会在缓存中，所以必须将这个块放入缓存中。即使拥有无限大的缓存，也会发生强制缺失。
- **capacity miss** ：如果缓存不能包含程序运行期间所需要的全部块，就会因为有些块先被丢弃之后再被调人而导致容量缺失(除了强制缺失之外)。
- **conflict miss** ：如果块放置策略不是全相联的，并且多个块映射到一个块的组中，对不同块的访问混杂在一起，那么一个块可能会被丢弃，之后再被调人，从而发生冲突缺失(除强制缺失和容量缺失之外)。

---

## Memory Technology and Optimizations

### SRAM

The first letter of SRAM stands for *static*.

DRAM 电路的动态本质要求在读取数据之后将其写回，因此在访问时间和周期时间之间存在差异，并需要进行刷新。

- SRAM不需要刷新，所以访问时间与周期时间非常接近。
- SRAM通常使用 6 个品体管保存 1 位数据，以防止在读取信息时对信息造成干扰。
- 在待机模式下，SRAM只需要很少的功耗来维持电荷。

??? note "about access time and the cycle time"
    访问时间是从发出读取请求到收到所需字之间的时间。
    
    周期时间是指对存储器发出的两次不相关请求之间的最短时间间隔。

片上缓存 SRAM 的宽度通常与缓存的块大小相匹配，每个块对应的标签都与其并行存储。这样就可以在单个时钟周期内读取或写入整个块。在将缺失后获取的数据写人缓存时，或在写回一个必须从缓存中清除的块时，此功能特别有用。

??? note "并行存储"
    数据存储时，多个数据单元可以同时被访问或传输。在片上缓存 SRAM 中，每个缓存块的数据和标签信息被存储在不同的存储单元中，但在访问时能够同时读取或写入。

---

### DRAM

在早期 DRAM 的容量增大时，由于封装需要提供所有必要的地址线，所以封装成本较高。解决方案是复用地址线，从而将地址管脚数减半。

先在行选通(row access strobe,**RAS**)期间发送一半地址，然后在列选通(column access strobe,**CAS**)期间发送另一半地址。行选通和列选通这两个名字源于芯片的内部结构，这些存储器的内部是一个按行和列寻址的长方形矩阵。

![DRAM的基本结构](./assets/2-1.png)

对 DRAM 的另一要求来自其第一个字母 D 表示的特性，即 dynamic。

为了在每个芯片中容纳更多的位，DRAM 仅使用一个晶体管(实际上相当于一个电容器)来存储一位数据。

这有两层含意：

1. 用来检测电荷的传感线必须进行预充电，使其设定为介于逻辑 0 和逻辑 1 之间的'中间”状态，这样，只需在单元中存储很少量的电荷就可以使灵敏放大器(sense amplifier)检测到逻辑 0 或 1 。
2. 在读取时，将一行放入行缓冲器中，CAS 信号可以在这里选择从 DRAM 中读取该行的一部分。因为对数据行的读取过程会破坏其中的信息，所以当不再需要该行时，必须将其写回。这一写回过程以重叠方式进行，但在早期的DRAM中，这意味着在读取一行并访问该行的一部分之后，还需要等待一定的时间才能读取一个新行。
此外，为了防止单元中的电荷泄漏(假设既没有读取它，也没有写人它)而导致信息丢失必须定期“刷新”每个位。幸运的是，只需对一行进行读取并将其写回，就可以同时刷新该行中的所有位。因此，存储器系统中的每个DRAM必须在特定时间窗口内(比如64ms)访问每一行。存储器控制器包括定期刷新 DRAM 的硬件。

### SDRAM

设计人员向 DRAM 接口中增加了一个时钟信号,这样重复进行的传输就不再需要额外的同步时间,这就是同步DRAM(synchronous DRAM, SDRAM)。

21世纪早期又推出了另外一项创新:双倍数据速率(double datarate，DDR)，它使 DRAM 在存储器时钟周期的上升沿和下降沿都能传输数据，从而使峰值数据传输速率翻了一番。

最后，SDRAM引入了体(bank，即存储体)，用于帮助功耗管理、缩短访问时间，并允许对不同存储体进行相互交织、重叠的访问。对不同存储体的访问可以相互重叠，每个存储体都有自己的行缓冲区。在一个 DRAM 中创建多个存储体实际上是为该地址又增加了一个段，现在的地址由存储体编号、行地址和列地址组成。在发出一个新存储体的地址时，必须打开这个存储体，从而增加延迟时间。存储体和行缓冲区的管理完全由现代存储器控制接口处理，所以当后续地址指定的是一个已打开存储体中的相同行时，只需发送列地址，从而可以快速进行访问。要发起一次新的访问过程，DRAM 控制器发送一个存储体编号和一个行号(在SDRAM中称为**激活**—— Activate ，之前称为 RAS ——行选通)。这个命令会打开该行，并将整行数据读人一个缓冲区中。然后会发送一个列地址，SDRAM 可以传送一个或多个数据项，具体取决于是单个请求还是突发请求。在访问新行之前，必须对存储体进行预充电。如果该行位于同一存储体内，则会感觉到预充电导致的延迟;但如果这个新行位于另一个存储体中，那么行的关闭和存储体的预充电可以与新行的访问重叠进行。在 SDRAM 中，这些命令周期中的每一个都需要整数个时钟周期。

**Reducing Power Consumption in SDRAMs**

动态存储芯片中的功耗由静态(或待机)功耗和读写期间消耗的动态功耗构成，这两者都取决于工作电压。存储体的增加也降低了功耗，这是因为每次仅读取一个存储体中的行。

除了这些变化之外，所有最新 SDRAM 都支持一种断电模式,通知 DRAM 忽略时钟即可进人这一模式。断电模式会禁用 SDRAM，但内部自动刷新除外(如果没有自动刷新，当进人省电模式的时间长于刷新时间时，将会导致存储器内容丢失)。从低功耗模式返回正常模式所需的确切延迟时间取决于 SDRAM .但一般的延迟为 200 个 SDRAM 时钟周期。

---

### Flash Memory

闪存是一种 EEPROM(电可擦可编程只读存储器)，它通常是只读的，但可以擦除。闪存的另一个重要特性是能在没有供电的情况下保存其内容。

Flash uses a very different architecture and has different properties than standard DRAM. The most important differences are

1. Reads to Flash are sequential and read an entire page.
2. Flash memory must be erased before it is overwritten, and it is erased **in blocks** rather than individual bytes or words.
3. Flash memory is nonvolatile. (非易失性的)
4. Flash memory limits the number of times that any given block can be written, typically at least 100,000.