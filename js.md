## 待整理

### 全局对象

浏览器的全局对象-window，就是一个哈希表，有很多属性，window的属性就是全局变量

```JavaScript
window 的属性
window.alert();
window.prompt();
window.comfirm();
window.console.log();
window.console.dir();
window.document();
window.document.createElement();
window.document.getElementById();
```

ECMAScript 规定全局对象叫做 global

```js
global.parseInt();
global.parseFloat();
global.Number();
global.String();
global.Boolean();
global.Object();
```

`window.xxx`

```JavaScript
(window.)history.back();// 等同于点击浏览器回退按钮
history.go(-1);// 等同于 history.back();

```

### 公用属性

[待修改]
即，继承自原型对象，原型链公用的属性。
`对象.__proto__`储存该对象的原型对象内存地址
并通过`对象.__proto__ = 原型对象`这一原型链使用

### js 添加 css 代码

```js
var styles = `

.sidebar__inner {
    width: 50px;
}

`
var styleSheet = document.createElement("style")
styleSheet.innerText = styles
document.head.appendChild(styleSheet)

```

### 鼠标事件


**鼠标点击**相关的有四个事件。

- `click`：按下鼠标（通常是按下主按钮）时触发。
- `dblclick`：在同一个元素上双击鼠标时触发。
- `mousedown`：按下鼠标键时触发。
- `mouseup`：释放按下的鼠标键时触发。

`click`事件可以看成是两个事件组成的：用户在同一个位置先触发`mousedown`，再触发`mouseup`。因此，触发顺序是，`mousedown`首先触发，`mouseup`接着触发，`click`最后触发。

双击时，`dblclick`事件则会在`mousedown`、`mouseup`、`click`之后触发。

**鼠标移动**相关的有五个事件。

- `mousemove`：当鼠标在一个节点内部移动时触发。当鼠标持续移动时，该事件会连续触发。为了避免性能问题，建议对该事件的监听函数做一些限定，比如限定一段时间内只能运行一次。
- `mouseenter`：鼠标进入一个节点时触发，进入子节点不会触发这个事件（详见后文）。
- `mouseover`：鼠标进入一个节点时触发，进入子节点会再一次触发这个事件（详见后文）。
- `mouseout`：鼠标离开一个节点时触发，离开父节点也会触发这个事件（详见后文）。
- `mouseleave`：鼠标离开一个节点时触发，离开父节点不会触发这个事件（详见后文）。

`mouseover`事件和`mouseenter`事件，都是鼠标进入一个节点时触发。两者的区别是，`mouseenter`事件只触发一次，而只要鼠标在节点内部移动，`mouseover`事件会在子节点上触发多次。

### animation 实现动画-css3

[refer_to_juejin-css动画之animation](https://juejin.cn/post/7031932651686756382)

`animation-name`
动画名称和`@keyframes`的名称需一致，`@keyframes`定义的动画效果就能应用在使用了`animation-name`的 dom 元素身上。
`animation-duration`
动画的时长。单位可以是秒或者毫秒。默认是0，即没有动画。

`animation-timing-function`
动画完成的速度。有以下值：

**cubic-bezier()**：三次贝塞尔曲线。，以下是其演化的关键字

- **ease**  默认值，动画开始缓慢，中间加速，结束缓慢。

- **linear** 动画会以恒定的速度从初始状态过渡到结束状态。

- **ease-in** 动画开始时缓慢，然后逐步加速，最后保持一定的速度直到动画停止。

- **ease-out** 动画开始很快，然后逐渐减慢。

- **ease-in-out** 使用这个定时函数，动画开始的行为类似于 ease-in 函数，动画结束时的行为类似于 ease-out函数，即先慢后快再慢。

**steps()** 函数包含两个参数，第一个为阶梯数，第二个参数为函数的方向 start｜end：
```
start: 表示开始时进行一次阶跃
end：表示结束时进行一次阶跃
```

- step-start：此关键字表示 `steps(1, start)`。使用这个定时函数，动画会立刻跳转到结束状态，并一直停留在结束状态直到动画结束。

- step-end：此关键字表示定时函数 `steps(1, end)`。使用这个定时函数，动画会一直保持初始状态直到动画结束，然后立刻跳转到结束状态。

`animation-delay`

表示动画延迟多久后开始执行，时间单位的数值，默认为0s

`animation-iteration-count`

表示动画执行的周期次数：

- infinite：无限次数
- 数字：表示周期数，可以为小数，例如1.5，表示一个半周期；

`animation-direction`

表示动画播放的方向，即是否反向播放；

- normal：默认值，每个动画周期都从起点开始
- reverse：每个动画周期都从终点开始
- alternate：动画周期交替运行，反向运行时，动画按步后退，同时，带时间功能的函数也反向，比如，`ease-in` 在反向时成为 `ease-out`。
- alternate-reverse：交替运行，由反向开始；

`animation-fill-mode`

设置动画开始之前和结束之后的样式状态；

- **none**：默认值，在开始之前，结束之后都不应用动画样式。
- **forwords**：动画结束后，元素保持最后一帧的动画状态。
- **backwords**：动画开始之前，元素应用第一帧动画的状态（开始之前，表示动画未开始前的一段时间，例如animation-delay的延迟时间内）。
- **both**：即同时应用 `forwords` 和 `backwords`。动画开始之前，元素应用第一帧，结束之后，应用最后一帧。

如果 `timing-function` 为`steps(1,end)`，`fill-mode` 设置了 `forwords` 才可以看出效果（结合steps函数便可以理解）。

`animation-play-state`

定义一个动画是运行状态还是暂停状态，

- running：动画正在运行。
- paused：动画暂停中。

这个属性有两个用处：

1. 通过查询 `animation-paly-state` 值，可以判断动画在运行还是暂停状态。
2. 通过改变 `animation-paly-state` 的值，可以改变当前动画的状态。

#### 与 animation 相关事件

与 `animation` 设置的动画相关的事件有：

- animationstart
- animationend

## 一

## JavaScript 基础知识

### 交互：alert、prompt 和 confirm

#### alert()

执行后弹出一个带有信息的小窗口(模态窗 modal `意味着用户在处理完窗口前不能与页面的其他部分进行交互`)，并等待用户按下"OK"

```javascript
alert("Hello");
```

#### prompt

prompt 函数将返回用户在 input 框内输入的文本，如果用户取消输入，则返回 null
·
![1.png](/md_data/Image001.png)

```javascript
let age = prompt('How old are you?', 100);

alert(`You are ${age} years old!`); // You are 100 years old!
```

`prompt`函数接收两个参数

```javascript
result = prompt(title,[default]);
title  显示给用户的文本
default  可选的第二个参数，指定 input 框的初始值
[]  语法中的方括号表示该参数的可选的，不是必须的
```

浏览器会显示一个带有文本信息的模态窗，并有 input 框 和 确定/取消按钮
当用户在提示输入栏输入内容，并按确认键，result 获取该内容；
当用户按取消键 或 按 Esc键 取消输入，返回 null 并赋值给 result

#### confirm

`confirm` 函数显示一个带有 `question` 以及确定和取消两个按钮的模态窗口。
点击确定返回 `true`，点击取消返回 `false`。
·
![1.png](/md_data/Image002.png)

```javascript
result = confirm(question);

let isBoss = confirm("Are you the boss?");
alert( isBoss ); // 如果“确定”按钮被按下，则显示 true
```

#### 用户与浏览器交互的特定函数总结

`alert` 显示信息。
 `prompt` 显示信息要求用户输入文本。点击确定返回文本，点击取消或按下 `Esc` 键返回 `null`。
  `confirm` 显示信息等待用户点击确定或取消。点击确定返回 `true`，点击取消或按下 `Esc` 键返回 `false`。
  这些方法都是模态的：它们暂停脚本的执行，并且不允许用户与该页面的其余部分进行交互，直到窗口被解除。 上述所有方法共有两个限制：
  1\. 模态窗口的确切位置由浏览器决定。通常在页面中心。
  2\. 窗口的确切外观也取决于浏览器。我们不能修改它。

### 类型转换

大多数情况下，运算符和函数会自动将赋予它们的值转换为正确的类型。

比如，`alert` 会自动将任何值都转换为字符串以进行显示。算术运算符会将值转换为数字。

在某些情况下，我们需要将值显式地转换为我们期望的类型。
>在本章中，我们不会讨论 object 类型。目前，我们将只学习原始类型。
之后，在我们学习完 object 类型后，我们会在 对象-原始值转换 章节中学习 对象-原始值转换。

#### 字符串转换

当我们需要一个字符串形式的值时，就会进行字符串转换。

比如，`alert(value)` 将 `value` 转换为字符串类型，然后显示这个值。

我们也可以显式地调用 `String(value)` 来将 `value` 转换为字符串类型。

#### 数字型转换

在算术函数和表达式中，会自动进行 number 类型转换。

比如，当把除法 / 用于非 number 类型：

```javascript
alert( "6" / "2" ); // 3, string 类型的值被自动转换成 number 类型后进行计算
```

我们也可以使用 Number(value) 显式地将这个 value 转换为 number 类型。

```javascript
let str = "123";
alert(typeof str); // string

let num = Number(str); // 变成 number 类型 123

alert(typeof num); // number

//如果该字符串不是一个有效的数字，转换的结果会是 NaN
let age = Number("an arbitrary string instead of a number");

alert(age); // NaN，转换失败
```

![1.png](/md_data/Image2022_06_24_16_44.png)

#### 布尔型转换

布尔（boolean）类型转换是最简单的一个。

它发生在逻辑运算中，但是也可以通过调用 Boolean(value) 显式地进行转换。

转换规则如下：

- 直观上为“空”的值（如 `0`、空字符串、`null`、`undefined` 和 `NaN`）将变为 `false`。
- 其他值（" "非空字符串）变成 `true`。

### 基础运算符，数学

### 术语：一元运算符，二元运算符，运算元

### 数学

### 用二元运算符 + 连接字符串

加号 + 用于字符串运算时，会连接字符串

```javascript
let s = "my" + "string";
alert(s); // mystring
//只要二个运算元中任意一个运算元为字符串，另一个也会转化为字符串
alert( '1' + 2 ); // "12"
alert( 2 + '1' ); // "21"

//此时有三个运算元，第三个为字符串，所以会从左到右依次运算，当二元加法运算时出现字符串时，
//才会开始连接字符串
alert(2 + 2 + '1' ); // "41"，不是 "221"
alert('1' + 2 + 2); // "122"，不是 "14"
```

二元 + 是唯一以这种方式处理字符串运算的运算符。
其他算数运算符只对数字起作用，并且总是将其运算元转换为数字。

```javascript
alert( 6 - '2' ); // 4，将 '2' 转换为数字
alert( '6' / '2' ); // 3，将两个运算元都转换为数字
```

### 数字转化，医院运算符 +

加号 + 有两种形式。一种是上面的二元运算符，还有一种是一元运算符。
加号 + 应用于单个值，对数字没有任何作用。
但是如果运算元不是数字，加号 + 则会将其转化为数字。

```javascript
// 对数字无效
let x = 1;
alert( +x ); // 1

let y = -2;
alert( +y ); // -2

// 转化非数字
alert( +true ); // 1
alert( +"" );   // 0
```

它的效果和 `Number(...)` 相同，但是更加简短。
如果我们想把它们当做数字对待，我们需要转化它们，然后再求和：

```javascript
let apples = "2";
let oranges = "3";

// 在二元运算符加号起作用之前，所有的值都被转化为了数字
alert( +apples + +oranges ); // 5

// 更长的写法
// alert( Number(apples) + Number(oranges) ); // 5

//一元运算符加号首先起作用，它们将字符串转为数字，然后二元运算符加号对它们进行求和。
```

### 运算符优先级

在 JavaScript 中有众多运算符。每个运算符都有对应的优先级数字。
数字越大，越先执行。如果优先级相同，则按照由左至右的顺序执行。
![1.png](/md_data/Image2022_06_24_22_54.png)
没有必要把这全记住，但要记住一元运算符优先级高于二元运算符）。

### 赋值运算符

### 原地修改

### 自增/自减

`++/--` 优先级比大部分的算数运算符要高。

前置则返回新的值，后置返回原来的值。

### 位运算符

位运算符把运算元当做 32 位整数，并在它们的二进制表现形式上操作。

这些运算符不是 JavaScript 特有的。大部分的编程语言都支持这些运算符。

下面是位运算符：

- 按位与( `&` )
- 按位或( `|` )
- 按位异或 ( `^` )
- 按位非( `~` )
- 左移 ( `<<` )
- 右移 ( `>>` )
- 无符号右移( `>>>` )

>这些运算符很少被使用，一般是我们需要在最低级别（位）上操作数字时才使用。
>我们不会很快用到这些运算符，因为在 Web 开发中很少使用它们。
>但在某些特殊领域中，例如密码学，它们很有用。

### 逗号运算符

逗号运算符能让我们处理多个语句，使用 `,` 将它们分开。
每个语句都运行了，但是只有最后的语句的结果会被返回。
会使用它把几个行为放在一行上来进行复杂的运算。

```javascript
// 一行上有三个运算符
for (a = 1, b = 3, c = a * b; a < 10; a++) {
 ...
}
//这样的技巧在许多 JavaScript 框架中都有使用。
```

逗号运算符的优先级非常低，比 `=` 还要低，因此上面你的例子中圆括号非常重要。

### 比较

#### 比较结果为 Boolean 类型

#### 字符串比较

#### 不同类型间的比较

#### 严格相等

#### 对 null 和 undefined 进行比较

#### 总结

### 逻辑运算符

#### ||（或）

两个竖线符号表示“或”运算符：

```javascript
result = a || b;
```

如果参与运算的任意一个参数为 `true`，返回的结果就为 `true`，否则返回 `false`。
一个或运算 `||` 的链，将返回第一个真值，如果不存在真值，就返回该链的最后一个值。

```javascript
alert( true || true );   // true
alert( false || true );  // true
alert( true || false );  // true
alert( false || false ); // false
//除了两个操作数都是 false 的情况，结果都是 true。
```

如果操作数不是布尔值，那么它将会被转化为布尔值来参与运算。

#### 或运算寻找第一个真值

一个或运算 `||` 的链，将返回第一个真值，如果不存在真值，就返回该链的最后一个值。

```javascript
result = value1 || value2 || value3;
//返回的值是操作数的初始形式，不会做布尔转换。
```

或运算符 `||` 做了如下的事情：

- 从左到右依次计算操作数。
- 处理每一个操作数时，都将其转化为布尔值。如果结果是 `true`，就停止计算，返回这个操作数的初始值。
- 如果所有的操作数都被计算过（也就是，转换结果都是 `false`），则返回最后一个操作数。

```javascript
alert( 1 || 0 ); // 1（1 是真值）

alert( null || 1 ); // 1（1 是第一个真值）
alert( null || 0 || 1 ); // 1（第一个真值）

alert( undefined || null || 0 ); // 0（都是假值，返回最后一个值）
```

#### 获取变量列表或者表达式中的第一个真值

例如，我们有变量 `firstName`、`lastName` 和 `nickName`，都是可选的（即可以是 undefined，也可以是假值）。

我们用或运算 `||` 来选择有数据的那一个，并显示出来（如果没有设置，则用 `"Anonymous"`）：

```javascript
let firstName = "";
let lastName = "";
let nickName = "SuperCoder";

alert( firstName || lastName || nickName || "Anonymous"); // SuperCoder
```

如果所有变量的值都为假，结果就是 `"Anonymous"`。

#### 短路求值（Short-circuit evaluation）

或运算符 `||` 的另一个用途是所谓的“短路求值”。

这指的是，`||` 对其参数进行处理，直到达到第一个真值，然后立即返回该值，而无需处理其他参数。

如果操作数不仅仅是一个值，而是一个有副作用的表达式，例如变量赋值或函数调用，那么这一特性的重要性就变得显而易见了。

在下面这个例子中，只会打印第二条信息：

```javascript
true || alert("not printed");
false || alert("printed");
```

在第一行中，或运算符 `||` 在遇到 `true` 时立即停止运算，所以 `alert` 没有运行。

有时，利用这个特性，只在左侧的条件为假时才执行命令。

#### &&（与）

两个 & 符号表示 `&&` 与运算符：
在传统的编程中，当两个操作数都是真值时，与运算返回 `true`，否则返回 `false`。

一个与运算链中，与运算寻找第一个假值，全部计算后没有假值时返回最后一个值，

#### 空值合并运算符 '??'

空值合并运算符（nullish coalescing operator）的写法为两个问号 `??`。
`a ?? b` 的结果是：

- 如果 `a` 是已定义的，即不是`null/undefined`，则结果为 `a`，
- 如果 `a` 不是已定义的，则结果为 `b`。

`??` 的常见使用场景是提供默认值。

```javascript
let user;

alert(user ?? "匿名"); // 匿名（user 未定义）

```

纵观 JavaScript 发展史，或 `||` 运算符先于 `??` 出现。它自 JavaScript 诞生就存在了
空值合并运算符 `??`和或 `||` 运算符之间重要的区别是：

- `||` 返回第一个 **真** 值。
- `??` 返回第一个 **已定义的** 值。
即，`||` 无法区分 `false`、`0`、空字符串 `""` 和 `null/undefined`。它们都一样 为假值（falsy values）。
考虑以下情况

```javascript
let height = 0;

alert(height || 100); // 100
alert(height ?? 100); // 0
```

- `height || 100` 首先会检查 `height` 是否为一个假值，它是 `0`，确实是假值。
  - 所以，`||` 运算的结果为第二个参数，`100`。
- `height ?? 100` 首先会检查 `height` 是否为 `null/undefined`，发现它不是。
  - 所以，结果为 `height` 的原始值，`0`。

实际上，高度 `0` 通常是一个有效值，它不应该被替换为默认值。所以 `??` 运算得到的是正确的结果。
·
`??` 运算符的优先级与 `||` 相同，它们的的优先级都为 `4`，意味着，就像 `||` 一样，空值合并运算符在 `=` 和 `?` 运算前计算，但在大多数其他运算（例如 `+` 和 `*`）之后计算。
所以需要需要在这样的表达式中添加括号：

```javascript
let height = null;
let width = null;

// 重要：使用括号
let area = (height ?? 100) * (width ?? 50);

alert(area); // 5000
```

#### 禁止 `??` 与 `&&` 和 `||` 一起使用

出于安全原因，JavaScript 禁止将 `??` 运算符与 `&&` 和 `||` 运算符一起使用，除非使用括号明确指定了优先级。

```javascript
let x = 1 && 2 ?? 3; // Syntax error

let x = (1 && 2) ?? 3; // 正常工作了

alert(x); // 2
```

### 循环

#### break，continue

禁止 break/continue 在 `?` 的右边。
注意非表达式的语法结构不能与三元运算符 `?` 一起使用。特别是 `break/continue` 这样的指令是不允许这样使用的。

```javascript
if (i > 5) {
  alert(i);
} else {
  continue;
}
//用三元运算符?表示
(i > 5) ? alert(i) : continue; // continue 不允许在这个位置
/ /代码会停止运行，并显示有语法错误。
//这是不（建议）使用问号 ? 运算符替代 if 语句的另一个原因。
```

#### break，continue 标签

**标签** 是在循环之前带有冒号的标识符：

```javascript
labelName: for (...) {
  ...
}
```

`break <labelname>` 语句跳出循环至标签处：</labelname>

```javascript
outer: for (let i = 0; i < 3; i++) {

  for (let j = 0; j < 3; j++) {

    let input = prompt(`Value at coords (${i},${j})`, '');

    // 如果是空字符串或被取消，则中断并跳出这两个循环。
    if (!input) break outer; // (*)

    // 用得到的值做些事……
  }
}
alert('Done!');
```

上述代码中，`break outer` 向上寻找名为 `outer` 的标签并跳出当前循环。

因此，控制权直接从 `(*)` 转至 `alert('Done!')`。

还可以将标签移至单独一行：

```javascript
outer:
for (let i = 0; i < 3; i++) { ... }
```

`continue` 指令也可以与标签一起使用。在这种情况下，执行跳转到标记循环的下一次迭代。
`continue` 只有在循环内部才可行。
`break` 指令必须在代码块内。

```javascript
label: {
  // ...
  break label; // 有效
  // ...
}
```

通常使用 `while(true)` 来构造“无限”循环。这样的循环和其他循环一样，都可以通过 `break` 指令来终止。

如果我们不想在当前迭代中做任何事，并且想要转移至下一次迭代，那么可以使用 `continue` 指令。

`break/continue` 支持循环前的标签。标签是 `break/continue` 跳出嵌套循环以转到外部的唯一方法。

## Object（对象）：基础知识

### 对象

#### 概念

JavaScript 中有七种原始类型，它们的值只包含一种东西（字符串，数字或者其他）。

对象则用来存储键值对和更复杂的实体。

一个属性就是一个键值对（“key: value”），其中键（key）是一个字符串（也叫做属性名），值（value）可以是任何值。

可以将一个对象类比为一个文件夹，键是文件夹外部标识，值是文件夹里存储的资料。

可以用下面两种语法中的任一种来创建一个空的对象。

```javascript
let user = new Object(); // “构造函数” 的语法
let user = {};  // “字面量” 的语法
```

>通常，我们用花括号。这种方式我们叫做**字面量**。

```javascript
let user = {     // 一个对象
  name: "John",  // 键 "name"，属性值 "John"
  age: 30        // 键 "age"，属性值 30
};
```

#### .key 和 [] 访问对象属性值

`.`用点符号访问`user`属性值

```javascript
// 读取文件的属性：
alert( user.name ); // John
alert( user.age ); // 30
```

属性的值可以是任意类型，例如布尔类型

```javascript
user.isAdmin = true;
```

可以用 `delete` 操作符移除属性：

```javascript
delete user.age;
```

也可以用`多字词语`来作为属性名，但必须给它们加上引号：

```javascript
let user = {
  name: "John",
  age: 30,
  "likes birds": true  // 多词属性名必须加引号
};
```

列表中的最后一个属性应以`逗号`结尾：

```javascript
let user = {
  name: "John",
  age: 30,
}
```

这叫做`尾随（trailing）`或`悬挂（hanging）`逗号。这样便于添加、删除和移动属性，因为所有的行都是相似的。

点符号要求 `key` 是有效的变量标识符。这意味着：不包含空格，不以数字开头，也不包含特殊字符（允许使用 `$` 和 `_`）。

```javascript
let user = {};
// 单引号或双引号都可以
// 设置
user["likes birds"] = true;

// 读取
alert(user["likes birds"]); // true

// 删除
delete user["likes birds"];
```

方括号提供了一种可以通过任意表达式来获取属性名的方法

```javascript
let key = "likes birds";

// 跟 user["likes birds"] = true; 一样
user[key] = true;
```

##### 计算属性

当创建一个对象时，我们可以在对象字面量中使用方括号。这叫做 计算属性。

```javascript
let fruit = prompt("Which fruit to buy?", "apple");
let bag = {
  // 在对象字面量中
  [fruit]: 5, // 属性名是从 fruit 变量中得到的
};
alert( bag.apple ); // 5 如果 fruit="apple"

//等同于

let fruit = 'apple';
let bag = {
  [fruit + 'Computers']: 5 // bag.appleComputers = 5
};
```

##### 对象 键值-属性名 的特殊

变量名不能是编程语言的某个保留字，如 “for”、“let”、“return” 等。

对象的属性名并不受此限制。

```javascript
// 这些属性都没问题
let obj = {
  for: 1,
  let: 2,
  return: 3
};

alert( obj.for + obj.let + obj.return );  // 6
```

属性命名没有限制。属性名可以是任何字符串或者 symbol。

其他类型则会被自动地转换为字符串。

当数字 `0` 被用作对象的属性的键时，会被转换为字符串 `"0"`：

```javascript
let obj = {
  0: "test" // 等同于 "0": "test"
};

// 都会输出相同的属性（数字 0 被转为字符串 "0"）
alert( obj["0"] ); // test
alert( obj[0] ); // test (相同的属性)
```

我们不能将 `__proto__` 设置为键名：

```javascript
let obj = {};
obj.__proto__ = 5; // 分配一个数字
alert(obj.__proto__); // [object Object] — 值为对象，与预期结果不同
```

##### 属性存在性测试，“in”操作符

JavaScript 的对象有一个需要注意的特性：能够被访问任何属性。即使属性不存在也不会报错

读取不存在的属性只会得到 undefined。所以我们可以很容易地判断一个属性是否存在：

```javascript
let user = {};

alert( user.noSuchProperty === undefined ); // true 意思是没有这个属性
```

用 检查属性是否存在的操作符 `"in"` 更方便

```javascript
let user = { name: "John", age: 30 };

alert( "age" in user ); // true，user.age 存在
alert( "blabla" in user ); // false，user.blabla 不存在。
`in` 的左边必须是 **属性名**。通常是一个带引号的字符串。
```

大部分情况下与 `undefined` 进行比较来判断就可以了。

但有一个例外情况，这种比对方式会有问题，但 `in` 运算符的判断结果仍是对的。

属性存在，但存储的值是 `undefined` 的时。

通常情况下不应该给对象赋值 `undefined`。我们通常会用 `null` 来表示未知的或者空的值。

##### “for…in” 循环

为了遍历一个对象的所有键（key），可以使用`for…in` 循环。

```javascript
let user = {
  name: "John",
  age: 30,
  isAdmin: true
};

// 所有的 “for” 结构体都允许我们在循环中定义变量，
// 像这里的 let key
for (let key in user) {
  // 输出 keys-键
  alert( key );  // name, age, isAdmin
  // 输出属性键的值
  alert( user[key] ); // John, 30, true
}
```

我们可以用其他属性名来替代 `key`，例如 `for(let prop in obj)`

##### for...in 循环 输出排序

整数属性会被进行排序，其他属性则按照创建的顺序显示，例如`+49`，`1.2`
>这里的“整数属性”指的是一个可以在不做任何更改的情况下与一个整数进行相互转换的字符串。

```javascript
let codes = {
  "49": "Germany",
  "41": "Switzerland",
  "44": "Great Britain",
  // ..,
  "1": "USA"
};

for(let code in codes) {
  alert(code); // 1, 41, 44, 49
}
```

JavaScript 中还有很多其他类型的对象：

- `Array` 用于存储有序数据集合，
- `Date` 用于存储时间日期，
- `Error` 用于存储错误信息。
- ……等等。

都继承自 `Object`，并对其扩展。

### 对象引用和复制

对象的内存地址存储在变量中，

所以针对 存有对象内存地址的变量 的操作只是对象地址值的传递，

虽然通过遍历 `引用变量["key"]` 可以完成对象的拷贝，

但仅限于存有原始类型的对象

当对象存有其他对象的引用，即对象里的对象，

此时遍历拷贝得到的又是存有对象内存地址的引用，

即，又需要一次遍历拷贝

因此需要通过递归遍历拷贝，并在每次递归后用`===`检查是否需要下一次递归

当然有现成的实现可以采用

>例如 lodash 库的 _.cloneDeep(obj)
><https://lodash.com/docs#cloneDeep>

#### 使用 const 声明的对象

使用 const 声明的对象 的属性可以被修改，但必须始终引用同一个对象
const 声明的是存有对象内存地址的常量，所以对象的属性可以修改

```javascript
const user = {
  name: "John"
};
```

无法更改`user`内的值

### 垃圾回收

#### 可达性（Reachability）

“可达”，即，存储在内存中可以通过某种方式访问。
固有的可达值基本集合（不能被释放）：

- 当前执行的函数，它的局部变量和参数。
- 当前嵌套调用链上的其他函数、它们的局部变量和参数。
- 全局变量。
- （还有一些内部的）
这些值称作 **跟（roots）**

#### 内部算法

垃圾回收的基本算法被称为 “mark-and-sweep”。

定期执行以下“垃圾回收”步骤：

- 垃圾收集器找到所有的根，并“标记”（记住）它们。
- 然后它遍历并“标记”来自它们的所有引用。
- 然后它遍历标记的对象并标记 **它们的** 引用。所有被遍历到的对象都会被记住，以免将来再次遍历到同一个对象。
- ……如此操作，直到所有可达的（从根部）引用都被访问到。
- 没有被标记的对象都会被删除。

##### 垃圾回收算法优化

- **分代收集（Generational collection）**—— 对象被分成两组：“新的”和“旧的”。许多对象出现，完成它们的工作并很快死去，它们可以很快被清理。那些长期存活的对象会变得“老旧”，而且被检查的频次也会减少。
- **增量收集（Incremental collection）**—— 如果有许多对象，并且我们试图一次遍历并标记整个对象集，则可能需要一些时间，并在执行过程中带来明显的延迟。所以引擎试图将垃圾收集工作分成几部分来做。然后将这几部分会逐一进行处理。这需要它们之间有额外的标记来追踪变化，但是这样会有许多微小的延迟而不是一个大的延迟。
- **闲时收集（Idle-time collection）**—— 垃圾收集器只会在 CPU 空闲时尝试运行，以减少可能对代码执行的影响。

- 垃圾回收由JavaScript引擎自动完成，不能强制执行或是阻止执行。
- 当对象是可达状态时，它一定是存在于内存中的。
- 被引用与可访问（从一个根）不同：一组相互连接的对象可能整体都不可达。

### 原型

#### 原型继承

即，重用某个对象，但并非复制，而是进行部分修改得到其变体

##### [[Prototype]\]

在 JavaScript 中，对象有一个特殊的隐藏属性 `[[Prototype]]`，用来设置继承行为

```JavaScript
[[Prototype]]
`注意事项`
为隐藏属性
值为`null`或`对另一个对象的引用`，而其他的类型都会被忽略。
从 `object` 中读取一个缺失的属性时，JavaScript 会自动从原型中获取该属性
```

##### 设置方式之一 \_\_proto\_\_

`__proto__`只能是`对象`或`null`。

```JavaScript
let animal = {
  eats: true
};
let rabbit = {
  jumps: true
};

rabbit.__proto__ = animal;
// 设置 rabbit.[[Prototype]] = animal
// 可使用 animal 的属性和方法
```

注意事项

- 一个对象不能从其他两个对象获得属性和方法
- 引用不能形成闭环

>`__proto__` 是 `[[Prototype]]` 的因历史原因而留下来的 getter/setter。`__proto__` 属性有点过时了。它的存在是出于历史的原因，现代编程语言建议应该使用函数 `Object.getPrototypeOf/Object.setPrototypeOf` 来取代 `__proto__` 去 get/set 原型。

##### 对公用属性写入不使用原型

写/删除操作直接在子对象上进行，它们不使用原型（假设它是数据属性，不是 通过setter修改）

##### “this” 的值

一个方法调用中，this 始终是调用方法时点符号 . 前面的对象

##### for…in 循环

`for..in` 循环也会迭代继承的属性
内建方法 [obj.hasOwnProperty(key)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty)用于确认对象自己的属性名，是-返回 true / 否-返回false。
`for..in` 只会列出可枚举的属性。

##### 总结

几乎所有 获取键/值方法，例`Object.keys` 和 `Object.values`，都忽略继承的属性。
它们只会对对象自身进行操作。**不考虑** 继承自原型的属性。

#### F.prototype

`F.prototype` 指的是 `F` 的一个名为 `"prototype"` 的常规属性，
值要么是一个对象，要么就是 `null`：其他值都不起作用，
虽然和[ [prototype] ]看起来类似，实际作用比较局限：

```js
// F 的构造函数储存 F 内存地址，
// new F 被调用时，
// 它为新对象的 [[Prototype]] 赋值，

// 如果在创建之后，F.prototype 属性有了变化
// （F.prototype = <another object>），
// 那么通过 new F 创建的新对象也将随之拥有新的对象
// 作为 [[Prototype]]，但已经存在的对象将保持旧有的值

```

```js
let animal = {
  eats: true
};

function Rabbit(name) {
  this.name = name;
}

Rabbit.prototype = animal;
// 执行 new Rabbit 时，把它的 [[Prototype]] 赋值为 animal

let rabbit = new Rabbit("White Rabbit"); //  rabbit.__proto__ == animal

alert( rabbit.eats ); // true
```

##### 默认的 F.prototype，构造器属性

每个函数默认都有 `prototype` 属性，
默认的 `prototype` 是一个只有属性 `constructor` 的对象，
属性 `constructor` 指向函数自身。

```js
function Rabbit() {}

/* default prototype
Rabbit.prototype = { constructor: Rabbit };
*/
alert( Rabbit.prototype.constructor == Rabbit ); // true
// constructor 属性可以通过 [[Prototype]] 给所有 rabbits 使用
```

可以使用 `constructor` 属性来创建一个新对象，该对象使用与现有对象相同的构造器。

```js
function Rabbit(name) {
  this.name = name;
  alert(name);
}

let rabbit = new Rabbit("White Rabbit");

let rabbit2 = new rabbit.constructor("Black Rabbit");
// 当一个对象，不知道使用了哪个构造器（例如它来自第三方库），
// 并且需要创建另一个类似的对象时，用这种方法就很方便。
```

JavaScript 自身并不能确保正确的 `constructor` 函数值。
它存在于函数的默认 `"prototype"` 中，
如果我们将整个默认 prototype 替换掉，那么其中就不会有 `constructor`。

```js
function Rabbit() {}
Rabbit.prototype = {
  jumps: true
};

let rabbit = new Rabbit();
alert(rabbit.constructor === Rabbit); // false

// 为了确保正确的 "constructor"，可以选择添加/删除属性到默认 "prototype"，
// 而不是将其整个覆盖
function Rabbit() {}
// 不要将 Rabbit.prototype 整个覆盖
// 可以向其中添加内容
Rabbit.prototype.jumps = true
// 默认的 Rabbit.prototype.constructor 被保留了下来

// 也可以手动重新创建 constructor 属性
Rabbit.prototype = {
  jumps: true,
  constructor: Rabbit
};
```

#### 原生的原型

##### Object.prototype

`"prototype"` 属性在 JavaScript 自身的核心部分中被广泛地应用。

```js
let obj = {};
alert( obj ); // "[object Object]"
// 新建对象时，[[Prototype]] 属性被设置为 Object.prototype
// alert() 执行时调用 obj toString()，
// 没找到则访问 Object.prototype.toString()，
// Object.prototype.toString()方法生成 "[object Object]"
```

验证：

```js
let obj = {};

alert(obj.__proto__ === Object.prototype); // true

alert(obj.toString === obj.__proto__.toString); //true
alert(obj.toString === Object.prototype.toString); //true
alert(Object.prototype.__proto__); // null
```

```js
let arr = [1, 2, 3];

// 它继承自 Array.prototype？
alert( arr.__proto__ === Array.prototype ); // true

// 接下来继承自 Object.prototype？
alert( arr.__proto__.__proto__ === Object.prototype ); // true

// 原型链的顶端为 null。
alert( arr.__proto__.__proto__.__proto__ ); // null

```

##### 其他内建原型

如图：访问时按照就近原则
![图 1](../images/67913027a7d0238555a6350edbae8bd2b148df35c712ea4e1902dc4bceb399a8.png)

浏览器内的工具，像 Chrome 开发者控制台也会显示继承性（可能需要对内建对象使用 `console.dir`）
![图 2](../images/477fab845e00380afeb64c6d04c620c46860c3220e0aaf0fb16212f610cf720f.png)

##### 基本数据类型

当访问不是对象的字符串、数字和布尔值的属性时，对应的临时包装器对象将会通过内建的构造器 `String`、`Number` 和 `Boolean` 被创建。它们提供操作字符串、数字和布尔值的方法然后消失。
>特殊值 null 和 undefined 比较特殊。它们没有对象包装器，所以它们没有方法和属性。并且它们也没有相应的原型。

##### 更改原生原型

```js
String.prototype.show = function() {
  alert(this);
};
// 向 String.prototype 中添加一个方法，
// 这个方法将对所有的字符串都是可用的。

"BOOM!".show(); // BOOM!
```

>原型是全局的，所以很容易造成冲突。如果有两个库都添加了 String.prototype.show 方法，那么其中的一个方法将被另一个覆盖。所以，通常来说，修改原生原型被认为是一个很不好的想法。

>只有一种情况下允许修改原生原型。那就是 polyfilling。
Polyfilling 是一个术语，表示某个方法在 JavaScript 规范中已存在，但是特定的 JavaScript 引擎尚不支持该方法，那么我们可以通过手动实现它，并用以填充内建原型。

```

if (!String.prototype.repeat) { // 如果这儿没有这个方法
  // 那就在 prototype 中添加它

  String.prototype.repeat = function(n) {
    // 重复传入的字符串 n 次

    // 实际上，实现代码比这个要复杂一些（完整的方法可以在规范中找到）
    // 但即使是不够完美的 polyfill 也常常被认为是足够好的
    return new Array(n + 1).join(this);
  };
}

```

##### 从原型中借用

#### 原型方法，没有 `__proto__` 的对象

`__proto__` 被认为是过时且不推荐使用的（deprecated），这里的不推荐使用是指 JavaScript 规范中规定，`__proto__` 必须仅在浏览器环境下才能得到支持。
应该使用这些方法来代替 `__proto__`。

- [Object.create(proto, [descriptors])](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/create) —— 利用给定的 `proto` 作为 `[[Prototype]]` 和可选的属性描述来创建一个空对象。
- [Object.getPrototypeOf(obj)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/getPrototypeOf) —— 返回对象 `obj` 的 `[[Prototype]]`。
- [Object.setPrototypeOf(obj, proto)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/setPrototypeOf) —— 将对象 `obj` 的 `[[Prototype]]` 设置为 `proto`。

```js
let animal = {
  eats: true
};

// 创建一个以 animal 为原型的新对象
let rabbit = Object.create(animal);

alert(rabbit.eats); // true

alert(Object.getPrototypeOf(rabbit) === animal); // true

Object.setPrototypeOf(rabbit, {}); // 将 rabbit 的原型修改为 {}
// Object.create 有一个可选的第二参数：属性描述器
// 我们可以在此处为新对象提供额外的属性
let animal = {
  eats: true
};

let rabbit = Object.create(animal, {
  jumps: {
    value: true
  }
});

alert(rabbit.jumps); // true

```

描述器的格式与 [属性标志和属性描述符](https://zh.javascript.info/property-descriptors) 一章中所讲的一样。

`Object.create` 提供了一种简单的方式来浅拷贝一个对象的所有描述符

```js
let clone = Object.create(Object.getPrototypeOf(obj),
Object.getOwnPropertyDescriptors(obj));
```

##### 原型简史

##### "Very plain" objects

### 对象方法，"this"

- 存储在对象属性中的函数被称为“方法”。
- 方法允许对象进行像 `object.doSomething()` 这样的“操作”。
- 方法可以将对象引用为 `this`。

`this` 的值是在程序运行时得到的。
在没有对象的情况下调用：`this == undefined`

- 一个函数在声明时，可能就使用了 `this`，但是这个 `this` 只有在函数被调用时才会有值。
- 可以在对象之间复制函数。
- 以“方法”的语法调用函数时：`object.method()`，调用过程中的 `this` 值是 `object`。

请注意箭头函数有些特别：它们没有 `this`。在箭头函数内部访问到的 `this` 都是从外部获取的。

### 构造器和操作符“new”

- 构造函数，或简称构造器，就是常规函数，但大家对于构造器有个共同的约定，就是其命名首字母要大写。
- 构造函数只能使用 `new` 来调用。这样的调用意味着在开始时创建了空的 `this`，并在最后返回填充了值的 `this`。

我们可以使用构造函数来创建多个类似的对象。

JavaScript 为许多内建的对象提供了构造函数：比如日期 `Date`、集合 `Set` 以及其他我们计划学习的内容。

### 可选链“?.”

可选链 `?.` 语法有三种形式：

1. `obj?.prop` ---如果 `obj` 存在则返回 `obj.prop`，否则返回 `undefined`。
2. `obj?.[prop]` ---如果 `obj` 存在则返回 `obj[prop]`，否则返回 `undefined`。
3. `obj.method?.()` ---如果 `obj.method` 存在则调回 `obj.method()`，否则返回 `undefined`。

正如我们所看到的，这些语法形式用起来都很简单直接。`?.` 检查左边部分是否为 `null/undefined`，如果不是则继续运算。

`?.` 链使我们能够安全地访问嵌套属性。

但是，我们应该谨慎地使用 `?.`，根据我们的代码逻辑，仅在当左侧部分不存在也可接受的情况下使用为宜。以保证在代码中有编程上的错误出现时，也不会对我们隐藏。

### symbol 类型

`symbol` 是唯一标识符的基本类型

symbol 是使用带有可选描述（name）的 `Symbol()` 调用创建的。

symbol 总是不同的值，即使它们有相同的名字。如果我们希望同名的 symbol 相等，那么我们应该使用全局注册表：`Symbol.for(key)` 返回（如果需要的话则创建）一个以 `key` 作为名字的全局 symbol。使用 `Symbol.for` 多次调用 `key` 相同的 symbol 时，返回的就是同一个 symbol。

symbol 有两个主要的使用场景：

1. “隐藏” 对象属性。

    如果我们想要向“属于”另一个脚本或者库的对象添加一个属性，我们可以创建一个 symbol 并使用它作为属性的键。symbol 属性不会出现在 `for..in` 中，因此它不会意外地被与其他属性一起处理。并且，它不会被直接访问，因为另一个脚本没有我们的 symbol。因此，该属性将受到保护，防止被意外使用或重写。

    因此我们可以使用 symbol 属性“秘密地”将一些东西隐藏到我们需要的对象中，但其他地方看不到它。

2. JavaScript 使用了许多系统 symbol，这些 symbol 可以作为 `Symbol.*` 访问。我们可以使用它们来改变一些内建行为。例如，在本教程的后面部分，我们将使用 `Symbol.iterator` 来进行 [迭代](https://zh.javascript.info/iterable) 操作，使用 `Symbol.toPrimitive` 来设置 [对象原始值的转换](https://zh.javascript.info/object-toprimitive) 等等。

从技术上说，symbol 不是 100% 隐藏的。有一个内建方法 [Object.getOwnPropertySymbols(obj)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertySymbols) 允许我们获取所有的 symbol。还有一个名为 [Reflect.ownKeys(obj)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Reflect/ownKeys) 的方法可以返回一个对象的 **所有** 键，包括 symbol。所以它们并不是真正的隐藏。但是大多数库、内建方法和语法结构都没有使用这些方法。

### 对象 - 原始值转换

对象到原始值的转换，是由许多期望以原始值作为值的内建函数和运算符自动调用的。

这里有三种类型（hint）：

- `"string"`（对于 `alert` 和其他需要字符串的操作）
- `"number"`（对于数学运算）
- `"default"`（少数运算符，通常对象以和 `"number"` 相同的方式实现 `"default"` 转换）

规范明确描述了哪个运算符使用哪个 hint。

转换算法是：

1. 调用 `obj[Symbol.toPrimitive](hint)` 如果这个方法存在，
2. 否则，如果 hint 是 `"string"`
    - 尝试调用 `obj.toString()` 或 `obj.valueOf()`，无论哪个存在。
3. 否则，如果 hint 是 `"number"` 或者 `"default"`
    - 尝试调用 `obj.valueOf()` 或 `obj.toString()`，无论哪个存在。

所有这些方法都必须返回一个原始值才能工作（如果已定义）。

在实际使用中，通常只实现 `obj.toString()` 作为字符串转换的“全能”方法就足够了，该方法应该返回对象的“人类可读”表示，用于日志记录或调试。

## 数据类型

### 原始类型的方法

JavaScript 允许像使用对象一样使用原始类型（字符串，数字等）。
先了解它的工作原理，毕竟原始类型不是对象。

1. 原始类型仍然是原始的。与预期相同，提供单个值
2. JavaScript 允许访问字符串，数字，布尔值和 symbol 的方法和属性。
3. 为了使它们起作用，创建了提供额外功能的特殊“对象包装器”，使用后即被销毁。
“对象包装器”对应原始类型，提供了不同的方法，为 `String`、`Number`、`Boolean`、`Symbol` 和 `BigInt`。

```javascript
// 字符串方法 str.toUpperCase() 返回一个大写化处理的字符串
let str = "Hello";

alert( str.toUpperCase() ); // HELLO
// 1. 字符串 `str` 是一个原始值。因此，在访问其属性时，会创建一个包含字符串字面值的特殊对象，并且具有有用的方法，如 `toUpperCase()`。
// 2. 该方法运行并返回一个新的字符串（由 `alert` 显示）。
// 3. 特殊对象被销毁，只留下原始值 `str`。
```

所以原始类型可以提供方法，但它们依然是轻量级的。
从形式上讲，这些方法通过临时对象工作，但 JavaScript 引擎可以很好地调整，以在内部对其进行优化，因此调用它们并不需要太高的成本。

### 数字类型

#### 总结

```javascript
let billion = 1000000000;
let billion = 1_000_000_000; // 使用下划线 `_` 作为分隔符
let billion = 1e9; //1e9--10^9

0xff ， 0Xff 都可以 // 十六进制
0b11111111  // 二进制形式的 255
0o377  // 八进制形式的 255
// 二者相等

num.toString(base)  // base 的范围可以从 2 到 36。默认情况下是 10
let num = 255;
alert( num.toString(16) );  // ff
alert( num.toString(2) );   // 11111111
(123456).toString(36) = 123456..toString(36)
// ..表明小数部分为空，并调用函数

let num = 12.34;
alert( num.toFixed(1) ); // "12.3"
// 这会向上或向下舍入到最接近的值
// toFixed 函数 toFixed(n) 将数字舍入到小数点后 n 位，结果是一个字符串。
// 如果小数部分比所需要的短，则在结尾添加零
// 可以使用一元加号或 Number() 调用，将其转换为数字，

alert( 0.1 + 0.2 == 0.3 ); // =0.30000000000000004，false，精度的损失
let sum = 0.1 + 0.2;
alert( sum.toFixed(2) ); // 0.30，借助方法 toFixed(n) 对结果进行舍入
alert( sum.toFixed(1) ); // 0.3

0 === -0

// Infinity（和 -Infinity）是一个特殊的数值，比任何数值都大（小）。
// NaN 代表一个 error。
// isFinite() 和 isNaN() 检查以上特殊值
// isFinite(value) 将其参数转换为数字，
// 如果是常规数字而不是 NaN/Infinity/-Infinity，则返回 true
alert( isFinite("15") ); // true
alert( isFinite("str") ); // false，因为是一个特殊的值：NaN
alert( isFinite(Infinity) ); // false，因为是一个特殊的值：Infinity
// isNaN(value) 将其参数转换为数字，然后测试它是否为 NaN
alert( isNaN(NaN) ); // true
alert( isNaN("str") ); // true
alert( NaN === NaN ); // false

let num = +prompt("Enter a number", '');
// 有时 isFinite 被用于验证字符串值是否为常规数字
// 结果会是 true，除非你输入的是 Infinity、-Infinity 或不是数字
alert( isFinite(num) );

// 在所有数字函数中，包括 isFinite()，空字符串或仅有空格的字符串均被视为 0

// 特殊的内建方法 Object.is，它类似于 === 一样对值进行比较
// 它适用于 NaN：Object.is(NaN，NaN) === true
// 值 0 和 -0 是不同的：Object.is(0，-0) === false，从技术上讲这是对的

// 使用加号 + 或 Number() 的数字转换是严格的。
// 如果一个值不完全是一个数字，就会失败
alert( +"100px" ); // NaN
// 唯一的例外是字符串开头或结尾的空格，因为空格会被忽略。

// parseInt 返回一个整数，而 parseFloat 返回一个浮点数
// parseInt 和 parseFloat可以从字符串中“读取”数字，直到无法读取为止。
// 如果发生 error，则返回收集到的数字
alert( parseInt('100px') ); // 100
alert( parseFloat('12.5em') ); // 12.5
alert( parseInt('12.3') ); // 12，只有整数部分被返回了
alert( parseFloat('12.3.4') ); // 12.3，在第二个点出停止了读取
alert( parseInt('a123') ); // NaN，第一个符号停止了读取

// parseInt 还可以解析十六进制数字、二进制数字等的字符串
alert( parseInt('0xff', 16) ); // 255
alert( parseInt('ff', 16) ); // 255，没有 0x 仍然有效
alert( parseInt('2n9c', 36) ); // 123456

// JavaScript 有一个内建的 Math 对象，包含一个小型的数学函数和常量库
alert( Math.random() ); // 0.5435252343232
alert( Math.random() ); // ... (任何随机数)
alert( Math.max(3, 5, -10, 0, 1) ); // 5
alert( Math.min(1, 2) ); // 1
alert( Math.pow(2, 10) ); // 2 的 10 次幂 = 1024

```

- 将 `"e"` 和 0 的数量附加到数字后。就像：`123e6` 与 `123` 后面接 6 个 0 相同。
- `"e"` 后面的负数将使数字除以 1 后面接着给定数量的零的数字。例如 `123e-6` 表示 `0.000123`（`123` 的百万分之一）。

对于不同的数字系统：

- 可以直接在十六进制（`0x`），八进制（`0o`）和二进制（`0b`）系统中写入数字。
- `parseInt(str，base)` 将字符串 `str` 解析为在给定的 `base` 数字系统中的整数，`2 ≤ base ≤ 36`。
- `num.toString(base)` 将数字转换为在给定的 `base` 数字系统中的字符串。

要将 `12pt` 和 `100px` 之类的值转换为数字：

- 使用 `parseInt/parseFloat` 进行“软”转换，它从字符串中读取数字，然后返回在发生 error 前可以读取到的值。

小数：

- 使用 `Math.floor`，`Math.ceil`，`Math.trunc`，`Math.round` 或 `num.toFixed(precision)` 进行舍入。
- 请确保记住使用小数时会损失精度。

更多数学函数：

- 需要时请查看 [Math](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Math) 对象。这个库很小，但是可以满足基本的需求。

在现代 JavaScript 中，数字（number）有两种类型：

1. JavaScript 中的常规数字以 64 位的格式 [IEEE-754](https://en.wikipedia.org/wiki/IEEE_754-2008_revision) 存储，也被称为“双精度浮点数”。这是大多数时候所使用的数字，将在本章中学习它们。

2. BigInt 数字，用于表示任意长度的整数。有时会需要它们，因为常规数字不能安全地超过 `253` 或小于 `-253`。由于仅在少数特殊领域才会用到 BigInt，因此在特殊的章节 [BigInt](https://zh.javascript.info/bigint) 中对其进行了介绍。

#### 数字的各种表示

```javascript
let billion = 1000000000;
let billion = 1_000_000_000;
let billion = 1e9;  // 10 亿，字面意思：数字 1 后面跟 9 个 0
let mcs = 0.000001;
let mcs = 1e-6; // 1 的左边有 6 个 0
```

#### 十六进制，二进制和八进制数字

[十六进制](https://en.wikipedia.org/wiki/Hexadecimal) 数字在 JavaScript 中被广泛用于表示颜色，编码字符以及其他许多东西。所以自然地，有一种较短的写方法：`0x`，然后是数字。

```javascript
alert( 0xff ); // 255
alert( 0xFF ); // 255（一样，大小写没影响）
```

二进制和八进制数字系统很少使用，但也支持使用 `0b` 和 `0o` 前缀：

```javascript
let a = 0b11111111; // 二进制形式的 255
let b = 0o377; // 八进制形式的 255

alert( a == b ); // true，两边是相同的数字，都是 255
```

只有这三种进制支持这种写法。对于其他进制，应该使用函数 `parseInt`（在本章后面看到）。

#### toString(base)

方法 `num.toString(base)` 返回在给定 `base` 进制数字系统中 `num` 的字符串表示形式。

```javascript
let num = 255;

alert( num.toString(16) );  // ff
alert( num.toString(2) );   // 11111111
```

`base` 的范围可以从 `2` 到 `36`。默认情况下是 `10`。

常见的用例如下：

- **base=16** 用于十六进制颜色，字符编码等，数字可以是 `0..9` 或 `A..F`。

- **base=2** 主要用于调试按位操作，数字可以是 `0` 或 `1`。

- **base=36** 是最大进制，数字可以是 `0..9` 或 `A..Z`。所有拉丁字母都被用于了表示数字。对于 `36` 进制来说，一个有趣且有用的例子是，当需要将一个较长的数字标识符转换成较短的时候，例如做一个短的 URL。可以简单地使用基数为 `36` 的数字系统表示：

```javascript
alert( 123456..toString(36) ); // 2n9c
//效果相同
alert( (123456).toString(36) ); // 2n9c
```

>使用两个点来调用一个方法
>如果想直接在一个数字上调用一个方法，比如上面例子中的 `toString`，那么我们需要在它后面放置两个点 `..`。

#### 舍入

舍入（rounding）是使用数字时最常用的操作之一。

这里有几个对数字进行舍入的内建函数：

`Math.floor`

向下舍入：`3.1` 变成 `3`，`-1.1` 变成 `-2`。

`Math.ceil`

向上舍入：`3.1` 变成 `4`，`-1.1` 变成 `-1`。

`Math.round`

向最近的整数舍入：`3.1` 变成 `3`，`3.6` 变成 `4`，中间值 `3.5` 变成 `4`。

`Math.trunc`（IE 浏览器不支持这个方法）

移除小数点后的所有内容而没有舍入：`3.1` 变成 `3`，`-1.1` 变成 `-1`。
>详见
>![1.png](/md_data/Image2022_07_01_17_49.png)

函数 `toFixed(n)` 将数字舍入到小数点后 `n` 位，并以字符串形式返回结果，如果小数部分比所需要的短，则在结尾添加零。

```javascript
let num = 12.34;
alert( num.toFixed(1) ); // "12.3"

let num = 12.34;
alert( num.toFixed(5) ); // "12.34000"，在结尾添加了 0，以达到小数点后五位
```

这会向上或向下舍入到最接近的值，类似于 Math.round
可以使用一元加号或 `Number()` 调用，将其转换为数字，例如 `+ num.toFixed(5)`。

```javascript
let num = 12.36;
alert( num.toFixed(1) ); // "12.4"

```

#### 不精确的计算

在内部，数字是以 64 位格式 IEEE-754 表示的，所以正好有 64 位可以存储一个数字：其中 52 位被用于存储这些数字，其中 11 位用于存储小数点的位置（对于整数，它们为零），而 1 位用于符号。
如果一个数字真的很大，则可能会溢出 64 位存储，变成一个特殊的数值 `Infinity`。
比起溢出，精度的缺失更容易发生。

```javascript
alert( 0.1 + 0.2 == 0.3 ); // false
alert( 0.1 + 0.2 ); // 0.30000000000000004
```

原因
>一个数字以其二进制的形式存储在内存中，一个 1 和 0 的序列。但是在十进制数字系统中看起来很简单的 0.1，0.2 这样的小数，实际上在二进制形式中是无限循环小数。
>什么是 0.1？0.1 就是 1 除以 10，1/10，即十分之一。在十进制数字系统中，这样的数字表示起来很容易。将其与三分之一进行比较：1/3。三分之一变成了无限循环小数 0.33333(3)。
>在十进制数字系统中，可以保证以 10 的整数次幂作为除数能够正常工作，但是以 3 作为除数则不能。也是同样的原因，在二进制数字系统中，可以保证以 2 的整数次幂作为除数时能够正常工作，但 1/10 就变成了一个无限循环的二进制小数。
>使用二进制数字系统无法 精确 存储 0.1 或 0.2，就像没有办法将三分之一存储为十进制小数一样。
>IEEE-754 数字格式通过将数字舍入到最接近的可能数字来解决此问题。这些舍入规则通常不允许我们看到“极小的精度损失”，但是它确实存在。

```javascript
alert( 0.1.toFixed(20) ); // 0.10000000000000000555
// 当我们对两个数字进行求和时，它们的“精度损失”会叠加起来。
```

最可靠的方法是借助方法 `toFixed(n)` 对结果进行舍入：

```javascript
let sum = 0.1 + 0.2;
alert( sum.toFixed(2) ); // 0.30
```

#### 测试：isFinite 和 isNaN

- `Infinity`（和 `-Infinity`）是一个特殊的数值，比任何数值都大（小）。

- `NaN` 代表一个 error。

它们属于 `number` 类型，但不是“普通”数字，需要用特殊函数来检查：
`isNaN(value)` 将其参数转换为数字，然后测试它是否为 `NaN`：

```javascript
alert( isNaN(NaN) ); // true
alert( isNaN("str") ); // true
// 值 “NaN” 是独一无二的，它不等于任何东西，包括它自身
alert( NaN === NaN ); // false
```

`isFinite(value)` 将其参数转换为数字，如果是常规数字而不是 `NaN/Infinity/-Infinity`，则返回 `true`：

```javascript
alert( isFinite("15") ); // true
alert( isFinite("str") ); // false，因为是一个特殊的值：NaN
alert( isFinite(Infinity) );
// false，因为是一个特殊的值：Infinity
```

有时 `isFinite` 被用于验证字符串值是否为常规数字：

```javascript
let num = +prompt("Enter a number", '');

// 结果会是 true，除非你输入的是 Infinity、-Infinity 或不是数字
alert( isFinite(num) );
```

在所有数字函数中，包括 `isFinite`，空字符串或仅有空格的字符串均被视为 `0`。

##### 特殊的内建方法 Object.is

![1.png](/md_data/Image2022_07_02_00_22.png)

#### parseInt 和 parseFloat

使用加号 `+` 或 `Number()` 的数字转换是严格的。如果一个值不完全是一个数字，就会失败：

```javascript
alert( +"100px" ); // NaN
// 唯一的例外是字符串开头或结尾的空格，因为它们会被忽略。
```

在现实生活中，我们经常会有带有单位的值，例如 CSS 中的 `"100px"` 或 `"12pt"`。并且，在很多国家，货币符号是紧随金额之后的，所以我们有 `"19€"`，并希望从中提取出一个数值。
这就是 `parseInt` 和 `parseFloat` 的作用。

它们可以从字符串中“读取”数字，直到无法读取为止。如果发生 error，则返回收集到的数字。函数 `parseInt` 返回一个整数，而 `parseFloat` 返回一个浮点数：

```javascript
alert( parseInt('100px') ); // 100
alert( parseFloat('12.5em') ); // 12.5

alert( parseInt('12.3') ); // 12，只有整数部分被返回了
alert( parseFloat('12.3.4') ); // 12.3，在第二个点出停止了读取
```

某些情况下，`parseInt/parseFloat` 会返回 `NaN`。当没有数字可读时会发生这种情况：

```javascript
alert( parseInt('a123') ); // NaN，第一个符号停止了读取
```

##### parseInt(str, radix) 的第二个参数

![1.png](/md_data/Image2022_07_02_00_28.png)

#### 其他数学函数

JavaScript 有一个内建的 Math 对象，它包含了一个小型的数学函数和常量库。

几个例子：

`Math.random()`

返回一个从 0 到 1 的随机数（不包括 1）。

```javascript
alert( Math.random() ); // 0.1234567894322
alert( Math.random() ); // 0.5435252343232
alert( Math.random() ); // ... (任何随机数)
```

`Math.max(a, b, c...)` / `Math.min(a, b, c...)`

从任意数量的参数中返回最大/最小值。

`Math.pow(n, power)`

返回 `n` 的给定（power）次幂。

`Math` 对象中还有更多函数和常量，包括三角函数，你可以在 [Math 对象文档](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Math) 中找到这些内容。

### 字符串

```javascript
str.trim() —— 删除字符串前后的空格 (“trims”)。
str.repeat(n) —— 重复字符串 n 次。


**单引号 双引号 反引号**
// 字符串可以包含在单引号、双引号或反引号中
// 单引号和双引号基本相同
// 反引号允许我们通过 ${…} 将任何表达式嵌入到字符串中
function sum(a, b) {
  return a + b;
}
alert(`1 + 2 = ${sum(1, 2)}.`); // 1 + 2 = 3.
// 使用反引号的另一个优点是它们允许字符串跨行
let guestList = `Guests:
 * John
 * Pete
 * Mary
`;
alert(guestList); // 客人清单，多行

**换行符（newline character）**
// 以支持使用单引号和双引号来创建跨行字符串
let guestList = "Guests:\n * John\n * Pete\n * Mary";
alert(guestList); // 一个多行的客人列表

**转义字符**
// Unicode 示例
alert( "\u00A9" ); // ©
alert( "\u{20331}" ); // 佫，罕见的中国象形文字（长 Unicode）
alert( "\u{1F60D}" ); // 😍，笑脸符号（另一个长 Unicode）
```

![1.png](/md_data/Image2022_07_03_00_47.png)

```javascript
// 所有的特殊字符都以反斜杠字符 \ 开始。它也被称为“转义字符”
alert( 'I\'m the Walrus!' ); // I'm the Walrus!
alert( `The backslash: \\` ); // The backslash: \

**字符串长度--length 属性**
// 请注意 str.length 是一个数字属性，而不是函数。后面不需要添加括号
alert( `My\n`.length ); // 3，注意 \n 是一个单独的“特殊”字符

**访问字符**
// 使用方括号 [pos] 或者调用 str.charAt(pos) 方法
let str = `Hello`;
// 第一个字符
alert( str[0] ); // H
alert( str.charAt(0) ); // H
// 最后一个字符
alert( str[str.length - 1] ); // o
// 方括号是获取字符的一种现代化方法，而 charAt 是历史原因才存在的

**字符串是不可变的**
let str = 'Hi';
str[0] = 'h'; // error
alert( str[0] ); // 无法运行
// 通常的解决方法是创建一个新的字符串，
// 并将其分配给 str 而不是以前的字符串。
let str = 'Hi';
str = 'h' + str[1];  // 替换字符串
alert( str ); // hi

**toLowerCase() 和 toUpperCase()**
// 改变大小写
alert( 'Interface'.toUpperCase() ); // INTERFACE
alert( 'Interface'.toLowerCase() ); // interface
alert( 'Interface'[0].toLowerCase() ); // 'i'

**str.indexOf(substr, pos)**
// 查找子字符串
// 它从给定位置 pos 开始，在 str 中查找 substr，
// 如果没有找到，则返回 -1，否则返回匹配成功的位置。
let str = 'Widget with id';
alert( str.indexOf('Widget') ); // 0，因为 'Widget' 一开始就被找到
alert( str.indexOf('widget') ); // -1，没有找到，检索是大小写敏感的
alert( str.indexOf("id") ); // 1，"id" 在位置 1 处（……idget 和 id）
// 可选的第二个参数允许我们从一个给定的位置开始检索。
// 例如，"id" 第一次出现的位置是 1。查询下一个存在位置时，我们从 2 开始检索：
let str = 'Widget with id';
alert( str.indexOf('id', 2) ) // 12
// "id" 第一次出现的位置是 1。查询下一个存在位置时，我们从 2 开始检索

**str.indexOf(substr, pos)**
// 如果需要获取所有存在位置，可以在一个循环中使用 indexOf。每一次新的调用都发生在上一匹配位置之后
let pos = 0;
while (true) {
  let foundPos = str.indexOf(target, pos);
  if (foundPos == -1) break;
  alert( `Found at ${foundPos}` );
  pos = foundPos + 1; // 继续从下一个位置查找
}
// 简写
let pos = -1;
while ((pos = str.indexOf(target, pos + 1)) != -1) {
  alert( pos );
}

// str.indexOf("String") != -1 更有效
let str = "Widget with id";
if (str.indexOf("Widget")) {
    alert("We found it"); // 不工作！
}
// alert 不会显示，因为 str.indexOf("Widget") 返回 0
if (str.indexOf("Widget") != -1) {
    alert("We found it"); // 现在工作了！

str.lastIndexOf(substr, pos)
还有一个类似的方法 str.lastIndexOf(substr, position)。
它从字符串的末尾开始搜索到开头。
它会以相反的顺序列出这些事件。

**按位（bitwise）NOT 技巧**
**只要记住：if (~str.indexOf(...)) 读作 if found **
// 它将数字转换为 32-bit 整数（如果存在小数部分，则删除小数部分），
// 然后对其二进制表示形式中的所有位均取反。
// 意味着一件很简单的事儿：对于 32-bit 整数，~n 等于 -(n+1)。
alert( ~2 ); // -3，和 -(2+1) 相同
alert( ~1 ); // -2，和 -(1+1) 相同
alert( ~0 ); // -1，和 -(0+1) 相同
alert( ~-1 ); // 0，和 -(-1+1) 相同
// 仅当 indexOf 的结果不是 -1 时，检查 if ( ~str.indexOf("...") ) 才为真
let str = "Widget";
if (~str.indexOf("Widget")) {
  alert( 'Found it!' ); // 正常运行
}
// 通常不建议以非显而易见的方式使用语言特性，
// 但这种特殊技巧在旧代码中仍被广泛使用，所以应该理解它。
// 只要记住：if (~str.indexOf(...)) 读作 “if found”

**includes，startsWith，endsWith**
// 方法 str.includes(substr, pos) 根据 str 中是否包含 substr 来返回 true/false
// pos-开始搜索的起始位置
// 方法 str.startsWith 和 str.endsWith 的功能
alert( "Widget".startsWith("Wid") ); // true，"Widget" 以 "Wid" 开始
alert( "Widget".endsWith("get") ); // true，"Widget" 以 "get" 结束

**substring、substr  slice**
// JavaScript 中有三种获取字符串的方法

**str.slice(start [, end])**
// 返回字符串从 start 到（但不包括）end 的部分
let str = "stringify";
alert( str.slice(0, 5) ); // 'strin'，从 0 到 5 的子字符串（不包括 5）
alert( str.slice(0, 1) ); // 's'，从 0 到 1，但不包括 1，所以只有在 0 处的字符

// 如果没有第二个参数，slice 会一直运行到字符串末尾
let str = "stringify";
alert( str.slice(2) ); // 从第二个位置直到结束

// start/end 也有可能是负值。它们的意思是起始位置从字符串结尾计算
let str = "stringify";

// 从右边的第四个位置开始，在右边的第一个位置结束
alert( str.slice(-4, -1) ); // 'gif'

// 不接受start 大于 end
alert( str.slice(2, 6) ); // "ring"（一样）
alert( str.slice(6, 2) ); // ""（空字符串）

**str.substring(start [, end])**

// 返回字符串在 start 和 end 之间 的部分
// 允许 start 大于 end
let str = "stringify";
alert( str.substring(2, 6) ); // "ring"
alert( str.substring(6, 2) ); // "ring"

**str.substr(start [, length])**

// 返回字符串从 start 开始的给定 length 的部分
let str = "stringify";
alert( str.substr(2, 4) ); // 'ring'，从位置 2 开始，获取 4 个字符

// 第一个参数可能是负数，从结尾算起
let str = "stringify";
alert( str.substr(-4, 2) ); // 'gi'，从第 4 位获取 2 个字符
```

回顾
![1.png](../md_data/Image2022_07_03_23_42.png)
仅仅记住这三种方法中的 slice 就足够了

#### 比较字符串

##### JavaScript 中字符串的内部表示

```javascript
**str.codePointAt(pos)**
// 返回在 pos 位置的字符代码
// 不同的字母有不同的代码
alert( "z".codePointAt(0) ); // 122
alert( "Z".codePointAt(0) ); // 90

**String.fromCodePoint(code)**
// 通过数字 code 创建字符
alert( String.fromCodePoint(90) ); // Z

// \u 后跟十六进制代码，
// 通过这些代码添加 Unicode 字符
alert( '\u005a' ); // Z
// 在十六进制系统中 90 为 5a

let str = '';
for (let i = 65; i <= 220; i++) {
  str += String.fromCodePoint(i);
}
alert( str );
// ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]
^_`abcdefghijklmnopqrstuvwxyz{|}
~// ¡¢£¤¥¦§¨©ª«¬­®¯°±²³´µ¶·¸¹º»
¼½¾¿ÀÁÂÃÄÅÆÇÈÉÊËÌÍÎÏÐÑÒÓÔÕÖ×ØÙÚÛÜ
// 所有小写字母追随在大写字母之后，因为它们的代码更大。
// 一些像 Ö 的字母与主要字母表不同。这里，它的代码比任何从 a 到 z 的代码都要大。

**str.localeCompare(str2)**
// 如果 str 排在 str2 前面，则返回负数。
// 如果 str 排在 str2 后面，则返回正数。
// 如果它们在相同位置，则返回 0。
alert( 'Österreich'.localeCompare('Zealand') );
// -1
```

#### 内部，Unicode

##### 代理对

##### 变音符号与规范化

### 数组

### 数组方法

### Iterable object（可迭代对象）

### Map and Set（映射和集合）

### WeakMap and WeakSet（弱映射和弱集合）

### Obje.keys，values，entries

### 解构赋值

### 日期和时间

### JSON 方法，toJSON

## 二

### Document

#### 浏览器环境，规格

#### DOM 树

#### 遍历 DOM

#### 搜索：getElement*，querySelector*

#### 节点属性：type，tag 和 content

#### 特性和属性（Attributes and properties）

#### 修改文档（document）

#### 样式和类

#### 元素大小和滚动

#### Window 大小和滚动

#### 坐标

### 事件简介

#### 浏览器事件简介

#### 冒泡和捕获

#### 事件委托

#### 浏览器默认行为

#### 创建自定义事件

### UI事件

#### 鼠标事件

#### 移动鼠标：mouseover/out，mouseenter/leave

#### 鼠标拖放事件

#### 指针事件

#### 键盘：keydown 和 keyup

#### 滚动

### 表单，控件

#### 表单属性和方法

#### 聚焦：focus/blur

#### 事件：change，input，cut，copy，paste

#### 表单：事件和方法提交

### 加载文档和其他资源

#### 页面生命周期：DOMContentLoaded，load，beforeunload，unload

#### 脚本：async，defer

#### 资源加载：onload，onerror

### 杂项

#### DOM 变动观察器（Mutation observer）

#### 选择（Selection）和范围（Range）

#### 事件循环：微任务和宏任务

# 其他文章
