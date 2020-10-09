# C++

## 命名空间

作用为解决命名冲突。使用方式可以分域解析操作符`::`以及`using`声明（using declaration）

命名空间内部可以声明或定义变量，函数，typedef等。起作用的范围是“空间范围”，是在编译过程中完成的，该空间范围具体是指C++中的代码块，也就是指一对花括号之间的空间，如果C++是以单一源文件作为一个隔绝的编译单元，因此如果`using namespace xx;`不落在任何`{}`中，则以当前源文件结束，出自[白话C++](https://www.zhihu.com/question/333847992)。

## main函数

### 1. argc和argv

https://blog.csdn.net/dcrmg/article/details/51987413