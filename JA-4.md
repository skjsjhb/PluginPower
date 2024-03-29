# JA-4 Java 面向对象（下）

## 非二元类型

### 是，还是不是？

两年前，当我还在编写 Alicorn 的时候，我们有过这样一个问题：**需要使用一个变量记录游戏是否在运行**。

如果是你，你会怎么实现？我们当中的**大多数人**都会选择这么做：

```java
boolean running = false;
```

游戏不是在运行，就是不在运行，这正好与 `boolean` 类型的特性很相似：要么是 `true`，要么是 `false`，没有其它可能。

然而，事情不总是一帆风顺的。

### 两种状态不太够用

用户很快就反馈，Alicorn 没有办法区分游戏到底是“**还没开始运行**”，还是“**游戏已经启动，但是崩溃了**”这两种情况。

我们需要把这些状态添加到程序中，这下，就有了**三种状态**：“运行中”、“未启动”，还有“已崩溃”。

`boolean` 不能满足我们的需要，我们得找到一种新的数据类型，它能表示**多于两种的状态**。

> **太多也不是什么好事**
>
> 有人（比如 Kirara）就要问了，难道不能使用 `int` 或者 `String` 吗？它们可以表示比两种更多的值，对不对？
>
> 使用 `int` 和 `String` 的问题在于，当我们赋值的时候，我们得**解释这个值的意思**。比如，如果我们写：
>
> ```java
> int running = 2;
> ```
>
> 也许你现在很清楚，`2` 就是“运行中”，但是，如果不加注释，除了写这行代码的人之外，没人看得懂它是什么意思。而且，人的记忆不太可靠，很快就连你自己都会忘掉它的意义。
>
> 同样的，如果我们用中文写：
>
> ```java
> String running = "运行中";
> ```
>
> 看上去好像清晰了一些，但是这也有问题 —— 来自其它国家的工程师就很难理解我们的意思。
>
> 此外，假如你不小心写错了代码：
>
> ```java
> String running = "运彳亍中";
> if (running == "运行中") {
>     // 这就永远不会执行！
> }
> ```
>
> 仅仅是因为打错了一个字，整个程序的逻辑就发生了变化。并且，由于字符串是很灵活的，这种错误或许要很久才能发现。
>
> 所以，并不是说 `int` 和 `String` 就不可以用来表示这些状态 —— 倒不如说，是因为它们太强大了，所以我们不太敢用它们，动漫里不也经常说，强大不总是好事嘛（笑）。

### 二生三，三生万物

为了解决这个问题，我们就可以使用 Java 中的**枚举（Enum）**，它可以用来表示“一些不同的状态”。

枚举是一种**特殊的类**，它不需要定义属性或者方法，**只需要定义它所有可能的取值**。

例如，如果我们想用一个枚举来表示星期几，我们可以这么写：

```java
enum Day {
    MON, TUE, WED, THU, FRI, SAT, SUN
}
```

一周只有七天，所以 `Day` 的值只能是 `MON`、`TUE`……`SUN` 中的一个，**没有其它可能**。

要给一个枚举类型的变量赋值，我们只需要这么写：

```java
Day today = Day.MON;
```

也就是说，要使用枚举的某个值（某种状态），只需要用 `枚举名.值` 的格式就可以了。

?> 枚举值（`MON`、`TUE` 等等）的名字通常用大写表示，这并非 Java 的要求，但软件工程们通常认为这样更能清晰地表示 `MON` 是一个值，而不是类型或者什么其它的东西。

下面我们再看一个 Minecraft 中的例子。

一把剑可以是木剑、石剑、铁剑、金剑、钻石剑或者下界合金剑，无外乎这六种材料之一，没有其它可能。所以，我们定义如下的枚举：

```java
enum SwordMaterial {
    WOODEN, STONE, IRON, GOLDEN, DIAMOND, NETHERITE
}
```

这样，如果我们想用一个变量来代表钻石剑的材质，我们就可以写：

```java
SwordMaterial mat = SwordMaterial.DIAMOND;
```

?> 枚举不是数字、逻辑或者字符串等类型的衍生物，它是一种**独立的类型**。

枚举为我们带来的最大好处，在于我们**只需要考虑几种情况之一**，不必费尽心思应对出乎意料的情况（比如年龄为 999 之类的）。除此之外，枚举的用法和数字、逻辑之类的值，没有什么不同。

## 把它写出来

请看下面的代码：

```java
int a = 123;
String b = "123";
```

你已经知道，`123` 和 `"123"` 是不一样的，一个是**数字**“一百二十三”，一个是**字符串**“一二三”。

如果现在我们想把一个数字转换成字符串，该怎么做呢？

你已经知道，要把一个字符串和另一个字符串比较，可以使用 `equals` 方法。既然已经知道了对象和方法的概念，那么你自然会问：

**数字类型的对象，有没有一个方法，可以把自身转换成字符串呢？**

这就是 `toString()` 方法。`toString()` 方法没有参数，它把数字按十进制写成字符串，然后把它返回回来。（注意，`toString` 本身并不把数字直接变成字符串 —— 对象的类型一旦确定，是**不可以改变**的。）

我们可以写出这样的代码：

```java
int a = 123;
if (a.toString() == "123") {
    // 这里会执行
}
```

`a.toString()` 被替换为 `toString` 方法的返回值，由于 `a` 是 `123`，因此这个方法返回十进制下的字符串 `"123"`，和右边比较，相等，所以 `if` 里面的东西会执行。

?> 当然了，我们之前还提到过，`字符串+数字` 这种写法，Java 会**先把数字转换成字符串**，再和字符串拼接到一起。因此如果想把数字转换到字符串，从简洁的角度来说，`"" + a`（一个空字符串拼上 `"123"`）也可以得到 `"123"`。但这不代表 `toString` 就没用了 —— 相反，Java 在“先把数字转换成字符串”的时候，**自动为我们调用了** `a.toString()`，因此，这种写法只能让代码简单一些，却并不是 `toString` 的替代品。

## 遗产回收计划

现在，想象你是 Mojang 的一位工程师，把时间倒退回 Minecraft 还在制作的早期，你们正在计划给游戏加上武器和食物系统。游戏里面已经有了各种各样的物品：木棍、木板、火把，甚至还有高*丛（高草丛）……为了描述这些物品，你的同事已经创建了许多许多类：

```java
class Stick {
    String name; // 物品名字
    Stick() {
        name = "木棍"; // 创建对象时，给物品默认的名字
    }   
}

class Planks {
    String name;
    Planks() {
        name = "木板";
    }   
}

class Torch {
    String name;
    Torch() {
        name = "火把";
    } 
}
```

这看上去确实没什么问题，当你把物品拿在手中时，或者在背包中把鼠标指针放在它上面时，物品的名称都会显示。所以，这里每个类型确实**都需要一个属性**来描述物品的名字。

但是，这么写有道理吗？我们会发现，单单是 `String name;` 这一行，我们就抄了好多回。Minecraft 里可有成百上千种物品呢，都这么写下去，不得人都给写没了！

也许，是时候再讲一个故事了。

> **高塔之下**
>
> 过去，在“光”上曾经发生了某种巨大的灾难。现在的六大岛之一，樱云岛的人类文明，本来不该延续下来 —— 刺骨的寒风，黄沙遍地，魔法元素互相反应，还有危险的猛兽和怪物……在自然面前，人类是很渺小的。
>
> 为求生存，也为求团结，人们作出了一个艰难的决定。王族用世代积聚的青金构筑成底座，猎龙者以龙的骨架撑起塔身，曾经镶在戒指上的彩石英被熔炼成水晶，而最古老的，也是最后一位纯血统的精灵，用自己的身躯点燃了烈火。就这样，一座座高塔在这片本该毁灭的小岛上立起。在古老魔法和精灵血脉的加持下，防御塔顶端的光球永不熄灭，不仅能照亮半个郡城的天空，也将来犯的外敌尽数烧为灰烬。七大郡城也废除了以前的区级划分，而以防御塔的名字命名地界。
>
> 然而，防御塔并不是万能的，也并不如想象那般强大。人们**不断修改着防御塔的图纸**，底座从青金换成了更坚固的光钻，外壳从飞崖石改为了更坚硬的能量护盾，伤害魔法从光束变成了更强大的火球，而在**偶然将一根代表生命的树芽插入塔身**后，再生魔法开始四散在周围的空气中，为这块不那么美好的小岛带来永恒的生机和希望。

如你所见，图纸在设计完成后，并不是就此封存，不再修改了。在上面这个故事里，当我们希望给防御塔添加一些新的功能的时候，我们**并不需要再从头画一张新的图纸**，而是“插一根树枝”或者“换掉某个配件”，就可以得到新的防御塔。

在 Java 中，这个概念也是类似的。一个类可以**基于**另一个类来定义，只需要在原本的类上**做一些修改**，而不需要再从头创建新的类型。

让我们回到原来的问题，我们希望给游戏加上武器和食物系统。但在此之前，武器、食物、火把……它们都是**物品**。我们希望首先创建“物品”这个类型来描述物品的**基本信息**（名字，数量……），再**基于**物品这个类，创建**具有独特属性**的“武器”类（伤害、耐久……）和“食物”类（饱食度、是否有毒……）。

这么说可能不太容易理解，我们直接看代码：

```java
class Item {
    String name; // 物品的名字
    int amount; // 物品的数量
}

class Sword extends Item {
    int damage; // 伤害
    int durability; // 剩余
}

class Food extends Item {
    int hunger; // 恢复饥饿
    boolean poisonous; // 是不是有毒
}
```

几乎和以前一样，我们**定义了三个类**，只不过，后面两个类的**类名**与类定义 `{}` 之间，多了一些东西：`extends Item`。

`extends` 的意思是“**扩展**”，`class A extends B` 的意思就是，定义类型 `A`，但是 `A` 除了包含**自己的**属性与方法，还**额外添加** `B` 的属性和方法。因为 `A` 是**在 `B` 的基础上“扩展”，“修改”而来的**，它具有 `B` 的全部内容，同时自己还添加一些。

像这样，一个类通过 `extends` 来“基于”另一个类进行定义，叫做类的**继承（Inheritance）**。`A extends B`，是指 `A` **继承** `B`。位于 `extends` 后的，被继承的类，是“基础”，所以叫做**基类（Base）**，也称**父类（Parent）**；而位于 `extends` 前的，正在进行定义的这个类，是由基类“衍生”，“派生”而来的，所以叫做**派生类（Derived）**，也叫**子类（Child）**。

我们来给 `Food` 加入一些方法，使得上面这个概念更加清晰：

```java
class Item {
    String name; // 物品的名字
    int amount; // 物品的数量
}

class Food extends Item {
    int hunger; // 恢复饥饿
    boolean poisonous; // 是不是有毒

    void eat() {
        sendMessage("你刚刚吃掉了" + name);
    }

    void sendMessage(String m) {
        // 把消息发送给玩家...
    }
}
```

我们省略了 `sendMessage` 的定义，你只需要知道：`sendMessage` 方法可以给玩家发送一条消息（显然，消息是字符串类型）。当然，这不是重点，请看 `eat` 方法的第二行，准确说，是后半段：

```java
"你刚刚吃掉了" + name
```

整个 `Food` 类里面可**都没有出现** `name` 这个属性！我们为什么能使用它呢？因为虽然 `Food` 中没有 `name`，但是 `Food` **继承了** `Item`（`class Food extends Item`），我们刚才说过，继承一个类，也就是相当于“获得”了它的所有属性和方法。我们发现，`Item` **类有属性** `name`（`String name`），而 `Food` 继承了 `Item`，**获得了这个属性**，所以现在 `Food` 类型中也拥有了 `name` 这个属性。

像这样继承而来的属性，虽然说有点特别，但是使用起来却和自身的属性是**没有什么区别**的。它们能在类型的方法中直接使用，也可以（在外部）通过 `对象.属性` 的方式来访问。

当然了，虽说上面的例子都是用属性来展示的，但**方法**的继承也和属性**完全相同**：派生类继承基类的方法，而且也同样可以在类型的方法中直接使用，或者（在外部）通过 `对象.方法(参数)` 的形式来调用。这里就不再单独举例说明了。

---

一个派生类是通过继承一个基类而产生的，**那么，这个基类本身能不能是继承其它的类而来的呢**？

答案是可以的，而且这件事并没有什么特别之处，请看下面的代码：

```java
class A1 {
    int a;
}

class A2 extends A1 {
    int b;
}

class A3 extends A2 {
    int c;
}
```

这里，`A3` 继承自 `A2`，而 `A2` 继承自 `A1`，因此：

- `A1` 只有一个属性 `a`。

- `A2` 拥有 `A1` 的属性 `a`，同时自己有一个属性 `b`，所以 `A2` 拥有属性 `a` 和 `b`。

- `A3` 拥有 `A2` 的属性 `a` 和 `b`，同时自己还有一个属性 `c`，所以 `A3` 拥有三个属性：`a`、`b` 和 `c`。

你会发现，这个过程没什么特殊之处 —— `extends` **仅仅是让左边的类拥有右边的类的属性和方法**，如果基类也有继承关系，那么先计算出基类拥有的属性和方法，再分析派生类就行了，并没有难以理解的陷阱或者是漏洞。

## 多级出厂设置

前面我们刚才提到了继承，知道**派生类可以获得基类的属性和方法**。似乎看上去没什么问题了……但是，有一个例外。这就是**构造方法**。

请看下面的代码：

```java
class Cup { // 基本的杯子
    double height;
    double radius;
    double volume;

    Cup (double h, double r) {
        height = h;
        radius = r;
        volume = 3.14 * r * r * h;
    }
}

class CupWithColor extends Cup { // 带颜色的杯子
    String color; // 增加了一个颜色属性

    CupWithColor() {
        // 这里应该写什么？
    }
}
```

如你所见，在编写派生类的构造方法的时候，我们遇到了一点小问题。

我们知道，`Cup` 类有构造方法，它需要进行一次“出厂设置”来给各个属性赋值，那么，在派生类 `CupWithColor` 中，我们显然不能跳过这个过程，如果我们只给 `color` 赋值，就会造出一个**只有颜色而没有高度和半径**的杯子 —— 这不太对！所以，请记住下面的规则：

**派生类的构造方法中，必须调用一次基类的构造方法。**

这件事情其实很好理解：派生类的构造方法完成**自己新增的那部分**属性的“出厂设置”，但基类也需要“出厂设置”，能做到这件事的是**基类的构造方法**。所以，需要在派生类的构造方法中**调用**基类的构造方法，才能确保这根继承关系链条上的每个类都被正确地进行“出厂设置”，而不会出现有颜色而没有大小的杯子，或者其它奇奇怪怪的错误。

为了做到这一点，我们会写出这样的代码：

```java
class Cup { // 基本的杯子
    double height;
    double radius;
    double volume;

    Cup(double h, double r) {
        height = h;
        radius = r;
        volume = 3.14 * r * r * h;
    }
}

class CupWithColor extends Cup { // 带颜色的杯子
    String color; // 增加了一个颜色属性

    CupWithColor(String c, double h, double r) {
        super(h, r);
        color = c;
    }
}
```

这里出现了一个比较特别的东西：`super(h, r)`。这个 `super`，其实就是指代**基类的构造方法**（`Cup(double h, double r)`）。

> Kirara：为什么不能直接写 `Cup(h, r)` 呢？

因为，构造方法**并不是普通的方法**，它们不能像一般的方法一样直接进行调用（`Cup(h, r)`），但是在这里你也不能搭配 `new` 来使用，因为这么做代表“**在构造方法的内部，再新建一个对象**”，可我们真正想做的，是把这个基类的构造方法，在**自己身上**调用一次，来执行所谓的“出厂设置”，而不是再弄出一个新的对象。

为了解决这个问题，就只能使用这样一个看起来怪怪的语法了。请记住：**在派生类的构造方法中，`super` 代表其基类的构造方法，可以通过 `super(参数)` 的形式调用**。

## 另一种可能

我们的 Saki 从刚才开始好像就一直有话想说。

> Saki：如果 `A` 继承了 `B`，但是 `A` 自己有个方法和 `B` 中的方法名字相同怎么办？

她指的是这种情况：

```java
class C1 {
    void foo() {
        // ...
    }
}

class C2 {
    void foo(int a) {
        // ...
    }
}
```

这其实无关紧要，因为 `C2` 从 `C1` 那里得到一个方法 `void foo()`，而它自己有一个方法 `void foo(int a)`，我们在两节之前就讲过，即使**方法名相同**也不必慌张，只要**参数不完全相同**，使用方法的时候 Java 就**能分清**该调用哪一个。

好啦，问题解决了，现在我们可以洗洗睡……哇！别生气别生气，我承认我是在糊弄你（笑）。

我们真正想解决的是这样一个问题：

```java
class C1 {
    void foo() {
        // ...
    }
}

class C2 {
    void foo() {
        // ...
    }
}
```

现在，这两个方法长得就完全一样了（都是 `void foo()`），Java 肯定分不清哪个是哪个了，对吧？这样做，会带来什么问题呢？

如果在派生类中定义了与基类中**同名且同参数**的方法，则这个方法被**重载（Override）**，使得所有**实际类型**为该派生类的对象，只要调用这个同名方法，就会调用到派生类中的**新方法**（而不是基类中的老版本）。

具体而言，就是说：

```java
C1 a = new C1();
a.foo(); // 调用的是第一个，这里没有牵扯到 C2

C2 b = new C2();
b.foo(); // 调用的是第二个，C2 中的 foo 方法覆盖了 C1 中的
```

在上面的例子中，`C2` 中的 `void foo()` 会在所有类型为 `C2` 的对象中，**覆盖掉** `C1` 中的 `void foo()` 方法。`a` 的类型是 `C1`，所以 `a.foo()` 调用的是 `C1` 中的版本，而 `b` 的类型是 `C2`，就调用了 `C2` 中的版本。

---

然而，问题并没有到此解决，最麻烦的事情是下面这样：

```java
C1 a = new C2();
a.foo(); // 调用哪一个？
```

你是不是已经糊涂了？为什么我们可以**把一个类型为 `C2` 的对象（`new C2()`），赋给一个类型为 `C1` 的变量**呢？这不是类型错误吗？

要回答这个问题，我们必须追溯“**继承**”这个词的原本意义。在这里，`C2` 是一个 `C1`。

……好吧，也许用代号还是不太直观，我们还是用 Minecraft 举例子。假设有这样的代码：

```java
class Item {
    // ...
}

class Sword extends Item {
    // ...
}
```

`Sword` 类继承自 `Item`，但是如果一个对象是 `Sword`，它肯定**是一种** `Item` —— **剑是物品的一种**，尽管它比物品描述得**更具体**，但它确实也**是一个物品**（如果不是，那它是方块？）。所以，我们可以把剑**看作是一个普通物品**，尽管在这个过程中，我们**丢失了一些细节** —— 独属于剑的那部分属性，但我们仍然可以使用属于“物品”这个类的所有属性和方法。

所以，当我们这么写：

```java
Item i = new Sword();
```

我们是在告诉 Java：**把这个类型为 `Sword` 的对象，当作是一个 `Item` 来记录**。以后，在使用变量 `i` 时，我们只能使用 `Item` 中定义的属性和方法，而无法访问 `Sword` 中**额外定义**的部分。

> **到底怎么回事？**
>
> 你可能会觉得，这么做不是自找麻烦嘛，本来一把剑可以攻击敌人，现在当作是物品，就不能攻击敌人了，做出来了东西，最后又把它剪掉，不是白做了吗？其实不然，有时候我们需要**牺牲这些具体性来换取共通性**，请看下面的案例：
>
> ```java
> void showItemName(Item i) {
>     String message = "物品的名字是：" + i.name;
>     // 把这个 message 显示出来...
> }
> ```
>
> 如果我们不把 `Sword` 转换成 `Item`，我们就必须为 `Sword` 再定义一个这样的方法，类似的还有木棍、木板、矿石……就因为不愿舍弃那一点细节（即使压根没用到），而其实我们**真正用到的**，不过只是 `Item` 类型中的 `name` 属性而已。
>
> 为了减少这些不必要的工作量，Java 就允许把派生类当作基类来直接使用。所以，如果你只用到 `name` 属性，就选择 `Item`，如果需要剑的一些**特别的**属性和方法，才使用 `Sword`。

现在回到刚才的问题：

```java
C1 a = new C2();
a.foo();
```

我们知道，`foo` 方法存在于类 `C1` 上，所以即使损失了一些细节，我们还是可以使用 `a.foo()`，问题在于，这个 `foo` 到底是 `C1` 中的 `foo`，还是 `C2` 中的 `foo`？

答案是**后者**。因为，对象调用哪个方法，是按照它的**实际类型**（而不是声称的类型）进行的。虽然我们这里让 Java 把 `a` 看作 `C1`，但是，`a` **是用 `C2` 的构造方法创建的**，被人**叫做**丑小鸭并不改变它**是**天鹅的事实 —— `a` 所包含的方法来自于 `C2`，所以调用 `foo` 的时候，将调用到 `C2` 中提供的方法。

这个机制被称作**多态**。指的是派生类的同名同参数方法可以拥有与基类不同的行为。如你所见，我们花了相当一部分篇幅来介绍这个机制，既然这么麻烦，为什么还要有多态呢？请看下面的“到底怎么回事”中的一个例子。

> **到底怎么回事？**
>
> 你已经知道可以用 `equals` 来比较字符串：
>
> ```java
> String a = "Ciallo～(∠・ω< )⌒☆";
> if(a.equals("123")) {
>     // 不会执行
> }
> ```
>
> 在 Java 中，其实所有的对象都有一个隐藏的基类，叫做 `Object`。这个类主要是包含了一些 Java 用于处理对象时需要的基本信息，而在 `Object` 中，也同样定义了 `equals` 方法：
>
> ```java
> boolean equals(Object another);
> ```
>
> `equals` 方法是 Java 用于比较两个对象的**内容是否相等**的方法（不能直接使用 `==`），问题在于，**不同的类型有不同的比较方式**：数字可以直接做减法，而字符串需要逐个比较第一个、第二个、第三个……每个字符。因此，`equals` 方法不能由 `Object` 来定义，而需要**各个类型自己定义**。而 `equals` 又必须存在在 `Object` 类型上 —— Java 要利用它来进行诸如排序、插入等操作时所必需的**相等比较**。换而言之，Java 规定了 `equals` **可以用来**判断对象是否相同，但却没规定**具体如何**来判断，这是留给各个类型自行决定的。
>
> 你会发现这样就很方便 —— 我们不用管两个 `Object` 到底实际上是什么类型，只需要知道如果 `equals` 返回 `true` 就代表两个对象相同。即使我们把所有的对象都当作 `Object`，在调用 `equals` 方法时，多态也会确保我们调用到正确的方法（类型**实际的** `equals` 方法）来进行比较。

顺便一提，**属性没有这样的能力**，所以不要在派生类中定义和基类相同的属性 —— 虽然 Java 不会给出任何错误，但执行的结果非常混乱，估计不会是你想要的。

## 把它藏起来

作为 Java 理论知识的最后一部分，我们来介绍访问修饰符。

```java
class Cup {
    double height;
    double radius;
    Cup(double h, double r) {
        height = h;
        radius = r;
    }
}
```

当我们创建了 `Cup` 的对象之后，我们就可以访问 `height` 和 `radius` 属性：

```java
Cup c = new Cup(5, 2);
c.height = 10; // 把高度改成 10
```

这看上去没什么问题，不过，杯子的大小，一般是出厂之后就不再改动的。或者即使改动，一般也是返厂修改，而不是让客户自己动手。在 Java 中，我们也会有类似的需求：如果我们**不希望 `height` 和 `radius` 被其它代码访问到，而只能在类定义的里面使用**，该怎么做呢？

我们只需要把代码改成这样：

```java
class Cup {
    protected double height;
    protected double radius;
    Cup(double h, double r) {
        height = h;
        radius = r;
    }
}
```

我们不过是在属性的前面加上了前缀 `protected`，这是一个**访问修饰符（Access Modifier）**，它决定外部代码能不能使用指定的变量和属性，以及如果能，具体哪些代码可以使用，哪些不可以。

访问修饰符能用于属性、方法，还有类型本身。它们有四种：

- `public` **公开**：只要 Java 能找到，任何地方的任何代码都可以使用，不受任何制约。

- `protected` **保护**：仅允许同一个**包**内的代码，自己，以及所有派生类使用，不允许其它代码访问。

- `package-private` **包内私有**：仅允许同一个包内的代码和自己使用，不允许其它代码访问（包括派生类）。

- `private` **私有**：仅允许类型自己访问。

其中，`public`、`protected` 和 `private` 都需要**手动注明**在属性和方法的**前面**，而如果不加任何注明，默认情况下就是 `package-private`。

在 Java 中，把一系列类收集起来的概念叫做**包（Package）**，让我们先介绍两个新事实：

- 在 Java 中，大多数公开的类是单独写在一个（硬盘上的）文件中的，**一个类一个文件**，而且**类名和文件名**相同。如果一个类型叫做 `Cup`，它就应该写在名为 `Cup.java` 的文件中。

- 可以把一系列类收集到一个**包**中，在硬盘上也就是把一组 `.java` 文件放进一个**文件夹**里。同一个包内的类比不同包的类要更加“亲近”一些，可以使用彼此 `package-private` 的方法。

也就是说，如果要把 `Cup` 正式地变成一个可以在任何地方使用的类，我们需要把它写在名为 `Cup.java` 的文件中，并且内容应该是：

```java
public class Cup {
    protected double height;
    protected double radius;

    public Cup(double h, double r) {
        height = h;
        radius = r;
    }
}
```

我们让 `Cup` 这个类变成了公开的（`public class Cup`），是因为我们希望不止 `Cup` 自己和它的包能使用，我们希望**任何代码**都可以用到我们设计的 `Cup` 类型。**除非有特殊的理由，否则通常情况下，我们都把类定义为公开的。**

在属性上使用 `protected` 是因为，我们不希望**其它代码直接触及**这两个属性，但我们希望**派生类也能使用**高度和半径这些属性（总不能让一个有图案的杯子没有高度吧）。而在构造方法上使用 `public` 是因为，`Cup` 类型**自身已经是公开的**了，如果其它代码想要使用 `Cup`，通常需要创建一个 `Cup` 类型的对象，而如果构造方法不是公开的，这样的写法就有可能出错：

```java
Cup c = new Cup();
```

如果 `Cup` 的构造方法前面没有前缀（也就是包内私有 `package-private`），而且这行代码和 `Cup` **不在同一个包里**，那么这段代码就**无法执行**，这并不是我们想要的。我们希望任何人都可以通过 `Cup` 直接做出一个杯子，所以，我们把构造方法设置成 `public`，告诉其它的类，“这是公开的，请随便用吧”。

?> 当然，具体哪些方法和属性是公开的，哪些是保护的，而哪些又是私有的，需要**根据实际问题来判断选择**，不能简单地一概而论。例如，假设我就是想要垄断整个杯子行业，我就把构造方法设置成 `private` 的，这样就只有我可以制造杯子啦，哈哈。

## 恭喜！

至此，你已经掌握了 Minecraft 插件开发所必备的，最为基础的 Java 理论知识。我们在这四节中仅仅是非常简要地概述了一下这些基本概念。Java 其实是一门大有学问的语言，单单有关 Java 的内容就可以写上好几本书，远非我们能在短短的几个章节内就讲明白的。不过，当读者了解了对象和类的概念后，就已经基本具备了编写插件**所需的编程知识**，剩下的不过是一些需要经验来处理的细节，而这些细节，我们希望能够在后续的几个项目的练习中，逐渐地磨合、调整，最终让读者能形成一套自己的思维方法。

从下一章开始，我们将开始介绍插件开发中的各种细节，所以如果你已经确信自己对于类和对象都了解得七七八八了，那我们就正式开始我们的旅程吧！
