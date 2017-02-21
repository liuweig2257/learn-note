了解（知道是什么） 熟悉（为什用） 掌握（怎么用） 精通
# jni简介 #
## Jni是什么 ##

jni是java和c之间的中间件
## 为什么用Jni ##

- 驱动开发（java不能开发驱动，java不能直接和系统交互，只能通过虚拟机进行交互）
- 运算效率高（界面的渲染，游戏，音视频）
- 代码复用（具有众多的函数库可以复用）
- 特殊业务场景，添加独立与系统之外的硬件

## 怎么用##

### 基本的编译命令 ###
 编译java cd E:\..      javac

    public static void main(String[] args){
		System.out.println("Hello world from java");
	}

c语言的头
    include<stdio.h>
	include<stdlib.h>

代码

    main{
		printf("Hello World From C");
		system("java Hello");
		system("pause");
	}
	
### c语言中的基本类型 ###
char int short float double long

c中表示java中的long用long long

0表示false，1表示true

类型的修饰符 signde unsigned void(不确定长度或者空)

float和double 默认保存6位

占位符必须和数据类型保持一致


    printf("char类型占%d个字节\n",sizeof(char));
	printf("int类型占%d个字节\n",sizeof(int));
	printf("long类型占%d个字节\n",sizeof(long));
	printf("float类型占%d个字节\n",sizeof(float));
	printf("double类型占%d个字节\n",sizeof(double));
	printf("short类型占%d个字节\n",sizeof(short));


    char类型占1个字节
	int类型占4个字节
	long类型占4个字节
	float类型占4个字节
	double类型占8个字节
	short类型占2个字节
### C语言的基本函数 ###
输入函数 scanf()

malloc()申请内存函数

realloc（）申请重新分配内存

typedef 别名

define 宏定义
### 指针 ###

指针变量 int* 指的是内存地址


# eclipse进行jni开发 #


