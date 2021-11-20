## 1.1、变量

> 变量保存的数据可以在需要时设置，更新或提取。赋值给变量的值都有对应的类型。JavaScript的类型有**数**、**字符串**、**布尔值**、**函数**、**对象**，还有**undefined**和**null**，以及**数组**、**日期**和**正则表达式**

### 变量作用域
> 作用域是指，在编写的算法函数中，我们能访问变量（在使用函数作用域时，也可以是一个函数）的地方。有**局部变量**和**全局变量**两种。

### 全局变量

``` JavaScript
var a = 'global';
console.log(a);   //global
function test(){
    console.log(a);   
}

test(); //global
```
### 局部变量



``` JavaScript
function test(){
    var a = 1;
    console.log(a)  // 1
}
console.log(a); // 报错
test();
console.log(a); // 报错
```

例子：
``` JavaScript
var myVariable = 'global';
myOtherVariable = 'global';

function myFunction(){
    var myVariable = 'local';
    return myVariable;
}

function myOtherFunction(){
    myOtherVariable = 'local';
    return myOtherVariable;
}

console.log(myVariable); // 输出 global,因为它是一个全局变量
console.log(myFunction()); //输出 local,因为myVariable是在myFunction函数中声明的局部变量，所以作用域仅在myFunction

console.log(myOtherVariable); //输出 global,这里引用的是初始化的全局变量myOtherVariable
console.log(myOtherFunction()); //输出 local,在myOtherFunction里，因为没有使用var 关键字修饰，所以这里引用的是全局变量myOtherVariable，并将其复制为local
console.log(myOtherVariable); //输出 local 因为在myOtherFunction里修改了myOtherVariable的值
```

## 1.2运算符

### 算数运算符

| 运算符 | 描述 |
| ------ | ---- |
| +      | 加法 |
| -      | 减法 |
| *      | 乘法 |
| /      | 除法 |
| %      | 系数 |
| ++     | 递加 |
| --     | 递减 |

### 赋值运算符
| 运算符 | 描述                            |
| ------ | ------------------------------- |
| =      | 赋值                            |
| +=     | 加赋值(x += y) == (x = x + y)   |
| -=     | 减赋值(x -= y) == (x = x - y)   |
| *=     | 乘赋值(x *= y) == (x = x * y)   |
| /=     | 除赋值(x /= y) == (x = x / y)   |
| %=     | 取余赋值(x %= y) == (x = x % y) |

### 比较运算符
| 运算符 | 描述           |
| ------ | -------------- |
| 运算符 | 描述           |
| ==     | 等于           |
| ===    | 等值等型       |
| !=     | 不相等         |
| !==    | 不等值或不等型 |
>|大于
><|小于
>=|大于或等于
><=|小于或等于
>?|三元运算符

### 逻辑运算符
| 运算符 | 描述   |
| ------ | ------ |
| &&     | 逻辑与 |
| \|\|   | 逻辑或 |
| !      | 逻辑非 |


### 位运算符
| 运算符 | 描述         | 例子   | 等同于      | 结果         | 十进制 |
| ------ | ------------ | ------ | ----------- | ------------ | ------ |
| &      | 与           | 5 & 1  | 0101 & 0001 | 0001         | 1      |
| \|     | 或           | 5      | 1           | 0101 \| 0001 | 0101   |
| ~      | 非           | ~ 5    | ~0101       | 1010         | 10     |
| ^      | 异或         | 5 ^ 1  | 0101 ^ 0001 | 0100         | 4      |
| <<     | 零填充左位移 | 5 << 1 | 0101 << 1   | 1010         | 10     |
>>|有符号右位移|	5 >> 1|0101 >> 1|0010|2
>>
>>>|零填充右位移|5 >>> 1|0101 >>> 1|0010|2


### 类型运算符
| 运算符     | 描述                                  |
| ---------- | ------------------------------------- |
| typeof     | 返回变量的类型。                      |
| instanceof | 返回 true，如果对象是对象类型的实例。 |

## 1.3 真值和假值



> 在JavaScript中，true和false有些复杂。在大多数编程语言中，布尔值true和false仅仅表示true/false结果。在JavaScript中，如abc这样的字符，也可以看作true。

| 数值类型  | 转换成布尔值                              |
| --------- | ----------------------------------------- |
| undefined | false                                     |
| null      | false                                     |
| 布尔值    | true是true，false是false                  |
| 数        | +0，-0和NaN都是false，其它都是true        |
| 字符串    | 如果字符串长度为零就是false，其它都是true |
| 对象      | true                                      |

让我们用代码来验证上面的总结。
``` JavaScript
function demo(val){
    return val ? console.log('true') : console.log('false');
}

demo(true); // true
demo(false); // false
demo(new Boolean(false)); // true   (因为对象始终是true)

demo(''); // false  (因为长度为零的字符串为false)
demo('false'); // true (因为长度大于零的字符串都为true)
demo(new String('')); // true   (因为对象始终是true)

demo(1);    // true
demo(-1);   // true
demo(NaN);  //false
demo(new Number(NaN));// true   (因为对象始终是true)

demo({}); // true   (因为对象始终是true)

var obj = { name : '张三' };
demo(obj); // true
demo(obj.name); // true
demo(obj.sex);  // false (sex属性不存在为undefined)
```

这两个相等运算符的使用可能会引起一些困惑。
我们来分析一下两者不同

## 1.4 相等运算符(==和===)

**“==” 的比较规则**

1. 先检查两个操作数的数据类型是否相同
2. 如果相同，则比较两个数是否相等
3. 如果不同，则先将两个数转换为相同数据类型，再进行比较

我们用表格来分析一下不同类型的值用相等运算符比较后的结果：
| 类型(x)    | 类型(y)    | 结果                |
| ---------- | ---------- | ------------------- |
| null       | undefined  | true                |
| undefined  | null       | true                |
| 数         | 字符串     | x == toNumber(y)    |
| 字符串     | 数         | toNumber(x) == y    |
| 布尔值     | 任何类型   | toNumber(x) == y    |
| 任何类型   | 布尔值     | x == toNumber(y)    |
| 字符串或数 | 对象       | x == toPrimitive(y) |
| 对象       | 字符串或数 | toPrimitive(x) == y |

- 如果两个操作数都是对象，则仅当两个操作数都引用同一个对象时才返回true。
- 如果一个操作数是null，另一个操作数是undefined，则返回true。
- 如果两个操作数是不同类型的，就会尝试在比较之前将它们转换为相同类型：
  - 当数字与字符串进行比较时，会尝试将字符串转换为数字值。
  - 如果操作数之一是Boolean，则将布尔操作数转换为1或0。
  - 如果操作数之一是对象，另一个是数字或字符串，会尝试使用对象的valueOf()和toString()方法将对象转换为原始值。
- 如果操作数具有相同的类型，则将它们进行如下比较：
  - String：true仅当两个操作数具有相同顺序的相同字符时才返回。
  - Number：true仅当两个操作数具有相同的值时才返回。+0并被-0视为相同的值。如果任一操作数为NaN，则返回false。
  - Boolean：true仅当操作数为两个true或两个false时才返回true。

toNumber 和 toPrimitive 方法是内部的，并根据以下表格对其估值

**toNumber** 方法对不同类型返回的结果如下：
| 值类型    | 结果                                   |
| --------- | -------------------------------------- |
| undefined | NaN                                    |
| null      | +0                                     |
| 布尔值    | 如果是true，返回1；如果是false，返回+0 |
| 数        | 数对应的值                             |

**toPrimitive** 方法对不同类型返回的结果如下：
| 值类型 | 结果                                                         |
| ------ | ------------------------------------------------------------ |
| 对象   | 如果对象的valueOf方法的结果是返回原始值，返回原始值；如果对象的toString方法返回原始值，就返回这个值；其它情况都返回一个错误 |

我们可以用例子来验证一下：

**例子1：**
``` JavaScript
console.log('demo' == true); // false
```
首先，布尔值会被 **toNumber** 方法转成数 ，因此得到：demo == 1。
其次，用toNumber 转换字符串值。因为字符串包含字母，所以会被转成NaN，表达式编程了 NaN == 1，结果就是false

**例子2**
``` JavaScript
console.log('demo' == false); // false
```
首先，布尔值会被 **toNumber** 方法转成数 ，因此得到：demo == 0。
其次，用toNumber 转换字符串值。因为字符串包含字母，所以会被转成NaN，表达式编程了 NaN == 0，结果就是false

**“===”的比较规则**

1. 先检查两个操作数的数据类型是否相同
2. 若不同，直接返回false
3. 若相同，则比较二者是否相等

我们可以用以下表格分析。
| 类型(x) | 类型(y)                   | 结果 |
| ------- | ------------------------- | ---- |
| 数      | x和y的值相同（但不是NaN） | true |
| 字符串  | x和y是相同字符            | true |
| 布尔值  | x和y都是true或false       | true |
| 对象    | x和y引用同一个对象        | true |

让我们用代码来验证一下：
``` JavaScript
console.log('张三' === true); // false (两者类型不相同)
console.log('张三' === '张三') // true

var person1 = { name : '张三' };
var person2 = { name : '张三' };

console.log(person1 === person2) // false (两者引用的是不同对象)
```

## 1.5 条件语句

> 条件语句用于基于不同条件执行不同的动作。

在您写代码时，经常会需要基于不同判断执行不同的动作。
您可以在代码中使用条件语句来实现这一点。
在 JavaScript 中，我们可使用如下条件语句
- 使用 **if** 来规定要执行的代码块，如果指定条件为 true
- 使用 **else** 来规定要执行的代码块，如果相同的条件为 false
- 使用 **else if** 来规定要测试的新条件，如果第一个条件为 false
- 使用 **switch** 来规定多个被执行的备选代码块

### if 语句

如果想让一个脚本在仅当条件是true时执行，可以使用if语句
语法:
``` JavaScript
if (条件) {
    //如果条件为 true 时执行的代码
} 
```
示例：
``` JavaScript
var num = 1;
if(num === 1){
    console.log('num 真的等于 1');
}
```
输出
``` 
num 真的等于 1
```

### else 语句



如果想在条件为true的时候执行脚本A，在条件为false的时候执行脚本B可以使用if...else语句。

语法：
``` JavaScript
if (条件) {
    // 脚本A，条件为 true 时执行的代码块
} else {
    // 脚本B，条件为 false 时执行的代码块
}
```
示例：
``` JavaScript
var elseVariable = 0;
if(elseVariable === 1){
    console.log('elseVariable 等于 1');
}else{
    console.log('elseVariable 不等于 1');
}
```
输出 
``` language
elseVariable 不等于 1
```

也可以使用三元运算符：
``` JavaScript
var elseVariable = 0;
elseVariable === 1 ? console.log('elseVariable 等于 1') : console.log('elseVariable 不等于 1');
```

### else if 语句



如果我们有多个脚本，可以多次使用if...else，根据不同条件执行不同的语句

语法：
``` 
if (条件 1) {
    条件 1 为 true 时执行的代码块
} else if (条件 2) {
    条件 1 为 false 而条件 2 为 true 时执行的代码块
 } else {
    条件 1 和条件 2 同时为 false 时执行的代码块
}
```
示例：
``` JavaScript
var month = 5;
if (month === 1){
    console.log('一月');
}else if (month === 2){
    console.log('二月');
}else if (month === 3){
    console.log('三月')
}else {
    console.log('月份不是一月，也不是二月或三月');
}
```
输出：
``` 
月份不是一月，也不是二月或三月
```

### switch
如果要判断的条件和上面的elseif一样，还可以使用switch语句

语法：
``` 
switch(表达式) {
     case n:
        代码块
        break;
     case n:
        代码块
        break;
     default:
        默认代码块
}
```
代码解释：
- 计算一次 switch 表达式
- 把表达式的值与每个 case 的值进行对比
- 如果存在匹配，则执行关联代码

示例：
``` JavaScript
var month = 5;
switch (month) {
    case 1:
        console.log('一月');
        break;
    case 2:
        console.log('二月');
        break;
    case 3:
        console.log('三月')
        break;
    default:
        console.log('月份不是一月，也不是二月或三月');
}
```
输出：
``` 
月份不是一月，也不是二月或三月
```

## 1.6 循环 

假如您需要运行代码多次，且每次使用不同的值，那么循环（loop）相当方便使用。
通常我们会遇到使用数组的例子：
不需要这样写：
``` JavaScript
var arr = ['张三','李四','王五','赵六','杨七'];
console.log(arr[0]);
console.log(arr[1]);
console.log(arr[2]);
console.log(arr[3]);
console.log(arr[4]);
```
可以使用for循环：
``` JavaScript
var arr = ['张三','李四','王五','赵六','杨七'];
for(let i = 0;i < arr.length;i++){
    console.log(arr[i]);
}
```

### 不同类型的循环
- **for** - 循环代码块一定的次数
- **for/in** - 循环遍历对象的属性
- **while** - 当指定的条件为 true 时循环指定的代码块
- **do/while** - 同样当指定的条件为 true 时循环指定的代码块

### for 循环

语法：
``` 
for (语句 1; 语句 2; 语句 3)
{
    被执行的代码块
}
```
代码解释：
**语句 1** （代码块）开始前执行
**语句 2** 定义运行循环（代码块）的条件
**语句 3** 在循环（代码块）已被执行之后执行

示例：
打印小于10的正整数：
``` JavaScript
for(let i = 1;i < 10;i++){
    console.log(i);
}
```

### for/in 循环
用for/in 语句遍历对象的属性
语法：
```
for(声明变量（即遍历数组的键名） in 数组){
   访问元素：数组[键名]
}
```
示例：
``` JavaScript
var studentScore = {chinese: 90, math: 93, english: 88};
for (let subject in studentScore){
    console.log(subject + '分数为：' + studentScore[subject]);
}
```
输出：
``` 
chinese分数为：90
math分数为：93
english分数为：88
```

### While 循环
while 循环会在指定条件为真时循环执行代码块。
语法:
``` 
while (条件) {
    要执行的代码块
}
```
示例：
打印小于10的正整数：
``` JavaScript
var num = 1;
while (num < 10){
    console.log(num);
    num++;
}
```

### do/while 循环

do/while 循环是 while 循环的变体。该循环会在检查条件是否为真之前执行一次代码块，然后如果条件为真的话，就会重复这个循环。
语法：
``` 
do
{
    需要执行的代码
}
while (条件);
```
示例：
打印小于10的正整数：
``` JavaScript
do {
    console.log(num);
    num++;
}while (num < 10);
```

### while与do...while的区别：

**while**
先判断条件是否满足，如果满足就执行循环体内的语句，执行完毕后再回来判断条件是否满足，如此无限重复；直到条件不满足时，执行while循环后边的语句。简单来讲就是说**while循环是先判断后循环**
**do...while**
与while循环的不同在于:它先执行循环中的语句,然后再判断表达式是否为真, 如果为真则继续循环；如果为假, 则终止循环。因此, do...while循环至少要执行一次循环语句。 简单来讲就是说**while循环是先循环后判断** 。


### break 和 continue 语句
>**break** 语句用于跳出循环。
>**continue** 用于跳过循环中的一个迭代。

### break 语句
break 语句可用于跳出循环。
break 语句跳出循环后，会继续执行该循环之后的代码（如果有的话）。
break 语句（不带标签引用），只能用在循环或 switch 中。

### continue 语句
continue 语句中断循环中的迭代，如果出现了指定的条件，然后继续循环中的下一个迭代。
continue 语句（带有或不带标签引用）只能用在循环中。



## 1.7 函数 

函数是由事件驱动的或者当它被调用时执行的可重复使用的代码块。JavaScript函数语法,函数就是包裹在花括号中的代码块，前面使用了关键词 function： 当调用该函数时，会执行函数内的代码。可以在某事件发生时直接调用函数（比如当用户点击按钮时），并且可由 JavaScript 在任何位置进行调用。

### 函数的声明

1. **定义式**
``` JavaScript
fun(); // this is a function.
function fun() {
    console.log('this is a function.')
}
fun(); // this is a function.
```
2. **变量式**
``` JavaScript
demo(); // 报错：demo is not a function
var demo = function () {
    console.log('this is a function.')
}
```
为什么这里在声明前调用会报错 **demo is not a function** 呢？而上面定义式的fun();又能在之前调用？
**javascript并不是严格的自上而下执行的语言** 。JavaScript有个东西叫**变量提升（hoisting）**，它会将当前作用域的所有变量的声明提升到程序的顶部。
``` JavaScript
num = 1;

console.log(num);
var num;
```
等价于
``` JavaScript
var num;
num = 1;

console.log(num);
```

那我们再来看一个例子：
``` JavaScript
console.log(num);  // undefined
var num = 1;
```

那为什么这里会打印 undefined 呢？原因为 JavaScript会将变量的声明提升到顶部，可是赋值语句并不会提升。
所以上面demo()函数的声明，变量demo会被提升到顶部，但是变量的值并没有提升,所以变量式声明函数时，函数的调用应该在该表达式的后面:
``` JavaScript
var demo = function () {
    console.log('this is a function.')
}
demo(); // this is a function.
```

我们再来说一个题外话：
``` JavaScript
fun();
function fun(){
    console.log('this is a function.');
}
var fun = 2;
```
你觉得上面会报**fun is not a function**吗？不，其实它会输出 this is a function. 当函数声明与其他声明一起出现的时候，是以谁为准呢？答案就是，**函数声明高于一切**。

### 构造器式
``` JavaScript
let constructor = new Function('name','age',"console.log(name + '的年龄为' + age);")
constructor('张三',18); // 张三的年龄为18
```

### 函数的返回值
当 JavaScript 到达 return 语句，函数将停止执行。
如果函数被某条语句调用，JavaScript 将在调用语句之后“返回”执行代码。
> 在JavaScript中不管我们指没指定函数的返回值,函数都会返回一个值
> 指定返回值 -> 返回指定的值
> 未指定返回值 -> 返回undefined

我们来用代码来展示效果：
``` JavaScript
var fun1 = function () {
    return '返回一个字符串';
}

var fun2 = function () {

}

console.log(fun1()); // 打印：返回一个字符串
console.log(fun2()); // undefined
```


### 为何使用函数？

您能够对代码进行复用：只要定义一次代码，就可以多次使用它。
您能够多次向同一函数传递不同的参数，以产生不同的结果。

## 1.8 面向对象

什么是类？什么是对象？

**类是一个抽象的概念，是对某一类事物的抽象。** 我们举个例子，人类可以看作一个类，这个类的共性有：第一、站立行走，第二、有一个很发达的大脑，上面这两点都是静态的，描述的是客观的属性(attributes)。人类还需要吃饭、需要睡觉，上面这两点都是动态的行为，即方法(methods)。类可以包含函数，函数在类中就是动态的行为，即方法。

**对象就是类的实例化**。人类是一个类，而每一个人就是人类的实例化，即每一个人就是一个对象，对象具有类的属性及方法（每个人都站立行走、有一个发达的大脑，并且需要吃饭睡觉）。

### JavaScript中类的声明

### 1. 普通声明，基于已有对象扩充其属性和方法

``` JavaScript
var obj = new Object();
obj.name = '张三';
obj.age = '18';
obj.run = function(){
    console.log(this.name + '开始奔跑');
}
obj.run(); // 张三开始奔跑
```
这种方式的弊端：这种对象的可复用性不强，如果需要使用多个对象，还需要重新扩展其属性和方法。

### 2. 键值对声明
``` JavaScript
var obj = {
    name : '张三',
    age : 18,
    run : function () {
        console.log(this.name + '开始奔跑');
    }
};

obj.run(); // 张三开始奔跑
```
可以看得到，键值对中的键就是对象的属性，值就是对应属性的值

### 3. 构造函数方式

``` JavaScript
function Person() {
    this.name = '张三';
    this.age = 18;

    this.run = function () {
        console.log(this.name + '开始奔跑');
    }

    console.log(this.name + '的年龄为' + this.age);
}


//实例化对象：
var person = new Person();  // 张三的年龄为18
person.run(); // 张三开始奔跑
```

### 4. 原型(“prototype”)方式
``` JavaScript
function Person() {

}

Person.prototype.name = '张三';
Person.prototype.age = 18;
Person.prototype.run = function () {
    console.log(this.name + '开始奔跑');
}

var person = new Person();  
person.run(); // 张三的年龄为18
```
使用原型存在的缺点：
1. 不能传参数；
2. 有可能会导致程序错误。如果使用原型方式来定义对象，那么生成的所有对象会共享原型中的属性，这样一个对象改变了该属性也会反映到其他对象当中。单纯使用原型方式定义对象无法在构造函数中为属性赋初值，只能在对象生成后再去改变属性值。


### 继承
创建一个或多个类的专门版本类方式称为继承（Javascript只支持单继承）。 创建的专门版本的类通常叫做子类，另外的类通常叫做父类。 在Javascript中，继承通过赋予子类一个父类的实例并专门化子类来实现。

让我们来看一下例子。
我们定义了 Student类作为 Person类的子类. 之后我们重定义了sayHello() 方法并添加了 squat() 方法
``` JavaScript
function Person(name) {
    this.name = name;
    this.sayHello = function () {
        console.log('我的名字叫' + name);
    }

    this.run = function () {
        console.log(name + '开始奔跑');
    }
}

// 定义学生类
function Student(name,age) {
    // 调用父类构造器, 确保(使用Function#call)"this" 在调用过程中设置正确
    Person.call(this,name);
    //初始化学生年龄
    this.age = age;

    /**
     * 更换Person类的sayHello方法
     */
    this.sayHello = function () {
        console.log('我的名字叫' + name + ',今年' + age + '岁')
    }
    this.squat = function () {
        console.log('蹲下来')
    }

}
// 建立一个由Person.prototype继承而来的Student.prototype对象
Student.prototype = Object.create(Person.prototype);
// 设置"constructor" 属性指向Student
Student.prototype.constructor = Student;

var student = new Student('张三',18);
student.sayHello(); // 我的名字叫张三,今年18岁
student.run();  // 张三开始奔跑
student.squat();    //蹲下来

console.log(student instanceof Person);  // true
console.log(student instanceof Student); // true
```



# 2、JavaScript数据结构

## 2.1 数组

>几乎所有的编程语言都原生支持数组类型，因为，数组是最简单的内存数据结构。当然JavaScript也不例外
>大多数语言的数组存储一系列同一种数据类型的值，但是在JavaScript中，数组可以保存不同类型的值

### 数组的创建和初始化
#### 使用new关键字
``` javascript
let days = new Array(7); // {1}
days = new Array('Monday','Tuesday','Wednesday','Thursday','Friday','Saturday','Sunday');// {2}
```
使用new关键字，能简单的声明并初始化一个数组，用这种方式，还可以创建数组的时候指定数组的长度如{1},还可以直接将数组元素作为参数传递给它的构造器如{2}
#### 使用中括号([])形式
``` javascript
let days = [];
days = ['Monday','Tuesday','Wednesday','Thursday','Friday','Saturday','Sunday'];
```
### 访问元素和迭代数组
访问指定位置的元素，可以用中括号传递数值位置:
``` javascript
console.log(days[5]);
```
假如我们想输出数组days里所有的元素，可以通过循环迭代数组、打印数组：
``` javascript
for(let i = 0; i < days.length; i++){
    console.log(days[i]);
}
```


### 添加元素
假如现有一个数组arr
``` javascript
let arr = [0,1,2,3,4,5];
```

#### 在数组末尾插入元素
>在JavaScript中，数组是一个可以修改的对象。如果添加元素，它的长度就会动态增长
``` javascript
arr[arr.length] = 6; // 直接赋值法
arr.push(7);         // 使用内置push()方法
arr.push(8,9,10);   // push()可以在末尾添加任意个元素
```
#### 在数组开头插入元素
目前数组的索引都有各自的元素，想在数组开头插入一个元素，则需要腾出数组的第一个元素的位置，把所有元素向右移动一位，再把我们想要的值赋给第一个位置（索引0）上。这个逻辑可以用下面代码表现
``` javascript
Array.prototype.insertFirst = function (value) {
    for (let i = this.length; i >= 0; i--) {
        this[i] = this[i - 1];
    }
    this[0] = value;
}
arr.insertFirst(-1);
```
图解：
![在数组开头插入元素.png](https://resources.yhong.info/users/10000/article/35/1624363878-DEE80A919746B81C868500AB77FF5BB6.png)

在JavaScript里，数组有个内置的方法unshift()，可以直接把数值插入数组的开头。这个方法的底层逻辑跟上面是一样的。
``` javascript
arr.unshift(-2);
arr.unshift(-3,-4,-5); // 当然unshift()与push()方法一样，都是可以添加任意个元素
```

### 删除元素
依上，加入现有个数组arr
``` javascript
let arr = [0,1,2,3,4,5];
```

#### 从数组末尾删除元素
使用**pop()**方法
``` javascript
arr.pop();
```
#### 从数组开头删除元素
想要从数组开头删除一个元素，可以把数组所有的元素都往左移了一位。可以用如下图表示：
![从数组开头删除元素.png](https://resources.yhong.info/users/10000/article/35/1624364363-BD4CC7EBE783F157D008B2680610513E.png)

这时候我们发现，虽然元素往左移动了一位，但是长度依旧没有变，这意味着数组中有额外的元素（值是undefined）；所以我们需要在arr.length - 1的时候停止循环：
``` javascript
Array.prototype.removeFirst = function () {
    for (let i = 0;i < this.length - 1;i++){
        this[i] = this[i + 1];
    }
}
arr.removeFirst();
```





### 在任意位置添加或者删除元素

#### 删除任意位置的元素
在JavaScript中我们可以用delete运算符来删除数组中的元素：
``` javascript
let arr = [0,1,2,3,4,5,6];
delete arr[0];
console.log(arr); // [undefined,1,2,3,4,5,6]
```
我们可以看到删除元素的时候，数组长度没有变，只是位置0的元素值变成了undefined；也就是delete arr[0]等同于 arr[0] = undefined


#### 使用splice()方法。通过指定位置删除相应位置上的指定数量的元素:
``` javascript
let arr = [0,1,2,3,4,5,6];
arr.splice(2,2);
console.log(arr); // [0,1,4,5,6]
```
上面代码就表示从数组索引2开始，删除2个元素。


**splice()**方法还可以在删除的时候插入新的元素：
``` javascript
let arr = [0,1,2,3,4,5,6];
arr.splice(2,0,8,8,8);
console.log(arr); // [0,1,8,8,8,2,3,4,5,6]
```
**splice()**方法接收的第一个参数，表示想要删除或者插入的元素索引值。第二个参数是删除元素的个数，**上面代码目的不是删除，而是添加元素**所以这里是传入0.第三个参数往后，就是要添加到数组里的值

## 2.2 二维数组与多维数组

我们来举个例子，如果只用一维数组的话，保存一个一年内每周的温度。那么只能这样表示：
``` javascript
let averageDayTemperature1 = [25,26,23,21,26,25,27];
let averageDayTemperature2 = [28,25,27,29,24,31,26];
let averageDayTemperature3 = [27,24,25,24,25,27,24];
```
每一周都额外多声明一个变量来保存。然而这不是最好的方法，还可以做得更好。我们可以使用矩阵（二维数组，或数组的数组）来存储这些信息。矩阵的行保存每天的数组，列对应第x周的数据
``` javascript
let averageDayTemperature = [];
averageDayTemperature[0] = [25,26,23,21,26,25,27];
averageDayTemperature[1] = [28,25,27,29,24,31,26];
averageDayTemperature[2] = [27,24,25,24,25,27,24];
```
用图来表示，如下：

![二维数组.png](https://resources.yhong.info/users/10000/article/39/1628052146-94BD8FA59B65D2CCD2ED0B6D20BDCF13.png)

###  二维数组的矢代：
``` javascript
for (let i = 0;i<averageDayTemperature.length;i++){ //遍历行
    for (let j = 0;j < averageDayTemperature[i].length;j++){ //遍历列
        console.log(`第${i + 1}周,第${j + 1}天的温度为：${averageDayTemperature[i][j]}℃`)
    }
}
```

### 多维数组
假设我们来表示一年级所有班级学生的座位
``` javascript
let seats = [];
// 1班
seats[0] = []
// 1班第一排
seats[0][0] = ['牟登','辛瑄经','保东扈','倪那']
// 1班第二排
seats[0][1] = ['喻汤','蓝祥','曾月宓','兰谈'];


// 2班
seats[1] = [];
// 2班第一排
seats[0][0] = ['卞秉','尤品','朱蓉牛','解谕屠']
// 2班第二排
seats[0][1] = ['苏琪刚','费尧初','戴璇何','安翁宇'];
```

```seats```即为矩阵3×3的结构。
![多维数组.png](https://resources.yhong.info/users/10000/article/39/1628076263-2C6A7F86EF47A7CBE53AE17FA5B72D1E.png)

## 2.3 数组的常用方法

在JavaScript里，数组是经过改进的对象，这意味着创建的每个数组都有一些可用的方法。
| 方法        | 描述                                                         |
| ----------- | ------------------------------------------------------------ |
| concat      | 连接2个或更多的数组，并返回结果                              |
| every       | 对数组中的每个元素运行给定函数，如果该函数对每个元素都返回true，则返回true |
| filter      | 对数组中的每个元素运行给定函数，返回该函数会返回true的元素组成的数组 |
| forEach     | 对数组中的每个元素运行给定函数，这个方法没有返回值，通常用来矢代数组 |
| join        | 将所有的数组元素连接成一个字符串                             |
| indexOf     | 返回第一个与给定参数相等的数组元素的索引，没有找到则返回-1   |
| lastIndexOf | 返回在数组中搜索到的与给定参数相等的元素的索引里最大值       |
| map         | 对数组中的每个元素运行给定函数，返回每次函数调用的结果组成数组 |
| reverse     | 颠倒数组中元素的顺序                                         |
| slice       | 传入索引值，将数组里对应索引范围内的元素作为新数组返回       |
| some        | 对数组中的每个元素运行给定函数，如果任一元素返回true，则返回true |
| sort        | 按照字母排序对数组排序，支持传入指定排序方法的函数作为参数   |
| toString    | 将数组作为字符串返回                                         |
| valueOf     | 和toString类似，将数组作为字符串返回。                       |

## 2.4 数组迭代

在JavaScript中内置了许多数组可用的迭代方法。
在本文例子中，我们需要用到的数组都为以下 numbers 数组，就不每个函数一一写出

``` javascript
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
```

### <span id="every">every() 方法迭代</span>
- every() 方法用于检测数组所有元素是否都符合指定条件（通过函数提供）。
- every() 方法使用指定函数检测数组中的所有元素：
  - 如果数组中检测到有一个元素不满足，则整个表达式返回 false ，且剩余的元素不会再进行检测。
  - 如果所有元素都满足条件，则返回 true。

**tips**:
every() 不会对空数组进行检测。
every() 不会改变原始数组。

语法：
``` javascript
array.every(function(currentValue,index,arr), thisValue)
```


示例：
我们判断numbers是不是全是偶数。
``` JavaScript
let isAllEven = numbers.every(x => x % 2 === 0);

console.log(isAllEven)  // false
```

数组的第一个元素是1，它不是2的倍数(1是奇数)，因此函数返回false，然后every执行结束

### <span id="some">some() 方法迭代</span>
- some() 方法用于检测数组中的元素是否满足指定条件（函数提供）。
- some() 方法会依次执行数组的每个元素：
  - 如果有一个元素满足条件，则表达式返回true , 剩余的元素不会再执行检测。
  - 如果没有满足条件的元素，则返回false。

示例：
我们判断numbers数组是否有偶数
``` JavaScript
let hasEven = numbers.some(x => x % 2 === 0)
console.log(hasEven);  // true
```
在这个例子中，numbers数组的第二个元素是2（为偶数），所以第二个被迭代的元素返回true。迭代结束


### <span id="forEach">forEach() 方法迭代</span>
forEach() 方法用于调用数组的每个元素，并将元素传递给回调函数。
注：**<font color="red">forEach() 本身是不支持的 continue 与 break 语句的</font>**

示例：
我们来判断一下numbers数组里每个元素的奇偶
``` JavaScript
numbers.forEach(x => {
    console.log(`数字${x}为${x % 2 === 0 ? '偶数' : '奇数'}`);
})
```
使用forEach和使用for循环的结果相同
### <span id="map">map() 方法迭代</span>
- map() 方法返回一个新数组，数组中的元素为原始数组元素调用函数处理后的值。
- map() 方法按照原始数组元素顺序依次处理元素。


示例：
获取numbers数组每个元素的奇偶性组成新数组：
``` javascript
const myMap = numbers.map(x => x % 2 === 0);
console.log(myMap) // [false, true, false, true, false, true, false, true, false, true]
```
### <span id="filter">filter() 方法迭代</span>
filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素。

示例：
我们获取numbers所有偶数组成新数组：
``` javascript
const evenNumbers = numbers.filter(x => x % 2 === 0);
console.log(evenNumbers) // [ 2, 4, 6, 8, 10 ]
```

### Tips:
以上方法的语法均为：
``` javascript
[数组].[方法名](function(currentValue,index,arr), thisValue)
```

参数详解：
<table> 
  <tbody><tr>
    <th style="width:25%">参数</th>
    <th>描述</th>
  </tr>  
  <tr>
    <td><em>function(currentValue, index,arr)</em></td>
    <td>必须。函数，数组中的每个元素都会执行这个函数<br>函数参数:<br><table class="reference"> 
  <tbody><tr>
    <th style="width:25%">参数</th>
    <th>描述</th>
  </tr>  
  <tr>
    <td><em>currentValue</em></td>
    <td>必须。当前元素的值</td>
  </tr>
  <tr>
    <td><em>index</em></td>
    <td>可选。当前元素的索引值</td>
  </tr>
    <tr>
    <td><em>arr</em></td>
    <td>可选。当前元素属于的数组对象</td>
  </tr>
</tbody></table>

    </td>
  </tr>
    <tr>
    <td><em>thisValue</em></td>
    <td>可选。对象作为该执行回调时使用，传递给函数，用作 "this" 的值。</td>
  </tr>
</tbody></table>



### <span id="reduce">reduce() 方法迭代</span>
- reduce() 方法接收一个函数作为累加器，数组中的每个值（从左到右）开始缩减，最终计算为一个值。
- reduce() 可以作为一个高阶函数，用于函数的 compose。

语法：
``` javascript
array.reduce(function(total, currentValue, currentIndex, arr), initialValue)
```
参数详解:
<table> 
  <tbody><tr>
    <th style="width:25%">参数</th>
    <th>描述</th>
  </tr>  
  <tr>
    <td><em>function(total,currentValue, index,arr)</em></td>
    <td>必需。用于执行每个数组元素的函数。<br>函数参数:<table class="tecspec"> 
  <tbody><tr>
    <th style="width:25%">参数</th>
    <th>描述</th>
  </tr>  
     <tr>
    <td><em>total</em></td>
    <td>必需。<em>初始值</em>, 或者计算结束后的返回值。</td>
     </tr>
  <tr>
    <td><em>currentValue</em></td>
    <td>必需。当前元素</td>
  </tr>
  <tr>
    <td><em>currentIndex</em></td>
    <td>可选。当前元素的索引</td>
  </tr>
    <tr>
    <td><em>arr</em></td>
    <td>可选。当前元素所属的数组对象。</td>
  </tr>
</tbody></table>

   </td>
  </tr>
    <tr>
    <td><em>initialValue</em></td>
    <td>可选。传递给函数的初始值</td>
  </tr>
</tbody></table>

示例：
我们对numbers数组中所有元素求和：
``` javascript
const sum = numbers.reduce((previous,current) => previous + current)
console.log(sum) // 55
```


### for...of循环迭代
ES2015（ES6）引入了迭代数组值的for...for循环。与for...in循环的差别就是前者迭代数组的值，后者迭代数组的索引
用法为：
``` javascript
for(let n of numbers){
    console.log(n % 2 === 0 ? '偶数' : '奇数');
}
```

### 使用@@iterator 对象迭代
ES2015（ES6）为Array类增加了一个@@iteratior属性，需要通过Symbol.iterator来访问。
``` JavaScript
let iterator = numbers[Symbol.iterator]();
console.log(iterator.next().value); // 1
console.log(iterator.next().value); // 2
console.log(iterator.next().value); // 3
console.log(iterator.next().value); // 4

```
通过迭代器的next()方法，就能依次得到数组中的值。如果想遍历数组的每个元素，假设数组长度为10，就要不断```iterator.next()``` 10次。当然可以用循环直接遍历迭代器来：
``` javascript
let iterator = numbers[Symbol.iterator]();
for (let n of iterator){
    console.log(n);
}
```



## 2.5 数组排序元素

本文只列举JavaScript中内置的一些排序元素的方法。常用的排序算法在后面会有提到。在本文就不列举了。
在本文例子中，我们需要用到的数组都为以下 numbers 数组，就不每个函数一一写出

``` javascript
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
```
###  <span id="reverse">reverse()方法</span> 
reverse() 方法用于颠倒数组中元素的顺序。
示例：
我们要把numbers内的元素顺序进行颠倒：
``` javascript
let reverseNumbers = numbers.reverse();
console.log(reverseNumbers) // [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
```

###  <span id="sort">sort()方法</span>
上面我们已经用reverse()方法把numbers数组颠倒元素顺序了，那我们再用sort试试：
``` javascript
console.log(numbers.sort()) // [1, 10, 2, 3, 4, 5, 6, 7, 8, 9]
```
结果输出[1, 10, 2, 3, 4, 5, 6, 7, 8, 9] 为何10又在2的前面呢？看起来不太对，是吧？这是因为sort方法在对数组做排序时，把元素默认当成字符进行相互比较。
我们来看一下语法：
``` javascript
arrayObject.sort(sortby)
```
参数
| 名称   | 说明               | 类型     |
| ------ | ------------------ | -------- |
| sortby | 可选。规定排序顺序 | Function |


注意：对数组的引用，数组在原数组上进行排序，不生成副本。
我们重新来试试：
``` javascript
let sortNumbers = numbers.sort((x,y) => x - y);
console.log(sortNumbers); // [1, 2, 3, 4,  5, 6, 7, 8, 9, 10]
```
当y大于x时，会返回负数，反之返回正数，如果相等就返回0 。sort()方法就根据返回值的情况对数组进行排序

#### 对象类型进行排序
``` JavaScript
const friends = [
    {name: '张三', age: 15},
    {name: '李四', age: 18},
    {name: '王五', age: 17}
];
let myFriendsSortByAge = friends.sort((a,b) => {
    if(a.age < b.age) return -1;
    if(a.age > b.age) return 1;
    return  0;
})
console.log(myFriendsSortByAge); /*
[
  { name: '张三', age: 15 },
  { name: '王五', age: 17 },
  { name: '李四', age: 18 }
]
*/
```

# 3 栈

> 栈是一种遵从后进先出（LIFO）原则的有序集合。新添加或待删除的元素都保存在栈的同一端，称作栈顶。在栈里，新元素都靠近栈顶，旧元素都接近栈底。

图片展示如下：

![栈的展示](E:\node\JavaScript\栈的展示.png)

## 3.1 基于数组的栈

我们来规划一下栈类需要的方法：

**push(element)**： 添加一个（或几个）新元素到栈顶

**pop()**：移除栈顶的元素，同时返回被移除的元素

**peek()**：返回栈顶的元素，不对栈做任何修改

**isEmpty()**：如果栈里没有任何元素就返回true,否则返回false

**clear()**：移除栈里所有元素

**size()**：返回栈里元素的个数

**toString()**：转成字符串

完整的Stack类如下

```javascript
class Stack {
    constructor() {
        this.items = [];
    }

    /**
     * 添加一个（或几个）新元素到栈顶
     * @param element
     */
    push(element) {
        this.items.push(element);
    }

    /**
     * 移除栈顶的元素，同时返回被移除的元素
     */
    pop() {
        return this.items.pop()
    }

    /**
     * 返回栈顶的元素，不对栈做任何修改
     */
    peek() {
        return this.items[this.items.length - 1];
    }

    /**
     * 如果栈里没有任何元素就返回true,否则返回false
     */
    isEmpty() {
        return this.items.length === 0;
    }

    /**
     * 移除栈里所有元素
     */
    clear() {
        this.items = [];
    }

    /**
     * 返回栈里元素的个数
     */
    size() {
        return this.items.length;
    }

    /**
     * 转成字符串
     * @return {string}
     */
    toString(){
        return this.items.toString();
    }
}
```

我们来使用一下Stack类

```javascript
let stack = new Stack();
stack.push(3);
stack.push(5);
stack.push(8);
console.log(stack.toString());
```

示例用图来绘制：

![栈元素的新增](E:\node\JavaScript\栈元素的新增.png)



删除栈顶示例：

```javascript
stack.pop();
stack.pop();
console.log(stack.toString());
```

![栈元素的删除](E:\node\JavaScript\栈元素的删除.png)



## 3.2 基于对象的栈

方法与上基于数组的栈方法规划一致

```javascript
class Stack {
    constructor() {
        this.count = 0;
        this.items = {};
    }

    /**
     * 添加一个（或几个）新元素到栈顶
     */
    push(element) {
        this.items[this.count] = element;
        this.count++;
    }

    /**
     * 移除栈顶的元素，同时返回被移除的元素
     */
    pop() {
        if (this.isEmpty()) {
            return undefined;
        }
        this.count--
        let result = this.items[this.count];
        delete this.items[this.count];
        return result;
    }

    /**
     * 返回栈顶的元素，不对栈做任何修改
     */
    peek() {
        return this.items[this.count - 1];
    }

    /**
     * 如果栈里没有任何元素就返回true,否则返回false
     */
    isEmpty() {
        return this.count === 0;
    }

    /**
     * 移除栈里所有元素
     */
    clear() {
        while (!this.isEmpty()) {
            this.pop();
        }
    }

    /**
     * 返回栈里元素的个数
     */
    size() {
        return this.count;
    }

    toString() {
        if (this.isEmpty()) {
            return '';
        }
        let content = this.items[0];
        for (let i = 1; i < this.count; i++) {
            content += ',' + this.items[i];
        }
        return content;
    }
}
```

## 3.3 栈的应用

### 从十进制到二进制

​		在现实生活中，我们主要是使用十进制。但在计算机科学中，二进制非常重要，因为计算机里的所有内容都是有二进制数字表示的（0和1）。没有十进制和二进制相互转换的能力，与计算机交流就很困难。

​		要把十进制转换成二进制，我们可以将该十进制数除以2（二进制是满2进1）并对商取整，直到结果是0为止。



举个例子，把十进制数字10转换成2进制，过程大概如下：



![十进制转二进制](E:\node\JavaScript\十进制转二进制.png)

实现代码如下：

```javascript
function decimalToBinary(number) {
    let stack = new Stack();
    let binaryString = '';
    while (number > 0) {
        stack.push(Math.floor(number % 2));
        number = Math.floor(number / 2);
    }
    while (!stack.isEmpty()) {
        binaryString += stack.pop().toString();
    }
    return binaryString;
}
```

使用：

```javascript
console.log(decimalToBinary(10));//1010
```

### 十进制转任意进制

```javascript
/**
 * 十进制转换任意进制
 * @param number
 * @param level
 * @return {string}
 */
function binaryConversion(number,level = 2) {
    let stack = new Stack();
    const digits = '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ';
    if(level < 2 || level > 36){
        return '';
    }
    let binaryString = '';
    while (number > 0){
        stack.push(Math.floor(number % level))
        number = Math.floor(number / level);
    }
    while (!stack.isEmpty()){
        binaryString += digits[stack.pop()];
    }
    return binaryString;
}
```

使用：

```javascript
console.log(binaryConversion(10,2)); //1010
```

# 4 队列

> 队列是遵循先进先出（FIFO，也称先来先服务）原则的一组有序的项。队列在尾部添加新元素，并从顶部移除元素。最新添加的元素必须排在队列的末尾。

在现实中，最常见的队列的例子就是排队。在电影院，学校饭堂，我们都会排队。排在第一位的人会先接受服务。

## 4.1 创建队列



**创建队列类Queue**

我们规划一下队列可用的方法：

**enqueue(element)**：向队列尾部添加一个（或）多个新的项。

**dequeue()**：移除队列的第一项（即排在队列最前面的项）并返回被移除的元素

**peek()**：返回队列中第一个元素，即最先添加的元素

**isEmpty()**：如果队列中不包含任何元素，返回true，否则返回false

**size()**：返回队列包含的元素个数。

**clear()**：清空队列

**toString()**：转成String

```javascript
class Queue {
    _count = 0; //用来记队列的大小
    _lowestCount = 0;   //因为队列需要操作第一个元素，需要一个变量来帮助追踪第一个元素
    _items = {};    // 存储队列元素
    constructor() {
    }

    /**
     * 向队列尾部添加一个（或）多个新的项
     * @param element
     */
    enqueue(element) {
        this._items[this._count] = element;
        this._count++;
    }

    /**
     * 移除队列的第一项（即排在队列最前面的项）并返回被移除的元素
     */
    dequeue() {
        if (this.isEmpty()) {
            return undefined;
        }
        let result = this._items[this._lowestCount];
        delete this._items[this._lowestCount];
        this._lowestCount++;
        return result;
    }

    /**
     * 返回队列中第一个元素，即最先添加的元素
     */
    peek() {
        if (this.isEmpty()) {
            return undefined;
        }
        return this._items[this._lowestCount];
    }

    /**
     * 如果队列中不包含任何元素，返回true，否则返回false
     */
    isEmpty() {
        return this.size() === 0;
    }

    /**
     * 返回队列包含的元素个数
     */
    size() {
        return this._count - this._lowestCount;
    }

    /**
     * 清空队列
     */
    clear() {
        this._items = {};
        this._count = 0;
        this._lowestCount = 0;
    }

    toString() {
        if (this.isEmpty()) {
            return '';
        }
        let str = this._items[this._lowestCount];
        for (let i = this._lowestCount + 1; i < this._count; i++) {
            str += ',' + this._items[i];
        }
        return str;
    }
}
```

使用队列：

```javascript
let queue = new Queue();
console.log(queue.isEmpty()); // true
queue.enqueue('张三');
queue.enqueue('李四');
console.log(queue.toString()) // 张三,李四
console.log(queue.size());  // 2
console.log(queue.peek()); // 张三
queue.dequeue();
console.log(queue.toString()) // 李四
```

## 4.2 双端队列

> 双端队列(deque，或称double-ended queue) 是一种允许我们同时从前端和后端添加和移除元素的特殊队列。

​    双端队列在现实生活中的例子有电影院、餐厅中排队的队伍等。举个栗子，一个刚买了票的人如果只是还需要再问一些简单的信息，就可以直接回到队伍的头部。另外，在队伍末尾的人如果赶时间，他可以直接离开队伍。

​    在计算机科学中，双端队列的一个常见应用是存储一系列的撤销操作。每当用户在软件中进行了一个操作，该操作会被存在一个双端队列中。当用户点击撤销按钮时该操作会被从双端队列中弹出，表示它被从后面移除了。在进行了预先定义的一定数量的操作后，最先进行的操作会被从双端队列的前端移除。由于双端队列同时遵守了**先进先出****和**后进先出**原则，可以说它是把对了和栈相结合的一种数据结构。

​    既然双端队列是一种特殊的队列，我们可以看到其有多个方法的代码与队列相同

**isEmpty()**：如果队列中不包含任何元素，返回true，否则返回false

**size()**：返回队列包含的元素个数。

**clear()**：清空队列

**toString()**：转成String

我们再规划一下其他可用的方法：

**addFront(element)**：在双端队列前端添加新元素

**addBack(element)**：在双端队列后端新增新的元素

**removeFront()**：从双端队列前端移除第一个元素，并返回该元素

**removeBack()**：从双端队列后端移除第一个元素，并返回该元素

**peekFront()**：返回双端队列前端第一个元素

**peekBack()**：返回双端队列后端第一个元素

实现代码如下：

```javascript
class Deque {
    _count = 0; //用来记队列的大小
    _lowestCount = 0;   //因为队列需要操作第一个元素，需要一个变量来帮助追踪第一个元素
    _items = {};    // 存储队列元素
    constructor() {
    }

    /**
     * 在双端队列前端添加新元素
     * @param element
     */
    addFront(element) {
        if (this.isEmpty()) {   //空队列
            this.addBack(element);
        } else if (this._lowestCount > 0) { // 一个元素已经被从双端队列的前端移除
            this._lowestCount--;
            this._items[this._lowestCount] = element;
        } else {
            //所有元素往后移动一位
            for (let i = this._count; i > 0; i--) {
                this._items[i] = this._items[i - 1];
            }
            this._count++;
            this._items[0] = element;
        }
    }

    /**
     * 在双端队列后端新增新的元素
     * @param element
     */
    addBack(element) {
        this._items[this._count] = element;
        this._count++;
    }

    /**
     * 从双端队列前端移除第一个元素，并返回该元素
     */
    removeFront() {
        if (this.isEmpty()) {
            return undefined;
        }
        let result = this._items[this._lowestCount];
        delete this._items[this._lowestCount];
        this._lowestCount++;
        return result;
    }

    /**
     * 从双端队列后端移除第一个元素，并返回该元素
     */
    removeBack() {
        if (this.isEmpty()) {
            return undefined;
        }
        this._count--
        let result = this._items[this._count];
        delete this._items[this._count];
        return result;
    }

    /**
     * 返回双端队列前端第一个元素
     */
    peekFront() {
        if (this.isEmpty()) {
            return undefined;
        }
        return this._items[this._lowestCount];
    }

    /**
     * 返回双端队列后端第一个元素
     */
    peekBack() {
        return this._items[this._count - 1];
    }

    /**
     * 如果队列中不包含任何元素，返回true，否则返回false
     */
    isEmpty() {
        return this.size() === 0;
    }

    /**
     * 返回队列包含的元素个数
     */
    size() {
        return this._count - this._lowestCount;
    }

    /**
     * 清空队列
     */
    clear() {
        this._items = {};
        this._count = 0;
        this._lowestCount = 0;
    }

    toString() {
        if (this.isEmpty()) {
            return '';
        }
        let str = this._items[this._lowestCount];
        for (let i = this._lowestCount + 1; i < this._count; i++) {
            str += ',' + this._items[i];
        }
        return str;
    }
}
```

### 使用双端队列Deque类

```javascript
let deque = new Deque();
console.log(deque.isEmpty()); //true
deque.addBack('张三');
deque.addBack('李四');
deque.addFront('王五');
console.log(deque.toString()) // 王五,张三,李四
deque.removeFront();
console.log(deque.toString()); // 张三,李四
deque.removeBack();
console.log(deque.toString()); // 张三
```

## 4.3 使用队列和双端队列来解决问题

### 4.3.1 击鼓传花游戏

> 击鼓传花游戏：孩子们围成一个圆圈，把花尽快地传给旁边的人。某一时刻传花停止。这个时候花在谁手里，谁就退出圆圈，结束游戏。重复这个过程，直到只剩一个孩子（胜者）。

```javascript
/**
 * 击鼓传花游戏
 * @param list 参与者列表
 * @param num 传花次数
 * @return {{winner: *, eliminate: []}}
 */
function hotPotato(list, num) {
    let queue = new Queue();
    let eliminatedList = [];
    //把所有参与者加入队列中
    for (let i = 0; i < list.length; i++) {
        queue.enqueue(list[i]);
    }
    while (queue.size() > 1) {
        for (let i = 0; i < num; i++) {
            queue.enqueue(queue.dequeue())
        }
        eliminatedList.push(queue.dequeue());
    }
    return {
        eliminate: eliminatedList,
        winner: queue.dequeue()
    }
}
```

应用hotPotato()算法：

```javascript
const names = ['张三','李四','王五','John','Jack'];
const result = hotPotato(names,8);
result.eliminate.forEach(name => {
    console.log(name + '在击鼓传花游戏中被淘汰。')
})
console.log('胜利者：' + result.winner)
```

以上输出如下：

![image-20210917163219830](E:\node\JavaScript\击鼓传花.png)

### 4.3.2 回文检查器

> 回文是正反都能读通的单词，词组、数或一系列字符的序列，例如：madam或racecar。

​    有不同的算法可以检查一个词组或字符串是否为回文。最简单的方式是将字符串反向排列并检查它和原字符串是否相同。如果两者相同，那么它就是一个回文。我们也可以用栈来完成，但是利用数据结构来解决这个问题的最简单方法就是使用双端队列



```javascript
/**
 * 回文检查器
 * @param content 需要检查的字符串
 * @return {boolean}
 */
function palindromeDetector(content) {
    if (content === undefined || content === null || content.length === 0) {
        return false;
    }
    let deque = new Deque();
    let lowerString = content.toLocaleLowerCase().split(' ').join(''); // 全转成小写并移除空格
    let isEqual = true;
    let firstChar, lastChar;
    for (let i = 0; i < lowerString.length; i++) {
        deque.addBack(lowerString.charAt(i));
    }
    while (deque.size() > 1 && isEqual) {
        firstChar = deque.removeFront();
        lastChar = deque.removeBack();
        if (firstChar !== lastChar) {
            isEqual = false;
        }
    }
    return isEqual;

}
```

我们来应用一下**palindromeDetector()**算法：

```JavaScript
console.log('a',palindromeDetector('a')); // true
console.log('aa',palindromeDetector('aa')); // true
console.log('kayak',palindromeDetector('kayak')); // true
console.log('hello',palindromeDetector('hello')); // false
```

# 5 链表

> 链表用来存储有序的元素集合，与数组不同，链表中的元素并非保存在连续的存储空间内，每个元素由一个存储元素本身的节点和一个指向下一个元素的指针构成。当要移动或删除元素时，只需要修改相应元素上的指针就可以了。对链表元素的操作要比对数组元素的操作效率更高

## 5.1 单项链表

下面是单项链表的数据结构展示图：

 ![单项链表展示](E:\node\JavaScript\单项链表展示.png)

 要表示链表中的元素，我们需要一个助手类，叫作**Node**。表示我们想要添加到链表中的项，它包含一个element属性，该属性表示要加入链表元素的值，和一个next属性，该属性是指向链表中下一个元素的指针。它的代码如下：

```javascript
class Node {
    constructor(element) {
        this.element = element;
        this.next = null;
    }
}

```

然后我们需要创建主类，叫LinkedList类，我们来规划一下这个类可用到的方法以及方法的作用。

**push(element)**： 向链表尾部添加节点

**insert(position, element)**： 在链表的指定位置插入节点

**removeAt(position)**：删除链表中指定位置的元素，并返回这个元素的值

**remove(element)**：删除链表中对应的元素

**indexOf(element)**：在链表中查找给定元素的索引

**getElementAt(position)**：返回链表中索引所对应的元素

**isEmpty()**：判断链表是否为空

**size()**：返回链表的长度

**getHead()**：返回链表的头元素

**clear()**：清空链表

**toString()**：辅助方法，按指定格式输出链表中的所有元素，方便测试验证结果

让我们从查找链表元素的方法**getElementAt()**开始，因为后面我们会多次用到它。

```JavaScript
getElementAt(position) {
    if (position < 0 || position >= this.length) return undefined;
    let current = this.head;
    for (let i = 0; i < position; i++) {
        current = current.next;
    }
    return current;
}
```

**向链表尾部添加元素**

向链表尾部添加一个元素时，可能有两种场景：

场景1：链表为空，那添加的就是第一个元素

![单项链表添加元素](E:\node\JavaScript\单项链表添加元素.png)

场景2：链表不为空

![单项链表向尾部添加元素](E:\node\JavaScript\单项链表向尾部添加元素.png)

实现代码如下：

```javascript
push(element) {
    let node = new Node(element);
    let current;
    if (this.head === undefined) {
        this.head = node;
    } else {
        current = this.head;
        while (current.next != null) {
            current = current.next;
        }
        current.next = node;
    }
    this.length++;
}
```

从链表中移除元素

**场景一**：删除第一个元素，如果要删除的节点为链表的头部，只需要将head移到下一个节点即可。如果当前链表只有一个节点，那么下一个节点为null，此时将head指向下一个节点等同于将head设置成null，删除之后链表为空。
![从链表中移除元素](E:\node\JavaScript\从链表中移除元素.png)
**场景二**：删除不是第一个元素，如果要删除的节点在链表的中间部分，我们需要找出position所在位置的前一个节点，将它的next指针指向position所在位置的下一个节点。总之，删除节点只需要修改相应节点的指针，使断开位置左右相邻的节点重新连接上。被删除的节点由于再也没有其它部分的引用而被丢弃在内存中，等待垃圾回收器来清除。
实现代码如下：

![Image](E:\node\JavaScript\单项链表从中间删除元素.png)

实现代码如下：

```javascript
/**
     * 删除链表中指定位置的元素，并返回这个元素的值
     * @param position
     */
    removeAt(position) {
        if (position < 0 || position >= this.length) return undefined;
        let current = this.head;
        if (position === 0) {
            this.head = current.next;
        } else {
            let previous = this.getElementAt(position - 1);
            current = previous.next;
            previous.next = current.next;
        }
        this.length--;
        return current.element;
    }
```



完整的LinkedList类代码如下：

```javascript
class Node {
    constructor(element) {
        this.element = element;
        this.next = null;
    }
}

class LinkedList {
    constructor() {
        this.length = 0;
        this.head = undefined;
    }

    /**
     * 向链表尾部添加节点
     * @param element
     */
    push(element) {
        let node = new Node(element);
        let current;
        if (this.head === undefined) {
            this.head = node;
        } else {
            current = this.head;
            while (current.next != null) {
                current = current.next;
            }
            current.next = node;
        }
        this.length++;
    }

    /**
     * 在链表的指定位置插入节点
     * @param position
     * @param element
     */
    insert(position, element) {
        // position不能超出边界值
        if (position < 0 || position > this.length) return false;
        let node = new Node(element);
        if (position === 0) {
            node.next = this.head;
            this.head = node;
        } else {
            let previous = this.getElementAt(position - 1);
            let current = previous.next;
            node.next = current;
            previous.next = node;
        }
        this.length++;
        return true;
    }

    /**
     * 删除链表中指定位置的元素，并返回这个元素的值
     * @param position
     */
    removeAt(position) {
        if (position < 0 || position >= this.length) return undefined;
        let current = this.head;
        if (position === 0) {
            this.head = current.next;
        } else {
            let previous = this.getElementAt(position - 1);
            current = previous.next;
            previous.next = current.next;
        }
        this.length--;
        return current.element;
    }

    /**
     *  删除链表中对应的元素
     * @param element
     */
    remove(element) {
        let index = this.indexOf(element);
        return this.removeAt(index);
    }

    /**
     * 在链表中查找给定元素的索引
     * @param element
     */
    indexOf(element) {
        let current = this.head;
        for (let i = 0; i < this.length; i++) {
            if (current.element === element) return i;
            current = current.next;
        }
        return -1;
    }

    /**
     * 返回链表中索引所对应的元素
     * @param position
     */
    getElementAt(position) {
        if (position < 0 || position >= this.length) return undefined;
        let current = this.head;
        for (let i = 0; i < position; i++) {
            current = current.next;
        }
        return current;
    }

    /**
     * 判断链表是否为空
     */
    isEmpty() {
        return this.length === 0;
    }

    /**
     * 返回链表的长度
     */
    size() {
        return this.length;
    }

    /**
     * 返回链表的头元素
     */
    getHead() {
        return this.head;
    }

    /**
     * 清空链表
     */
    clear() {
        this.head = null;
        this.length = 0;
    }

    /**
     * 辅助方法，按指定格式输出链表中的所有元素，方便测试验证结果
     */
    toString() {
        let current = this.head;
        let content = '';
        while (current) {
            let next = current.next;
            next = next ? next.element : null;
            content += `{ element: ${current.element}, next: ${next} },`;
            current = current.next;
        }
        if (content) {
            content = content.substring(0, content.length - 1);
        }
        content = `[${content}]`;
        return content;
    }
}
```

**应用LinkedList类：**

```JavaScript
let linkedList = new LinkedList();
linkedList.push('张三');
linkedList.push('李四');
linkedList.push('王五');
linkedList.push('Cat');
linkedList.push('Dog');
console.log(linkedList.toString())
linkedList.removeAt(2);
console.log(linkedList.toString())
linkedList.remove('张三')
console.log(linkedList.toString())
linkedList.insert(2,'阿狗')
console.log(linkedList.toString())
console.log(linkedList.indexOf('阿狗'))
```

以上效果输出如下：

![image-20210918221849631](E:\node\JavaScript\单项链表输出.png)



## 5.2 双向链表

> 链表有多种不同的类型，**双向链表**和**普通链表**的区别在于，在链表中，一个节点只有链向下一个节点的链接；而在双向链表中，链接是双向的：**一个链向下一个元素，另一个链向前一个元素。**

如图所示：

![双向链表展示](E:\node\JavaScript\双向链表展示.png)

由于双向链表具有单向链表的所有特性，因此我们的双向链表类可以继承自前面的单向链表类，不过辅助类Node需要添加一个prev属性，用来指向前一个节点。

```JavaScript
class Node{
    constructor(element) {
        this.element = element;
        this.next = null;
        this.pre = null;
    }
}
```

下面是继承自`LinkedList`类的双向链表类的基本骨架：

```JavaScript
class DoubleLinkedList extends LinkedList {
    constructor() {
        super();
        this.tail = null;
    }
}
```



先来看看`push()`方法的实现。当链表为空时，除了要将head指向当前添加的节点外，还要将tail也指向当前要添加的节点。当链表不为空时，直接将tail的next指向当前要添加的节点node，然后修改node的pre指向旧的tail，最后修改tail为新添加的节点。我们不需要从头开始遍历整个链表，而通过tail可以直接找到链表的尾部，这一点比单向链表的操作要更方便。最后将length的值加1，修改链表的长度。

```JavaScript
push(element) {
    let node = new Node(element);
    // 当链表为空
    if (this.head === null) {
        this.head = node;
        this.tail = node;
    } else {
        //否则将当前节点添加到链表尾部
        this.tail.next = node;
        node.pre = this.tail;
        this.tail = node;
    }
    this.length++;
}
```



我们同时还需要修改`insert()`和`removeAt()`这两个方法。记住，与单向链表唯一的区别就是要同时维护head和tail，以及每一个节点上的next和prev指针。

```JavaScript
insert(element, index) {
    if (index >= 0 && index <= this.length) {
        let node = new Node(element);
        let current = this.head;
        if (index === 0) {
            if (this.head === null) { // 如果链表为空
                this.head = node;
                this.tail = node;
            } else {
                node.next = this.head;
                current.pre = node;
                this.head = node;
            }
        } else if (index === this.length) {
            current = this.tail;
            current.next = node;
            node.pre = current;
            this.tail = node;
        } else {
            let previous = this.getElementAt(index - 1);
            current = previous.next;
            node.next = current;
            previous.next = node;
            current.pre = node;
            node.pre = previous;
        }
        this.length++;
        return true;
    }
    return false
}
```

```JavaScript
removeAt(position) {
    // position不能超出边界值
    if (position < 0 || position >= this.length) return null;
    let current = this.head;
    let previous;
    if (position === 0) { // 移除头部元素
        this.head = current.next;
        this.head.pre = null;
        if (this.length === 1) this.tail = null;
    } else if (position === this.length - 1) { // 移除尾部元素
        current = this.tail;
        this.tail = current.pre;
        this.tail.next = null;
    } else { // 移除中间元素
        current = this.getElementAt(position);
        previous = current.pre;
        previous.next = current.next;
        current.next.pre = previous;
    }
    this.length--;
    return current.element;
}
```

完整的`DoubleLinkedList`代码：

```javascript
class DoubleLinkedList extends LinkedList {
    constructor() {
        super();
        this.tail = null;
    }

    push(element) {
        let node = new Node(element);
        // 当链表为空
        if (this.head === null) {
            this.head = node;
            this.tail = node;
        } else {
            //否则将当前节点添加到链表尾部
            this.tail.next = node;
            node.prev = this.tail;
            this.tail = node;
        }
        this.length++;
    }

    insert(element, index) {
        if (index >= 0 && index <= this.length) {
            let node = new Node(element);
            let current = this.head;
            if (index === 0) {
                if (this.head === null) { // 如果链表为空
                    this.head = node;
                    this.tail = node;
                } else {
                    node.next = this.head;
                    current.pre = node;
                    this.head = node;
                }
            } else if (index === this.length) {
                current = this.tail;
                current.next = node;
                node.pre = current;
                this.tail = node;
            } else {
                let previous = this.getElementAt(index - 1);
                current = previous.next;
                node.next = current;
                previous.next = node;
                current.pre = node;
                node.pre = previous;
            }
            this.length++;
            return true;
        }
        return false
    }

    removeAt(position) {
        // position不能超出边界值
        if (position < 0 || position >= this.length) return null;
        let current = this.head;
        let previous;
        if (position === 0) { // 移除头部元素
            this.head = current.next;
            this.head.pre = null;
            if (this.length === 1) this.tail = null;
        } else if (position === this.length - 1) { // 移除尾部元素
            current = this.tail;
            this.tail = current.pre;
            this.tail.next = null;
        } else { // 移除中间元素
            current = this.getElementAt(position);
            previous = current.pre;
            previous.next = current.next;
            current.next.pre = previous;
        }
        this.length--;
        return current.element;
    }

    getTail() {
        return this.tail;
    }

    toString() {
        let current = this.head;
        let s = '';

        while (current) {
            let next = current.next;
            let previous = current.prev;
            next = next ? next.element : 'null';
            previous = previous ? previous.element : 'null';
            s += `[element: ${current.element}, prev: ${previous}, next: ${next}] `;
            current = current.next;
        }

        return s;
    }
}
```

我们写测试

```JavaScript
let doubleLinkedList = new DoubleLinkedList();
doubleLinkedList.push(1);
doubleLinkedList.push(3);
doubleLinkedList.push(5);
doubleLinkedList.push(7);
doubleLinkedList.push(9);

console.log(doubleLinkedList.toString())
console.log(doubleLinkedList.size())
console.log(doubleLinkedList.getElementAt(1).element);
console.log(doubleLinkedList.getElementAt(2).element);
console.log(doubleLinkedList.getElementAt(3).element);

doubleLinkedList.insert('Jack',1)
console.log(doubleLinkedList.toString())
doubleLinkedList.removeAt(1)
console.log(doubleLinkedList.toString())
```

运行结果如下：

![image-20210925172403111](E:\node\JavaScript\双向链表运行结果.png)

## 5.3 循环链表

> 循环链表可以像链表一样只有单向引用，也可以像双向链表一样有双向引用。循环链表和链表之间唯一的区别在于，最后一个元素指向下一个元素的指针(tail.next)不是引用undefined而是指向第一个元素(head)

结构示意图如下：

![循环链表结构示意图](E:\node\JavaScript\循环链表结构示意图.png)

**双向循环链表**有指向head元素的tail.next和指向tail元素的head.pre

![双向循环链表结构示意图](E:\node\JavaScript\双向循环链表结构示意图.png)

我们来看创建`CircularLinkedList`类的代码。

```JavaScript
class CircularLinkedList extends LinkedList {
    constructor() {
        super();

    }

    push(element) {

        let node = new Node(element);
        if (this.head === undefined) {
            this.head = node;
        } else {
            let current = this.getElementAt(this.length - 1);
            current.next = node;
        }
        node.next = this.head;
        this.length++;
    }

    insert(position, element) {
        if (position < 0 || position >= this.length) return false;
        let node = new Node(element);
        if (position === 0) {
            node.next = this.head;
            let current = this.getElementAt(this.length - 1);
            current.next = node;
            this.head = node;
        } else {
            let previous = this.getElementAt(position - 1);
            node.next = previous.next;
            previous.next = node;
        }
        this.length++;
        return true;
    }

    removeAt(position) {
        if (position < 0 || position >= this.length) return false;
        let current = this.head;
        if (position === 0) {
            this.head = current.next;
        } else {
            let previous = this.getElementAt(position - 1);
            current = previous.next;
            previous.next = current.next;
        }
        this.length--;
        if (this.length > 1) {
            let last = this.getElementAt(this.length - 1);
            last.next = this.head;
        }
        return current.element;
    }

    toString() {
        let current = this.head;
        let s = '';

        for (let i = 0; i < this.length; i++) {
            let next = current.next;
            next = next ? next.element : 'null';
            s += `[element: ${current.element}, next: ${next}] `;
            current = current.next;
        }

        return s;
    }
}
```

我们来写几个`CircularLinkedList`测试用例：

```JavaScript
let circularLinkedList = new CircularLinkedList();
circularLinkedList.push(1);
circularLinkedList.push(3);
console.log(circularLinkedList.toString());

circularLinkedList.insert(0, 7);
circularLinkedList.insert(3, 9);
console.log(circularLinkedList.toString());

console.log(circularLinkedList.removeAt(0));
console.log(circularLinkedList.toString());
```

运行结果如下：

![image-20210925201619714](E:\node\JavaScript\循环链表测试用例.png)



# 6 集合

> **集合**是由一组无序且唯一（即不能重复）的项组成。该数据结构使用了与有限集合相同的数学概念，但应用在计算机科学的数据结构中。

## 6.1 创建Set类

用下面的Set类以及它的构造函数声明作为开始

```JavaScript
class Set {
    constructor() {
        this.items = {};
    }
}
```

接下来我们需要声明一些集合可用的方法：

`add(element)`：向集合添加一个新的项
`delete(element)`：从集合里移除一个值
`has(element)`：如果值在集合中，返回true，否则返回false
`clear()`：移除集合中的所有项
`size()`：返回集合所包含元素的数量，与数组的length属性类似
`values()`：返回一个包含集合中所有值的数组

### 6.1.1 has(element)方法

由于`has(element)`方法会被add、delete等其它方法调用。它用来检验某个元素是否存在于集合中。所以我们先来实现它：

```JavaScript
has(element){
    return Object.prototype.hasOwnProperty.call(this.items,element);
}
```

Object原型有`hasOwnProperty`方法。该方法返回一个表明对象是否具有特定属性的布尔值。

### 6.1.2 add(element)方法

```javascript
add(element){
    if(!this.has(element)){
        this.items[element] = element;
        return true
    }
    return false;
}
```

对于给定的element，可以检查它是否存在于集合中。如果不存在，就把element添加到集合，返回true。如果集合已经有了这个元素就返回false不进行添加

### 6.1.3 delete()和clear()方法

```javascript
delete(element){
    if(this.has(element)){
        delete this.items[element];
        return true;
    }
    return  false;
}
```

delete方法依旧要验证是否存在element。

```JavaScript
clear(){
    this.items = {};
}
```

### 6.1.4 size()方法

该方法有三种实现方式。

第一种方式是使用一个length变量，每次使用add或者delete方法时就控制它。

第二种方式是使用JavaScript中Object类的一个内置方法

```javascript
size(){
    return Object.keys(this.items).length
}
```

JavaScript的Object类有一个keys方法，它返回一个包含给定对象所有属性的数组。然后可以使用这个数组的length属性来返回items对象的属性个数。

第三种方式是手动提取items对象的每一个属性，记录属性的个数并返回这个数。

```JavaScript
sizeLegacy(){
    let count = 0;
    for (let key in this.items){
        if(this.items.hasOwnProperty(key)) count++;
    }
    return count;
}
```

### 6.1.5 values()方法

要实现values()方法。有两种方式。

第一种是使用Object类的values()方法。

```JavaScript
values(){
    return Object.values(this.items);
}
```

`Object.values()`方法返回一个包含给定对象所有属性值的数组。

第二种是矢代items对象的所有属性，把它们添加到一个数组中，并返回该数组。

```JavaScript
valuesLegacy(){
    let values = [];
    for (let key in this.items){
        if(this.items.hasOwnProperty(key)) values.push(key);
    }
    return values;
}
```

下面是Set类的所有代码

```javascript
class Set {
    constructor() {
        this.items = {};
    }

    /**
     * 向集合添加一个新元素
     * @param element
     * @return {boolean}
     */
    add(element){
        if(!this.has(element)){
            this.items[element] = element;
            return true
        }
        return false;
    }

    /**
     * 从集合添加一个新元素
     * @param element
     * @return {boolean}
     */
    delete(element){
        if(this.has(element)){
            delete this.items[element];
            return true;
        }
        return  false;
    }

    /**
     * 返回一个包含集合中所有元素的数组
     * @return {unknown[]}
     */
    values(){
        return Object.values(this.items);
    }
    valuesLegacy(){
        let values = [];
        for (let key in this.items){
            if(this.items.hasOwnProperty(key)) values.push(key);
        }
        return values;
    }
    /**
     * 如果元素在集合中，返回true，否则返回false
     * @param element
     * @return {boolean}
     */
    has(element){
        return Object.prototype.hasOwnProperty.call(this.items,element);
    }

    /**
     * 移除集合中所有元素
     */
    clear(){
        this.items = {};
    }

    /**
     * 返回集合所包含元素的数量，与数组的length属性类似
     * @return {number}
     */
    size(){
        return Object.keys(this.items).length
    }
    sizeLegacy(){
        let count = 0;
        for (let key in this.items){
            if(this.items.hasOwnProperty(key)) count++;
        }
        return count;
    }
}
```

### 6.1.6 使用Set类

我们来写几个测试用例

```JavaScript
let set = new Set();
set.add(1);
console.log(set.values());
console.log(set.has(1));
console.log(set.size());

set.add(3);
console.log(set.values());
console.log(set.has(3));
console.log(set.size());

set.delete(1);
console.log(set.values());

set.delete(3);
console.log(set.values());
```

下面是运行的结果：

![image-20210925233628077](E:\node\JavaScript\Set类测试用例结果.png)

## 6.2 集合运算

我们可以对集合进行如下运算。

**并集**：对于给定的两个集合，返回一个包含两个集合中所有元素的新集合。

**交集**：对于给定的两个集合，返回一个包含两个集合中共有元素的新集合。

**差集**：对于给定的两个集合，返回一个包含所有存在于第一个集合且不存在于第二个集合的元素的新集合。

**子集**：验证一个给定集合是否是另一个集合的子集。

### 6.2.1 并集

集合A和集合B的并集表现如下：
$$
A\cup B
$$


该集合定义如下：
$$
A \cup B \{x|x \in A \lor x \in B\}
$$
意思是x（元素）存在于A中，或者x存在于B中。下图展示了并集运算：

![并集](E:\node\JavaScript\并集.png)



现在来实现Set类的`union()`方法

```JavaScript
union(otherSet){
    let unionSet = new Set();
    this.values().forEach(value => unionSet.add(value));
    otherSet.values().forEach(value => unionSet.add(value));
    return unionSet;
}
```

以上使用的为`forEach`方法来矢代数组的元素，但它是ECMAScript2015中才引入的。也可以把`union`方法写成下面这样，不适用`forEach`和箭头函数：

```JavaScript
unionLegacy(otherSet){
    let unionSet = new Set();
    let values = this.values();
    for (let i = 0;i < values.length;i++){
        unionSet.add(values[i]);
    }
    values = otherSet.values();
    for (let i = 0;i < values.length;i++){
        unionSet.add(values[i]);
    }
    return unionSet;
}
```

我们来写测试用例：

```javascript
let setA = new Set();
setA.add(1);
setA.add(2);
setA.add(3);

let setB = new Set();
setB.add(3);
setB.add(4);
setB.add(5);
setB.add(6);

let unionSet = setA.union(setB);
console.log(unionSet.values())
```

运行结果为`[ 1, 2, 3, 4, 5, 6 ]`。注意元素3同时存在于setA和setB中，它在结果集合中只出现一次。

### 6.2.2 交集

集合A和集合B的交集表示如下：
$$
A \cap B
$$
该集合定义如下：
$$
A \cap B \{x|x \in A \land x \in B\}
$$
意思是x（元素）存在于A中，且x存在于B中。下图展示了交集运算：

![交集](E:\node\JavaScript\交集.png)

现在来实现Set类的intersection方法

```JavaScript
intersection(otherSet) {
    let intersectionSet = new Set();
    let values = this.values();
    for (let i = 0; i < values.length; i++) {
        //验证是否存在otherSet中,存在则添加
        if (otherSet.has(values[i])) {
            intersectionSet.add(values[i]);
        }
    }
    return intersectionSet;
}
```

 来写个测试用例：

```javascript
let setA = new Set();
setA.add(1);
setA.add(2);
setA.add(3);

let setB = new Set();
setB.add(2);
setB.add(3);
setB.add(4);

let intersectionAB = setA.intersection(setB);
console.log(intersectionAB.values());
```

运行结果为`[ 2, 3 ]`，因为2和3同时存在于两个集合中。



### 6.2.3 差集

集合A和集合B的差集表示为 A - B，定义如下：
$$
A - B = \{x|x \in A \land x \not \subset B\}
$$
意思是x（元素）存在于A中，且x不存在于B中。下图展示了集合A和集合B的差集运算。

![差集](E:\node\JavaScript\差集.png)

现在来实现Set类的`difference`方法

```JavaScript
difference(otherSet){
    let differenceSet = new Set();
    this.values().forEach(value => {
        if(!otherSet.has(value)){
            differenceSet.add(value);
        }
    });
    return differenceSet;
}
```

写个测试用例来测试以上方法：

```javascript
let setA = new Set();
setA.add(1);
setA.add(2);
setA.add(3);

let setB = new Set();
setB.add(2);
setB.add(3);
setB.add(4);

let differenceAB = setA.difference(setB);
console.log(differenceAB.values());
```

输出结果为`[ 1 ]`，因为1是唯一一个仅存在于`setA`的元素。如果我们执行`setB.difference(setA)`,会得到`[ 4 ]`作为输出结果，因为4是只存在于`setB`中的元素

### 6.2.4 子集

子集的数学概念是集合A是集合B的子集，表示如下：
$$
A \subseteq B
$$
该集合的定义如下：
$$
\{x|\forall x \in A \Rightarrow x \in B\}
$$
意思是集合A中的每一个x（元素），也需要存在于集合B中。下图展示了集合A是集合B的子集：

![子集](E:\node\JavaScript\子集.png)

现在来实现Set类的`isSubsetOf()`方法：

```javascript
isSubsetOf(otherSet) {
    //当前set类的大小必须要大于otherSet实例大小
    if (this.size() > otherSet.size()) return false;

    let isSubset = true;
    this.values().every(value => {
        if (!otherSet.has(value)) {
            isSubset = false;
            return false;
        }
        return true;
    })
    return  isSubset;
}
```

在`isSubsetOf()`方法中，我们不像并集、交集和差集中使用`forEach`方法。我们使用`every()`方法代替，这个方法的回调函数只要返回false，那么循环就会停止。不需要再往下循环。

写个测试检验一下上面的代码效果：

```javascript
let setA = new Set();
setA.add(1);
setA.add(2);

let setB = new Set();
setB.add(1);
setB.add(2);
setB.add(3);

let setC = new Set();
setC.add(2);
setC.add(3);
setC.add(4);

console.log(setA.isSubsetOf(setB)); // true
console.log(setA.isSubsetOf(setC)); // false
```

# 7 字典和散列表

## 7.1 字典

> 我们知道，集合表示一组互不相同的元素（不能重复的元素）。在字典中，存储的是[键, 值]对，其中键名是用来查询特定元素的。字典和集合很相似，集合以[值, 值]的形式存储元素，字典则是以[键, 值]的形式来存储元素。字典也称作**映射**、**符号表**或**关联数组**

### 7.1.1 创建字典类

以下就是我们`Dictionary`类的骨架：

```JavaScript
function defaultToString(key) {
    if(key === null){
        return 'NULL'
    }else if (key === undefined){
        return  'UNDEFINED';
    }else if(typeof key === 'string' || key instanceof String){
        return `${key}`;
    }
    return key.toString();
}
export default class Dictionary {
    constructor(toStringFn = defaultToString) {
        this.toStringFn = toStringFn;
        this.table = {};
    }
}
```

在字典中，理想的情况是用字符串作为键名，值可以是任何类型。但是JavaScript不是强类型语言，我们不能保证键一定是字符串。我们需要把所有作为键名传入的对象化转为字符串，使得从`Dictionary`类中搜索和获取值更简单。

为了在字典中保存value，我们将key转化为了字符串，而为保存信息需要，我们同样要保存原始的key。因此，我们不只是将value保存在字典中，而是要保存两个值：原始的key和value。所以我们需要声明一个[键，值对类：

```javascript
class ValuePairs {
    constructor(key, value) {
        this.key = key;
        this.value = value;
    }

    toString() {
        return `[#${this.key}: ${this.value}]`
    }
}
```

然后我们需要声明一些字典所能使用的方法：

`set(key,value)`：向字典中添加新元素。如果key存在，那么已存在的value会被新的值覆盖

`get(key)`：通过以键名作为参数查找特定数值并返回

`remove(key)`：通过使用键名作为参数从字典中移除键名对应的数据值

`has(key)`：如果某个键存在于字典中，返回true，否则返回false

`keyValues()`：将字典中所有[键,值]对返回

`values()`：将字典所包含的所有数值以数组形式返回

`keys()`：将字典所包含的所有键名以数组形式返回

`clear()`：删除字典中所有值

`size()`：返回字典所包含值的数量

`isEmpty()`：判断是否是空字典

`forEach(callback)`：迭代字典中所有的键值对。callback有两个参数：key和value。该方法可以在回调函数返回false时被终止

我们来完善一下上面方法的代码：

```javascript
/**
 * Created by yh on 2021/9/26
 */
function defaultToString(key) {
    if (key === null) {
        return 'NULL'
    } else if (key === undefined) {
        return 'UNDEFINED';
    } else if (typeof key === 'string' || key instanceof String) {
        return `${key}`;
    }
    return key.toString();
}

class ValuePairs {
    constructor(key, value) {
        this.key = key;
        this.value = value;
    }

    toString() {
        return `[#${this.key}: ${this.value}]`
    }
}

export default class Dictionary {
    constructor(toStringFn = defaultToString) {
        this._toStringFn = toStringFn;
        this.table = {};
    }

    /**
     * 向字典中添加新元素。如果key存在，那么已存在的value会被新的值覆盖
     * @param key
     * @param value
     */
    set(key, value) {
        let tableKey = this._toStringFn(key);
        this.table[tableKey] = new ValuePairs(key, value);
    }

    /**
     * 通过以键名作为参数查找特定数值并返回
     * @param key
     * @return {*}
     */
    get(key) {
        let valuePairs = this.table[this._toStringFn(key)];//获取所有[键，值]队类
        if (valuePairs) {
            return valuePairs.value;
        }
        return undefined;
    }

    /**
     * 通过使用键名作为参数从字典中移除键名对应的数据值
     * @param key
     * @return {boolean}
     */
    remove(key) {
        if (this.has(key)) {
            delete this.table[this._toStringFn(key)];
            return true;
        }
        return false;
    }

    /**
     * 如果某个键存在于字典中，返回true，否则返回false
     * @param key
     * @return {boolean}
     */
    has(key) {
        return Object.prototype.hasOwnProperty.call(this.table, this._toStringFn(key));
    }


    /**
     * 将字典中所有[键,值]对返回
     * @return {[]}
     */
    keyValues() {
        let valuePairs = [];
        for (let key in this.table) {
            if (this.has(key)) {
                valuePairs.push(this.table[key]);
            }
        }
        return valuePairs;
    }

    /**
     * 将字典所包含的所有数值以数组形式返回
     */
    values() {
        return this.keyValues().map(valuePair => valuePair.value);
    }

    /**
     * 将字典所包含的所有键名以数组形式返回
     * @return {string[]}
     */
    keys() {
        return this.keyValues().map(valuePair => valuePair.key);
    }

    /**
     * 删除字典中所有值
     */
    clear() {
        this.table = {};
    }

    /**
     * 返回字典所包含值的数量
     * @return {number}
     */
    size() {
        return Object.keys(this.table).length;
    }

    /**
     * 判断是否是空字典
     * @return {boolean}
     */
    isEmpty() {
        return this.size() === 0;
    }


    /**
     * 矢代字典中所有的键值对。callback有两个参数：key和value。该方法可以在回调函数返回false时被终止
     * @param callback
     */
    forEach(callback) {
        if (typeof callback !== 'function') return;
        let valuePairs = this.keyValues();
        for (let i = 0; i < valuePairs.length; i++) {
            let result = callback(valuePairs[i].key, valuePairs[i].value);
            if (result === false) {
                break;
            }
        }
    }

    toString() {
        if (this.isEmpty()) {
            return '';
        }
        let valuePairs = this.keyValues();
        let objString = `${valuePairs[0].toString()}`
        for (let i = 1; i < valuePairs.length; i++) {
            objString = `${objString},${valuePairs[i].toString()}`
        }
        return objString;
    }
}
```

### 7.1.2 使用Dictionary类：

```JavaScript
let dictionary = new Dictionary();
dictionary.set("张三","Lu0@email.net");
dictionary.set("李四","UGFuT70lwe@email.com");

console.log(dictionary.size());
console.log(dictionary.toString());

console.log(dictionary.has("李四"));
console.log(dictionary.get('李四'));

dictionary.remove("李四");
dictionary.set("John","kGR2y@email.com")

console.log(dictionary.keys());
console.log(dictionary.values());
```

运行结果如下：

![image-20210929140429664](E:\node\JavaScript\Dictionary类运行结果1.png)

我们再试试`forEach()`方法来迭代字典类元元素

```JavaScript
dictionary.forEach((key,value) => {
    console.log(`${key}的电子邮箱号码为：${value}`);
});
```

运行结果为：

![image-20210929140546700](E:\node\JavaScript\Dictionary类运行结果2.png)



## 7.2 散列表

> 散列表（或者叫哈希表），是一种改进的Dictionary，它将key通过一个固定的算法（散列函数或哈希函数）得出一个数字，然后将Dictionary中key所对应的value存放到这个数字所对应的数组下标所包含的存储空间中。在原始的Dictionary中，如果要查找某个key所对应的value，我们需要遍历整个字典。为了提高查询的效率，我们将key对应的value保存到数组里，只要key不变，使用相同的散列函数计算出来的数字就是固定的，于是就可以很快地在数组中找到你想要查找的value。

![散列表示意图](E:\node\JavaScript\散列表示意图.png)



散列表有一些在计算机科学中应用的例子。因为它是字典的一种实现，所以可以用作关联数组。它也可以用来对数据库进行索引。当我们在关系型数据库中创建一个新的表时，一个不错的做法就是同时创建一个索引来更快地查询到记录的key。在这情况下，散列表可以用来保存键和对表中记录的引用。另一个很常见的应用是使用散列表来表现对象。JavaScript语言内部就是使用散列表来表示每个对象。此时，对象的每个属性和方法（属性）被存储为key对象类型，每个key指向对应的对象成员。

接下来我们来使用最常见的散列函数-**lose lose 散列函数**，方法是简单地将每个键中的每个字母的ASCII值相加得到散列值，如下图所示：

![lose lose 散列函数](E:\node\JavaScript\lose lose 散列函数.png)



### 7.2.1 创建散列表

```JavaScript
function defaultToString(key) {
    if (key === null) {
        return 'NULL'
    } else if (key === undefined) {
        return 'UNDEFINED';
    } else if (typeof key === 'string' || key instanceof String) {
        return `${key}`;
    }
    return key.toString();
}

class ValuePairs {
    constructor(key, value) {
        this.key = key;
        this.value = value;
    }

    toString() {
        return `[#${this.key}: ${this.value}]`
    }
}

export default class HashTable {
    constructor(toStringFn = defaultToString) {
        this._toStringFn = toStringFn;
        this.table = {};
    }
}
```

然后我们给类添加一些基本方法：

`put(key,value)`：向散列表增加一个新的项（也能更新散列列表）

`get(key)`：返回根据键名检索到的特定的值

`remove(key)`：根据键名从散列表中移除值

`has(key)`：如果某个键存在于字典中，返回true，否则返回false

`keyValues()`：将散列表中所有[键,值]对返回

`values()`：将散列表所包含的所有数值以数组形式返回

`keys()`：将散列表所包含的所有键名以数组形式返回

`clear()`：删除字典中所有值

`size()`：返回散列表所包含值的数量

`isEmpty()`：判断是否是空散列表

`forEach(callback)`：迭代散列表中所有的键值对。callback有两个参数：key和value。该方法可以在回调函数返回false时被终止

**创建散列函数**

在实现这三个方法之前，我们要实现的第一个方法是散列函数，代码如下：

```javascript
loseLoseHashCode(key) {
    //如果是一个数则直接返回
    if (typeof key === 'number') {
        return key;
    }
    // 把key转为一个字符串
    const tableKey = this._toStringFn(key);
    let hash = 0;   // 散列值的总和
    for (let i = 0; i < tableKey.length; i++) {
        // 从ASCII表中查到的每一个字符对应的ASCII值加到hash变量中。
        hash += tableKey.charCodeAt(i);
    }
    // 为了得到比较小的数值，我们会使用hash值和任意数做除法的余数，这样可以规避操作数超过数值变量变大表示范围的风险
    return hash % 37;
}
```

完整代码：

```javascript
function defaultToString(key) {
    if (key === null) {
        return 'NULL'
    } else if (key === undefined) {
        return 'UNDEFINED';
    } else if (typeof key === 'string' || key instanceof String) {
        return `${key}`;
    }
    return key.toString();
}

class ValuePairs {
    constructor(key, value) {
        this.key = key;
        this.value = value;
    }

    toString() {
        return `[#${this.key}: ${this.value}]`
    }
}

export default class HashTable {
    constructor(toStringFn = defaultToString) {
        this._toStringFn = toStringFn;
        this.table = {};
    }

    loseLoseHashCode(key) {
        //如果是一个数则直接返回
        if (typeof key === 'number') {
            return key;
        }
        // 把key转为一个字符串
        const tableKey = this._toStringFn(key);
        let hash = 0;   // 散列值的总和
        for (let i = 0; i < tableKey.length; i++) {
            // 从ASCII表中查到的每一个字符对应的ASCII值加到hash变量中。
            hash += tableKey.charCodeAt(i);
        }
        // 为了得到比较小的数值，我们会使用hash值和任意数做除法的余数，这样可以规避操作数超过数值变量变大表示范围的风险
        return hash % 37;
    }

    hashCode(key) {
        return this.loseLoseHashCode(key);
    }

    /**
     * 向散列表增加一个新的项（也能更新散列列表）
     * @param key
     * @param value
     */
    put(key, value) {
        if (key === null && value === null) return false;
        let position = this.hashCode(key);  
        this.table[position] = new ValuePairs(key, value);
        return true;
    }

    /**
     * 根据键名从散列表中移除值
     * @param key
     */
    remove(key) {
        let hash = this.hashCode(key);
        let valuePairs = this.table[hash];
        if (valuePairs != null) {
            delete this.table[hash];
            return true;
        }
        return false;
    }

    /**
     * 返回根据键名检索到的特定的值
     * @param key
     */
    get(key) {
        let valuePairs = this.table[this.hashCode(key)];
        return valuePairs == null ? undefined : valuePairs.value;
    }

    /**
     * 如果某个键存在于散列表中，返回true，否则返回false
     * @param key
     * @return {boolean}
     */
    has(key) {
        return Object.prototype.hasOwnProperty.call(this.table, this.hashCode(key));
    }

    /**
     * 将散列表中所有[键,值]对返回
     * @return {[]}
     */
    keyValues() {
        let valuePairs = [];
        for (let key in this.table) {
            if (this.has(key)) {
                valuePairs.push(this.table[key]);
            }
        }
        return valuePairs;
    }

    /**
     * 将散列表所包含的所有数值以数组形式返回
     */
    values() {
        return this.keyValues().map(valuePair => valuePair.value);
    }

    /**
     * 将散列表所包含的所有键名以数组形式返回
     * @return {string[]}
     */
    keys() {
        return this.keyValues().map(valuePair => valuePair.key);
    }

    /**
     * 删除散列表中所有值
     */
    clear() {
        this.table = {};
    }

    /**
     * 返回散列表所包含值的数量
     * @return {number}
     */
    size() {
        return Object.keys(this.table).length;
    }

    /**
     * 判断是否是空散列表
     * @return {boolean}
     */
    isEmpty() {
        return this.size() === 0;
    }


    /**
     * 矢代散列表中所有的键值对。callback有两个参数：key和value。该方法可以在回调函数返回false时被终止
     * @param callback
     */
    forEach(callback) {
        if (typeof callback !== 'function') return;
        let valuePairs = this.keyValues();
        for (let i = 0; i < valuePairs.length; i++) {
            let result = callback(valuePairs[i].key, valuePairs[i].value);
            if (result === false) {
                break;
            }
        }
    }

    toString() {
        if (this.isEmpty()) {
            return '';
        }
        let keys = Object.keys(this.table);
        let objString = `{${keys[0]} => ${this.table[keys[0]].toString()}}`
        for (let i = 1; i < keys.length; i++) {
            objString = `${objString},{${keys[i]} => ${this.table[keys[i]].toString()}}`
        }
        return objString;
    }


}
```

### 7.2.2 使用HashTable类

我们来写几个测试用例去测试一下HashTable类：

```javascript
let hash = new HashTable();
hash.put('Gandalf', 'gandalf@email.com');
hash.put('John', 'john@email.com');
hash.put('Jack', 'jack@email.com');

console.log(hash.toString())

console.log(hash.get('John'));
console.log(hash.get('Mane'));

hash.remove('John');
console.log(hash.get('John'));
```

运行结果：

![image-20210930234116466](E:\node\JavaScript\HashTable测试用例.png)

### 7.2.4 处理散列表中的冲突

有时候，一些键会有相同的散列值。不同的值在散列表中对应相同位置的时候，我们称其为**冲突**。例如我们看看下面的代码会得到怎么样的输出结果：

```javascript
let hash = new HashTable();

hash.put('Gandalf', 'gandalf@email.com');
hash.put('John', 'john@email.com');
hash.put('Tyrion', 'tyrion@email.com');
hash.put('Aaron', 'aaron@email.com');
hash.put('Donnie', 'donnie@email.com');
hash.put('Ana', 'ana@email.com');
hash.put('Jamie', 'jamie@email.com');
hash.put('Sue', 'sue@email.com');
hash.put('Mindy', 'mindy@email.com');
hash.put('Paul', 'paul@email.com');
hash.put('Nathan', 'nathan@email.com');
```

通过对每个提到的名字调用`hash.hashCode()`方法，输出结果如下：

![image-20210930234839859](E:\node\JavaScript\散列表冲突测试用例结果.png)

从结果中可以看到，尽管有些keys不同，但是通过我们提供的散列函数居然得到了相同的hash值，这显然违背了我们的设计原则。在哈希表中，这个叫做散列冲突，为了得到一个可靠的哈希表，我们必须尽可能地避免散列冲突。那如何避免这种冲突呢？这里介绍两种解决冲突的方法：**分离链接**和**线性探查**。

### 7.2.5 分离连接

**分离连接**法包括为散列表的每一个位置创建一个链表并将元素存储在里面。它是解决冲突的最简单的方法，但是在`HashTable`实例之外还需要额外的存储空间。

如图所示（为了简化，图中的值被省略了）：

![分离连接示意图](E:\node\JavaScript\分离连接示意图.png)



新的采用了分离链接的`HashTableSeparateChaining`类可以继承自前面的`HashTable`类，完整的代码如下：

```javascript
import HashTable from "./HashTable.js";
import LinkedList from "./LinkedList.js";

class ValuePairs {
    constructor(key, value) {
        this.key = key;
        this.value = value;
    }

    toString() {
        return `[#${this.key}: ${this.value}]`
    }
}

export default class HashTableSeparateChaining extends HashTable {
    put(key, value) {
        if (key == null && value == null) return false;
        const position = this.hashCode(key);
        // 如果当前位置为空，那就new一个链表进行赋值
        if (this.table[position] == null) {
            this.table[position] = new LinkedList();
        }
        // 往链表中添加元素
        this.table[position].push(new ValuePairs(key, value));
        return true;
    }

    get(key) {
        const position = this.hashCode(key);
        const linkedList = this.table[position];
        // 验证在特定的位置是否有元素存在，且链表不为空
        if (linkedList != null && !linkedList.isEmpty()) {
            let current = linkedList.getHead();
            // 迭代链表元素寻找匹配key
            while (current != null) {
                if (current.element.key === key) {
                    return current.element.value;
                }
                current = current.next;
            }
        }
        return undefined;
    }

    remove(key) {
        const position = this.hashCode(key);
        const linkedList = this.table[position];
        // 验证在特定的位置是否有元素存在，且链表不为空
        if (linkedList != null && !linkedList.isEmpty()) {
            let current = linkedList.getHead();
            // 迭代链表元素寻找匹配key
            while (current != null) {
                if (current.element.key === key) {
                    linkedList.remove(current.element);
                    if (linkedList.isEmpty()) {
                        delete this.table[position];
                    }
                    return true;
                }
                current = current.next;
            }
        }
        return false;
    }

    size() {
        return this.keyValues().length;
    }
    
    keyValues() {
        let valuePairs = [];
        for (let i in this.table) {
            let linkedList = this.table[i];
            if (linkedList === undefined) continue;
            let current = linkedList.getHead();
            while (current) {
                valuePairs.push(current.element)
                current = current.next;
            }
        }
        return valuePairs;
    }

    toString() {
        let objString = "";
        for (let i in this.table) {
            let linkedList = this.table[i];
            if (linkedList === undefined) continue;
            objString += `${i}: `;
            let current = linkedList.getHead();
            while (current) {
                objString += current.element.toString();
                current = current.next;
                if (current) objString += ', ';
            }
            objString += '\r\n';
        }
        return objString;
    }

}
```

下面是`HashTableSeparateChaining`类的测试用例及结果：

```javascript
let hash = new HashTableSeparateChaining();
hash.put('Gandalf', 'gandalf@email.com');
hash.put('John', 'john@email.com');
hash.put('Tyrion', 'tyrion@email.com');
hash.put('Aaron', 'aaron@email.com');
hash.put('Donnie', 'donnie@email.com');
hash.put('Ana', 'ana@email.com');
hash.put('Jamie', 'jamie@email.com');
hash.put('Sue', 'sue@email.com');
hash.put('Mindy', 'mindy@email.com');
hash.put('Paul', 'paul@email.com');
hash.put('Nathan', 'nathan@email.com');

console.log(hash.toString());
console.log(`size: ${hash.size()}`);
console.log(hash.get('John'));

console.log(hash.remove('Ana'));
console.log(hash.remove('John'));
console.log(hash.toString());
```

![分离连接测试用例](E:\node\JavaScript\分离连接测试用例.png)

### 7.2.6 线性探查

​		另一种解决冲突的方法是线性探查。之所以称作线性，是因为它处理冲突的方法是将元素直接存储到表中，而不是在单独的数据结构中。

​		当想向表中某个位置添加一个新元素的时候，如果索引为position的位置已经被占据了，就尝试`position + 1`的位置。如果`position + 1`的位置也被占据了，就尝试`position + 2`的位置，以此类推，直到散列表中找到一个空闲的位置。

下图展示了这个过程：



![线性探查示意图](E:\node\JavaScript\线性探查示意图.png)

​		当我们从散列表中移除一个键值对的时候，仅仅在所实现位置移除是不够的。如果我们只是移除了元素，就可能在查找有相同的hash（位置）的其它元素时找到一个空的位置，这个会导致算法出现问题。

​		线性探查技术分为两种。第一种是**软删除**方法。我们使用一个特殊的值标记来标识键值对被删除了，而不是真的删除它。经过一段时间，散列表被操作过后，我们会得到一个标记了若干删除位置的散列表。这回逐渐降低散列表的效率，因为搜索键值会随时间变得更慢。能快速访问并找到一个键是我们使用散列表的重要原因。下图展示了这个过程：

![线性探查(软删除)示意图](E:\node\JavaScript\线性探查(软删除)示意图.png)

​		第二种方法需要检验是否有必要将一个或多个元素移动到之前的位置。当搜索一个键时，这种方法可以避免找到一个空位置。如果移动元素是必要的，我们就需要在散列表中挪动键值对。下图展现了这个过程：

![线性探查示（删除移动元素）意图](E:\node\JavaScript\线性探查示（删除移动元素）意图.png)



两种方法都各有各的优缺点，我们来实现一下第二种方法：

```javascript
import HashTable, {ValuePairs} from "./HashTable.js";


export default class HashTableLinearProbing extends HashTable {
    put(key, value) {
        if (key == null && value == null) return false;
        const position = this.hashCode(key);
        if (this.table[position] == null) {
            this.table[position] = new ValuePairs(key, value);
        } else {
            let index = position + 1;
            while (this.table[index] != null) {
                index++;
            }
            this.table[index] = new ValuePairs(key, value);
        }
        return true;
    }

    get(key) {
        const position = this.hashCode(key);
        if (this.table[position] != null) {
            if (this.table[position].key === key) {
                return this.table[position].value;
            } else {
                let index = position + 1;
                while (this.table[index] != null && this.table[index].key !== key) {
                    index++;
                }
                if (this.table[index] != null && this.table[index].key === key) {
                    return this.table[index].value;
                }
            }
        }
        return undefined;
    }

    remove(key) {
        const position = this.hashCode(key);
        if (this.table[position] != null) {
            if (this.table[position].key === key) {
                delete this.table[position];
                this._verifyRemoveSideEffect(key, position);
                return true;
            }
            let index = position + 1;
            while (this.table[index] != null && this.table[index].key !== key) {
                index++;
            }
            if (this.table[index] != null && this.table[index].key === key) {
                delete this.table[index];
                this._verifyRemoveSideEffect(key, index);
                return true;
            }
        }
        return false;
    }

    _verifyRemoveSideEffect(key, removedPosition) {
        const hash = this.hashCode(key);
        let index = removedPosition + 1;
        while (this.table[index] != null) {
            const posHash = this.hashCode(this.table[index].key);
            if (posHash <= hash || posHash <= removedPosition) {
                this.table[removedPosition] = this.table[index];
                delete this.table[index];
                removedPosition = index;
            }
            index++;
        }
    }
}
```

我们来写一下测试用例：

```javascript
let hash = new HashTableLinearProbing();
hash.put('Ygritte', 'ygritte@email.com');
hash.put('Jonathan', 'jonathan@email.com');
hash.put('Jamie', 'jamie@email.com');
hash.put('Jack', 'jack@email.com');
hash.put('Jasmine', 'jasmine@email.com');
hash.put('Jake', 'jake@email.com');
hash.put('Nathan', 'nathan@email.com');
hash.put('Athelstan', 'athelstan@email.com');
hash.put('Sue', 'sue@email.com');
hash.put('Aethelwulf', 'aethelwulf@email.com');
hash.put('Sargeras', 'sargeras@email.com');

console.log(hash.toString());

hash.remove('Jonathan');

console.log('删除Jonathan后：')
console.log(hash.toString());
```

运行结果如下：

![线性探查测试用例](E:\node\JavaScript\线性探查测试用例.png)

# 8 树

树是一种分层的抽象模型。现实生活中最常见的树的例子就是家谱，或是公司的组织架构图，如下图所示：![Image](https://resources.iyanghong.cn/users/10000/article/60/1635555929-41FC69143E3A03CD39B2F910270B3A35.png)


### 树的相关术语

一个树结构包含一系列存在父子关系的节点。每个节点都有一个父节点（除了顶层的第一个节点）以及零个或多个子节点。
![Image](https://resources.iyanghong.cn/users/10000/article/60/1635558243-0041B311851898E0038414692585CB01.png)
位于树顶部的节点叫作根节点。它没有父节点。树种的每个元素叫做节点，节点分为内部节点和外部节点。至少有一个子节点的节点称为内部节点。**没有子元素的节点称为外部节点或叶节点**
一个节点可以有祖先和后代，一个节点（除了根节点）的祖先包括父节点、祖父节点等。一个节点的后代包括子节点、孙节点等
有关树的另一个术语是**子树**。子树由节点和它的后代构成。
节点的一个属性是深度，节点的深度取决于它的祖先节点数量。
树的高度取决于所有节点深度的最大值。

### 8.1 二叉树和二叉搜索树
二叉树种的节点最多只能有两个子节点：一个是左侧子节点。另一个是右侧子节点。这个定义有助于我们写出更搞笑地在树种插入、查找、删除节点的算法。
二叉搜索树（BST）是二叉树的一种，但是只允许你在左侧节点存储（比父节点）小的值，在右侧节点存储（比父节点）大的值。

#### 8.1.1 创建BinarySearchTree类

我们先来创建Node类来表示二叉搜索树种的每个节点，代码如下：

```javascript
class Node {
    constructor(value) {
        this.value = value; // 节点值
        this.left = null;   // 左侧子节点引用
        this.right = null;  // 右侧子节点引用
    }
}
```

下图展现了二叉搜索树数据结构的组织方式。

![二叉搜索树结构示意图](E:\node\JavaScript\二叉搜索树结构示意图.png)

和链表一样，我们将通过指针来表示节点之间的关系。在双向链表中，每个节点包含两个指针，一个指向下一个节点，一个指向上一个节点。对于树，使用同样的方式（也使用两个指针），但是一个指向左侧节点，一个指向右侧节点。
下面我们来声明`BinarySearchTree`类的基本结构

```javascript
export default class BinarySearchTree {
    constructor() {
        this.root = null; // 根节点
    }
}
```

然后我们需要实现一些方法：

`insert(value)`：向树中插入一个新的键。

`search(value)`：在树中查找一个键。如果节点存在，则返回true；如果不存在，则返回false。

`inOrderTraverse()`：通过中序遍历方式，遍历所有节点。

`preOrderTraverse()`：通过先序遍历方式，遍历所有节点。

`postOrderTraverse()`：通过后序遍历方式，遍历所有节点。

`min()`：返回树中最小的值。

`max()`：返回树中最大的值。

`remove(value)`：从树中移除某个键

#### 8.1.2 向二叉搜索树中插入一个键

我们先来写插入方法的主体方法：

```javascript
insert(value) {
    if (this.root == null) {
        //如果树为空，则直接添加根节点
        this.root = new Node(value);
    } else {
        //否则使用递归寻找位置插入
        this.insertNode(this.root, value)
    }
}
```

我们来写一下递归用到的辅助方法：

```javascript
insertNode(node, value) {
    //判断大小，小则往左边插入，大则往右边插入
    if (value < node.value) {
        if (node.left == null) {
            node.left = new Node(value);
        } else {
            //重新递归调用
            this.insertNode(node.left, value);
        }
    } else {
        if (node.right == null) {
            node.right = new Node(value);
        } else {
            this.insertNode(node.right, value);
        }
    }
}
```

我们来尝试用一下`insert()`

```javascript
let bst = new BinarySearchTree();

bst.insert(11);
bst.insert(7);
bst.insert(15);
bst.insert(5);
bst.insert(3);
bst.insert(9);
bst.insert(8);
bst.insert(10);
bst.insert(13);
bst.insert(12);
bst.insert(14);
bst.insert(20);
bst.insert(18);
bst.insert(25);
```

上面就会创建如图所示的树结构：

![二叉搜索树插入示意图(1)](E:\node\JavaScript\二叉搜索树插入示意图(1).png)

同时我们想要插入一个值为6的，执行以下代码：

```javascript
bst.insert(6);
```

运行示意图如下：

![二叉搜索树插入示意图(2)](E:\node\JavaScript\二叉搜索树插入示意图(2).png)

### 8.2 树的遍历

遍历一棵树是指访问树的每个节点对他们进行某种操作的过程。但是我们应该怎么去做呢？应该从树的顶端还是低端开始呢？从左开始还是右开始呢？访问树的所有节点有三种方式：中序、先序和后序

#### 8.2.1 中序遍历

中序遍历是一种以上行顺序访问BST所有节点的遍历方式，也就是从最小到最大的顺序访问所有节点。中序遍历的一种应用就是对数进行排序操作。

我们先来写主方法：

```javascript
inOrderTraverse(callback) {
    this.inOrderTraverseNode(this.root, callback)
}
```

`inOrderTraverse`方法接收一个回调函数作为参数。回调函数用来定义我们对遍历到每个节点进行的操作（这也叫做访问者模式）。由于我们需要用到递归用到的辅助方法，下面来写：

```javascript
inOrderTraverseNode(node, callback) {
    if (node != null) { // 先检查传入的node是否为null，这就是停止递归继续的判断条件。
        this.inOrderTraverseNode(node.left, callback);
        callback(node.value);
        this.inOrderTraverseNode(node.right, callback)
    }
}
```

我们来用一下上面的方法：

```javascript
bst.inOrderTraverse((value) => console.log(value))
```

下面的结果会在控制台上输出（每个数将会输出在不同的行上）

3  5  6  7  8  9  10  11  12  13  14  15  18  20  25

下图绘制了`inOrderTraverse`方法的访问路径。

![二叉搜索树中序遍历](E:\node\JavaScript\二叉搜索树中序遍历.png)

#### 8.2.2 先序遍历

先序遍历是以优先于后代节点的顺序访问每个节点的。先序遍历的一种应用是打印一个结构化的文档：

下面我们来看实现：

```javascript
preOrderTraverse(callback) {
    this.preOrderTraverseNode(this.root, callback);
}

preOrderTraverseNode(node, callback) {
    if (node != null) {
        callback(node.value);
        this.preOrderTraverseNode(node.left, callback);
        this.preOrderTraverseNode(node.right, callback);
    }
}
```

下面描绘了`preOrderTraverse`方法的路径：

![二叉搜索树先序遍历](E:\node\JavaScript\二叉搜索树先序遍历.png)

#### 8.2.3 后序遍历

后序遍历则是先访问节点的后代节点，再访问节点本身。后序遍历的一种应用是计算一个目录及其子目录中所有文件占用空间的大小。

我们来看实现：

```javascript
postOrderTraverse(callback) {
    this.postOrderTraverseNode(this.root, callback);
}

postOrderTraverseNode(node, callback) {
    if (node != null) {
        this.preOrderTraverseNode(node.left, callback);
        this.preOrderTraverseNode(node.right, callback);
        callback(node.value);
    }
}
```

下图描绘了`postOrderTraverse`方法的访问路径：

![二叉搜索树后序遍历](E:\node\JavaScript\二叉搜索树后序遍历.png)

### 8.3 搜索树中的值

在树中，有三种经常用到的搜索类型：

- 搜索最小值
- 搜索最大值
- 搜索特点的值

我们依次来看：

#### 8.3.1 搜索最小值和最大值

我们使用下面的树作为示例：

![二叉搜索树搜索最大值和最小值](E:\node\JavaScript\二叉搜索树搜索最大值和最小值.png)

只用眼睛看这张图，你能立刻找到两个最小值和最大值吗？

如果你看一眼树最后一层最左的节点，会发现它的值为3，这是树中最小的值。如果你再看一眼最右端的节点，会发现它的值是25，是这颗树的最大值。

所以我们来实现：

```javascript
/**
 * 寻找最小值
 * @returns {*}
 */
min() {
    return this.minNode(this.root);
}

minNode(node) {
    let current = node;
    while (current != null && current.left != null) {
        current = current.left;
    }
    return current;
}

/**
 * 寻找最大值
 * @returns {*}
 */
max() {
    return this.maxNode(this.root);
}

maxNode(node) {
    let current = node;
    while (current != null && current.right != null) {
        current = current.right;
    }
    return current;
}
```

#### 8.3.2 搜索特定的值

我们依旧用递归的方式去寻找值这个跟插入有些类似：

```javascript
search(value) {
    return this.searchNode(this.root, value);
}

searchNode(node, value) {
    if (node == null) {
        return false;
    }
    if (value < node.value) {
        return this.searchNode(node.left, value);
    } else if (node.value > value) {
        return this.searchNode(node.right, value);
    } else {
        return true;
    }
}
```

我们可以用过以下代码来测试这个方法：

```javascript
console.log(bst.search(1) ? '找到1' : '找不到1');
console.log(bst.search(8) ? '找到8' : '找不到8');
```

输出结果如下：

```cmd
找不到1
找到8
```

### 8.4 移除一个节点

我们来为二叉搜索树来实现最后一个方法，也就是`remove`。这个方法比较复杂我们来慢慢解析

我们通过画图来比较直观的呈现过程：

**1、移除一个叶节点**

![二叉搜索树移除叶节点](E:\node\JavaScript\二叉搜索树移除叶节点.png)

**2、移除有一个左侧或右侧子节点的节点**

![二叉搜索树移除有一个左侧或右侧子节点的节点](E:\node\JavaScript\二叉搜索树移除有一个左侧或右侧子节点的节点.png)

**3、移除有两个子节点的节点**

![二叉搜索树移除有两个子节点的节点](E:\node\JavaScript\二叉搜索树移除有两个子节点的节点.png)

接下来我们用代码实现：主方法：

```javascript
remove(value) {
    this.root = this.removeNode(this.root, value);
}
```

我们再来看看递归辅助方法的实现：

```javascript
removeNode(node, value) {
    if (node == null) {
        return null;
    }
    if (value < node.value) {
        node.left = this.removeNode(node.left, value);
        return node;
    } else if (value > node.value) {
        node.right = this.removeNode(node.right, value);
        return node;
    } else {
        //键等于key
        //第一种情况：左右节点都为空
        if (node.left == null && node.right == null) {
            node = null;
            return node;
        }
        //第二种情况：有一个子节点
        if (node.left == null) {
            node = node.right;
            return node;
        } else if (node.right == null) {
            node = node.left;
            return node;
        }
        //第三种情况：有两个子节点
        const aux = this.minNode(node.right);
        node.kty = aux.value;
        node.right = this.removeNode(node.right, aux.value);
        return node;

    }
}
```

### 8.4 自平衡树

BST树会存在一个问题：取决于你添加的节点数，树的一条边可能会非常深；也就是说树的一条分支会有很多层，而其它却有几层，如下图所示

![BST树深度差异](E:\node\JavaScript\BST树深度差异.png)

这会在需要的某条边上添加、移除和搜索某个节点时引起一些性能问题。为了解决这个问题，我们需要去平衡它的高度。

#### 8.4.1 自平衡树-AVL树

AVL树是一种自平衡树。添加或移除节点时，AVL树会尝试保持自平衡，任意一个节点（不论深度）的左子树和右子树高度最多相差1.添加或移除节点时,AVL树会尽可能尝试转换为完全树。

我们开始创建`AVLTree`类：

```javascript
export default class AVLTree extends BinarySearchTree {
    constructor() {
        super();
        this.root = null;
    }
}
```

AVL树也是一个BST，我们继承`BinarySearchTree`类，只需要重写`insert`、`insertNode`和`removeNode`方法。

在AVL树中插入或移除节点和BST完全相同。然而，AVL树的不同之处在于我们需要检验它的平衡因子，如果需要，会将其逻辑应用于树的自平衡。

**1.节点的高度和平衡因子**

我们知道，节点的高度是从节点到其任意子节点的边的最大值。如图所示：

![节点高度](E:\node\JavaScript\节点高度.png)

所以我们需要一个计算节点高度的方法：

```javascript
getNodeDeep(node) {
    if (node == null) {
        return -1;
    }
    return Math.max(this.getNodeDeep(node.left), this.getNodeDeep(node.right)) + 1;
}
```

**结点的平衡因子 = 左子树的高度 - 右子树的高度**

插入和删除操作都会导致AVL树的自我调整（自我平衡），使得所有结点的平衡因子保持为+1、-1或0。

当子树的根结点的平衡因子为+1时，它是**左倾斜**的（left-heavy)。

当子树的根结点的平衡因子为 -1时，它是**右倾斜**的(right-heavy)。

**一颗子树的根结点的平衡因子就代表该子树的平衡性**。

计算一个节点的平衡因子方法：

```javascript
const BalanceFactor = {
    UNBALANCED_RIGHT: 1,
    SLIGHTLY_UNBALANCED_RIGHT: 2,
    BALANCED: 3,
    SLIGHTLY_UNBALANCED_LEFT: 4,
    UNBALANCED_LEFT: 5
}
getBalanceFactor(node) {
    const heightDifference = this.getNodeDeep(node.left) - this.getNodeDeep(node.right); //左子树的高度 - 右子树的高度
    switch (heightDifference) {
        case -2:
            return BalanceFactor.UNBALANCED_RIGHT;
        case -1:
            return BalanceFactor.SLIGHTLY_UNBALANCED_RIGHT;
        case 1:
            return BalanceFactor.SLIGHTLY_UNBALANCED_LEFT;
        case 2:
            return BalanceFactor.UNBALANCED_LEFT;
        default:
            return BalanceFactor.BALANCED;
    }
}
```

**保持所有子树几乎都处于平衡状态，AVL树在总体上就能够基本保持平衡**。

**2.平衡操作-AVL旋转**

在对AVL树进行添加或移除节点后，我们要计算节点的高度平验证树是否需要旋转。分为四种场景：

- 左-左（LL）：向右的单旋转
- 右右（RR）：向左的单旋转
- 左-右（LR）：向右的双旋转（先LL旋转，再RR旋转）
- 右-左（RL）：向左的双旋转（先RR旋转，再LL旋转）

