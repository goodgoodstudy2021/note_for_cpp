# Variables C++
    变量的大小取决于编程者的需要，类型自己翻手册，在程序中查类型的大小可以sizeof(byte)

# Functions in C++
    函数，一个输入一个输出，我们提供特定的参数，它返回给我们一个返回值
    函数的意义在于防止代码重复，但不要每行代码都写进一个函数，编译器每调用一个函数  
    都需要为了这个函数创建一整个stack frame(栈框架)，会加重编译负担  
# header file
    头文件中包含了函数的声明，当你需要用到这个函数的时候，调用函数的头文件，可以将  
    函数的声明粘过来，在运行的时候，找到该函数，链接过去。  

    #pragma once是一种被称为header guard(头文件保护符)，它的作用是防止我们把单个  
    头文件多次的include到一个cpp文件中。它的功能可以用一 个空的结构体来代替，结构  
    体必须有唯一的名字，如果你多次include会报错，表示有重复。  
     
     #ifdef,#define以及#endif  
     #ifdef会检查后边跟着的符号是否存在，如果没有，他会将下边的代码include到编译里  
     ，有的话就不会被include，会全部被禁用  
      
    include后边用“”或者<>取决于include的对象的位置为了区分c++标准库和c标准库，  
    c标准库中头文件有.h扩展名，c++没有

# How to debug c++ in vs
    断点和读取内存是调试的两个主要部分，需要设置断点来读取内存，逐过程看自己要监视的参数就行  


# conditions and branches
    if循环语句是在汇编语言中写出跳转语句，然后跳转到内存中去判断，所以使用太多会降低代码的效率， 
    如果要让代码运行效率提高就尽量减少使用
# for循环和while循环
    两个循环
# contral flow in c++
    continue,break,return,和循环一起用  
1.return 语句的作用  
 (1) return 从当前的方法中退出,返回到该调用的方法的语句处,继续执行。  
 (2) return 返回一个值给调用该方法的语句，返回值的数据类型必须与方法的声明中的返回值的类型一致。  
 (3) return后面也可以不带参数，不带参数就是返回空，其实主要目的就是用于想中断函数执行，返回调用函数处。   
2.break语句的作用  
（1）break在循环体内，强行结束循环的执行，也就是结束整个循环过程，不在判断执行循环的条件是否成立，直接转向循环语句下面的语句。   
（2）当break出现在循环体中的switch语句体内时，其作用只是跳出该switch语句体。  
  3.continue 语句的作用
      终止本次循环的执行，即跳过当前这次循环中continue语句后尚未执行的语句，接着进行下一次循环条件的判断。   
# pointer（指针） 
    指针只是一个整数，一个地址，一个内存所在的地址的"门牌号"  
1.内存地址不会为0，0意味着这个指针无效。
2.使用&（取地址符）可以获取变量的地址，变量的地址可以放进指针中  

    int var=8;  
    void * ptr=&var;   
    *ptr是var的值  
    ptr是var的内存地址
指针的类型是void，int还是double都不重要，它所表示的地址都是同一个
# references(引用)
    引用是指针的一个扩展，其他变量的引用
    引用必须引用一个已存在的变量，引用本身并不是一个新的变量并不真正占用内存
# class（类）
    C中没有类的概念，c++中有
    c++支持面向过程，基于对象，面向对象，泛型编程四种
    类的作用主要是面向对象编程中的，为一类对象创建一个专属于这个对象的类
    类的类型名必须唯一，使用花括号包起来，括号的外边还有一个引号
    类内的函数称作method（方法）
# c++中类classes和结构体structs的区别
    从作用上来说，基本没有什区别，只有一个很小的区别
    class中默认类型是私有的（private），而struct默认是共有的（public）
    从出现来说，struct是c的概念，所以保留了下来 
    （个人理解）struct用来保存一些数据之类的，class用于实现面向对象的东西
