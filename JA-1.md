# JA-1 Java 基础知识

在接下来的几个章节里，我会为你铺垫一些插件开发中用到的 Java 编程知识。可能有些长，也可能有些枯燥乏味，但我会尽量让它变得简单而快乐一些。

每个小节只介绍一个核心概念，所以如果你已经知道它们，或者在其它编程语言中接触过它们，就可以快速阅读乃至跳过不看。

## 用代码描述世界

没学过编程的读者，如果想要描述插件的部分功能，他们会这么说……

```
给玩家一组钻石
```

这么说很易懂，所有人都能读得懂这句话的意思。然而，这种**自然语言**对于计算机是无效的。计算机比较死板，它当然看不懂这样的描述。

稍有经验的 Minecraft 玩家就会想到，我们可以使用命令：

```
/give player minecraft:diamond 64
```

编写插件和编写命令，其实也就差不多，如果想让 Bukkit 服务端做同样的事情，我们会编写出这样的**代码**：

```java
player.getInventory().addItem(new ItemStack(Material.DIAMOND, 64));
```

看上去长了不少，不过如果翻译成中文，读起来就是“玩家获取物品栏增加一个新的物品钻石 64”，整理一下，也就是“获得玩家的物品栏，在其中新增一个物品，64 个钻石”。

是不是不难懂？即使对于 Java 一无所知，你也可以大致理解这一行代码的含义。

这就是所谓**用代码描述世界**。如果想让用 Java 编写的 Bukkit 服务端为我们做什么事情，我们就必须按照 Java 规定的**语法（Grammar）**，编写出它能看懂的代码。

其实说白了，代码不过也就是结构复杂了那么一丢丢，用法灵活了一丢丢的命令而已，这么说来，是不是就有信心了呢？好的，那么接下来，就让我们真正开始学习这种特殊的“命令”。

> Kirara：这些代码要写在哪呢？

命令敲在聊天框里，而我们的代码要写在**开发工具**当中的**编辑器**里。不过这一点让我们先按下不表，先学会“怎么写”，再考虑“写在哪”。

## 想致富，先撸数

### 我们从一个数字开始

```java
1
```

这是个数字 1，很小巧，对吧？即使不需要任何编程知识，你也能读懂它的含义。

这个数字 `1` 代表的就是 1，是它的**字面含义**，因此，像这样**直接写出来**的，“**一看就知道**”是什么东西的，在 Java 中被称作**字面量（Literal）**。

在数字中，负号和小数点可以正常使用，就像数学中一样，因此，你可以直接写出下面这样的数字：

```java
-32768
114.514
```

?> 在软件工程中，我们用英文句号 `.` 来表示小数点。请把你的输入法切换到英文模式，然后找个地方敲一敲试试。`114.514` 是对的，而 `114。514` 不对。

这种**数字类型**很简单，不过，Java 当中不仅有数字类型，还有一些其它的类型。

### 不白之谓黑

```java
true
false
```

这就是**逻辑类型**。`true` 代表“真的”或者“对的”，`false` 代表“假的”或者“错的”，它们两个是天生的一对，合称**布尔值（Boolean Value）**，又名**逻辑值**。

数字有 0、1、2……等等，但是逻辑值**只有两个**：不是 `true` 就是 `false`，没有其它可能。

?> `true` 和 `false` 是完全独立的一种体系，它们不是数字，也和数字没有关系。

### 让电脑处理文字

```java
"这是一个字符串，但是锟斤拷烫烫烫"
"Ciallo～(∠・ω< )⌒☆"
```

这就是**字符串类型**。用双引号（`""`）**加在一些文字的两端**，就把它变成一个**字符串（String）**。

好吧，也许术语很难懂，但**字符串其实就是文字**，只不过是，可以被程序处理的文字。`"abc"` 代表的就是 abc 这三个字母，很简单，很直接。

> Kirara：为什么要加引号呢？

这是为了告诉 Java：“**这是一些文字，请不要把它当作代码**”。我们来举个例子说明一下：

> **你的地址**
>
> 如果我想知道 Kirara 的家在哪里，我会告诉她：“请写下你的地址”。
>
> 你肯定不会这么写：
>
> ```
> 你的地址
> ```
>
> （不过，Kirara 可能会这么干，这小丫头比较调皮……）
>
> 而是
>
> ```
> 樱云岛 光点郡 花海塔 风月街 21 号
> ```
>
> 她**解读**了我所说的“你的地址”的意思，并把它**换成了**自己的真正住址。这也是 Java 解读你的代码时的通常情况。
>
> 但是，如果我就是想让她**写出“你的地址”这四个字**怎么办？我不能再提出同样的请求，因为她还是会尝试解读这个词的意思，我也不能指望她一时抖机灵，因为 Java 可不会抖机灵。
>
> 这个时候，我们通常会说：“请写下‘你的地址’这四个字。”看到这里的**单引号**了吗？这是为了告诉听到这句话的人：**请把“你的地址”四个字按原样写出来，不要解释**。
>
> 在 Java 中，想做类似的事情也是一样的，要想写任意的文字而不让 Java 解读，就需要加上引号。

当你用 Word 之类的软件写文字的时候，你是在**写作**，文章的内容你可以任意发挥，因为 Word **不会尝试解读你的文章**。但是 Java 不一样，在开发软件的时候，我们是在**编码**，而编码是有**很固定的语法**的，如果你瞎写乱画，Java 就不给你干。

所以，如果我们想让 Java 处理一些任意文字（比如 `"Ciallo～(∠・ω< )⌒☆"`），却又**不想让它觉得我们是在瞎写乱画**，就要在两边**加上引号**，告诉 Java：“**你就把这些原样记住，别管我什么意思**”，使得 Java 不要把它**当作代码**，而是**当作普普通通的文字**。

例如，`123` 是一个数字，读作“一百二十三”，但 `"123"` 却是一个字符串，读作“一二三”。因为，不带引号的 `123` **很特殊**，Java 会把它当作数字来对待，而在两边**加上引号** `""` 后，它就变得**没那么特殊**了，Java 会把它看作普普通通的文字，也就是**字符串**啦。

?> 软件工程师们通常喜欢用 `"blahblah"` 这样两边带引号的写法，来强调他们所说的是个字符串。你只需要知道，两端的引号是用来**标记**字符串的，却**不是字符串内容的一部分**。

当然，只能写一些字面量是没什么意思的，1 就是 1，2 就是 2，哪怕是复杂如 `"Ciallo～(∠・ω< )⌒☆"` 这样带特殊符号的字符串，也不过就是一些字。它们虽然在这里，却做不了什么事情。**1 不会自动和 2 加起来变成 3，而字符串也不会自己显示在屏幕上**，这可没什么意思。

## 连词成句

### 不仅仅是加法！

事情是从这里开始变得好玩的。

```java
1 + 1
```

你几乎要脱口而出 `2`，不过现在暂且把它理解为将两个数相加这一**行为**。很显然，这里的 `+` 符号有加法的意思，它是一个**运算符（Operator）**，这你在数学中已经学过。不过，这里还有一个更重要的概念：

**`1 + 1` 是一个整体，它的值是 2。**

这个由值和运算符构成的“整体”，学名为**表达式（Expression）**。

> **到底怎么回事？**
>
> 表达式可以看成是“**还没有算出结果的算式**”，它把“要做什么”写了出来，而不是直接写出结果。
>
> 在小学数学中我们就知道，每一个算式都有一个**结果**，所以当 Java 看到一条表达式的时候，它就会**计算出来它的结果**，即所谓的**值（Value）**。紧接着，它把**整个表达式换成这个结果**，然后继续下一步。
>
> 所以，像是 `1 + (1 + 2)` 这样的表达式，是先变成 `1 + 3` 再变成 `4` 的。
>
> 除此之外，**单一的字面量也可以看作表达式**，比如 `2`，虽然它没有什么要计算的，但是它的结果确实是 `2`，不是吗？

相比一个字面量 `2`，一个表达式能做的事情**更多**：它虽然也代表 2，但是它很清楚地**表达**了一个操作：把两个 `1` **加起来**。产生结果 `2` 并不是它的目的，它的目的是要告诉 Java：**你得做点什么，把两个数相加！**

计算机能够**计算**表达式的**值（Value）**：`1 + 1` 计算出来的值是 `2`，而 `30 * 30` 计算出来的值是 `900`。工程师们把这个计算过程称为**求值（Evaluate）**。

### 写一些算式

你可以把加减乘除各种符号组合起来，写出这样的表达式：

```java
3.1416 * (7 * 7 - 5 * 5) * (4 + (1 + 2))
```

加法 `+`，减法 `-`，乘法 `*`（键盘上没有×这个键）以及除法 `/`（也没有÷）都可以在 Java 中直接使用，它们的作用也和数学中基本相同。此外，你还可以用小括号 `()` 来让一部分算式优先计算。

唯一和数学中不一样的是，这里没有中括号和大括号，如果想在括号里套括号，就请全都用小括号吧（笑），Java 会把括号自动配对。

### 彳 + 亍 = 行

```java
"Cia" + "llo~"
```

等一下，字符串是怎么“相加”的？实际上，`+` 不仅有数学上的加法含义，它还能用来将两个字符串“粘贴”在一起。

这个表达式的值，是将两个长度分别为 3 和 4 的字符串**拼接（Concatenate）**，得到一个长为 7 的字符串 `"Ciallo~"`。

```java
"我是 No." + 1
```

**字符串和数字**做加法……好吧，事实上，在 Java 里面这么写的时候，Java 会先把 `1` **转换为字符串** `"1"`，然后再进行拼接，得到 `"我是 No.1"`。

> Kirara：那为什么不是把字符串转换为数字，然后做加法呢？

—— 要不你试试，告诉我怎么把 `"锟斤拷烫烫烫"` 转换成对应的数字。

## 记忆是个糟糕的东西

### 开辟一块空间

在 Minecraft 中，玩家身上的空间是非常少的：27 格背包，9 格快捷栏，1 格副手，4 格装备栏。每当你下矿挖掘的时候，那些各式各样的石头总会很快填满你的背包。

这个时候，你就想要找一个**箱子**，把身上的东西**存储**在里面。为此，你拿起 8 个木板，摆成一圈……

在 Java 中，事情也是非常类似的。把表达式组合起来，可以产生很多很多的数据，而如果想要把数据暂时保存一下，我们就要使用**变量（Variable）**。

```java
int a = 21;
```

这就代表，我们在 Java 当中开辟了一块空间，名字叫做 `a`，用来保存一个整数 `int`，并且在里面放一个 `21`。

术语上来说，这件事情叫做**定义（Define）**。我们定义了一个整数变量 `a`。

### 里面装的是什么？

开头的 `int` 是什么呢？这是变量的**类型**。

**使用变量时，需要指定它的类型。**

相信没有人会喜欢在一大堆箱子里面翻找某天缴获来的命名牌，如果你给你的箱子上面放上告示牌，写上“建筑方块”、“战斗物品”、“红石材料”这样的**类型**，即使不用打开箱子，你也知道里面放的是什么，对不对？

如果想要保存一个整数，我们就要使用 `int`，想要保存小数，我们可以选择 `double` 或者 `float`，字符串是 `String`，逻辑值是 `boolean`……诸如此类。

哦对了，还有很重要的一点：存储东西时，要给它选择合适的“盒子”，也就是**选择合适的类型**。如果把字符串保存在整数里，那就乱了套啦！

### 你是我，那我是谁？

知道了有关变量的事情，Kirara 就写出这样的代码：

```java
double a = 114.514;
String a = "blahblah";
boolean a = false;
```

呃，有些不对。虽然说你可以随意在 Java 中开辟新的空间，但是有一条规则：

**同名的变量只能有一个。**

为什么只能有一个？试想如果现在突然出现一个和你同名同姓身份证号还一样的人，会发生什么？到底谁是谁啊，一定会引起大混乱的（笑）。同样的，在后面使用 `a` 这个名字的时候，Java 肯定不知道你指的是哪个 `a`。如果是你，你知道吗？

因此，我们需要取一些不一样的名字。

```java
double 1145 = 114.514;
String str = "blahblah";
boolean c = false;
```

呃，还是不对，原因主要是 `1145` 并不是一个**有效的变量名**（可真是麻烦！）。

变量名有如下的要求：

- 只允许使用大小写英文字母，下划线`_`，美元符`$`和数字。
- 数字不可以在开头。（~~`1Password`~~ 不行）
- 不可以与关键字重复。（~~`int`~~ 不行，但是`int1` 可以）

> **你是职业选手吗？**
>
> 其实变量名可以用包括中文在内的很多特殊符号，但是为了规范起见，这里只提供大多数 Java 工程师公认的版本。曾经有人的插件里面使用的变量名叫做 `pei置`，希望你不会是下一个。

## 文不加“点”

### 做这个，再做那个

大家都知道，Java 程序是一步一步执行的，这里，每“一步”就是一条**语句（Sentence）**。

一条语句相当于口语中的“一句话”，我们做计划的时候也是“做这个，做那个”……一步一步地执行。在 Java 中，语句也是一条一条，一步一步执行的。

下面是**三条**语句：

```java
int a = 1;
int b = a + 1;
String c = "str";
```

这就是做了三件事情（三个步骤）：

- 定义变量`a`，类型是整数，值为`1`。
- 定义变量`b`，类型是整数，值为`a + 1`（`2`）。
- 定义变量`c`，类型是字符串，值为`"str"`。

和命令一样，语句的先后顺序很重要，不可以随意调换。

### 一行更比六行强

你会发现，每一条语句都以分号 `;` 结尾，这个分号的作用，就相当于中英文中的句号。

**分号代表一条语句的结束。**

多条语句可以写在同一行中，一条语句也可以拆到多行之中 —— 只要它其中没有分号，Java 就会将它解释为一个整体。

```java
String a = "这段话太长，所以我把它" +
           "拆成两行来写。";

String b = "这两条语句"; String c = "可以写在同一行";
```

你可能会想，一般的书本当中，一个自然段内是不换行的：

> 僵尸猪灵会保持敌对 20 至 40 秒，不过即使这个时间已过，僵尸猪灵仍然会追赶被标记的玩家，除非玩家逃离它们 40 格远的追踪范围。接近一个已经敌对的僵尸猪灵（35 格内）会导致它发出一个警告，并激怒 40 格范围以内的僵尸猪灵。未加载区块里的僵尸猪灵的宽恕计时器会停止。因此，如果玩家进入了一个下界传送门并……

但是在软件开发中，通常一条语句**占据单独的一行**。这不仅仅是为了好看，更有助于代码的逻辑清晰。

```java
String a = "缤纷纨绔绒，纯绚绵绝缎。";
String b = "Fine and functional foppery for the fashion-forward fighter."; 
String c = a + b;
```

### 说话要说完整

语句是程序执行的基本单元，Java 在执行你的语句的时候，总是一条一条语句执行的。

**不形成语句的东西，是没办法被执行的。**

现在这里有一段被剪掉了一半的代码：

```java
int a = 2 +
```

这就不能成为一条语句。Java 知道你的意思是**给 `a` 赋值**，也知道 `a` 的值是 `2` 加上什么东西，但是**到底加什么**？空格？上一行的变量？还是硬盘里面某个传统而古老路径的一张图片？**仅凭已有的信息，不足以知道程序的目的**，所以 Java 会**继续向后读**，直到找到一条**完整的语句**。

我们把剪掉的后半段放回来：

```java
int a = 2 +
3;
```

Java 读到第二行的时候，终于发现了加法 `+` 的另一个被加数，同时也看到它心心念念的分号 `;`（代表语句的结束），现在它终于明白，我们要计算的是 `2 + 3`，它算出来 `5`，然后将它赋给 `a`。

所以现在，我们得到一个很重要的结论：

**如果我们想让 Java 做什么，我们需要写出一些语句，来让 Java 执行。**

## 做点修改

### 来找点东西偷偷

你可以把箱子里面的东西拿出来再放新的东西进去，同样的，变量可以在创建后再**修改**：

```java
int a = 5;
a = 10;
```

这样，`a` 一开始是 `5`，但是随后立马就被修改成了 `10`。于是，从这一行之后，`a` 里面放的东西就不再是 `5`，而是 `10`。

这就是对 `a` 进行**赋值（Assign）**，我们会说，把 `a` “赋值为” `10`，或者，把 `10` “赋给” `a`。

### 全新的我

既然我们可以修改变量的值，我们就可以来做一些好玩的事情了！

```java
int a = 1;
a = a + 1;
```

你几乎又要脱口而出“无解！”，对吧？但是等一下，这可不是什么方程，`a = a + 1` 的意思是：**把 `a` 赋值为 `a + 1`。** `a + 1` 是什么？`2`。所以，`a` 现在是 2。

你可以发现，像是这样的赋值操作是**有方向**的 —— 从右往左。如果写成 `a <- a + 1`，就容易理解多了。

Java 在进行这样的**赋值**运算时，总是先计算等号右边的**表达式**（还记得吗，表达式可以计算出一个值），再把等号左边的变量**修改成**这个计算出来的值。表达式中如果含有变量，会把变量**代换成它现在的值**。简而言之：

**赋值，是把等号左边变量的值，改成等号右边表达式的值。**

## 稍后再用

### 打包带走！

假设我们要施展一种非常复杂的“魔法”来对变量 `a` 进行一些修改：

```java
int a = 5;

a = a + 1
a = a * 2;
a = a * a + 9;

a = a + 1;
a = a * 2;
a = a * a + 9;

a = a + 1;
a = a * 2;
a = a * a + 9;
```

像上面这样**复制粘贴**代码，就会让程序变得**像学术垃圾一样** —— 又长又枯燥无味，而且显得很愚蠢。

我们可以使用一种**特殊的结构**来把一些语句**打包**起来：

```java
int a = 5;

void hello() {
    a = a + 1;
    a = a * 2;
    a = a * a + 9;
}

hello();
hello();
hello();
```

原本我们是把 `a = a + 1 ... + 9` **这几行**写三遍，而现在我们只需要**事先将它写一遍**，用一对括号 `{}` 把它们**打包**起来，然后像变量一样给它**取个名字**（这里是 `hello`），之后只需要**使用**它三遍就行了。是不是很像数学定理？只需要先证明一遍，就可以在各种地方**重复使用**，而不需要每次都从上下五千年再说起。

像这样**将一些语句打包起来，可以重复使用的结构**，就叫做**方法（Method）**，也称**函数（Function）**。大括号 `{}` 内部是被方法“打包”起来的语句，叫做**方法体（Method Body）**，从左括号 `{` 开始，到右括号 `}` 结束。

> **你是职业选手吗？**
>
> 许多工程师认为，使用**函数**一词在 Java 中是不规范的，原因是 Java 作为严格面向对象的语言，适用于对象的**方法**一词比函数式编程的**函数**一词更能体现 Java 的特性。不过据我所查找到的资料来看，混用这两个词的人不少，其中甚至不乏许多高级工程师，本着方便起见的考量，本书中也就不做严格区分。

打包语句成为方法的操作叫做**定义**方法，也可以说是**创建**方法。使用已经定义好的方法，叫做**调用**方法。

?> 在**定义方法**的时候，方法体是**不执行**的。也就是说，`void hello() {}` 的大括号 `{}` 中的三条语句不会立刻执行，而是直到下面**调用**的时候才会执行。`a` 的值直到最后三行之前，都不会发生变化。就像设计师**画蓝图**一样，画蓝图的时候并不是**一边画一边搬砖盖房子**，而是画完之后，**有需要时再使用**蓝图来盖房子。

### 我还不能使用

下面我们先介绍方法的**调用**，请看这一行：

```java
hello();
```

这句话的意思就是告诉 Java：**我要使用方法 `hello` 了，请准备一下！**

`hello` 是**方法名**，是你打包了语句之后给它取的名字。就像使用变量需要用变量名一样，调用方法也需要**提供方法的名字**。

方法名后有一对小括号 `()`，这可不是为了显得可爱（虽然确实有这个作用），这表示“**使用**”，只要写出了方法名，并在后面**加上**一对小括号 `()`，就自动构成一个**方法调用**。换而言之，**Java 一旦看到小括号 `()`，就会在这里开始执行 `hello` 方法中的内容**。

知道了这些，你就可以试试下面的练习：

```java
int a = 1;

void hello() {
    a = a * 2;
    a = a + 1;
}

hello();
a = a - 1;
hello();
```

在上面的程序中，`a` 从 `1` 变成了 `5`。`a` 从 `1` 开始，`hello()` 调用将它变成 `1 * 2 + 1` 即 `3`，然后是 `a = a - 1` 将其改为 `2`，最后又是一个 `hello()` 将其变成 `2 * 2 + 1` 即 `5`。怎么样，没那么难吧？

### 设计一个方法

现在你已经会使用方法了，那么，是时候看看怎么定义（创建）一个方法了：

```java
void hello() {
    a = a + 1;
    a = a * 2;
    a = a * a + 9;   
}
```

先忽略第一个 `void`，我们看到 `hello()`，这**很像**方法调用，但是由于它后面有一个 `{`，所以这**不是**方法调用，而是方法**定义**。

写在小括号前的 `hello` 是方法的**名字**，大括号 `{}` 中的内容是方法包含的要执行的语句。

除此之外，还有一对小括号 `()`。为什么需要一对小括号呢？你已经知道，变量的定义是这样的：

```java
int a = 1;
```

如果方法定义不加这对括号 `()` 的话，就不方便区分到底**是方法还是变量**了 —— 它们可是两个完全不同的东西！

*其实，加括号完全是语法规范 —— 这就是刻意的游戏设计，没有所谓的原因。不过，为了理解方便，请允许我糊弄你一下。*

在名字后面加上 `()`，就可以告诉 Java：“**我们不是在定义变量，而是在定义方法。**”

总结一下，我们只需要把要重复利用的语句**用 `{}` 打包**起来，在**前面加上**方法名和一对小括号 `()`，再在**最前面**添上一个神秘的 `void`，就可以**定义一个方法**以供日后使用。

?> 方法名的限制和变量名一样：大小写字母和数字，但不能以数字开头，不能包含除下划线 `_` 和美元符 `$` 之外的特殊字符，也不能与已有的关键字重复。当然了，即使一个是方法，一个是变量，也**不能**在同一个程序中用一样的名字，不然要引起大混乱的。

### 进一步偷懒

```java
String a = "丁真";
String b = " skjsjhb";

void foo() {
    a = "你好，我是" + a;
}

void bar() {
    b = "你好，我是" + b;
}
```

这里**定义**了两个方法（但是没有调用！所以，`a` 和 `b` 的值暂且还保持不变），一个在 `a` 前面加上 `"你好，我是"`，另一个在 `b` 前面加上同样的内容。

如果把它们分别**调用**一下：

```java
foo();
bar();
```

在这两行执行之后，`a` 变成 `"你好，我是丁真"`，而 `b` 变成 `"你好，我是 skjsjhb"`。

不过，这样好麻烦啊，明明都是在前面加上**同样的**内容，做的事情**这么相似**，只因**使用的变量不同**，就要定义**两个不同**的方法，很不公平。如果是有 1000 个变量，岂不是要**定义 1000 个**不同的方法？

这么一看，我们本来是想要**避免**学术垃圾那样的**复制粘贴**，结果到头来，除了那点不同之外，不**还是复制粘贴**吗？方法如果只能做这些，那也太没用了！

有没有一种办法，可以在**定义方法的时候不指定**用哪些变量，而在**调用方法的时候再决定**用哪个呢？

设计 Java 的人已经考虑到了这个问题，我们在下下一节中介绍。

## 这个，是献给你的

在继续有关方法的复杂内容之前，我们先来讲点轻松的。

我特别喜欢英文中的一句话，现在分享给大家：

> People talking without speaking. People hearing without listening.

翻译成古汉语就是：

> 道而不述，闻而不名。

或者，不那么准确地：

> 说了跟没说一样，听到了装没听到。

你知道，Java 会一板一眼地严格执行你的代码，不论你写什么它都会听。

如果我们想写一些**给人类阅读，而不是给 Java 执行**的内容呢？这就是所谓**注释**。

```java
int a = 1;
// 这是注释，Java 不会执行
// 即使这一行写了 a = 2
// a 也不会变成 2
a = a + 2;
// 现在 a 是 3 (1 + 2)
```

如果有一行中含有**行内注释符号** `//`，那么，从 `//` 开始，**包括它本身**，直至**这一行结束**，其中的内容都会被 Java 忽略。Java 既不会尝试解读，也不会试图把它保存下来，就好像这些文字从来不存在一样。

> Saki：我认为字符串应该也可以做到相同的事情？Java 同样也不会解读 `""` 中的内容，的说？

这么说是有些道理，不过**字符串**和**注释**还是有些区别……

> **空气不是真空**
>
> 尽管 Java 不会尝试解读字符串中的内容，但它会把它**记忆下来**。作为一种字面量，字符串可以被赋值给变量：
>
> ```java
> String s = "这是一个字符串，不会被解读";
> ```
>
> 尽管 Java 不理解引号里的意思，但它还是尽职尽责地将它记录下来，然后将 `s` 的值设置为它。
>
> 然而，对于注释则是完全不一样的。注释会在 Java 执行代码的时候**完全忽视**，所以像这样的代码：
>
> ```java
> String s = // 这是注释，它不会被处理
> ```
>
> 这行代码实际上是**错的**……因为，赋值运算符 `=` **两边都需要有东西**，注释会被 Java 直接**抹掉**，所以 `=` 的右边**什么也没有**，Java 不知道怎么修改 `s` 的值。

注释能够让工程师在代码里面**插入一些人类的语言**，对程序进行一些**解释**，使得程序更易读。

我们之前提到过，代码有很严格的格式规范，即使是用来解释代码的文字也会被 Java 认为是“瞎写乱画”，所以我们需要使用注释来告诉 Java：“这是**说的人话**，可不要看哦。”

## 选择合约

### 交出你的钱

在我们介绍有关方法的进一步内容之前，先让我讲一个故事。

> **猫猫刺客 Neko**
>
> Neko 曾经是 Saki 的一位好朋友，她们不仅是业务上的同事，更是生死之交 —— 在 Saki 成为一名游戏设计师之前，她是一位侦探。而她的同事 Neko，则是**职业杀手**。她活跃于光环郡的飞雪防御塔附近，猎杀着雇主指定的目标。
>
> 所有和 Neko 进行过交易的人，都明白这当中的规矩：**只需要用一张纸条，上面写上仇敌的名字**，用它裹住一块小奶酪，在月圆的前一个晚上，挂在落雪之森从北向南数第六颗树的树枝上，你的仇敌就会在几天内由于“意外事件”消失不见：被独角兽刺穿喉咙，失足坠落，以及破伤风感染，等等。在此之后，一个用他们的心脏制成的灵球会悄悄出现在你的窗台上，**作为“任务完成”的提醒**。
>
> 虽然没人曾从她口中打听到，但理事厅的长老们都一致认为，Neko **才不关心死亡名单上的人是谁**，她只是默默收下任务命令和报酬，然后，借着夜色的保护，悄悄地……！
>
> 无论是强大无比的防御塔还是尽职尽责的守卫，都拦不住 Neko 刺出的利爪。飞雪塔因此成为樱云岛上最和平的地方 —— 一开始，人们相互之间总是毕恭毕敬，生怕得罪了什么人而招来杀身之祸。而时间久了之后，这也就从压力下的作态变成了真情实感。
>
> 啊啊，和平不来自花朵，而是来自剑锋啊。

回到现实中来。

还记得之前我们提出的问题吗？要怎么在**使用**方法的时候再决定用哪个变量呢？

我们原本的方法是这样的：

```java
void hello() {
    // 做点什么
}
```

如果我们想要让方法**从外界获取**一些变量的信息，我们就**把它写在小括号** `()` 里：

```java
void hello(int a) {
    // 做点什么
}
```

如果想要使用**不止一个**变量，还可以把多个变量**用逗号 `,` 分隔**开：

```java
void hello(int a, boolean b, String c, int d) {
    // 做点什么
}
```

这些变量是**从外界获取**的，也就是说，方法在定义的时候，本身并不决定 `a`、`b`、`c` 和 `d` 的值，它们的值是在**调用**的时候由**调用方法的语句**来提供的。

这些变量是发送给方法“**参考**”的值，所以它们叫做“用来参考的数据”，简称**参数（Argument 或 Parameter）**。请记住这条规则：

**参数以逗号 `,` 分隔，并写在方法后的小括号 `()` 里。**

参数的作用是提供给方法**用作参考**，我们不必为了计算 `a` 设计一个方法，计算 `b` 又设计另一个方法……只需要设计**一个**方法，然后在**调用**的时候，通过**参数**告诉方法，该使用哪个变量。

### 收下我的愿望

怎么样给方法提供参数呢？请看下面的例子。

```java
void hello(int a, int b) {
    a + b;
}

hello(1, 2);
```

我们说过，参数是在**调用**的时候，给方法**用作参考**的。

所以，要给方法提供参数，需要先写出**调用**方法的代码：**方法名，加上一对小括号** `()`。（最后再添上一个分号 `;` 来构成一条完整的语句）

```java
hello();
```

然后呢，要提供参数，我们就直接把参数**对号入座**地放进小括号里：

```java
hello(1, 2);
```

这样，在这一次调用 `hello` 的时候，在方法的内部，`a` 就被 Java 自动赋值为 `1`，`b` 被赋值为 `2`。

然后……就 OK 了，是不是很简单？

> **到底怎么回事？**
>
> 你应该已经发现了，当**定义**方法的时候，我们把形似变量的**参数**放在小括号 `()` 里，这些变量没有赋值，它们的作用仅仅是**占个位置**，等待着被填入实际的值。
>
> 当**调用**方法的时候，我们把**实际的**参数值**对号入座**，从而给这些变量完成“赋值”。
>
> 每一次调用的时候都可以**提供不同的参数**，方法可以**参考**这些不同的参数，**决定**自己要做什么。

现在我们写出这样的代码：

```java
void hello(int a, int b) {
    a + b;
}

hello(1, 2);
hello(3, 4);
```

第一次调用方法的时候（`hello(1, 2)`），我们**提供的参数**是 `1` 和 `2`，于是，在 Java 计算 `a + b` 的值的时候，它把 `a` 换成对应的 `1`，`b` 换成 `2`，计算 `1 + 2` 得到 `3`。

第二次调用方法的时候，事情如出一辙，唯一的不同是**参数变成了** `3` 和 `4`，于是 Java 计算 `3 + 4` 得到 `7`。

发现了吗？不管参数**怎么变**，`hello` 做的事情就是简单把两个数**相加**。我们**不需要**为了计算 `1 + 2` **定义一个**方法，又为了计算 `3 + 4` **再定义一个**方法……只需要**创建唯一一个带参数的方法**，然后在**每次调用**的时候**提供**我们这次想让它计算的**参数**就行了。

> **你是职业选手吗？**
>
> 在 Java 中，像是 `3 + 4;` 这样的无意义语句是**不允许的**，也就是说，我们在 `hello` 方法中写的东西，其实是不对的……
>
> 但是，出于教学目的，我想要凸显出“没有被使用”这个特点，如果我写 `int c = 3 + 4;`，那么，在向读者介绍有关变量作用域的内容之前，读者肯定心生疑问：“明明是赋给 `c` 了，怎么就没用上呢？”
>
> 而如果现在就解释这个，又会变得很麻烦，所以，请专业的你稍微忍耐一下，这个错误，我们后面再行纠正。

对了，虽然这里我们使用了 `3`、`4` 这样的字面量，但不代表方法的参数就**只能**使用字面量（那还是很没用啊），方法的参数可以是任意的表达式，所以你也可以写：

```java
hello(1, 1 + 1);

int x = 2;
hello(1, x);

int y = 1 + 2;
hello(y, y + 1);
```

### 交易必须公平公正

> Kirara：前面算出来的 `3` 还有 `7` 去哪里了呢？

我们之前提到过，表达式

```java
3 + 4;
```

虽然加了分号变成一条**语句**，但 `3 + 4` 既没有**被赋值**给某个变量，也没有**参与其它表达式的计算**，也没有**被用作方法的参数**，所以，Java 辛辛苦苦**算完**这个表达式之后，发现它没有被用到，只好伤心地将它**丢掉了**。

这可不行啊，好不容易做出来的东西，如果没办法**返回**给**调用方法**的地方，那不就是白做了吗？就连 Neko 也知道要把灵球放在雇主的窗台上来告诉他们“**任务完成**”，如果 Java 的方法做不到，可就太没用了。

让我们重新看一下 `hello` 方法：

```java
void hello(int a, int b) {
    a + b; // a + b 计算了，但没被用上
}
```

`a + b` 暂时还没用上，不过，我们只需要**稍加修改**，就可以让这个结果被利用起来：

```java
int hello(int a, int b) {
    return a + b;
}
```

好啦，这样 `hello` 就可以把 `a + b` 的结果，**返回给**调用它的代码了！

具体怎么用呢？你就这样使用 `hello`：

```java
int c = hello(1, 2);
```

我们**调用**了 `hello` 方法，为它提供了**参数** `1, 2`，并且把它**返回的结果**赋给了变量 `c`，就是这么自然，像数学中的函数 `y = f(x)` 一样，**给它提供参数，它就会给你结果**。

**所有的方法调用 `方法(参数)` 都会得出一个结果，这个结果可以被调用方法的代码使用。**

这个由方法返回给调用代码的数据，叫做**返回值（Return Value）**，它是方法执行完的**结果**，可以在调用它的代码中使用。谁调用了方法，这个值就返回给谁。

> **到底怎么回事？**
>
> 形似 `hello(1, 2)` 的这个写法，除了执行方法里面的代码，它本身还是一个**表达式**，和 `3 + 4` 这样普普通通的表达式没有什么区别。
>
> 为什么是这样呢？嗯，我们已经说过，**返回值是方法执行完的结果**，虽然长得不像算式，但 `hello(1, 2)` 确实能得出一个结果，而表达式也能**求值**得出一个结果……所以 `hello(1, 2)` 就是一个表达式，好像也没什么奇怪之处。数学里不也经常写，`g(x) = 1 + 2 * f(x)` 嘛，大致就是类似的意思。
>
> 所以，**如果 `hello(1, 2)` 返回 `3` 的话**，在下面的代码中：
>
> ```java
> int c = hello(1, 2) * 3;
> ```
>
> 我们就可以**把 `hello(1, 2)` 换成** `3`，于是我们知道 `c` 最终等于 `9`。

### 你，会给我什么？

标记在**方法名**前面的，是 `void` 还有 `int` 这样的东西，你知道 `int` 代表“整数”，它是个**类型**。

写在方法名前面的的类型，正是**方法返回值的类型**。

由于在定义方法的时候，返回值还**没有算出来**，因此它的**值**是**无法预测**的。不过，虽然**值**无法预测，但是它的**类型**却是可以预知的。就像**定义变量需要类型**（`int a = 1`）一样，定义方法的时候，也要说明**它的返回值是什么**。试想一下，如果 Neko 完成了刺杀任务，**不提前跟你打招呼**，就突然把血淋淋的心脏摆在你面前，你一定会吓一跳的。

我们还是拿 `hello` 举例子：

```java
int hello(int a, int b) {
    // 里面的东西省略...
}
```

这就告诉每一个使用 `hello` 方法的人：`hello` 执行完了后，会给你一个 `int` 类型的值。

这样，当 Java 看到形如 `hello(1, 2) * 3` 这样的写法时，**即使不需要计算**，它也知道 `hello(1, 2)` 的值是一个 `int`，“数字和数字做乘法，没什么奇怪的嘛”，所以，Java 就不会感到惊讶。

### 没你的份

有一个特殊情况：如果返回值类型这里写了 `void`，就代表“什么也没有”，也就是说这个方法**没有返回值**。

由于 Java 的设想是每个方法**都要返回点什么**，但是有些方法确实就**没有要返回的东西**，这种情况可以用 `void` 告诉 Java：“我**什么也不会给你**，别做梦了！”

如果一个方法什么也不返回，就**不能把它当作一个表达式**，比如：

```java
int hello(int a) {
    // ...
}

void hello2(int b) {
    // ...
}

int c = hello(1) + 1; // 可以执行

int d = hello2(); // 不对！
```

这里的 `c` 可以被正常赋值：虽然我们不知道 `hello(1)` **具体是多少**，但我们知道它返回一个 `int`，而 `int` 可以和 `1` 相加再得到一个 `int`，我们把它赋给 `c`。

但是最后一行就出问题了：`hello2()` **什么也不返回**，所以等号 `=` 的右边相当于**什么也没有**……没什么东西可以赋值给 `d`，Java 就要犯迷糊了。

所以，如果方法没有返回值，我们就只能把它单独丢在一边了：

```java
hello2();
```

### 提交返回值

现在我们回到 `hello` 的里面，在这里，有一个 `return a + b;`。这是什么呀？

`return a + b;`  是**返回语句**，它代表：**我的返回值是** `a + b`。

我们已经在方法名的前面指定了方法的返回值**类型**，但类型毕竟只是个空壳，需要有一个实际的**值**来填满它。

`return` 正是做这件事的：它把方法的返回值设置为它右边**表达式**的值。

下面还有一些如何使用 `return` 的例子：

```java
int add(int a, int b) {
    return a + b;
}

int magic() {
    return (3 + 7) * 21; 
}

String ciallo() {
    return "Cia" + "llo" + "~";
}
```

Java 会先算出这些表达式的值，再把它们**返回**回去。

### 把它们都放在一起！

所以综合起来，**完整的**方法定义和调用看上去像是这样：

```java
int add(int a, int b) {
    return a + b;
}

int c = add(1, 2);
```

我们来捋一捋这一段代码的流程：

- `int add(int a, int b)` 这三行**定义**了一个方法 `add`：接受**两个参数**（都是 `int`），并且返回值的**类型**是 `int`。我们先跳过这三行（还记得吗，方法在定义时**不执行**）。
- 下一行是 `int c = add(1, 2)`，这是**赋值**，赋值是把等号 `=` 右边的值给左边的变量，右边的值是 `add(1, 2)`，这是**调用**方法 `add`：提供给它两个参数 `1` 和 `2`，并且期望从它那里得到一个值。

  - 由于要调用方法`add`，因此我们现在**进入**`add` 里面，把**参数对号入座**，`a` 是`1`，`b` 是`2`。
  - 下一行是`return a + b`，`return`**把返回值设成**它右边的值，它右边是`a + b`，算出来是`3`。
  - 方法到此结束了，于是我们带着刚刚算出来的返回值`3`，回到原来的地方。
- 现在我们知道，`add(1, 2)` 这个**表达式**的结果是刚才的**返回值** `3`，把它换进去，就得到 `int c = 3`，于是我们知道 `c` 最终是 `3`。

把上面的程序稍微扩展一下，你就可以得到这样的结果：

```java
int d = add(add(1, 2), 3);
```

这里有两个 `add` 方法，第一个 `add` 方法的**两个参数分别是** `add(1, 2)` 和 `3`，而第二个的参数就是 `1` 和 `2`。

`add(1, 2)` 这么**大个的东西**放在参数上好像有点奇怪，不过我们已经知道它不过是个**表达式**，而方法的**参数可以是表达式**，这么一想，也挺合理的。

按照上面的流程分析，我们马上知道 `add(1, 2)` 的值是 `3`，把 `3` 换进去得到 `add(3, 3)`，它的值是 `6`，所以 `d` 是 `6`。

再看一个：

```java
int e = 5;
e = add(e, e) * add(e, 1);
```

要注意一点，即使第二行要改变 `e` 的值，但直到右边的东西被算出来**之前**，`e` 的值都是**不变**的 —— 它还是 `5`，虽然只是，暂时的。

首先我们计算 `add(e, e)`，调用 `add` 方法，`a` 和 `b` 都代入 `e` 的值，也就是 `5`，所以表达式 `add(e, e)` 的值是 `10`。类似的，`add(e, 1)` 的值是 `6`。右边变成 `10 * 6` 就是 `60`，所以最终 `e` 被修改成 `60`。

## 恭喜……到目前为止。

从代码中的第一个数字开始，到表达式、变量、语句、方法和返回值，你已经历许多。这一节的内容很长，即使讲了一些故事，也难免枯燥。我在很多概念的解释上反复解释，花了很多笔墨，虽然不够简洁，但如果对于哪个概念不清楚的话，把我写的东西再仔细读一下，你应该能理解不少。

本节中所提到的内容，是后续用于构建包括类和对象在内更为复杂的系统所必需的，它们是组成庞大物件的微小原子，而即使是再为复杂的程序也是由基本的符号构成的。

Java 是一门很强大但学起来也不是那么简单的语言，虽然我尽可能压缩了用到的内容，省略了晦涩难懂的部分，但还是免不了长篇大论絮絮叨叨。如果你想找些额外的资料，这里有一些可以参考：

- [Java 教程](https://www.runoob.com/java/java-tutorial.html)，菜鸟教程出品的中文指南，有点老了但是很容易读。
- [Java Tutorial](https://www.w3schools.com/java/)，W3Schools 的英文教程，更全面但需要不错的英文水平。
