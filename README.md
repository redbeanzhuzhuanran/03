知识点1：引用（从地址的角度去看）：在学习语法的过程中，要多输出多看看
（1）引用是 C++ 重要的语言特性，引用是某一变量的一个别名，对引用的操作与对变量直接操作完全一样。引用的格式：类型& 引用名 = 已定义过的变量名
例1：这段代码是为了从地址层面更好看清楚
#include <iostream>
using namespace std;

int main()
{
	int i=7;
	cout <<"i的地址:"<<&i<<" " <<"i的数值:"<<i<<'\n';
	int & a = i;
	cout << "a的地址:" << &a<<" "<< "a的数值:" <<a<< endl;
	return 0;
}

运行结果说明引用或别名并不会新增加地址，a是一个i的别名，但其共用一个地址

（2）常引用：
例2：
    const int& cr = i;
    cr = 7;	                   // error: cr refers to const
    i = 8;
    cout << cr << endl;    // write out the value of i (that’s 8)

常引用的别名不可以被更改，但是其i可以更改值
函数调用传常量引用的一个非常有用的特性是在函数内部不会意外的修改传进来的对象；传常量引用参数相比于传值更加高效，同时具有传值的安全性；传常量引用参数是一种有用的、常用的机制，特别是对于参数对象较大的情况。

（3）基于范围循环：（chapter 03 PPT 28没看懂）
string s = “Hello world!”; 

for ( char ch : s ){               // ch is a copy of some s[i]
cout << ch << endl;
}

for ( char& ch : s ){             // value of s[i] is modifided to ‘ ’
cout << ch << endl;
}

for ( const char& ch : s )  ch = ‘ ’;  // Error, const reference 

程序输出
Hello world!
++++++++++++


（3）传值与传地址：
C++如何输出字符串指针的地址呢？
由于C++标准库中I/O类对<<操作符重载，因此在遇到字符型指针时会将其当作字符串名来处理，输出指针所指的字符串。
既然这样，那么我们就别让它知道那是字符型指针，所以得用到强制类型转换，不过不是C的那套，我们得用static_cast来实现，把字符串指针转换成无类型指针

#include <iostream>
using namespace std;
 
int main()
{
    const char *pszStr= "this is a string";
   //输出字符串
    cout<< "字符串：" <<pszStr << endl;
                
    //输出地址值
    cout<< "字符串起始地址值：" <<static_cast<const void *>(pszStr)<< endl;
    return 0;
}
