# C++算法竞赛入门经典

[TOC]

## 第1部分 语言篇

### 第1章 程序设计入门

#### 1.1 算术表达式

##### 程序1-1 计算并输出1+2的值

```c++
#include<iostream>
using namespace std;

int main()
{
	cout << 1+2 << endl;
	return 0;
}
```



##### 程序1-2 计算并输出8/5的值，保留小数点后1位

* 方法1

```C++
#include <iostream>
using namespace std;

int main()
{
	printf("%.1f\n", 8.0/5.0);
	return 0;
}
```



* 方法2

```C++
#include <iostream>
#include <iomanip>	//必要头文件
using namespace std;

int main()
{
	cout << fixed << setprecision(1) << 8.0/5.0 << endl;
	
	return 0;
}
```



> 输出：1.6



* 衍生

1.  把%.1f中的数字1改成2，结果如何？

```C++
#include <iostream>
using namespace std;

int main()
{
	printf("%.2f\n", 8.0/5.0);
	return 0;
}
```

> 输出：1.60



2. 如果把小数点和1都删除，%f的含义是什么？

> 输出：1.600000
>
> 含义：输入输出为浮点型



3. 字符串%.1f不变，把8.0/2.0改成原来的8/5，结果如何？

> 输出：0.0



4. 字符串%.1f改成原来的%d，8.0/5.0不变，结果如何？

> 输出：324058680



##### 程序1-3 复杂的表达式计算

```C++
#include <iostream>
#include <math.h>
using namespace std;

int main()
{
	printf("%.8f\n", 1+2*sqrt(3)/(5-0.1));
	
	return 0;
}
```



> 输出：1.70695951
>
> 解释：
>
> * 计算式$1+\dfrac{2*\sqrt{3}}{5-0.1}$
> * **5-0.1** : 整数 - 浮点数 = 浮点数
>   * 5先变成5.0，在进行加减



#### 小结

* 整数值用%d输出，实数（浮点数）用%f输出
* 整数 / 整数 = 整数； 浮点数 / 浮点数 = 浮点数



#### 1.2 变量及其输入

#####  例题1-1 圆柱体的表面积

```C++
#include <iostream>
#include <math.h> 
using namespace std;

int main()
{
	const double pi = acos(-1.0);	// 求-1.0的反余弦，即派
	float r, h, area;
	cin >> r >> h;
	area = 2 * pi * r * r + 2 * pi * r * h;
	cout << area << endl;
	
	return 0;
}
```

> 输出：274.899



#### 1.3 顺序结构程序设计

##### 例题1-2 三位数反转

输入一个三位数，分离出它的百位、十位和个位，反转后输出。

```C++
#include <iostream>
#include <math.h> 
using namespace std;

int main()
{
	int num;
	cin >> num;
	cout << num%100%10 << num/10%10 << num/100 << endl;
	
	return 0;
}
```

> 输入：127
>
> 输出：721



##### 例题1-3 交换变量

输入两个整数a和b，交换二者的值，然后输出。

**法1**

```C++
#include <iostream>
#include <math.h> 
using namespace std;

int main()
{
	int a, b, temp;
	cin >> a >> b;
	temp = a;
	a = b;
	b = temp;
	cout << a << " " << b;
	
	return 0;
}
```

**法2**

```C++
#include <iostream>
#include <math.h> 
using namespace std;

int main()
{
	int a, b, temp;
	cin >> a >> b;
	a = a + b;
	b = a - b;	//此时b=a+b-b=a 
	a = a - b;	//此时a=a+b-a=b 
	cout << a << " " << b;
	
	return 0;
}
```

> 输入： 824 16
>
> 输出： 16 824

##### 

##### 例题1-4 鸡兔同笼

已知鸡和兔的总数量为n，总腿数为m。输入n和m，依次输出鸡的数目和兔的数目。如果无解，则输出"No answer"。

```C++
#include <iostream>
#include <typeinfo.h>
using namespace std;

int main()
{
	int n, m, c , r;
	cin >> n >> m;
	
	// 草稿纸上推导
	r = (m- 2 * n) / 2;
	c = n - r;
	if (m%2 != 0 || r < 0 || c < 0 || typeid(r).name() != "int" || typeid(c).name() != "int")
		cout << "No answer" << endl;
		
	else
		cout << c << " " << r << endl;
	
	return 0; 
}
```

> 输入：14 32
>
> 输出： 12 2

> 输入： 14 36
>
> 输出： No answer



##### 例题1-5 三整数排序

输入3个整数，从小到大排序后输出。

**法1 if-else枚举**

```
#include <iostream>
#include <typeinfo.h>
using namespace std;

int main()
{
	int a, b, c, max, min, mid;
	cin >> a >> b >> c;
	if (a >= b && b >= c)	cout << c << " " << b << " " << a;
	else if (a >= b && c >= a)	cout << b << " " << a << " " << c;
	else if (b >= a && a >= c)	cout << c << " " << a << " " << b;
	else if (b >= a && c >= b)	cout << a << " " << b << " " << c;
	else if (c >= a && a >= b)	cout << b << " " << a << " " << c;
	else cout << a << " " << c << " " << b;
	
	return 0; 
}
```



**法2 交换法**

```C++
#include <iostream>
#include <typeinfo.h>
using namespace std;

int main()
{
	int a, b, c, temp;
	cin >> a >> b >> c;
	if (a > b) {
		temp = a;
		a = b;
		b = temp;
		// 此时 b >= a 
	} 
	if (a > c) {
		temp = a;
		a = c;
		c = temp;
		// 此时 a >= c  
	} 
	
	if (b > c) {
		temp = b;
		b = c;
		c = temp;
	}
	
	cout << a << " " << b << " " << c;
	
	return 0; 
}
```



#### 习题

##### 习题1-1 平均数

输入3个整数，输出它们的平均值，保留3位小数。

```C++
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
	int a, b, c;
	double res;
	cin >> a >> b >> c;
	res = static_cast<double>(a+b+c)/3.0;	//将int型转为double型 
	
	cout << fixed << setprecision(3) << res << endl;
	
	return 0;
}
```

###### 注意事项——float和double的区别

> 在C++中，`float`和`double`都是用来表示浮点数的数据类型，但它们在精度和存储方面有一些区别。
>
> 1. **精度：**
>    - `float`：通常是单精度浮点数，占用4个字节（32位），能够表示大约6到7位有效数字。这意味着它在小数部分的精度上可能会受到限制。
>    - `double`：通常是双精度浮点数，占用8个字节（64位），能够表示大约15到17位有效数字，因此具有更高的精度。
> 2. **存储范围：** 由于`double`使用更多的位来表示数字，它能够覆盖比`float`更大的数值范围。这对于处理非常大或非常小的数值时很有用。
> 3. **性能：** 在某些情况下，使用`float`可能会稍微快于使用`double`，因为`float`占用的内存更少，计算速度可能更快。然而，现代计算机通常能够高效地处理`double`运算，所以性能差异通常不是主要关注点。
> 4. **内存消耗：** `double`占用的内存空间比`float`多，这意味着在存储大量浮点数的情况下，会占用更多的内存。
>
> 一般来说，如果你需要更高的精度和更大的数值范围，或者在科学计算、工程领域等需要更精确计算的情况下，推荐使用`double`。如果内存消耗或性能是关键因素，可以考虑使用`float`，但要注意可能出现的精度问题。
>
> 例如，在你之前提到的求平均值的代码中，使用`double`可以确保更准确的计算结果。



##### 习题 1-2 温度

输入华氏温度f，输出对应的摄氏温度c，保留3位小数。提示：c=5(f-32)/9。

```C++
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
	double c, f;
	cin >> f;
	c = 5 * (f - 32) / 9;
	cout << fixed << setprecision(3) << c << endl;
	
	return 0;
} 
```



##### 习题1-3 连续和

输入正整数n，输出1+2+$...$+n的值。提示：目标是解决问题，而不是练习编程。

```C++
#include <iostream>
using namespace std;

int main()
{
	int n, sum;
	cin >> n;
	sum = (1 + n) * n / 2;
	cout << sum << endl;
	
	return 0;
}
```



##### 习题1-4 正弦和余弦

输入正整数n（n<360），输出n度的正弦、余弦函数值。提示：使用数学函数。

```C++
#include <iostream>
#include <cmath>
using namespace std;

int main()
{
	int n;
	cin >> n;
	
	//将角度转换为弧度
	double radian = n * M_PI / 180.0;
	
	double sinValue = sin(radian);
	double cosValue = cos(radian);
	cout << sinValue << " " << cosValue << endl;
	
	return 0;
}
```



##### 习题1-5 打折

一件衣服95元，若消费满300元，可打八五折。输入购买衣服件数，输出需要支付的金额（单位——元），保留两位小数。

```c++
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
	int n;
	double cost;
	cin >> n;
	// n > 3时，可打八五折
	
	if (n > 3)	cost = 0.85 * 95 * n;
	else cost = 95 * n;
	cout << fixed << setprecision(2) << cost << endl;
	return 0;
}
```



##### 习题1-6 三角形

输入三角形3条边的长度值（均为正整数），判断是否能为直角三角形的三条边长。如果可以，则输出yes，如果不能，则输出no。如果根本无法构成三角形，则输出not a triangle。

```C++
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
	double a, b, c;
	cin >> a >> b >> c;
	          
	if (a + b > c && a + c > b && b + c > a) {
		if (a * a + b * b == c * c || a * a + c * c == b * b || b * b + c * c == a * a)
			cout << "yes" << endl;
		else
			cout << "no" << endl;
	}
	else
		cout << "not a triangle" << endl;
		
	return 0;
}
```



##### 习题1-7 年份

输入年份，判断是否为闰年。如果是，则输出yes，否则输出no。

提示：公历纪年法中，能被4整除的大多是闰年，但能被100整除而不能被400整除的年份不是闰年，如1900年是平年，2000年是闰年。

```C++
#include <iostream>
using namespace std;

int main()
{
	int a;
	cin >> a;
	
	//能被4整除的大多是闰年，但能被100整除而不能被400整除的年份不是闰年
	if (a % 4 == 0){
		if (a % 100 == 0) {
			if (a % 400 == 0)
				cout << "yes" << endl;
			else
				cout << "no" << endl;
		}
		else
			cout << "yes" << endl;
	}
	else
		cout << "no" << endl;
		
	return 0;
}
```
