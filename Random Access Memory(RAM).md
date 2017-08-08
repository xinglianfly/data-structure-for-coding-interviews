# data-structure-for-coding-interviews

## Random Access Memory(RAM)

当电脑运行一段代码的时候，需要跟踪一些变量（numbers,strings,arrays,etc）。

这些变量是被存储在 **radom access memory（RAM）中**  。我们有时候会叫RAM“工作内存”或者仅仅叫“内存”。

> RAM不是MP3s或者app存储的地方。说到"内存",我们的电脑里有storage（有时候我们称它为"persistent storage"或者"disc"）.memory我们说的是保存变的函数可以分配内存，storage是我们保存文件的地方，像mp3，视频，word文档或者执行程序或者apps。emory(RAM)速度很快，但是空间很少，storage或者disk速度会更慢一些但是空间很多。现代笔记本可能会有500GB的storage，但是可能只有16GB的RAM。

你可以把RAM想象成书架，这个书架上面有很多格子，几亿个格子。


![](https://www.interviewcake.com/images/svgs/cs_for_hackers__ram_empty_no_indices.svg?bust=150)

格子上面会有数字标识。

![](https://www.interviewcake.com/images/svgs/cs_for_hackers__ram_empty_with_indices.svg?bust=150)

我们把这些数字叫做 **地址(address)** 。

每个格子装有8**比特(bits)**。每一个比特就是一个小的电子开关。“开”和“关”分别代表1和0。

![](https://www.interviewcake.com/images/svgs/cs_for_hackers__ram_bits.svg?bust=150)

8 bits 称为1 **字节(byte)** .每个格子都有一个8byte的存储空间。
当然，我们还有一个处理器。这个处理器做更具体的工作。

![](https://www.interviewcake.com/images/svgs/cs_for_hackers__ram_processor.svg?bust=150)

处理器和 **内存控制器（memory controller)** 相连。内存控制器从RAM中读取和写入数据。它和RAM的每个格子都有直接的联系。

![](https://www.interviewcake.com/images/svgs/cs_for_hackers__ram_memory_controller.svg?bust=150)

内存控制器和每个格子都有直接的联系这个很重要。这意味着我们可以访问0地址，然后可以立即访问91133这个地址。

这就是我们为什么要叫它Random Access Memory(RAM)————我们可以立即访问到任意一个地址的比特。

> 硬盘（hard drives）没有随机访问这个功能。因为没有和每个byte直接相连的东西。但是，有一个reader——叫做 **head** ——这个可以在disk的表面移动（就像
电唱机上面的那个针）。读取字节的时候花的时间会更长一些因为你得等到那个head移动到disc上面的那个位置。


即使内存控制器可以在任意远的内存地址之间跳跃，程序更倾向访问靠近的内存。 **所以如果读内存的地址彼此靠近的话，电脑运行的速度回更快一些** 。下面是它如何工作的：

处理器有一个**缓存(cache)**，这个缓存存储着最近从RAm读到的数据的拷贝。

![](https://www.interviewcake.com/images/svgs/cs_for_hackers__ram_cache.svg?bust=150)

> 实际上，它有很多的缓存。但是我们可以把他们想象成一个缓存。


从cache中读取数据要比从RAM中读取快得多，所以如果从cache中读取数据的话，处理器可以节省很多时间。

 **当处理器请求给定内存地址的内容的时候，内存控制器会把靠近这个内存地址的内存的内容都给它。** 然后处理器就把他们都存到cache中。

所以如果处理器第一次请求地址951的数据,然后请求952,953,954的数据...，这些数据都会从RAM中被一次性读取出来，下一步只要再从cache中读取数据就会快的多了。

但是如果处理器也需要读地址951的数据，地址362，然后地址419....这个时候cache就不会有帮助了，它会从RAM中一次一次的读取。

所以读取连续的内存地址比跳跃的内存地址会更快一些。


## Binary numbers
.....

到目前为止，我们已经讲过 **无符号数（unsigned integers）** 了。(“无符号”指的是非负，"integer"指的是整数，不是分数或小数)。存储其他的数字并不困难。下面是一些数字是怎么存储的。

 **分数(Fractions):**  存储两个数字：分子和分母。

 **小数（Decimals):** 依然是存储两个数字： 1) the number with the decimal point taken out, and 2) the position where the decimal point goes (how many digits over from the leftmost digit).带有小数点的数字和小数点所在的位置（小数点左边有几位数）。
 
 **负数（Negative Numbers）:** 保留最左边的那一位来表示符号，0代表正1代表负。

在现实生活中，我们可能会做的有点不一样。但是这些方法是可行的，它们可以使用0和1来表示很复杂的数字。

> 我们已经讲了10进制和2进制...你可能也已经见过16进制，也叫hexadecimal 或者hex. 在16进制中，使用的数字有 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, a, b, c, d, e, and f.16进制数一般都用"0x"或者"#"作为前缀。
在CSS中，颜色值有时候也使用16进制数来表示。Interview Cake’s签名的蓝色的颜色值是"#5bc0de"。


## Fixed-width integers

我们使用1字节（8个比特）可以表示多少不同的数字呢？

2的8次方是256个不同的数字。为什么是2的8次方呢？

> 我们使用8比特无符号数(11111111)来表示255，如果我们加1会发生什么？256需要9比特(100000000)，但是我们只有8比特。

这叫做 **integer overflow.** 好的情况下，我们可能只是得到错误。坏的情况下，我们的电脑可能计算出了正确的数字，但是只使用了8比特0来表示（00000000）而不是(100000000)来表示256。（python 已经知道这个结果不固定所以自动分配更多的内存来存储大的数字）

1byte可以表示256个不同的数字，这太有局限性了。 **所以我们通常使用4byte或8byte（32或64bits）来存储整数。** 

* 32-bit整数有2的32次方种可能--超过40亿
* 64-bit整数有2的64次方种可能--超过100亿

> **“为什么我从来没有想过我的整数有多少比特呢？”** 或许你想过只是你不知道而已。

你是否意识到在某些语言中（像java或者c）有时候数字是Interger类型有时候他们是Long类型？它们之间的区别就是他们的比特数不同（在java中，Integer是32位而Long是64位）

> **什么时候32比特还不够？当你计算一个视频的观看次数时** 。当Gangnam Style这个视频在YouTube上面的点击量超过2的32次方的时候，YouTube出现了问题，[ forcing them to upgrade their view counts from 32-bit to 64-bit integers.](https://arstechnica.com/information-technology/2014/12/gangnam-style-overflows-int_max-forces-youtube-to-go-64-bit/)

大部分的integers都是 **固定宽度（fixed-width）** 或者 **固定长度(fixed-length)** 的，这意味着他们占用的比特数目不会变。

通常来说假定一个整数是固定长度的是很安全的，除非你被明确告知。可变大小的数字是存在的，但是他们只在特殊情况下使用。

如果我们有64比特的固定长度的整数，这个整数是0还是193457都是无所谓的，它仍旧占用RAM中相同的空间:64比特。

在bit [O notation](https://www.interviewcake.com/article/python/big-o-notation-time-and-space-complexity?)中，**固定长度的正主占用常数级空间或者说O(1)空间。** 

因为他们都有一个固定的比特数， **大部分固定宽度的整数的简单操作（加、减、乘、除）所用的时间也是常数的(O（1）time)** .

因此，固定宽度的整数是空间高效和时间高效的。

但是，这种高效是有代价的---他们所表示的数字是有限的。也就是说他们只能有2的n次方种可能性，n是比特数。

所以有一个权衡。正如我们看到的，这是数据结构的一种趋势，为了得到一些好的特性，我们往往会失去一些东西。

