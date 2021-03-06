# cpp
1. 编译过程

   1. 预处理器
   2. 编译器
   3. 汇编器
   4. 链接器

2. inline函数

   - 优点
     - 宏在编译器被预处理器移走，编译错误时难以调试
     - 减少函数调用的额外开销
   - 缺点
     - **增加目标码大小**。在一台内存有限的机器上，过度热衷inlining会导致程序体积太大（对可用空间而言）。即使拥有虚内存，inline造成的代码膨胀亦会导致额外的**换页行为**，**降低指令告诉缓存装置的击中率**，以及伴随这些而来的效率损失。注意：如果inline函数本体很小，编译器针对”函数本体“所产出的码可能比针对”函数调用“所产出的码更小。果真如此，将函数inlining确实可能导致较小的目标码和较高的指令高速缓存装置击中率。
   - 循环、递归、virtual函数尽量避免使用内联函数
     - virtual意味着等待，知道运行期才确定调用哪个函数
     - inline意味着执行前，先将调用动作替换为被调用函数的本体

3. 转型

   1. C风格转型动作

      - （T）expression
      - T(expression)

   2. C++四种新式转型

      - const_cast<T>(expression):

        通常是用来将对象的常量性转除。它也是唯一有此能力的c++style转型操作符。

      - dynamic_cast<T>(expression)：

        主要用来执行”安全向下转型“，也就是用来决定某对象是否归属继承体系中的某个类型。它是唯一无法由旧时语法执行的动作，也是唯一可能耗费重大运行成本的转型动作。

      - reinterpret_cast<T>(expression)

        执行低级转型，实际动作（及结果）可能取决于编译器，这也就表明它不可移植。例如将pointer to int 转型为int.

      - static_cast<T>(expression)

        用来强迫隐式转换，例如将non-const对象转换为const对象，或将int转化为double等。它也可以用来执行上述多种转换的反向转换，例如将void*指针转换为typed指针，将pointer-to-base转为pointer-to-derived。但它无法将const转为non-const——这个只有const-cast才办得到。

   3. 。

4. 虚函数https://jacktang816.github.io/post/virtualfunction/

   1. 多态：c++作为面向对象的语言，主要有三大特性：继承、封装、多态。关于多态，简而言之就是用父类型的指针指向其子类的实例，然后通过父类的指针调用实际子类的成员函数。这种技术可以让父类的指针有“多种形态”，这是一种泛型技术。所谓泛型技术，说白了就是试图使用不变的代码来实现可变的算法。比如：模板技术，RTTI技术，虚函数技术，要么是试图做到在编译时绑定，要么试图做到运行时绑定。因此C++的多态分为静态多态（编译时多态）和动态多态（运行时多态）两大类。静态多态通过重载、模板来实现；动态多态就是通过本文的主角虚函数来体现的。
   2. 虚函数的内存分布
      - 虚函数通过虚表实现，是一个类的虚函数的地址表
      - 

   

