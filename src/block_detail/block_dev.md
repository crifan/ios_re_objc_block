# Block正向开发

Block函数定义：

```c
double (^multiplyTwoValues)(double, double);
```

Block函数写法：

```c
^ (double firstValue, double secondValue) {
    return firstValue * secondValue;
}
```

显示指定返回值类型：

```c
^ double (double firstValue, double secondValue) {
    return firstValue * secondValue;
}
```

调用：

```c
double (^multiplyTwoValues)(double, double) =
                          ^(double firstValue, double secondValue) {
                              return firstValue * secondValue;
                          };

double result = multiplyTwoValues(2,4);

NSLog(@"The result is %f", result);
```

可以从作用域内，直接引用值：

```c
- (void)testMethod {
    int anInteger = 42;
 
    void (^testBlock)(void) = ^{
        NSLog(@"Integer is: %i", anInteger);
    };
 
    testBlock();
}
```

TODO：

* 继续整理
  *【整理】iOS的ObjC的基础知识：正向开发时Block相关知识
