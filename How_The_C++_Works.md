# 1.HOW C++ works
    使用c++编程，只需要将c++在一个文本中写好，然后传入编译器产生某种可执行的二进制文件
    （binary）,这个binary可以说是某种库，或者是实际可执行的文件

![](photo/Hellow%20World.png)

    #include<iostream>
 这是preprocessor语句（预处理语句），任何一#开头的都是预处理语句，预处理文件发生在真正的编译之前，这里  
是找有一个叫iostream的文件，该文件中的所有内容会被复制黏贴到当前的文件中。
被include的文件被称为header file（头文件），使用iostream是因为我们需要一个函数：cout声明，可以使我们能够打印东西到console（控制台），

     int main()
每个c++程序都有类似main函数的东西，被称作入口点(entry point)，即进入我们程序的入口，也就是说我们要运行代码时，计算机会从这个函数的代码开始执行，程序入口不一定非得是main函数，也可自己定义，但不推荐瞎搞，没啥意思。  
main函数虽然在这里是int，但main函数不需要返回任何类型的值，如果你不返回，它自己返回0  

     std::cout<<"Hellow World!"<<std::endl;
     std::cin.get();
"<<"是重载运算符，也是一个函数，就像"std::cout.print("Hellow World!").print(std::endl)" 
"endl"即endLine,告诉控制台前进到另一行
cin.get()函数是等待我们输入回车，然后才会接着执行下一行代码

***
## 1.1从代码到exe
    编译器(compiler)与链接器(Linker)
c++程序在被写出来之后，先通过编译器(compiler)将每个cpp编译出来，windows平台下会被编译成object文件（obj格式），而链接器(LInker)则可以将这些obj链接，生成一个exe可执行文件。
//头文件(header file)在编译过程中不被编译，在被include到cpp文件里的时候，是被编译的时候
***
## 1.2declaration(声明)与definition(定义)
    声明表示这个函数存在
    定义来说这个函数是什么，即函数的主体
由于函数编译是一个一个cpp的编译的，所以，当一个cpp要使用其他cpp的函数的时候，如果不进行声明，编译器会报错，但声明之后，编译器就相信你了，所以编译器是小傻子
在linker将每个obj进行链接的时候，会根据main函数里的调用去找函数的定义，找不到就会报错

# 2.How the c++ compiler works
     c++编译器唯一要做的事情就是把文本变成中继格式obj
     项目里的每个cpp，都会被编译器编译成一个obj，这些cpp文件也叫translation unity
     (编译单元)
 在将文本变成obj格式的  
 第一步，是预处理(preprocess)我们的代码，所有的preprocessor语句还会在那个时候被评估。  
 第二步，被预处理后，我们会进入tokenizing(标记解释)和parsing(解析)阶段，基本就是将c++文本处理成编译器能懂和处理的语言，结果是创建某种叫做abstract syntax tree(抽象语法树)，以抽象语法树的形式表达代码  

    说到底，编译器的工作既是把代码转化成要么是constant data(常数资料)，要么是instruction(指令)
在创建抽象语法树之后，就可以开始产生代码了，这个代码是cpu会执行的机器码，同时我们也会得到一些存储信息，，比如某个地方存储着我们所有的constant variables(常量变量)  

文件不重要如.c和.h，如果你想，可以以任何格式作为c++文件，只要告诉编译器将这当做c++编译  

    include预处理语句，编译器处理的时候，会将被include的内容粘贴归来
    define预处理语句，会将后边第一个词换成后边第二个 
    if 预处理语句，依据特定条件包含或者剔除代码

![](/photo/define.png)
![](/photo/define1.png)  
# 3.How the c++ Linker works  
    链接器的主要作用是把编译过程中生成的所有对象文件链接起来，还会导入我们可能会用到的库
编译器编译之后的是一个个的obj文件，链接器可以将他们链接成一个程序，即使没有其他文件，只有一个obj，也需要链接器来链接主函数和其他东西  

    编译器的错误是以C开头的语法错误  
    链接器的错误是以LNK开头的  

例如，如果代码中没有main函数，那么就会报错，LNK一大堆，告诉你没有入口函数   
## 3.1常见的LNK错误

     unresolved external symbol(未解决的外部符号)  
当链接器找不到它需要的东西时，就会发生这种情况，例如，在一个cpp中调用另一个cpp的一个函数，但是另一个cpp并没有这个函数，就会报LNK错误，解决办法，可以确保调用函数的声明和定义没有任何问题，如果该函数只是为这个cpp声明的，可以在函数前边加上Static。    

     one or more multiply define symbels found(重复符号的错误信息)
当我们用同一个符号表示了不同的函数，那么链接器在工作的时候会分不清楚那个是要链接的