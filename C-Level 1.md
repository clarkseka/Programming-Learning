# C语言入门
## 前言
这是好久之前听翁恺老师的慕课时做的笔记。很多内容现在都已浑忘了，最近想重新学起来。往后学深了再回头看这些笔记肯定会觉得很有趣吧😂。
## 心得
目前学习阶段，要养成多刷题的习惯！<br>
否则光知道一大堆理论和语句，面对实际需求却连printf也写不出来的。<br>
即使写得出程序，结果也是错漏百出的。<br>
## 備忘錄
- 20190823：儘快在每段代碼前補充其對應的需求。最近想重新看看之前的代碼例，發現某些稍複雜的代碼的某些步驟要結合需求才能弄懂。
- 20190823：目前學習到函數部分。 
- 20210217：把这篇心得markdown化后上传到GitHub。
## 本文
***
1. 程序框架
```
  #include <stdio.h>
    int main()
  {
    return 0;
  }
```
- `stdio.h`是C的一个头文件，其定义了三个变量类型、一些宏和各种函数来执行输入和输出。
  - [这是详细介绍](http://www.runoob.com/cprogramming/c-standard-library-stdio-h.html)。
- `include <>`在编程中用来声明使用了哪些头文件。
- `main(){;return 0;}`称为主函数。
  - `int main()`可写成`main()`。不调取返回参数时可写成`int main(void)`，不要写成`void main()`。
***
2. 输出"Hello World" 
```
#include <stdio.h>
int main()
{
  printf("Hello World\n");
  return 0;
}
```
- 不要忘了最后的分号。
- `printf()`是指输出。f是指格式化。
- `\n`和`\t`是最常用的两个转义字符：
  - `\n`用来换行，让文本从下一行的开头输出；
  - `\t`用来占位，一般相当于四个空格，或者tab键的功能。
- 双引号以内的称为字符串。
***
3. 四则运算
```
#include <stdio.h>
int main()
{
	printf("12+34=%d\n",12+34);
  return 0;
}
```
- 要计算的内容应该是在双引号以外的。不要写成`printf("12+34=%d,12+34")`，否则计算机会直接输出为12+34=0,12+34。
- `%d`是指十进制整数。
- 其他四则运算：+，-，*，/，%（取余数）。
***
4. 简单找零
```
#include <stdio.h>
int main()
{
	int price=0,pay=0;
	printf("请输入价格：");
	scanf("%d",&price);
	printf("请输入付款金额：");
	scanf("%d",&pay);
	int change=pay-price;
	printf("找您%d元\n",change);
	return 0;
}
```
- `int price=0,pay=0;`是指定义整型变量price和pay，并令其初始值为0。
  - int是一种整型的数据类型。 
  - price、pay是该变量的标识符。标识符只能由字母、数字以及下划线组成；不能是C语言的关键字；首位不可以为数字。
  - 命名方法：
	1. 匈牙利命名法：开头字母用变量类型的缩写，其余部分用变量的英文或英文的缩写，要求单词第一个字母大写。例如iPrice等等。
	2. 驼峰式命名法：第一个单词首字母小写，后面其他单词首字母大写。例如myAge，manHeight。
	3. 帕斯卡命名法：又叫大驼峰式命名法。每个单词的第一个字母都大写。例如MyAge，ManHeight。
  - 变量=0这个过程称为变量赋值，没有赋予初始值的变量的初始值可能为任何数字。
  - ANSI C要求程序编写者只能在代码开头的地方定义变量。但C99允许在变量被调用前的任何位置定义变量。
- `scanf("%d",&price);`是指输入一个十进制整数，并将其储存在变量price中。
  - `scanf()`是指输入格式化后的数据，&是一种指针。
- 关于常量（C99-）
  - 使用常量时尽量不要直接写入表达式，而是应该先定义(const int)后再使用，以便他人理解和自己检查和修改。
  - 常量的标识符应尽量使用大写字母以便区分。
  - 每个常量只能被赋值一次，多次赋值会出现"read-only variable is not assignable"的错误提示。
***
5. 单位换算（一）
```
#include <stdio.h>
int main()
{
	printf("请分别输入身高的英尺和英寸，"
	"如输入\"5 7\"表示5英尺7英寸：");
	double foot=0,inch=0;
	scanf("%lf %lf", &foot, &inch);
	printf("身高是%f米。\n",
	((foot + inch / 12) * 0.3048));
	return 0;
}
```
- 如果需要输入双引号可以在两个双引号前各加一个"\"号。
- `double foot=0,inch=0;`是指定义浮点数变量foot和inch并令其初始值为0。
  - double表示双精度浮点数，float表示单精度浮点数。
  - 浮点数是计算机内部表示非整数的一种形式。
      |   名称    |所占字节数|有效数位|   表示范围  |
      | :----:    |:----:   |:----: | :----:     |
      |单精度浮点数|4        | 8     |[±3.40E+38] |
      |双精度浮点数| 8       | 16    |[±1.79E+308]|
- 将数值导入float变量时使用`%f`，导入double变量时使用`%lf`。导出时都使用`%f`。
  - 需要保留n位小数的浮点变量表示为：`%.nf`。
***
6. 时间差计算
```
#include <stdio.h>
int main()
{
	int hour=0,hour_1=0,hour_2=0,minute=0,minute_1=0,minute_2=0;
	printf("请输入开始时间,\n"
	"例如10时35分请输入\"10 35\"：");
	scanf("%d %d",&hour_1,&minute_1);
	printf("请输入结束时间,\n"
	"例如10时35分请输入\"10 35\"：");
	scanf("%d %d",&hour_2,&minute_2);
	hour=hour_2-hour_1;
	minute=minute_2-minute_1;
	//处理可能出现的负数结果
	if (hour<0){
		hour+=24;
		}
	if (minute<0){
		minute+=60;
		--hour;
		}
	printf("相差%d小时%d分钟\n",hour,minute);
	return 0;
}
```
- 要在代码中间添加注释时需在注释前后添加/* */ ，系统会自动将其中内容替换为空格。C99允许编写者在单行使用//来表示注释。
- `if(hour<0){ }`的意思是，如果满足()内的条件，便执行{ }内的内容。
  - 注意格式是：
    ```
    if (条件){
    执行的命令;
    }
    else{
    执行的命令;
    }
    ```
  - 多条件嵌套时更需要使用大括号以区分条件判断的顺序。也可以使用更简洁的级联格式：
	  ```
    if (条件1){
    执行的命令;
    }
    else if (条件2){
    执行的命令;
    }
    else{
    执行的命令;
    }
    ```
- 尽量单一输出（在if语句后单条输出而不是在if语句中多条输出）。
- `hour<0`，`minute+=60`这些算式里面的"hour""minute""0""24""60"称为算子，"<""+=""--"这些称为运算符。
  | 優先級 |              意義              |       運算符      |
  |--------|:------------------------------:|:-----------------:|
  |    1   | 圆括号                         | ()                |
  |    2   | 非、正、负、递加、递减         | !、+、-、++、--   |
  |    3   | 乘、除、取余                   | *、/、%           |
  |    4   | 加、减                         | +、-              |
  |    5   | 大于等于、小于等于、大于、小于 | >=、<=、＞、＜    |
  |    6   | 相等、不相等                   | ==、!=            |
  |    7   | 且                             | &&                |
  |    8   | 或                             | \|\|              |
  |    9   | if、else                       | ?、:              |
  |   10   | 赋值、等加、等减、等乘、等除   | =、+=、-=、*=、/= |
  |   11   | 运算结果                       | ，                |
  |   12   | &                              |                   |
***
7. 判断数字有几位
```
#include <stdio.h>
int main()
{
	int x=0,n=0;
scanf("%d",&x);
while (x!=0){
    	x/=10;
    	n++;
}
printf("%d\n",n);
return 0;
}
```
- `while(  ){}`的意思是只要满足()内的条件，就一直执行{循环体}内的命令，直到不满足()内的条件为止。
- 如果代码表达如下：
  ```
	do{
	执行的命令;
	}while(x!=0);
  ```
  则表示先进行一次循环后再判断是否进入下一次循环。
***
8. 计数器
```
#include <stdio.h>
int main()
{
	for (i=0,i<n,i++){
	}
return 0;
}
```
- `for (初始动作,判断条件,后续动作){}`就是一个计数器。
  - 圆括号内首项为计数器初始动作，中间项为判断条件，最后一项为执行命令后计数器的后继动作。
  - 计数器开始先做初始动作，然后判断是否满足中间项条件：如满足便执行{循环体}内的命令，并执行计数器的后续动作。
***
9. 逻辑判断
```
#include <stdio.h>
#include <stdbool.h>
int main()
{
    bool a=6>5;
    bool b=2;
    bool c=true;
    bool d=6<5;
    bool e=0;
    printf ("%d %d %d %d %d\n",a,b,c,d,e);
return 0;
}
```
- 使用bool函数前须先声明我们使用`stdbool.h`这个头文件。
- bool用于是或否的判断。如所定义的布尔量为真则输出1，反之则输出0。
  - 该程序最后输出的值为：1,1,1,0,0。
***
10. 多路分支
```
#include <stdio.h>
int main()
{
	int a=1
	const int A=2
	switch (a){
		case 1:printf("case1\n");
		case 2:printf("case2\n");
			break;
		case :printf("case3\n");
			break;
		case 4:printf("case4\n");
			break;
		default:printf("default\n");
			break;
		}
	return 0;
}
```
- 上面的语句表示，如果变量a的值等于常量1,便执行case 常量1:后的命令；如果变量a的值等于常量2,便执行case 常量2:后的命令...如此类推。
  - 使用的变量必须为整数型的，否则会提示statement requires expression of interger type. 
  - 其中的case相当于一个标记，标明它所在的位置以便程序进行switch；case以后要跟一个常量，也可以跟一个整数运算的表达式，如1+1。
  - break相当于一个分支的一个出口。如果其中一个分支没有break;执行完那个分支的命令以后不会切出，而是会自动跳转到下一个分支中。
  - default分支表示都不匹配时执行的命令。如果没有该分支，遇到全不匹配的情况会直接跳出switch语句。
- const int和case在ANSIC中不可同时使用，但C99的标准中允许这种写法。
- 如这个代码的case以后都是以printf输出语句为主的话，为了使输出单一化，可以通过特定手段对字符或字符串进行处理（还没学）。
***
11. 对数求解
```
#include <stdio.h>
int main()
{
	int x=64,n=0;
	int t=x;
	while (x>1){
		x/=2;
		n++;
	}
	printf("log2 %d = %d\n",t,n);
	return 0;
}
```
- 编写程序前考虑一下：如何因应需求创建变量和表达式（例如右面n初始值应该是多少，while后面的条件和每回执行的命令应该是什么等等）。
- 进行计算前尽量先定义一个变量来保存原始数据，然后用另一个变量进行计算。
- 编写程序时根据实际情况关注一下循环的输出次数以及各个变量的值。
  - 可在程序中插入输出语句让程序进行输出。
  - 可以使用IDE内的变量值跟踪功能。
- 完成后检查一下需要输出（或不需要输出）的值有没有输出；检查循环次数较多的代码时可以先设置一个比较少的循环次数来模拟运行。
***
12. 猜数字游戏
```
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
int main(int argc, char **argv) {
	int computer=0,user=0,retry=0;
	srand(time(0));
	computer=rand()%100+1;
	scanf("%d",&user);
	retry++;
	while (user!=computer){
		if (user>computer){
			printf("大\n");
			}
       else {
			printf("小\n");
			}
       scanf("%d",&user);
       retry++;
	}
    printf("对了，猜%d次",retry);
	return 0;
}
```
- `srand(time(0))`可以使每次产生的随机数都与上次的不一样。
- `rand()`可使计算机产生一个随机的9位整数，将这个数%100以后就可以取得它的十位和个位(00-99)。在此基础上+1便能得到1-100之间的整数了。
- 使用`rand()`和`srand()`这两个命令之前需声明使用stdlib.h和time.h两个头文件。
***
13. 判断是否质数：多层循环控制。
```
#include <stdio.h>
int main()
{
	int user=0,i=2,status=1;
	scanf("%d",&user);
	if (user==0||user==1)
	{
    	status=2;
    	goto out;
	}
	else
	{
		for (i=2;i<user;i++){
       		if (user%i==0){
       			status=0;
       		break;
			}
		}
	}
	out:
	if (status==0){
		printf("否,i=%d",i);
	}
	else if(status==2){
		printf("否,i=%d",user);
	}
	else{
		printf("是");
	}
	return 0;
}
```
- 我们使用if语句来判断for给出的数字是否为user。
  - 当我们找到符合if要求的，for循环便没有继续进行下去的必要了。
  - 所以我们使status为0以后，需要添加break;命令，以避免for循环继续进行下去。
- break;只能用在循环语句或开关语句（switch）里。
- 需要注意的是，break只能令距离它最近的for停止执行。如果需要跳过本次循环剩下的语句直接进入下一轮，应该使用continue。
- `goto 标号;（……）标号:`可以使程序直接跳过（……）的部分。
***
14. 数组利用：平均数进阶1
```
#include <stdio.h>
int main()
{
	int input=0,count=0,length=0,i=0;
	scanf("%d",&length);
	int number[length];
	double average=0,sum=0;
	scanf("%d",&input);
	while(count!=length){
		sum+=input;
		number[count]=input;
		count++;
		if (count==length){
			break;
		}
		else{
		scanf("%d",&input);
		}
	}
	if (count>0){
		average=sum/count;
 		printf("%.2f\n",average);
 			for (i=0;i<count;i++){
				if (number[i]>average){
   					printf("%d\n",number[i]);
				}
			}
	}
	return 0;
}
```
- `int number[length]`代表我们定义的是一个名为number且长度为length值的整数型数组。当我们需要存储每一个输入的数的数值时，我们便需要利用数组。
	- 数组中的所有的元素都具有相同的数据类型，在内存中是连续依次排列的。
		- 容量只能是整数，且创建后不能改变其长度。
		- C99之前的协议要求数组容量必须是一个常数（编译时刻确定的字面量），从C99协议开始才允许使用变量来表示数组容量。
- `number[count]=input`是对数组中的元素进行赋值（令count位置上的数值为x）。
	- 此时[]中的内容称为下标或索引，由0开始计数。赋值号的左边称为左值，右边称为右值。
		- 因为数组由0开始计数，所以其有效的下标值应该在[0,数组容量-1]。
		- 越界的数组读写有可能会导致程序崩溃。编译时**可能会**出现segmentation fault之类的错误提示，但编译器和IDE不会检查下标值是否越界，所以程序员需自行检查。
		- 如下标为字符，编译器会将其转化为ASCLL代码。例如A的ASCLL代码为65。
- ```
  for (i=0;i<count;i++){
	  if (number[i]>average){
   	  printf("%d\n",number[i]);
			}
	}
  ```
  则是使用数组中的元素（遍历数组）。
***
15. 数组利用：计算每个数字出现的次数。
```
#include <stdio.h>
int main()
{
	int i=0,input=0;
	const int A=10;
	int number[A];
	for (i=0;i<A;i++){
		number[i]=0;
	}
	scanf("%d",&input);
	while(input!=-1){
		if(input>=0&&input<=9){
			number[input]++;
		}
		scanf("%d",&input);
	}
	for (i=0;i<A;i++){
		printf("%d:%d\n",i,number[i]);
	}
	return 0;
}
```
- 这是一个很经典的利用数组的例子，它具有这些环节：
  1. `const int A=10;`创建一个常量来描述数组的大小。
  2. `int number[A];`定义一个整型数组，数组容量为A。
  3. `for (i=0;i<A;i++){number[i]=0;}`初始化数组，使数组中的每一个数字都为0。
  4. `number[input]++;`让数组参与运算。
  5. `for (i=0;i<A;i++){printf("%d:%d\n",i,number[i]);}`输出数组中的内容。
***
16. 函数
```
#include <stdio.h>
void sum_1(begin,end)
{
	int i=0,sum=0; 
	for (i=begin;i<=end;i++){
		sum+=i;
	}
	printf("%d到%d的和是%d\n",begin,end,sum);
}
int main()
{
	sum_1(10,20);
	sum_1(20,30);
	sum_1(30,40);
	
	return 0;
}
```
- 上面的sum和main都称为函数。
  - 函数是一块代码，它接收0个、1个或多个参数后执行命令，然后返回0个或1个值。
  - 当某段代码将会被重复利用时，应该将其抽出并定义为函数后，在编程中直接调用它。
  - 这样做的好处在于使代码变得简洁且容易维护。
- `void sum(begin,end)`称为函数头，大括号里面的内容称为函数体。函数的大括号不可省略。
- 在上面的函数头中，void是这个函数的返回类型(无返回)；sum是这个函数的名称；`(begin,end)`是这个函数的参数表，参数之间以逗号分隔。
- 定义函数以后，我们以`函数名(参数值);`的方式来调用函数。注意参数的个数和类型要符合定义。
- 另外不要漏了小括号，哪怕没有参数都要有小括号（例如`int main()`）。
***
