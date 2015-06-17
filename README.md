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

