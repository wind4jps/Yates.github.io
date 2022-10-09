# #ifdef、#ifndef与#endif用法学习

****

## 头文件中使用，防止头文件被多重调用

基本格式为：

```c++
#ifndef 标识符
#define 标识符

//头文件程序段

#endif
```

- **如果一个头文件被引用多次，编译器会处理两多次头文件的内容，这将产生错误。为了防止这种情况，标准的做法是把文件的整个内容放在条件编译语句中。示例如下：**

```c++
#ifndef _A
#define _A
#include "B.h"
class A
{
public:
	int a;
	B* objectb;
public:
	A();
	int geta();
	void handle();
	void hello();
};
#endif 
```

在这个示例中，即使其他多个文件含有头文件A.h，但是仅处理一次，第二次处理时_A宏已存在

*#ifndef后的标识符一般以当前头文件命名，并将.替换为_，最前面加上_，单词间用_隔开*

***

## 作为调试使用，省去注释代码的麻烦

- **有时候当代码比较多的时候，要做测试，但是全部注释很麻烦，这时候使用#ifdef非常好用。示例如下：**

```c++
#include <iostream>
#include "A.h"
#define INIT_B
using namespace std;
B::B()
{
	#ifdef _DEBUG
	this->b=200;
	#endif
}
```

此时语句`this->b = 200;`不执行

*一般地为了便于阅读，#ifdef后的标识符会写为_DEBUG*