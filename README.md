# data-structure-for-coding-interviews

## Random Access Memory(RAM)

当电脑运行一段代码的时候，需要跟踪一些变量（numbers,strings,arrays,etc）。

这些变量是被存储在 **radom access memory（RAM）中**  。我们有时候会叫RAM“工作内存”或者仅仅叫“内存”。

> RAM不是MP3s或者app存储的地方。说到"内存",我们的电脑里有storage（有时候我们称它为"persistent storage"或者"disc"）.memory我们说的是保存变的函数可以分配内存，storage是我们保存文件的地方，像mp3，视频，word文档或者执行程序或者apps。emory(RAM)速度很快，但是空间很少，storage或者disk速度会更慢一些但是空间很多。现代笔记本可能会有500GB的storage，但是可能只有16GB的RAM。

你可以把RAM想象成书架，这个书架上面有很多格子，几亿个格子。


![](https://www.interviewcake.com/images/svgs/cs_for_hackers__ram_empty_no_indices.svg?bust=150)

格子上面会有数字标识。

![](https://www.interviewcake.com/images/svgs/cs_for_hackers__ram_empty_with_indices.svg?bust=150)

我们把这些数字叫做 **址(address)** 。

每个格子装有8**比特(bits)**。每一个比特就是一个小的电子开关。“开”和“关”分别代表1和0。

![](https://www.interviewcake.com/images/svgs/cs_for_hackers__ram_bits.svg?bust=150)

8 bits 称为1 **字节(byte)** .每个格子都有一个8byte的存储空间。
当然，我们还有一个处理器。这个处理器做更具体的工作。

![](https://www.interviewcake.com/images/svgs/cs_for_hackers__ram_processor.svg?bust=150)

处理器和 **内存控制器（memory controller)** 相连。内存控制器从RAM中读取和写入数据。它和RAM的每个格子都有直接的联系。

![](https://www.interviewcake.com/images/svgs/cs_for_hackers__ram_memory_controller.svg?bust=150)

内存控制器和每个格子都有直接的联系这个很重要。这意味着我们可以访问0地址，然后可以立即访问91133这个地址。

这就是我们为什么要叫它Random Access Memory(RAM)————我们可以立即访问到任意一个地址的比特。

硬盘（hard drives）没有随机访问这个功能。因为没有和每个byte直接相连的东西。但是，有一个reader——叫做 **head** ——这个可以在disk的表面移动（就像
电唱机上面的那个针）。读取字节的时候花的时间会更长一些因为你得等到那个head移动到disc上面的那个位置。

即使内存控制器可以在任意远的内存地址之间跳跃，程序更倾向访问靠近的内存。 **所以如果读内存的地址彼此靠近的话，电脑运行的速度回更快一些** 。下面是它如何工作的：

处理器有一个**缓存(cache)**，这个缓存存储着最近从RAm读到的数据的拷贝。

![](https://www.interviewcake.com/images/svgs/cs_for_hackers__ram_cache.svg?bust=150)

实际上，它有很多的缓存。但是我们可以把他们想象成一个缓存。

从cache中读取数据要比从RAM中读取快得多，所以如果从cache中读取数据的话，处理器可以节省很多时间。

 **当处理器请求给定内存地址的内容的时候，内存控制器会把靠近这个内存地址的内存的内容都给它。** 然后处理器就把他们都存到cache中。

所以如果处理器第一次请求地址951的数据,然后请求952,953,954的数据...，这些数据都会从RAM中被一次性读取出来，下一步只要再从cache中读取数据就会快的多了。

但是如果处理器也需要读地址951的数据，地址362，然后地址419....这个时候cache就不会有帮助了，它会从RAM中一次一次的读取。

所以读取连续的内存地址比跳跃的内存地址会更快一些。
