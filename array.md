# 数 组

## 定义

* 引入：如何记录很多数？
  * 数组的定义：

```c
int number[x];
```

<img src="C:\Users\33640\AppData\Roaming\Typora\typora-user-images\image-20201201152740783.png" alt="image-20201201152740783" style="zoom:50%;" />

注意[n]里的数字是数组元素的个数，而数组下标是从0开始到 n-1。

* C99开始已经可以用变量定义数组的大小了

* 数组的特点：

  1.是一种容器

  2.其中所有的院所都具有相同的数据类型。

  3.每个的单元的地址都是相邻的。

* 

<img src="C:\Users\33640\AppData\Roaming\Typora\typora-user-images\image-20201201153042019.png" alt="image-20201201153042019" style="zoom:33%;" />

## 数组的单元

* 使用数组时放在[]中的数字叫做下表或索引。
* 数组的每个单元就是数组类型的一个变量。

* C的编译器和运行环境都不会检查数组下标是否越界的，舆论时对数组单元做读还是写。
  * 但以但程序运行，越界的数组访问可能造成问题没导致程序崩溃。



## 数组的个数统计

<img src="C:\Users\33640\AppData\Roaming\Typora\typora-user-images\image-20201201153911641.png" alt="image-20201201153911641" style="zoom:50%;" />

```
#include<stdio.h>

int main(void)
{
	const int number = 10;
	int x;
	int count[10];
	int i;
	for (int i = 0;i<number;i++)//初始化数组**一定要初始化数组
	{
		count[i] = 0;
	}
	scanf_s("%d", &x);
	while (x != -1)
	{
		if (x>=0&&x<=9)
		{
			count[x]++;
			
		}
	scanf_s("%d", &x);
	}
	for (i = 0; i < number; i++)
	{
		printf("%d:%d\n", i, count[i]);

	}
	return  0;
}
```

注意数组的初始化

* 使用数组的步骤：

<img src="C:\Users\33640\AppData\Roaming\Typora\typora-user-images\image-20201201160455457.png" alt="image-20201201160455457" style="zoom:50%;" />

## 数组运算

<img src="C:\Users\33640\AppData\Roaming\Typora\typora-user-images\image-20201201160557501.png" alt="image-20201201160557501" style="zoom:50%;" />

* 若有：

  ```
  int a[13] = {2};
  ```

  则结果为：![image-20201201160856387](C:\Users\33640\AppData\Roaming\Typora\typora-user-images\image-20201201160856387.png)

  只给第一个元素赋值，其他变量都是为初始量。

### 集成初始化时的定位

<img src="C:\Users\33640\AppData\Roaming\Typora\typora-user-images\image-20201201161017639.png" alt="image-20201201161017639" style="zoom:50%;" />

* 1.用[n]在初始化数据中给出定位

  2.没有定位的数据接在前面的位置后面

  3.其他位置的值补零

  4.也可以不给出数组大小，让编译器算

  5.特vi额适合初始数组稀疏的数组

```
#include <stdio.h>
int main(void)
{
	int a[13] = { [1] = 2,4,[5] = 6 };
	int i;
	for ( i = 0; i < 13; i++)
	{
		printf("%d\t", a[i]);
	}
	printf("\n");
	return 0;
}
```

运行结果：![image-20201201161506044](C:\Users\33640\AppData\Roaming\Typora\typora-user-images\image-20201201161506044.png)

### 数组的大小

* sizeof给出整个数组所占据内容的大小，单位是**字节**。

  （一个数字的大小是4个字节）

* sizeof给出整个数组所占据的内容的大小，单位是字节

  ```
  sizeof(a)/sizeof(a[0]);
  ```

* sizeof（a[0]）给出数组中单个元素的大小，于是相除就得到了数组的单元个数。

* 这样的代码，以但修改数组的初始的数据，就不需要修改遍历的代码。



### 数组的赋值

<img src="C:\Users\33640\AppData\Roaming\Typora\typora-user-images\image-20201201162211612.png" alt="image-20201201162211612"  />

* 数组变量本身不能被赋值

* 要把一个数组的所有元素交给另一个数组，必须采用遍历。

  ![image-20201201162312068](C:\Users\33640\AppData\Roaming\Typora\typora-user-images\image-20201201162312068.png)

* 通常都是使用for循环，让循环变量i从0到<数组的长度，这样循环体内最大的i整啊hi是数组最大的有效下标。

* 常见错误：

  * 循环结束条件是<=数组长度，或：

    离开循环后，继续用i的值来做数组元素的下标

查找一个数字：

```
#include<stdio.h>
int search(int key, int a[], int length);	//函数原形
int main(void)
{
	int a[] = { 2,5,5,5,5,4,5,45,45,4,5 };
	int x;
	int loc;
	printf("请输入一个数字：");
	scanf_s("%d", &x);
	loc = search(x, a, sizeof(a) / sizeof(a[0]));
	if (loc != -1) {
		printf("%d在第%d个位置上\n", x, loc);

	}
	else {
		printf("%d都不存在\n", x);
	}
	return 0;

}
int search(int key, int a[], int length)
{
	int ret = -1;
	int i;
	for (i = 0; i < length; i++) {
		if (a[i] == key) {
			ret = i;
			break;
		}
	}
	return ret;
}
```

![image-20201201164756264](C:\Users\33640\AppData\Roaming\Typora\typora-user-images\image-20201201164756264.png)

* 数组作为函数的参数时：
* 不能在[]中给出数组的大小
* 不能再利用sizeof来计算数组的元个数（由于指针的限制）

## 如何判断素数

对于原来的不用数组的函数：(思路：从2到x-1测试是否可以整除)

```
int isPrime(int x)
{
	int ret = 1;
	int i;
	if(x==1) ret = 0;
	for(i=1;i<x;i++){
	if(x%i==0){
	ret = 0;
	break;
	}
	}
	return ret;
}
```

**优化：**去掉偶数后，从3到x-1,每次加2

```
int is Prime(int x)
{
	int ret = 1;
	int i;
	if(x==1||
	(x%2 == 0 && x!=2))
	ret = 0;
 for(i = 3;i<x;i+2){
  if(x%i ==0){
  ret 0;
 break;
}

 }
 return 0;
}
```

* 如果x是偶数，立刻
* 否则要循环(n-3)/2+1遍
* 当N很大时就是n/2遍

## 二维数组

### 二维数组的遍历

* a[i][j]是一个整数
* 表示第i行第列上的单元

### 二维数组的初始化

![image-20201201171241363](C:\Users\33640\AppData\Roaming\Typora\typora-user-images\image-20201201171241363.png)

* **列数时必须给出的，行数可以由编译器来数**
* 每一行{}，逗号分隔
* 最后的逗号可以存在，有古老的传统
* 如果圣洛，表示补零
* 也可以用定位

<img src="C:\Users\33640\AppData\Roaming\Typora\typora-user-images\image-20201201171837137.png" alt="image-20201201171837137" style="zoom:50%;" />

```
#include<stdio.h>
#define size 3 
int main(void)
{
	const int SIZE = 3;
	int board[size][size];	//定义一个二维数组
	int i, j;
	int numofX;
	int numofO;
	int result = -1;	//-1没人赢； 1：x赢 ；0：O赢

	//读入矩阵
	for (i = 0; i < SIZE; i++) {
		for (j = 0; j < SIZE; j++) {
			scanf("%d", &board[i][j]);
		}
	}
	//检查行
	for (i = 0; i < SIZE && result == -1; i++)
	{	
		numofO = numofX = 0;
		for (j = 0;j<size;j++)
		{
			if (board[i][j]==1)
			{
				numofX++;
			}
			else
			{
				numofO++;
			}
		}
		if (numofO ==size)
		{
			result = 0;
		}
		else if(numofX ==size)
		{
			result == 1;
		}
	
	}

	return 0;
}
//分别检查列，对角线。。。最终完善判定。


```

