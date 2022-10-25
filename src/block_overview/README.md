# Block概览

* `Block`
  * 名称
    * 官方标准叫法其实是：`Blocks`
    * 大家常简称为：`Block`=`代码块`
  * 是什么：
    * Objc的对象
      * `iOS`的`ObjC`中的一个将`数据`与相关`行为`相结合的**对象**
    * (ObjC对）`C`语言扩展
      * `Blocks`是添加到`C`、`Objective-C`和`C++`的语言级功能，它允许您创建不同的代码段，这些代码段可以像值一样传递给方法或函数。
      * 它们还具有从封闭范围捕获值的能力
        * 类似：其他语言中的`闭包`=`closure`、`lambda`
  * 功能和用途：用于创建匿名函数，实现函数的异步（或同步）调用
  * 相关底层机制
    * Block可以从局部变量中获取值； 发生这种情况时，必须动态分配内存。
      * 初始分配是在堆栈`Stack`上完成的，但是运行时提供了一个`Block_copy`函数，给定一个块指针，该函数要么将底层块对象复制到堆`Heap`，将其引用计数设置为 1 并返回新的块指针，要么（如果`Block`对象已经在堆`Heap`上）将其引用计数增加 1
      * 配对函数是`Block_release`，它将引用计数减少 1，如果计数达到零并且在堆`Heap`上，则销毁该对象
  * 官网
    * [Working with Blocks](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/WorkingwithBlocks/WorkingwithBlocks.html)
    * [Objective-C Automatic Reference Counting (ARC) — Clang 16.0.0git documentation](https://clang.llvm.org/docs/AutomaticReferenceCounting.html#background)

## 为何要研究ObjC中的Block？

iOS逆向期间，最初是要找到某函数被调用的地方，通过函数调用堆栈，找到最后，发现找不下去了

之后发现其实是`Block`的机制实现的：`Block` = 实现了`函数（同步或）异步的回调`

TODO：

* 找到Block的函数如何被调用的  = Block函数的上层调用函数
  * 【整理】iOS逆向调试心得：如何找到Block的_pthread_wqthread和_dispatch_call_block_and_release的函数调用最初来源
