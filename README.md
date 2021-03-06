# Job-Interview
##1. 迅雷2014C++研发笔试卷C
* **有关 #include \<stdio.h\> 和 #include "stdio.h" 的区别；**

<>引用的是编译器的类库路径里面的头文件，""引用的是你程序目录的相对路径中的头文件。假如你编译器定义的自带头文件引用在C:\Keil\c51\INC\下面，则#include<stdio.h>引用的就是C:\Keil\c51\INC\stdio.h这个头文件，不管你的项目在什么目录里，C:\Keil\c51\INC\stdio.h这个路径就定下来了。一般是引用自带的一些头文件：stdio.h、conio.h、string.h、stdlib.h等等之类的。

假如你的项目目录是在D:\Projects\tmp\，则#include "my.h" 引用的就是D:\Projects\tmp\my.h这个头文件。一般是用来引用自己写的一些头文件，如果使用""，它是会先在你项目的当前目录查找是否有对应头文件。如果没有，它还是会在对应的引用目录里面查找对应的头文件。意思就是，使用#include "stdio.h"如果你项目目录里面，没有stdio.h这个头文件，它还是会定位到C:\Keil\c51\INC\stdio.h这个头文件的。

**总结：**面试的时候这样回答就可以了：

<>引用的是编译器的类库路径里面的头文件;

""引用的是你程序目录的相对路径中的头文件，在程序目录的相对路径中找不到该头文件时会继续在类库路径里搜寻该头文件。 


* **在C++中，sizeof运算符，.成员运算符，.\*成员指针运算符，::作用域解析运算符以及?:条件运算符不能被重载；**


* **不能作为重载函数的调用的依据是：函数类型。可以的是：参数个数、参数类型和函数名称（返回类型）；**

**引用传递和指针传递还可以用是否加const来重载。**对于函数值传递的情况，因为参数传递是通过复制实参创建一个临时变量传递进函数的，函数内只能改变临时变量，但无法改变实参。则这个时候无论加不加const对实参不会产生任何影响。但是在引用或指针传递函数调用中，因为传进去的是一个引用或指针，这样函数内部可以改变引用或指针所指向的变量，这时const 才是实实在在地保护了实参所指向的变量。因为在编译阶段编译器对调用函数的选择是根据实参进行的，所以，只有引用传递和指针传递可以用是否加const来重载搜索。

* **建立派生类对象时,3种构造函数分别是a(基类的构造函数)、b(成员对象的构造函数)、c(派生类的构造函数)这3种构造函数的调用顺序为: abc;**


* **如果友元函数重载一个运算符时，其参数表中没有任何参数则说明该运算符是：重载错误；**

* **拷贝构造函数的特点；**

拷贝函数和构造函数没有返回值； 拷贝构造函数的参数可以使一个或多个，但左起第一个必须是类的引用对象； 若类定义中没有声明拷贝构造函数，则编译器会自动生成一个缺省的拷贝构造函数，但是不会是该类的保护成员； 通过拷贝函数可以将另一个对象作为对象的初值。

* **在C++中，函数的重载取决于函数的参数列表。同名的函数，参数列表不一样则函数不一样。参数列表一样，返回类型不一样不代表函数被重载；**


* **有一幢100层高的大楼，给你两个完全相同的玻璃围棋子。假设从某一层开始，丢下玻璃棋子就会破碎。那么怎么利用手中的两颗棋子，用一种什么样的最优策略，知道这个临界的层高呢？ ;**

第一种策略：最简单的想法，利用手头的一颗围棋子从第一层开始逐层往下扔，遍历楼层。最好的情况是第一层就碎了，一次找出临界层高；最差的情况是到了第一百层才碎了，用了一百次才发现临界层高。 

第二种策略：由于手头不止一颗围棋子，而是两颗，所以可以利用一颗作为“探子”，用二分的思想进行探查。例如先在第五十层扔一次，如果没有碎，可以在七十五层再扔一次，如果这时候棋子碎了，则可以用手头的另一颗棋子从五十层开始逐层往下扔，最多二十五次会找出临界的层高；而如果第一次在五十层扔下碎了，则从第一层开始逐层往下扔，这时候最多扔五十次即可找出临界的层高，尽管这时候扔的情况看起来和第一种策略扔的次数一样，但意义不同，因为这次我们是明确知道了最多只会到达五十层而非一百层。

第三种策略：首先,为了保证成功，两颗棋子不能全碎。那么经过计算，第一次应该在16层尝试。如棋子碎则从1-15层继续尝试。这样最多尝试16次可以得到结果。如16层棋子未碎，则第二次应该在16+16-1=31层尝试。这样可以保证最多尝试次数仍然为16次。往下类似，这样得到最终结果是: 第一颗棋子应该依次在16,31,45,58,70,81,91这七层尝试。如在其中某层碎了则继续用第2颗在相邻两次尝试楼层中间继续尝试，这样最多只需要16次尝试可以确定此临界值。



* **用c++写一个函数，如Foo(const char \*str)，打印出str的全排列，如abc的全排列：abc, acb, bca, dac, cab,cba ；**

```C++
#include "iostream"
using namespace std;

void permutation(char * Str, char * pBegin){

	if (*pBegin == '\0')
		cout << Str << endl;
	else{

		for (char * i = pBegin; i != '\0'; i++){

			swap(*pBegin, *i);
			permutation(Str, pBegin + 1);
			swap(*pBegin, *i);

		}

	}

}

int main(){

	char * str = new char(10);
	str = "abc";
	permutation(str, str);

	return 0;
}
```


##2. 腾讯2014研发笔试卷
###2.1 **常用排序算法稳定性分析**

> **【1】 选择排序、快速排序、希尔排序、堆排序不是稳定的排序算法**

冒泡排序、插入排序、归并排序和基数排序都是稳定的排序算法。

> **【2】 研究排序算法的稳定性有何意义？**

首先，排序算法的稳定性大家应该都知道，通俗地讲就是能保证排序前两个相等的数据其在序列中的先后位置顺序与排序后它们两个先后位置顺序相同。

再简单具体一点，如果A i == A j，Ai 原来在 Aj 位置前，排序后 Ai  仍然是在 Aj 位置前。 

下面我们分析一下稳定性的好处：

**（1）如果排序算法是稳定的，那么从一个键上排序，然后再从另一个键上排序，第一个键排序的结果可以为第二个键排序所利用。**

基数排序就是这样，先按低位排序，逐次按高位排序，那么，低位相同的数据元素其先后位置顺序即使在高位也相同时是不会改变的。详细请参见随笔《基数排序》。

**（2）学习排序原理时，可能编的程序里面要排序的元素都是简单类型，实际上真正应用时，可能是对一个复杂类型（自定义类型）的数组排序，**而排序的键值仅仅只是这个元素中的一个属性，对于一个简单类型，数字值就是其全部意义，即使交换了也看不出什么不同。

但是，对于复杂类型，交换的话可能就会使原本不应该交换的元素交换了。比如：一个“学生”数组，欲按照年龄排序，“学生”这个对象不仅含有“年龄”，还有其它很多属性。

假使原数组是把学号作为主键由小到大进行的数据整理。而稳定的排序会保证比较时，如果两个学生年龄相同，一定不会交换。

那也就意味着尽管是对“年龄”进行了排序，但是学号顺序仍然是由小到大的要求。

**（3）如果排序算法稳定，对基于比较的排序算法而言，元素交换的次数可能相对会少一些（个人感觉，没有证实）。** 

> **【3】 各种排序算法稳定性分析**

现在分析一下常见的排序算法的稳定性，每个都给出简单的理由。 

**（1）冒泡排序**

冒泡排序就是把小的元素往前调（或者把大的元素往后调）。注意是相邻的两个元素进行比较，而且是否需要交换也发生在这两个元素之间。

所以，如果两个元素相等，我想你是不会再无聊地把它们俩再交换一下。

如果两个相等的元素没有相邻，那么即使通过前面的两两交换把两个元素相邻起来，最终也不会交换它俩的位置，所以相同元素经过排序后顺序并没有改变。

所以冒泡排序是一种稳定排序算法。 

**（2）选择排序**

选择排序即是给每个位置选择待排序元素中当前最小的元素。比如给第一个位置选择最小的，在剩余元素里面给第二个位置选择次小的，

依次类推，直到第n-1个元素，第n个元素不用选择了，因为只剩下它一个最大的元素了。

那么，在一趟选择时，如果当前锁定元素比后面一个元素大，而后面较小的那个元素又出现在一个与当前锁定元素相等的元素后面，那么交换后位置顺序显然改变了。

呵呵！比较拗口，举个例子：序列5 8 5 2 9， 我们知道第一趟选择第1个元素5会与2进行交换，那么原序列中两个5的相对先后顺序也就被破坏了。

所以选择排序不是一个稳定的排序算法。 

**（3）插入排序**

插入排序是在一个已经有序的小序列的基础上，一次插入一个元素。当然，刚开始这个有序的小序列只有1个元素，也就是第一个元素（默认它有序）。

比较是从有序序列的末尾开始，也就是把待插入的元素和已经有序的最大者开始比起，如果比它大则直接插入在其后面。

否则一直往前找直到找到它该插入的位置。如果遇见一个与插入元素相等的，那么把待插入的元素放在相等元素的后面。

所以，相等元素的前后顺序没有改变，从原无序序列出去的顺序仍是排好序后的顺序，所以插入排序是稳定的。 

**（4）快速排序**

快速排序有两个方向，左边的i下标一直往右走（当条件a[i] <= a[center_index]时），其中center_index是中枢元素的数组下标，一般取为数组第0个元素。

而右边的j下标一直往左走（当a[j] > a[center_index]时）。

如果i和j都走不动了，i <= j, 交换a[i]和a[j],重复上面的过程，直到i>j。交换a[j]和a[center_index]，完成一趟快速排序。

在中枢元素和a[j]交换的时候，很有可能把前面的元素的稳定性打乱，比如序列为 5 3 3 4 3 8 9 10 11 

现在中枢元素5和3(第5个元素，下标从1开始计)交换就会把元素3的稳定性打乱。

所以快速排序是一个不稳定的排序算法，不稳定发生在中枢元素和a[j]交换的时刻。 

**（5）归并排序**

归并排序是把序列递归地分成短序列，递归出口是短序列只有1个元素(认为直接有序)或者2个序列(1次比较和交换)，

然后把各个有序的段序列合并成一个有序的长序列，不断合并直到原序列全部排好序。

可以发现，在1个或2个元素时，1个元素不会交换，2个元素如果大小相等也没有人故意交换，这不会破坏稳定性。

那么，在短的有序序列合并的过程中，稳定是是否受到破坏？

没有，合并过程中我们可以保证如果两个当前元素相等时，我们把处在前面的序列的元素保存在结果序列的前面，这样就保证了稳定性。

所以，归并排序也是稳定的排序算法。 

**（6）基数排序**

基数排序是按照低位先排序，然后收集；再按照高位排序，然后再收集；依次类推，直到最高位。

有时候有些属性是有优先级顺序的，先按低优先级排序，再按高优先级排序，最后的次序结果就是高优先级高的在前，高优先级相同的情况下低优先级高的在前。

基数排序基于分别排序，分别收集，所以其是稳定的排序算法。

**（7）希尔排序**

希尔排序是按照不同步长对元素进行插入排序，当刚开始元素很无序的时候，步长最大，所以插入排序的元素个数很少，速度很快；

当元素基本有序时，步长很小，插入排序对于有序的序列效率很高。所以，希尔排序的时间复杂度会比O(N^2)好一些。

由于多次插入排序，我们知道一次插入排序是稳定的，不会改变相同元素的相对顺序，

但在不同的插入排序过程中，相同的元素可能在各自的插入排序中移动，最后其稳定性就会被打乱。

所以shell排序是不稳定的排序算法。 

**（8）堆排序**

我们知道堆的结构是节点i的孩子为2*i和2*i+1节点，大顶堆要求父节点大于等于其2个子节点，小顶堆要求父节点小于等于其2个子节点。

在一个长为n的序列，堆排序的过程是从第n/2开始和其子节点共3个值选择最大（大顶堆）或者最小（小顶堆），这3个元素之间的选择当然不会破坏稳定性。

但当为n/2-1, n/2-2, ...1这些个父节点选择元素时，就会破坏稳定性。

有可能第n/2个父节点交换把后面一个元素交换过去了，而第n/2-1个父节点把后面一个相同的元素没有交换，那么这2个相同的元素之间的稳定性就被破坏了。

所以，堆排序不是稳定的排序算法。


**综上，得出结论: 选择排序、快速排序、希尔排序、堆排序不是稳定的排序算法，而冒泡排序、插入排序、归并排序和基数排序是稳定的排序算法。**


###2.2 **多级存储体系**

在一个计算机系统中，对存储器的容量、速度和价格这三个基本性能指标都有一定的要求。存储容量应确保各种应用的需要；存储器速度应尽量与CPU的速度相匹配并支持I/O操作；存储器的价格应比较合理。然而，这三者经常是互相矛盾的。例如存储器的速度越快，则每位的价格就越高；存储器的容量越大，则存储器的速度就越慢。按照目前的技术水平，仅仅采用一种技术组成单一的存储器是不可能同时满足这些要求的。只有采用由多级存储器组成的存储体系，把几种存储技术结合起来，才能较好地解决存储器大容量、高速度和低成本这三者之间的矛盾。

高速缓冲存储器（Cache）设置在CPU和主存之间，可以放在CPU 内部或外部。**其作用也是解决主存与CPU的速度匹配问题。**Cache一般是由高速SRAM组成，其速度要比主存高1到2个数量级。由主存与Cache构成的“主存－Cache存储层次，从CPU来看，有接近于Cache的速度与主存的容量，并有接近于主存的每位价格。通常，Cache还分为一级Cache和二级Cache。

多级存储结构构成的存储体系是一个整体。从CPU看来，这个整体的速度接近于Cache和寄存器的操作速度、容量是辅存（或海量存储器）的容量，每位价格接近于辅存的位价格。从而较好地解决了存储器中速度、容量、价格三者之间的矛盾，满足了计算机系统的应用需要。

###2.3 TCP/IP协议栈（网络层次结构）

| 应用层（OSI 5 到 7层）     |  例如HTTP、FTP、DNS（如BGP和RIP这样的路由协议，尽管由于各种各样的原因它们分别运行在TCP和UDP上，仍然可以将它们看作网络层的一部分）  |
| :----:    | :----:  |
| 传输层（OSI 4层）     |  例如TCP、UDP、RTP、SCTP（如OSPF这样的路由协议，尽管运行在IP上也可以看作是网络层的一部分）     |
| 网络互连层（OSI 3层）       |  对于TCP/IP来说这是因特网协议（IP）（如ICMP和IGMP这样的必须协议尽管运行在IP上，也仍然可以看作是网络互连层的一部分；ARP不运行在IP上）    |
| 网络接口层（OSI 1和2层）         |  例如以太网、Wi-Fi、MPLS等。  |
  

TCP/IP协议，或称为TCP/IP协议栈，或互联网协议系列。

TCP/IP协议栈（按TCP/IP参考模型划分），TCP/IP分为4层，不同于OSI，他将OSI中的会话层、表示层规划到应用层。

* 应用层 FTP SMTP HTTP ...
* 传输层 TCP UDP
* IP网络层 IP ICMP IGMP
* 网络接口层 ARP RARP以太网令牌环FDDI ...


###2.4 编译系统VS解释系统 

下面是对编译型语言和解释型语言介绍：

**编译型语言：**

编译是指在应用源程序执行之前，就将程序源代码“翻译”成目标代码(机器语言)，因此其目标程序可以脱离其语言环境独立执行，使用比较方便、效率较高。但应用程序一旦需要修改，必须先修改源代码，再重新编译生成新的目标文件(＊ .OBJ)才能执行，只有目标文件而没有源代码，修改很不方便。现在大多数的编程语言都是编译型的。编译程序将源程序翻译成目标程序后保存在另一个文件中，该目标程序可脱离编译程序直接在计算机上多次运行。大多数软件产品都是以目标程序形式发行给用户的，不仅便于直接运行，同时又使他人难于盗用其中的技术C、C++、Fortran、Visual Foxpro、Pascal、Delphi、Ada都是编译实现的。

**解释型语言：**

解释型语言的实现中，翻译器并不产生目标机器代码，而是产生易于执行的中间代码，这种中间代码与机器代码是不同的，中间代码的解释是由软件支持的，不能直接使用硬件，软件解释器通常会导致执行效率较低。用解释型语言编写的程序是由另一个可以理解中间代码的解释程序执行的。与编译程序不同的是，解释程序的任务是逐一将源程序的语句解释成可执行的机器指令，不需要将源程序翻译成目标代码后再执行。解释程序的优点是当语句出现语法错误时，可以立即引起程序员注意，而程序员在程序开发期间就能进行校正。对于解释型Basic语言，需要一个专门的解释器解释执行 Basic程序，每条语言只有在执行才被翻译。这种解释型语言每执行一次就翻译一次，因而效率低下。一般地，动态语言都是解释型的，如Tcl、Perl、Ruby、VBScript、 JavaScript等。

**混合型：**

Java很特殊，Java程序也需要编译，但是没有直接编译称为机器语言，而是编译称为字节码，然后在Java虚拟机上用解释方式执行字节码。Python 的也采用了类似Java的编译模式，先将Python程序编译成Python字节码，然后由一个专门的Python字节码解释器负责解释执行字节码。(Java虚拟机对字节码的执行相当于模拟一个cpu，而ruby1.8--在虚拟机还未出现前--是通过解释成语法树执行。) 

个人认为，java是解释型的语言，因为虽然java也需要编译，编译成.class文件，但是并不是机器可以识别的语言，而是字节码，最终还是需要jvm的解释，才能在各个平台执行，这同时也是java跨平台的原因。所以可是说java即是编译型的，也是解释型，但是如果非要归类的话，从概念上的定义，恐怕java应该归到解释型的语言中。


###2.5 类成员访问权限

类定义的外部，可以被访问的成员有:

* public: 公有访问，类外部可访问； 

* private：私有访问，类本身成员函数可访问； 

* protected：保护访问，类本身以及派生子类可访问 

关于一个类的静态成员的描述中:

* 类的对象共享其静态成员变量的值 

* 静态成员变量可被该类的所有方法访问

* 该类的静态方法只能访问该类的静态成员变量 

* 该类的静态数据成员变量的值可修改（静态只有常量不可修改，指针指向的值可以修改）

##3. 腾讯研发工程师A笔试卷
###3.1 关于Cache 

系统开机或复位时，Cache 中无任何内容。当CPU送出一组地址去访问内存储器时，访问的存储器的内容才被同时“拷贝”到Cache中。此后，每当CPU访问存储器时，Cache 控制器要检查CPU送出的地址，判断CPU要访问的地址单元是否在Cache 中。若在，称为Cache 命中，CPU可用极快的速度对它进行读/写操作；若不在，则称为Cache未命中，这时就需要从内存中访问，并把与本次访问相邻近的存储区内容复制到Cache 中。未命中时对内存访问可能比访问无Cache 的内存要插入更多的等待周期，反而会降低系统的效率。而程序中的调用和跳转等指令，会造成非区域性操作，则会使命中率降低。因此，提高命中率是Cache 设计的主要目标。

###3.2 磁盘访问时间计算

数据存储在磁盘上的排列方式会影响I/O服务的性能，一个圆环的磁道上有 10 个物理块，10 个数据记录R1------R10 存放在这个磁道上，顺序存放。假设磁盘的旋转速度为20ms/周，磁盘当前处在R1 的开头处，若系统顺序扫描 后将数据放入单缓冲区内，处理数据的时间为4ms（然后再读取下个记录）， 则处理这10 个记录的最长时间为（204ms）

**原理：**磁盘会一直朝某个方向旋转，不会因为处理数据而停止。本题要求顺序处理R1到R10，起始位置在R1，一周是20ms，共10个记录，所以每个记录的读取时间为2ms。首先读R1并处理R1，读R1花2ms，读好后磁盘处于R1的末尾或R2的开头，此时处理R1，需要4ms，因为磁盘一直旋转，所以R1处理好了后磁盘已经转到R4的开始了，这时花的时间为2+4=6ms。这时候要处理R2，需要等待磁盘从R5一直转到R2的开始才行，磁盘转动不可反向，所以要经过8\*2ms才能转到R1的末尾，读取R2需要2ms，再处理R2需要4ms，处理结束后磁盘已经转到R5的开头了，这时花的时间为2\*8+2+4=22ms。等待磁盘再转到R3又要8\*2ms，加上R3自身2ms的读取时间和4ms的处理时间，花的时间也为22ms，此时磁盘已经转到R6的开头了，写到这里，大家已经可以看到规律了，读取并处理后序记录都为22ms，所以总时间为6+22\*9=204ms。 

**计算过程：**
```C++

S1：访问R1 ： 2ms ， 处理 R1 ：4ms ,  

S2：经过 8*2ms 之后，到达 R2 头，访问 R2 : 2ms ， 处理 R2 ：4ms 

S3：经过 8*2ms 之后，到达 R3 头， 访问 R3: 2ms ， 处理 R3 : 4ms 

...

S10：经过 8*2 ms 之后，到达 R10 头， 访问 R10 ： 2ms, 处理 R10 :4ms 

计算上述时间 : 

R1: 6ms , R2->R10 : (4ms +9*2ms) *9 =6+ 198 = 204ms 

```


###3.3 私有IP

随着IP 网络的发展，为了节省可分配的注册IP 地址，有一些地址被拿出来用于私有IP 地址。私有IP地址共有三个范围段： 

 A:10.0.0.0~10.255.255.255 /8 

 B:172.16.0.0~172.31.255.255 /12 

 C:192.168.0.0~192.168.255.255 /16 

###3.4 设计模式

* 桥接模式产生原因：同一个类型,有两个变化的维度（两个维度的抽象：一个抽象部分的抽象，一个实现部分的抽象）。Bridge模式是一种抽象与其实现相分离的模式。它主要应用于：当事物是一组变化量，和对这些事物的操作方法(实现)也是一组变化量的情况，也就是说它们都是多变的。

* 组合模式（Composite）属于结构性模式，它描述了对象间的组合关系。对象间常常通过树结构来组织（包含）起来，以实现整体-部分的层次结构。 

* Facade外观模式，是一种结构型模式，它主要解决的问题是：组件的客户和组件中各种复杂的子系统有了过多的耦合，随着外部客户程序和各子系统的演化，这种过多的耦合面临很多变化的挑战。 

* 单例模式是一种常用的软件设计模式。在它的核心结构中只包含一个被称为单例类的特殊类。 


###3.5 C++将父类的析构函数定义为虚函数

C++中假设有基类为fa，它的派生类为son，如果有*fa = new son();在delete fa或者释放*fa的时候将只会调用基类的析构函数；如果基类的析构函数为虚函数，在delete fa或者释放*fa的时候会先调用派生类（这里也就是son）的析构函数，再调用基类的析构函数。 

C++的多态肯定是使用父类的指针指向子类的对象，所以肯定是释放子类的对象，如果不使用虚函数的话， 父类的指针就只能够释放父类的对象。

###3.6 关系数据库的特点

数据库管理系统将具有一定结构的数据组成一个集合，它主要具有以下几个特点： 

**1. 数据的结构化**　数据库中的数据并不是杂乱无章、毫不相干的，它们具有一定的组织结构，属于同一集合的数据具有相似的特征。

**2. 数据的共享性**　在一个单位的各个部门之间，存在着大量的重复信息。使用数据库的目的就是要统一管理这些信息，减少冗余度，使各个部门共同享有相同的数据。

**3. 数据的独立性**　数据的独立性是指数据记录和数据管理软件之间的独立。数据及其结构应具有独立性，而不应该去改变应用程序。

**4. 数据的完整性**　数据的完整性是指保证数据库中数据的正确性。可能造成数据不正确的原因很多，数据库管理系统通过对数据性质进行检查而管理它们。

**5. 数据的灵活性**　数据库管理系统不是把数据简单堆积，它在记录数据信息的基础上具有很多的管理功能，如输入、输出、查询、编辑修改等。

**6. 数据的安全性**　根据用户的职责，不同级别的人对数据库具有不同的权限，数据库管理系统应该确保数据的安全性。


###3.7 原地逆序的话，数组比线性表慢。

```C++
void reverse2(LinkList &list) 
{ 
	LinkList p=list,q; 
	list=NULL;
	while(p) {
		 q=p->next;
		 p->next=list;
		 list=p; 
		 p=q;
	}
}
```

###3.8 关于sizeof()和strlen()的区别

`char str[] = "Hello"; //sizeof()为6；strlen()为5。`

`char* ss = "0123456789"; //sizeof(ss) 结果为4，因为ss是指向字符串常量的字符指针，sizeof()获得的是一个指针所占的空间。`

对字符串进行sizeof 操作的时候，会把字符串的结束符"\0"计算进去的，进行strlen 操作求字符串的长度的时候，不计算"\0"的。 数组作为函数参数传递的时候，已经退化为指针了，Func 函数的参数str_arg只是表示一个指针，那个100不起任何作用的。 

sizeof(str)是数组大小，数组创建时为hello长度加截止符。函数参数为数组的话，会转换为指针,sizeof()一个指针的话，获得的是一个指针所占的空间大小，为4。

```C++
void Func(char str_arg[2])
{
 	int m = sizeof(str_arg); //指针的大小为4
 	int n = strlen(str_arg); //对数组求长度，str_arg 后面的那个2没有任何意义，数组已经退化为指针了
 	printf("%d\n",m);
 	printf("%d\n",n);
}

int main(void)
{
 	char str[]="Hello";
 	Func(str);
}
```
str_arg数组已经退化为了指针，所以指向的是原来的hello。指针大小为4。strlen只是对传递给 Func 函数的那个字符串求长度，跟str_arg中的那个2 是没有任何关系的， 即使把2 改为200 也是不影响输出结果的，结果是5。



###3.9 typedef char *String\_t; 和#define String_d char * 的区别

typedef char \*String\_t 定义了一个新的类型别名，有类型检查。而#define String\_d char \* 只是做了个简单的替换，无类型检查，前者在编译的时候处理，后者在预编译的时候处理。

同时定义多个变量的时候有区别，主要区别在于这种使用方式String\_t a,b; String\_d c,d; a,b ,c 都是char*类型，而d 为char 类型。

由于typedef 还要做类型检查，而#define 没有，所以typedef 比#define 安全。


###3.10 已知rand7()可以产生1~7的7个数(均匀概率),利用rand7()产生rand10()1~10(均匀概率)。 

```C++

int rand10()
{
	int temp;
	int temp2;
	
	do {
		temp = rand7();
	} while (temp > 5);//temp 1到5

	do {
		temp2 = rand7();
	} while (temp2 > 2);//temp2 1到2

	return temp + (temp2 - 1) * 5;
} 
```

###3.11 对一个正整数作如下操作:如果是偶数则除以 2,如果是奇数则加 1,如此进行直到 1 时操作停止,求经过 9 次操作变为 1 的数有多少个? 
![答案](http://7xjspk.com1.z0.glb.clouddn.com/QQ图片20150617181516.png)


###3.12 求一个字符串的最长重复子串

举例： ask not what your country  can do for you ,but what you can do for your   country 

最长的重复子序列：can do for you 

思路：使用后缀数组解决 

分析： 

1、由于要求最长公共子序列，则需要 找到字符串的所有子序列 ，即通过产生字符串的后缀数组实现。 

2、由于要求最长的重复子序列，则需要对所有子序列进行排序，这样可以把 相同的字符串排在一起 。 

3、比较相邻字符串 ，找出两个子串中，相同的字符的个数。 

注意，对于一个子串，一个与其重复最多的字符串肯定是紧挨着自己的两个字符串。 

步骤： 

1、对待处理的字符串产生后缀数组   

2、对后缀数组排序   

3、依次检测相邻两个后缀的公共长度   

4、取出最大公共长度 的前缀   


举例： 输入字符串 banana 

1、字符串产生的后缀数组：
a[0]:banana

a[1]:anana

a[2]:nana

a[3]:ana

a[4]:na

a[5]:a 


2、对后缀数组进行快速排序，以将后缀相近的（变位词）子串集中在一起 

a[0]:a

a[1]:ana

a[2]:anana

a[3]:banana

a[4]:na

a[5]:nana 

之后可以依次检测相邻两个后缀的公共长度并取出最大公共的前缀


```C++
#include <iostream> 
#include <algorithm> 
#include <string> 

using namespace std;

const int MaxCharNum = 5000000;

bool StrCmp(char* str1, char* str2);
void GenSuffixArray(char* str, char* suffixStr[]);
int ComStrLen(char* str1, char* str2);
void GenMaxReStr(char* str);

int main()
{
	char str[MaxCharNum];
	cin.getline(str, MaxCharNum);//遇到回车结束 
	GenMaxReStr(str);
	system("pause");
	return 0;
}

void GenMaxReStr(char* str)
{
	int len = strlen(str);
	int comReStrLen = 0;
	int maxLoc = 0;
	int maxLen = 0;
	char* suffixStr[MaxCharNum];

	GenSuffixArray(str, suffixStr);//产生后缀数组 


	//对后缀数组进行排序 
	sort(suffixStr, suffixStr + len, StrCmp);

	//统计相邻单词中相同的字符数，并输出结果 
	for (int i = 0; i < len - 1; i++)
	{
		comReStrLen = ComStrLen(suffixStr[i], suffixStr[i + 1]);
		if (comReStrLen > maxLen)
		{
			maxLoc = i;
			maxLen = comReStrLen;
		}
	}
	//输出结果 
	for (int i = 0; i < maxLen; i++)
	{
		cout << suffixStr[maxLoc][i];
	}
	cout << endl;
}


/*为字符串产生其后缀数组，并存放到数组suffixStr中*/
void GenSuffixArray(char* str, char* suffixStr[])
{
	int len = strlen(str);
	for (int i = 0; i < len; i++)
	{
		suffixStr[i] = &str[i];
	}
}


/*返回str1和str2的共同前缀的长度*/
int ComStrLen(char* str1, char* str2)
{
	int comLen = 0;
	while (*str1 && *str2)
	{
		if (*str1 == *str2)
		{
			comLen++;
		}
		str1++;
		str2++;
	}
	return comLen;
}


//字符串升序排序 
bool StrCmp(char* str1, char* str2)
{
	if (strcmp(str1, str2) >= 0)
	{
		return false;
	}
	return true;
}

```