# How to write a c++ class
    先确定自己需要什么功能，再去类里实现这样的功能
# Static in c++
    static的使用有两种：  
*** 
    在类class或者结构体struct外使用static  
类外的static修饰的符号在LINK阶段是局部的，也就是只对定义它的编译单元（.obj）可见
无论实例化多少次，这个静态（static）变量之会有这一个实例  
当你在类或结构体外定义一个静态函数或静态变量，这意味着，你定义的函数和变量只对它声明所在的
cpp文件（编译单元）是"可见"的
如果变量和函数其他编译单元不需要用的话，最好设成static，可以避免麻烦（如果不是static的意味着是全局变量，全局变量在全局中通用，容易出现bug）
***
    在类class或者结构体struct内
在内的static表示这部分内存是这个类的所有实例共享的，就像是这个类的全局实例
静态方法没有类实例，静态方法不通过类的实例就可以调用（使用类名加范围解析运算符::就可以访问），静态方法不能访问非静态变量    

      local atatic(静态局部)，局部作用域中的static
与之前的static的用法的区别在于变量的生命周期和作用域
静态局部变量允许我们声明一个变量，它的生命期是整个程序的生存期，但是作用域被限制在这个作用域中
也就是说，局部静态和在class中的静态声生命周期是一样的，但是作用域不同  
# Enums（枚举） in C++
    枚举（Enums）就是一些数的集合，枚举的作用在于给一个值指定一个名称，在需要给一些整数表示特定的状态或数值的时候很有用
![](/photo/enums1.png) ![](../photo/enums2.png)  
上图就是将A，B，C放进枚举中，默认的值是0，1，2.
![](../photo/Enums3.png)  
枚举后边可以改变数据类型
# Constructors(构造函数) in c++
    构造函数的意义，在于初始化，简单来说，c++中，你必须手动的初始化所有的基本类型的内存为0，  
    构造函数就是干这个的，  不然他们就会被设置为之前留存在内存中的值  构造函数在每次实例化的时候运行 
![](../photo/构造函数1.png)  

    构造函数的定义与其他一样，不同的是构造函数没有返回类型，而且它的命名必须和类名一样     
![](../photo/Constructors1.png)
如果没有添加构造函数，就会出现一个这样的空函数体，神毛野没有做，在java中，基本数据如int和float类型会被默认初始化为0，但c++中，必须手动来做    
![](/photo/构造函数2.png)       
# destructor(析构函数)
    构造函数的邪恶双兄弟，构造函数在创建一个对象实例的时候运行，析构函数在销毁一个对象的时候运行  
    析构函数可以用在释放任何内容或者需要清理内存空间的时候，同样也适用于栈和堆分配内存，如果用new关键字创造一个对象（存在于堆上），然后调用detele，析构函数就会被调用如果只有基于栈的对象，当跳出作用域的时候这个对象会被删除，所以这个时候析构函数也会被调用    
![](../photo/destructor1.png)
# inheritance(继承) in c++
    继承提供了这样一种方式：把一系列类的通用的代码（功能）放进基类中，以减少重复  
![](../photo/继承1.png)
这表示class player是Entity的子类，player类不仅仅是player类型，也是Entity类型，就是说它同时是这两种类型，player有了Entity的一切  
# Virtual function (虚函数)
    在一个父类函数，被子类重写之后，在调用的时候，还是会调用父类的方法，所以如果想重写一个父类的函数，  
    就必须把基类的原函数设置为虚函数,c++11新标准允许给被重写的函数用"override"关键字标记  
    虚函数的成本有：  
    1、需要额外的内存来存储虚表，这样就可以分配到正确的函数，基类里还有一个指针成员指向虚表  
    2、每次调用虚函数的时候，我们必须遍历虚表去找到最终要运行的函数
# interfaces(接口) in c++ (Pure virtual function纯虚函数)  
    纯虚函数允许我们定义一个在基类中没有实现的函数，然后强制子类去实现这个函数  
    创建一个只包含未实现方法，然后交由子类去实际实现功能的类，被称为接口
    接口就是一个只包含未实现的方法并作为一个模板的类，所以实际上，接口不包含方法实现，我们无法初始化这个类  
![](../photo/interface1.png)
这仍然被定义为虚函数，但是=0实际上将它变成了一个纯虚函数，意味着如果想实例化这个类，那么函数必须在子类中实现。之后就不知道实例化基类了，只能实例化完成了这个接口的子类，即只能实例化一个实现了所有虚函数的类
![](../photo/interface2.png)  
在这里已经不能实例化基类了
![](../photo/interface3.png)
在一个子类中实现这个函数后，就可以实例化这个子类了
# visibility（可视化） in c++ 
    c++三个基础访问修饰符：public，protected，public 
    class默认为private，struct默认为public
    private:只有本类和友元（friend）函数可以读取和更改（友元的意思就是允许你访问这个类的私有成员）
    protected：可见性比private高，比public低。意思是这个类以及所有的派生类都可以访问
    public:任何人都可以访问

# Arrays（数组） in c++
    数组是一些元素的集合，按照特定顺序排列的东西
    在使用中，注意数组的边界
    如果要返回在函数内创建的数组，那就要用new关键字来创建，因为new分配的内存，会一直存在，直到手动删除它
![](../photo/Array1.png)
为了使数组不出现一些奇怪的问题（内存跳跃），最好先定义一个静态的常量，再用来声明数组的大小。
![](../photo/Array4.png)
![](../photo/Array2.png)
![](../photo/Array5.png)
c++新标准中，使用std::array定义数组的方法如上
# How Strings（字符串） work in C++
    c++中的字符串，都是使用Ascall码来对应的
    将字符和单词串联表示出来，就是字符串，即一种可以处理和表示文本的方式 
    字符串就是字符数组
    字符串从指针的内存地址开始，直到0结束，字符串在内存中以ascll对应的16进制形式存在
    string中的string其实是const char *类型，string头文件中的这个操作符的被重载，实现了c++中string的操作，字符串是从指针的内存地址开始，从0（控制终止符）结束
    允许我们把字符串传入输出流。
# string Literals(字符量) in C++
    字符串字面量总是存储在只读内存中
![](/photo/Litrals1.png)  
这就是一个字符串面量，他是长度为7的const char数组，是因为字符串的末尾会有一个额对的空终止符效果等同于  
![](../photo/Literals2.png)    

    即，你定义字符串之后，会在字符串的结尾放一个空字符，来表示结束，如果没有这些的话，  
    字符串的存储空间是根据定义来的，它在内存中的表示会将剩余的字符都表示出来，  
    会在你想要的字符串后边添加很多东西   
    另外，字符串在处理的时候是以空字符为结尾的，如果在字符串中间加\0，那就会在\0处作为字符串的结尾
![](../photo/Literals3.png)
还有以上这些不同的char类型，char16与wchar都是两个字符的，区别在于，wchar的字符数是由编译器来决定有1字节还是两字节的，char16则都是两字节。 
![](../photo/Literals4.png)
输出字符串的小用法
# Const(常量) in c++
    const意思是，承诺修饰的东西时不会改变的（因为是承诺，所以可以不用遵守）
    声明一个我不会去改动的变量的一种很简单的方式（即常量）
    const int *和int const*是一个意思，要让指针变成常量，使它不能被重新分配，要把const放在*后边在变量名之前。  
![](../photo/const2.png)  

这两个是一样的，重要的是*的位置，这个的意思是，指针指向的内容是常量，不允许改变了。
![](../photo/const4.png)  
这个意思是可以改变指针指向的内容，即将指针变成常量，但不能把指针自身重新赋值让它指向其他东西。   

    const放在方法的后边，意味着这个方法不会修改任何实际的类，即在这个方法里，不允许修改任何变量，是一个只读的方法  
![](../photo/const5.png)  
![](../photo/const6.png)
这个定义的意思是，这个一个不能修改指针，不能修改指针内容的只读的函数   

![](../photo/const7.png)  
被mutable修饰的常数，是可以任意修改的函数，方法后用了const的也可以修改  
# Mutable（可以改变的） keyword
    在使用了const修饰的方法中使用，可以修改其中的变量
    在lambda中使用