## 内存 （Memory）
### 硬件层面（Hardware）
### 软件层面（Software）
在软件层面，内存通常指的是操作系统从主储存器（内存条）。

这时，内存又分为两类：`栈内存（Stack Memory）`和`堆内存（Heap Memory）`。
#### 栈内存（Stack Memory）
##### 栈（Stack）
栈是一种常见的数据结构，只允许在结构的一端操作数据，并且所有数据都遵循后进先出`（Last-In First-Out，LIFO）原则`。

可将 栈 类比为羽毛球桶。

栈内存是一个有着 简单直接的结构 的连续内存空间，因此栈内存的访问和操作速度都非常快。

栈内存的容量较小，主要用于存放函数调用信息和变量等数据，大量的内存分配操作会导致`栈溢出（Stack overflow）`。

栈内存的数据储存基本都是临时性的，数据会在使用完之后立即被回收（如函数内创建的局部变量在函数返回后就会被回收）。

即，栈内存适合存放生命周期短、占用空间小且固定的数据。

![stack.webp](/md_data/\stack1.webp)
>栈内存的大小
>栈内存由操作系统直接管理，所以栈内存的大小也由操作系统决定。
>通常来说，每一条线程（Thread）都会有独立的栈内存空间，Windows 给每条线程分配的栈内存默认大小为 1MB。
#### 堆内存（Stack Memory）
堆内存虽然名字里有个“堆”字，但是它和数据结构中的堆没关系。

堆内存是一大片内存空间，堆内存的分配是动态且不连续的，程序可以按需申请堆内存空间，但是访问速度要比栈内存慢。

堆内存里的数据可以长时间存在，无用的数据需要程序主动去回收，如果大量无用数据占用内存就会造成`内存泄露（Memory leak）`。

即，堆内存适合存放生命周期长，占用空间较大或占用空间不固定的数据。
>堆内存的上限
>在 Node.js 中，堆内存默认上限在 64 位系统中约为 1.4 GB，在 32 位系统中约为 0.7 GB。
>而在 Chrome 浏览器中，每个标签页的内存上限约为 4 GB（64 位系统）和 1 GB（32 位系统）。
#### 函数调用（Function Calling）
了解栈内存与堆内存是什么后，现在来看看当一个函数被调用时，栈内存和堆内存会发生什么变化。

当函数被调用时，会将函数推入栈内存中，生成一个栈帧（Stack frame），
>栈帧可以理解为由函数的返回地址、参数和局部变量组成的一个块

当函数调用另一个函数时，又会将另一个函数也推入栈内存中，周而复始；

直到最后一个函数返回，便从栈顶开始将栈内存中的元素逐个弹出，

直到栈内存中不再有元素时则此次调用结束。

![stack.webp](/md_data/\stack2.webp)

在同一线程下（JavaScript 是单线程的），所有被执行的函数以及函数的参数和局部变量都会被推入到同一个栈内存中

##### 函数调用过程中的储存变量（Store variables）
当 JavaScript 程序运行时，在非全局作用域中产生的局部变量均储存在栈内存中。

但是，只有原始类型的变量是真正地把值储存在栈内存中。

而引用类型的变量只在栈内存中储存一个`引用（reference）`，这个引用指向堆内存里的真正的值。

![stack.webp](/md_data/\stack3.webp)

>原始类型（Primitive type）
>又称基本类型，包括 string、number、bigint、boolean、undefined、null 和 symbol（ES6 新增）。
>原始类型的值被称为原始值（Primitive value）。
>补充：虽然 typeof null 返回的是 'object'，但是 null 真的不是对象
##### 栈内存中的原始值不可更改
+ 当我们定义一个原始类型变量的时候，JavaScript **在栈内存中激活一块内存来储存变量的值（原始值）**。
·
+ 当我们更改原始类型变量的值时，实际上**会再激活一块新的内存来储存新的值，并将变量指向新的内存空间**，而不是改变原来那块内存里的值。
·
+ 当我们将一个原始类型变量赋值给另一个新的变量（也就是复制变量）时，也是**会再激活一块新的内存，并将源变量内存里的值复制一份到新的内存里**。
·
![](/md_data/stack4.webp)
##### 栈内存中的对象引用（Object references）可更改
引用类型的变量在栈内存中储存的只是一个指向堆内存的引用。
+ 当我们定义一个引用类型的变量时，
JavaScript 会先在堆内存中找到一块合适的地方来储存对象，
并激活一块栈内存来储存对象的引用（堆内存地址），
最后将变量指向这块栈内存。
·
+ 所以当我们通过变量访问对象时，实际的访问过程应该是：
变量 -> 栈内存中的引用 -> 堆内存中的值
·
+  当我们把引用类型变量赋值给另一个变量时，
会将源变量指向的栈内存中的对象引用复制到新变量的栈内存中，
所以实际上只是复制了个对象引用，并没有在堆内存中生成一份新的对象。
·
+  而当我们给引用类型变量分配为一个新的对象时，
则会直接修改变量指向的栈内存中的引用，
新的引用指向堆内存中新的对象。
·
![](/md_data/stack5.webp)




>引用类型（Reference type）
>除了原始类型外，其余类型都属于引用类型，包括 Object、Array、Function、Date、RegExp、String、Number、Boolean 等等...
>引用类型的值被称为引用值（Reference value）。
>实际上 Object 是最基本的引用类型，其他引用类型均继承自 Object。也就是说，所有引用类型的值实际上都是对象。
##### 特别注意（Attention）
全局变量以及被闭包引用的变量（即使是原始类型）均储存在堆内存中。
##### 全局变量（Global variables）
在全局作用域下创建的所有变量都会成为全局对象（如 window 对象）的属性，
也就是全局变量。

而全局对象储存在堆内存中，所以全局变量必然也会储存在堆内存中。
##### 闭包（Closures）
在函数（局部作用域）内创建的变量均为局部变量，

当一个局部变量被当前函数之外的其他函数所引用（也就是发生了逃逸），

此时这个局部变量就不能随着当前函数的返回而被回收，

那么这个变量就必须储存在堆内存中，而这里的“其他函数”就是我们说的闭包。
>闭包是一个非常重要且常用的概念，许多编程语言里都有闭包这个概念。
![](/md_data/Image2022_06_27_15_27.png)

就如下面这个例子：
```
function getCounter() {
  let count = 0;
  function counter() {
    return ++count;
  }
  return counter;
}
// closure 是一个闭包函数
// 变量 count 发生了逃逸
let closure = getCounter();
closure(); // 1
closure(); // 2
closure(); // 3
```

#### 浅拷贝与深拷贝
在浅拷贝中，简单的赋值只会复制对象的引用，

实际上新变量和源变量引用的都是同一个对象，修改时也是修改的同一个对象，

想要真正的复制一个对象，就必须新建一个对象，将源对象的属性复制过去；

如果遇到引用类型的属性，那就再新建一个对象，继续复制；

此时我们就需要借助递归来实现多层次对象的复制，这也就是我们说的深拷贝。

### 待补充
#### 内存生命周期（Memory life cycle）
#### 垃圾回收（Garbage collection）
##### 可达性（Reachability）
##### 内存泄漏（Memory leak）
##### 垃圾回收算法（Algorithms）
#### 内存管理（Memory management）-内存优化（Memory optimization）
#### 如何分析内存（Analyze）


[思否-JavaScript 内存详解 & 分析指南-陈皮皮]
 :https://segmentfault.com/a/1190000038967810














