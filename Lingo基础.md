# 第一章 Lingo基础

### 一、Lingo基本界面

**Step1：**打开Lingo。

**Step2：**弹出一个对话窗，点击`Cancel`左边的`Never Register`即可，其余内容用不到。

**Step3：**界面自动弹出名为“Lingo Model-Lingo 1”的窗口，用于书写代码

**Step4：**（Ctrl+鼠标滚轮【放大缩小】）
以解方程的题目：x+1=2为例，写完代码后，点击![img](00D9B101.png)，运行程序。

**Step5：**首先Lingo会弹出一个名为“Solver Status”的对话框，它显示运行时间。

![image-20210326181732242](image-20210326181732242.png)

**Step6:**读取到运行的时间是0时0分0秒

![image-20210326181822757](image-20210326181822757.png)

**Step7:**然后弹出一个名为“Solution Report”的界面。
![image-20210326182042748](image-20210326182042748.png)

**Step8：**由此可知变量x的数值为1。
![image-20210326182334591](image-20210326182334591.png)

**Step9：**如果是求解线性规划的话，目标值也会在“Solution Report”中给出，到时在说。

### 二、用Lingo解方程

:one:每个方程必须以“ ; ”结束

:two:请注意：Lingo的所有符号都是英文格式下的符号。

:three:Lingo的加减乘除分别是：+、-、*、/。

<font color='red'>【ps】</font>
:a:`2*x+1`不能写为`2x+1`,乘号不能省略

:b:注意“ / ”的形状

【例题】求解方程组
$$
\begin{cases}2x+2y+1=5 \\ 3x-5y+5=3 \end{cases}
$$
<font color='red'>【解】</font>

2* x+2* y+1=5;
3* x-5* y+5=3;

![image-20210326184322655](image-20210326184322655.png)

### 三、lingo变量

:one:Lingo默认所有变量为大于等于0的数字，因而非负的条件不必多写。
:two:万一遇到一个变量可以小于0,后面会讲到一个函数叫做`@free`, 来使其定义域为R。
:three:Lingo默认所有变量为大于等于0的数字，因而非负的条件不必多写。Lingo内部无法识别字母大小写。
:four:无论是C、Matlab 还是Lingo,变量均由字母数字下划线组成，且数字不能在首位。
<font color='cornflowerblue'>正确的命名示范: x ，x1，max_x，_x</font>
<font color='red'>错误的命名示范: 1x，max-x</font>
注意:矩阵x，其第一个元素是x(1)， 不是x1。

<font color='cornflowerblue'>【例题】</font>
$$
\begin{cases}x^2+y^2+2x=103
\\ 2x+y=12
\\x>0
\\y<5
\end{cases}
$$
<font color='red'>【解】</font>

`x^2+y^2+2*x=103;`

`2*x+y=12;`

`x>0;`

`y>5;`

注意：
:one:不要忘记分号。
:two:不要忘记乘号。
:three:不要忘了x>0是Lingo默认条件，不用写。

### 四、线性规划基础

:one:一个线性规划中只含一个目标函数。(两个以上是多目标线性规划，Lingo 无法直接解)
:two:求目标函数的最大值或最小值分别用max= ..或min=...来表示。
:three:以!开头，以;结束的语句是注释语句
:four:线性规划和非线性规划的本质区别是目标函数是否线性，其余致，故不需要区分。但值得注意的是，非线性规划的求解十分困难，基本得不到全局最优解。

<font color='cornflowerblue'>【例题】</font>
某工厂有两条生产线，分别用来生产M和P两种型号的产品，利润分别为200元/个和300元/个，生产线的最大生产能力分别为每日100 和120，生产线每生产一个M产品需要1个劳动日(1个工人工作8小时称为1个劳动日)进行调试、检测等工作，而每个P产品需要2个劳动日，该厂工人每天共计能提供160劳动日，假如原材料等其他条件不受限制，问应如何安排生产计划，才能使获得的利润最大?

<font color='red'>【解】</font>设两种产品的生产量分别为x和x，则该问题的数学模型为:
目标函数: $max z= 200x_1 + 300x_2$,
约束条件为:
$$
\begin{cases}x_1 \leq 100
\\x_2 \leq 120
\\x_1+x_2 \leq 160
\\x_i \geq 0,i=1,2
\end{cases}
$$
由lingo信息可知，运行时间依旧0秒，目标值为29000，此时x_1是100，x_2是30。

![image-20210326192709585](image-20210326192709585.png)



# 第二章 Lingo入门

### 一、例题引入

<font color='cornflowerblue'>【例】</font>已知模型如下，其中a_i=i，i=1,2,…,5，请编程求解：
$$
max S
$$

$$
s.t.
\begin{cases}x_1 \leq 100
\\S=a_ix_i, i=1,2,…,5
\\\sum_{i=1}^5x_i=5000
\end{cases}
$$

<font color='red'>【解】暴力枚举法</font>
$$
max S
$$

$$
s.t.
\begin{cases}S=a_1x_1
\\S=a_2x_2
\\S=a_3x_3
\\S=a_4x_4
\\S=a_5x_5
\\x_1+x_2+x_3+x_4+x_5=5000
\end{cases}
$$

![image-20210326194835418](image-20210326194835418.png)

点评：太过笨拙
所以将要学习Lingo中的“集合”

### 二、矩阵工厂

**2.1 矩阵工厂：生产一维矩阵**
例子：（Lingo不读取空格）

```lingo
sets:
factory/1..6/:a,b;
plant/1..3/:x,y;
andsets
```

对以上程序对应知识点：
:one:factory和plant都是制造矩阵的工厂，但它们是两家不同的工厂。
:two:factory工后面的/1..6/ 说明它专门生产lx6的矩阵。
	 factory工厂最后面出现的a和b,都是lx6的矩阵。
:three:
plant工厂后面的/1../说明它专门生产1x3的矩阵。
plant工厂最后面出现的x和y,都是lx3的矩阵。
:four:矩阵工厂的名字factory是随便起的，工厂所生产行矩阵的名字a和b也是随便起的。
:five:以上这四句话，本质是定义了四个行矩阵的大小，矩阵工厂只是中介。
:six:生产完矩阵后，工厂和矩阵之间将脱开联系。
:seven:Lingo不是一行一行读代码的，所以用sets:和endsets表示矩阵工厂生产流程的起止。



![image-20210326195532615](image-20210326195532615.png)

<font color='cornflowerblue'>【例1】</font>

阅读以下代码，请问a和b两个举证有联系吗？

```
sets:
nanfu/1..6/:a,b;
endsets
```

<font color='red'>【解】</font>
没有联系，只是a和b都是一行六列的矩阵。

<font color='cornflowerblue'>【例2】</font>
阅读以下代码可否让代码简洁一点



```
sets:
ctgu/1..6/:a;
mcm/1..6/:b;
endsets
```

<font color='red'>【解】</font>

```
sets:
easy/1..6/:a,b;
endsets
```

<font color='cornflowerblue'>【例3】</font>
阅读以下代码,请问有和问题

```
sets:
ceshi/1..6/apple,Apple;
endsets
```

<font color='red'>【解】</font>
Lingo不区分大小写，两个矩阵名字一样

**2.2矩阵的赋值**
矩阵工厂不能只生产矩阵，还要给矩阵赋初值才行，例子如下:

```
sets:
factory/1..6/:a,b;
plant/1..3/:c,x;
endsets

data:
a=1,2,3,4,5,6;
b=6.0,5.0,4.0,3.0,2.0,1.0;
c=10,20,30;
enddata
```

以上程序对应以下知识点: 
:one:不是每个矩阵都要赋值，有些矩阵正是我们要求解的变量。
:two:需要赋值的矩阵必须赋满，不能给6个元素的矩阵只赋3个数值。
:three:Lingo中可以给矩阵赋整数，也可以赋小数。
:four:Lingo不是一行一行读代码的，所以用`data:`和`enddata`表示矩阵赋值的起止。

**2.3 循环与求和**
<font color='cornflowerblue'>【例】</font>已知模型如下，其中a_i=i，i=1,2,…,5，请编程求解：
$$
max S
$$

$$
s.t.
\begin{cases}x_1 \leq 100
\\S=a_ix_i, i=1,2,…,5
\\\sum_{i=1}^5x_i=5000
\end{cases}
$$

<font color='cornflowerblue'>【for循环】</font>

题中的约束条件可以利用for循环一步到位。

```
@for(gc(i):S=a(i)*x(i));
```

:one:for循环，括起整行语句，因为S=ax，i=1,2..,5 相当于5个约束条件:
$$
\begin{cases}
S=a_1x_1
\\S=a_2x_2
\\S=a_3x_3
\\S=a_4x_4
\\S=a_5x_5
\end{cases}
$$
:two:for循环内部，先写工厂，以告诉for循环几次，之后再上接约束条件。
:three:此处的i可带可不带，甚至可以换成六k或m等等。
:four:2维矩阵工厂出现后，同时会出现i和，那时必须带i和。

<font color='cornflowerblue'>【sum求和】</font>

题中的约束条件可以利用sum求和一步到位。

```
@sum(gc(i):x(i))=5000;
```

:one:sum求和，不可以括起完整的约束条件，因为-般的求和的结构是这样的:
$$
x_1+x_2+x_3+x_4+x_5=5000
$$
:two:sum求和内部，先写工厂”，以告诉sum求和几次，之后再上接约束条件。
:three:此处的/可带可不带。
:four:二维矩阵工厂出现后，同时会出现i和j，那时必须带。

<font color='cornflowerblue'>【for与sum出现的标志】</font>
:one:约束条件后面有 i=1,2,3… ，一定在最后套上for。
:two:约束条件前面是求和符号$\sum_{i=1}^5x_i$，一定在中间加上sum。



【例】已知模型如下，其中a_i = i , i = 1 , 2 , …… ，5，，请编程求解：

程序如下：

```
model:

sets:
gc/1..5/:a,x;
endsts

data:
a = 1,2,3,4,5;
enddata

max = S;
@for(gc(i):a(i)*x(i) = S);
@sum(gc(i):x(i)) = 5000;

end
```

PS：使用了矩阵工厂创建矩阵后，整个程序需用<font color='cornflowerblue'> model:</font>和 <font color='cornflowerblue'>end</font> 包起来。



### 三、工厂合并

先来看看例子：

```
sets:
factory /1..6/ : a;
plant /1..8/ : d;
Cooperation(factory,plant) : c, x;
endsets
```

以上程序可以得到以下结论：
① Cooperation 大工厂是由 factory 和 plant 两家小工厂合并而办，可生产 6 × 8 的矩阵。
②a 是 1 × 6 的矩阵，d 是 1 × 8 的矩阵，c 和 x 都是 6 × 8 的矩阵。
③ 如果将 `Cooperation(factory,plant)`中的 factory 与 plant 调换位置，则生产 8 × 6 的矩阵。
④ 工厂合并的名字 Cooperation 是随便起的，矩阵的名字 c 和 x 也是随便起的。

**3.2 矩阵的赋值**

```
data:
c=6,2,6,7,4,2,5,8
 4,9,5,3,8,5,8,2
 5,2,1,9,7,4,3,3
 7,6,7,3,9,2,7,1
 2,3,9,5,7,2,6,5
 5,5,2,2,8,1,4,3;
enddata
```

**3.3 例题**

<font color='cornflowerblue'>【例】</font>请编程求解以下模型，已知条件如右侧所示：
$$
min z = \sum_{i=1}^{6}\sum_{j=1}^{8}c_{ij}.x_{ij}
\\\
\\s.t.
\begin{cases}x_1 \leq 100
\\ S=a_ix_i, i=1,2,…,5
\\\sum_{i=1}^{8}x_{ij}\leq a_i , j=1,2,...,6
\\\sum_{i=1}^{6}x_{ij}= d_j , j=1,2,...,8
\\x_{ij}\geq 0,i=1,2,...,6,j=1,2,...,8
\end{cases}
\\\
\\a = 60,55,51,43,41,52;
\\b = 35,37,22,32,41,32,43,38;
\\c=6,2,6,7,4,2,5,8
\\ 4,9,5,3,8,5,8,2
\\ 5,2,1,9,7,4,3,3
\\ 7,6,7,3,9,2,7,1
\\ 2,3,9,5,7,2,6,5
\\ 5,5,2,2,8,1,4,3
$$
<font color='red'>【解】</font>

```
sets:
factory /1..6/ : a;
plant / 1..8 / : b;
coo (factory,plant): c , x;
endsets

data:
a = 60,55,51,43,41,52;
b = 35,37,22,32,41,32,43,38;
c = 6,2,6,7,4,2,5,8
 	4,9,5,3,8,5,8,2
 	5,2,1,9,7,4,3,3
 	7,6,7,3,9,2,7,1
 	2,3,9,5,7,2,6,5
 	5,5,2,2,8,1,4,3;
enddata

min = @sum(coo(i,j):c(i,j)*x(i,j));
!min = @sum( factory(i):@sum(plant(j):c(i,j) * x(i,j)) );

@for ( factory(i) : @sum(plant(j):x(i,j)) <= a(i) );

@for ( plant(j) : @sum(factory(i):x(i,j)) = b(j) );
```

# 第三章 罗辑运算符&内置函数

### 一、运算符

**1.1 算术运算符**

<font color='cornflowerblue'>【例】</font>若 $x=2$ ，求解 $3x^{10}+6/(15-\sqrt x)$ 的数值

```
x = 2;
y = 3*x^10 + 6/(15-x^(1/2));
```

**1.2 关系运算符**

① 关系运算符往往用在约束条件中，用来指定约束条件左右两边必须满足的关系。
②Lingo 只有三种关系运算符：“=”、“>=”以及“<=”。 
	没有单独的“>”和“<”，若出现，Lingo 则视为省略了“=”。 若想严	格表达 A 大于 B，可以用以下方式：

```
B = 10;
w = 0.00001;
A - e > B;
```

**1.3 逻辑运算符**

### 二、lingo内置函数

**2.5 其他函数**

`@wrap`

使用方式：

它需要两个参数，INDEX和LIMIT。

作用：

例如J=@WRAP(INDEX, LIMIT)，它会把J的值调整至满足1 <= J < LIMIT+1之间

| 类别 |   函数名   |                      返回值 |
| :--: | :--------: | --------------------------: |
|      | @WRAP(x,y) | $x,x\leq y$<br /> $x-y,x>y$ |

