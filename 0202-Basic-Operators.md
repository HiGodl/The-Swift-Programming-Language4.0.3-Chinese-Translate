运算符是用来检查、改变、结合值的特殊符号或表达。例如使用加法运算符（`+`） 使两个值相加 `let i = 1 + 2`， 通过逻辑与运算符（`&&`）结合两个布尔值 `if enteredDoorCode && passedRetinaScan`。

Swift 支持大部分 C 语言中的标准运算符并且加入了消除常见编码错误的能力。为了能够防止在使用判等(`==`)符号在使用时错写为赋值符号(`=`)，赋值符号在使用时并没有返回值。算数符号(`+, -, *, /, %`等等)为了避免在存储的数据超出当前类型所允许的范围是出现非预期结果，在使用时会进行检查以避免溢出。可以使用溢出运算符定义数据溢出时的操作，详细参见[溢出运算符](0226-Advanced-Operators.md#overflowOperators)章节。

Swift还提供了在 C 中并没有定义的范围运算符，例如`a..<b`，`a...b`，作为一定范围内一组值的简写表达方式。

本章节介绍了Swift中基础运算符。[高级运算符](0226-Advanced-Operators.md) 章节讲解了高级运算符的使用，并且描述了如何自定义运算符以及如何重写运算符的默认实现方式。

####术语
运算符分为一元、二元、三目运算符：

- 一元运算符直接作用于单个数值（例如`-a`），前置一元运算符直接写在被操作数的前面（例如`!b`），后置一元运算符写在被操作数之后(例如`c!`)。

- 二元运算符作用于两个数值(例如`2 + 3`)且写于两个被操作数中间。

- 三目运算符作用于三个数值。像 C 一样，Swift中只有一种三目运算符，是一个条件运算符(`a ? b : c`)

运算符影响的值为操作数。在表达式`1 + 2`中，`+` 是二元运算符，`1`和`2`是两个操作数。

####赋值运算符

赋值运算符(`a = b`)使用值`b`初始化或更新`a`的值：

```Swift

let b = 10
var a = 5
a = b
// a is now equal to 10

```

如果赋值运算符右侧是元祖或者复合值，它的元素可以一次性分解为多个常量或变量：

```Swift

let (x, y) = (1, 2)
// x is equal to 1, and y is equal to 2

```

与 C 和 Objective-C 不同的是，Swift中的赋值运算符并不返回任何值。下面例子中的写法是错误的：

```Swift

if x = y {
    // This is not valid, because x = y does not return a value.
}

```

这个特性可以防止在使用判等符号（`==`）时误用为赋值运算符（`=`）。通过定义`if x = y`为非法状态，Swift编码过程中可以避免此类错误的产生。


####算数运算符

对于数值类型，Swift支持四种标准算数运算符：

- 加法（`+`）
- 减法（`+`）
- 乘法（`*`）
- 除法（`/`）

```Swift
1 + 2       // equals 3
5 - 3       // equals 2
2 * 3       // equals 6
10.0 / 2.5  // equals 4.0

```

与 C 和 Objective-C 不同的是，Swift算符运算符默认不允许有溢出。可以选择是否使用溢出运算符来进行操作(例如`a &+ b`)。参见[溢出运算符](0226-Advanced-Operators.md#overflowOperators)

加法运算符也支持字符串连接：

```Swift

hello, " + "world"  // equals "hello, world”

```


#####取余运算符
取模运算符（`a % b`）用来得到 `a/b` 的余数。

>注意
>>取余运算符(`%`) 在其他语言中被称为取模运算符。然而严格来说对于该运算符对于负数的运算结果，取余更合适些。

下面我们来说取余运算符如何工作。计算`9%4`， 首先要算出在`9`中有多少个`4`：

![](/assets/WX20180131-150224@2x.png)

你会发现，在`9`中包含2个`4`，余数为`1`（橙色部分）。

Swift中，你可以这样写：

```Swift
9 % 4    // equals 1
```

为了得到`a%b`的结果，`%`运算符会通过下面的公式计算并最终将`remainder`作为返回值：

```Swift

a = (b x some multiplier) + remainder

```

`some multiplier`是`a`中最多能包含多少个`b`的值。

将`9`和`4`填入上面的公式中就是：

```Swift
9 = (4 x 2) + 1
```

对于负数的余数同样如此：

```Swift
-9 % 4 //equals -1
```

将`-9` 和 `4` 填入公式中：

```
-9 = (4 x -2) + -1
```

余数为`-1`

在计算中并不会考虑`b`为负数的情况，也就是`a % b`与`a % -b`得到的结果是一样的。

#####一元减法运算符

可以通过在数值类型前加`-`(也就是一元减法运算符)来取反：

```Swift
let three = 3
let minusThree = -three       // minusThree equals -3
let plusThree = -minusThree   // plusThree equals 3, or "minus minus three”

```
一元减法运算符直接写在被操作数的前面，不能有空格。

#####一元加法运算符

一元加法运算符(`+`)直接返回被操作数的值，并不会作任何改变：

```Swift
let minusSix = -6
let alsoMinusSix = +minusSix  // alsoMinusSix equals -6
```
虽然一元加法运算符并不会作任何事，但是在使用正数的同时有负数的存在，可以通过添加一元加法运算符保持代码的对称性。

####复合赋值运算符

像C一样，在Swift中提供了复合赋值运算符（将`=`与其他运算符结合）。例如加法赋值运算符(`+=`):
```Swift
var a = 1
a += 2
// a is now equal to 3

```

表达式 `a += 2` 为`a = a + 2` 的简写形式。将加法运算符与赋值运算符结合为一个同时进行两种操作的运算符写起来更加方便。

>注意
>>复合赋值运算符并没有返回值。例如`let b = a+= 2`是不对的。

更多Swift标准库提供的运算符的信息，请参考[运算符声明](https://developer.apple.com/documentation/swift/operator_declarations)


<span id="comparisonOperators"></span>

####比较运算符
Swift提供所有C标准库的比较运算符：

- 等于 (a == b)
- 不等 (a != b)
- 大于 (a > b)
- 小于 (a < b)
- 大于等于 (a >= b)
- 小于等于 (a <= b)

>注意
>>Swift 也提供两种恒等运算符 (identity operator) (===和!==)，用来判断两个对象是否引用同一个实例。更多信息请参考[类和结构体](0209-Classes-And-Structures.md)

比较运算符会返回`Bool`值来表明该表达式是否正确：

```Swift
1 == 1   // true because 1 is equal to 1
2 != 1   // true because 2 is not equal to 1
2 > 1    // true because 2 is greater than 1
1 < 2    // true because 1 is less than 2
1 >= 1   // true because 1 is greater than or equal to 1
2 <= 1   // false because 2 is not less than or equal to 1
```

比较运算符经常用在条件表达式中，例如`if`表达式：

```Swift
let name = "world"
if name == "world" {
    print("hello, world")
} else {
    print("I'm sorry \(name), but I don't recognize you")
}
// Prints "hello, world", because name is indeed equal to "world".
```

更多`if`表达式的信息，请参考[流程控制](0205-Control-Flow.md) 章节

如果两个元组中包含相同类型相同个数的元素，可以通过比较运算符进行比较。元组比较的顺序是从左到右，一次比较一个值，直到两个值不同为止。比较两个不同的值，并将比较结果作为元组的比较结果。如果所有元素都相等，那么元组也相等。例如：

```Swift
(1, "zebra") < (2, "apple")   // true because 1 is less than 2; "zebra" and "apple" are not compared
(3, "apple") < (3, "bird")    // true because 3 is equal to 3, and "apple" is less than "bird"
(4, "dog") == (4, "dog")      // true because 4 is equal to 4, and "dog" is equal to "dog”

```

在上面例子中，第一行说明了元组从左向右比较的特性。因为`1` 小于 `2`，`(1, "zebra")` 便小于 `(2, "apple")`， 无论后面元素是啥都无所谓。即使`zebra`大于`apple`，由于此次比较已经在第一个元素处结束了，所以对结果并没有影响。但如果第一个元素相同的时候，就会继续比较第二个元素——例子中的第二行代码便说明了此问题。

只有在元组中的元素可以通过比较运算符进行比较时才能通过比较运算符比较两个元组。例如在下面的代码中，可以比较两个`(String, Int)`类型的元组，因为`String`和`Int`都可以使用`<`运算符。相反，如果元组的类型为`(String, Bool)`，由于`Bool`类型不能通过`<`运算符进行比较，所以该类型元组不能使用`<`运算符进行比较。

```Swift
("blue", -1) < ("purple", 1)        // OK, evaluates to true
("blue", false) < ("purple", true)  // Error because < can't compare Boolean values
```
>注意
>>Swift标准库中，只实现了包含元素个数小于7个的元组的比较运算符。如果需要比较的元组元素个数大于等于7，那就需要自定义实现元组的比较运算符。

####三目运算符

三目运算符是是包含了三部分的特殊的运算符，格式为`question ? answer1 : answer2`。它是`question`为对或错时作不同操作的简写方式。如果`question`是对的，那么该表达式执行`answer1`并返回执行结果；否则执行`answer2`并返回执行结果。

三目运算符为下面代码的简写：

```Swift
if question {
    answer1
} else {
    answer2
}
```

下面我们通过计算`table`的行高来说明该运算符如何使用。如果该行包含头部的话，该行的行高为`contentHeight + 50`， 否则为`contentHeight + 20`

```Swift
let contentHeight = 40
let hasHeader = true
let rowHeight = contentHeight + (hasHeader ? 50 : 20)
// rowHeight is equal to 90
```

这个例子为下面代码的简写：

```Swift
let contentHeight = 40
let hasHeader = true
let rowHeight: Int
if hasHeader {
    rowHeight = contentHeight + 50
} else {
    rowHeight = contentHeight + 20
}
// rowHeight is equal to 90
```

第一个例子中表明了`rowHeight`可以用三目运算符通过一行代码设置合适的高度，这要比第二个例子中的方式更简洁。

三目运算符对于只有两种情况的操作来说是一种更有效更简洁的书写方式，但是如果过度使用的话会使得代码难以理解。避免将三元条件运算符的多个实例组合成一个复合语句。

####nil聚合运算符(??)
nil聚合运算符(a ?? b) 运算方式——如果可选类型`a`有值则解包并返回`a`的值，否则返回默认值`b`。表达式`a`必须为可选类型。表达式`b`返回的必须为`a`中存储的类型。
nil聚合运算符为下面例子的简写形式：

```Swift
a != nil ? a! : b
```

上面的代码中使用了三目运算符，如果`a`不为`nil`则强制解包`a`并返回存储的值，否则返回`b`。nil聚合运算符通过简洁可读性更强的形式实现了条件检查及解包操作。

>注意
>>如果`a`的值为非空，那么`b`就不会被赋值。这种方式叫做短路求值

下面例子中通过nil聚合运算符赋值`colorNameToUse`，赋值结果为用户自定义颜色名称或者是默认颜色名称。

```Swift
let defaultColorName = "red"
var userDefinedColorName: String?   // defaults to nil
 
var colorNameToUse = userDefinedColorName ?? defaultColorName
// userDefinedColorName is nil, so colorNameToUse is set to the default of "red”
```

`userDefinedColorName`为可选字符串类型，默认值为`nil`。由于`userDefinedColorName`为可选类型，所以可以使用nil聚合运算符判断其值。在例子中，通过运算符给字符串类型的`colorNameToUse`赋初始值。由于`userDefinedColorName`为`nil`，所以`userDefinedColorName ?? defaultColorName`表达式返回值为`defaultColorName`的值`red`。

如果`userDefinedColorName`赋值为非空，再次执行该运算符检查赋值，`userDefinedColorName`就会解包并赋值给`colorNameToUse`

```Swift
userDefinedColorName = "green"
colorNameToUse = userDefinedColorName ?? defaultColorName
// userDefinedColorName is not nil, so colorNameToUse is set to "green”

```

<span id="rangeOperators"></span>
####区间运算符

Swift提供了集中区间运算符作为某一区间一组值的简写。

#####闭合区间运算符

闭合区间运算符(`a...b`)定义一组从`a`到`b`并且包含`a`和`b`的值。`a`的值必须小于等于`b`。

在遍历一组连续的值的时候闭合区间运算符比较好用，例如 `for-in` 循环：

```Swift
for index in 1...5 {
    print("\(index) times 5 is \(index * 5)")
}
// 1 times 5 is 5
// 2 times 5 is 10
// 3 times 5 is 15
// 4 times 5 is 20
// 5 times 5 is 25
```
更多`for-in`循环的介绍，请参见[流程控制](0205-Control-Flow.md)章节

#####半开区间运算符

半开区间运算符(`a..<b`)定义`a`到`b`之间不包含`b`的一组值。因为只包含第一个值，不包含最后一个值，所以叫半开。与闭合区间运算符相同，`a`必须要小于等于`b`。如果`a`和`b`相等，那么定义的区间为空。

半开区间运算符在完整遍历索引从0开始的列表（例如数组）时比较好用：

```Swift
let names = ["Anna", "Alex", "Brian", "Jack"]
let count = names.count
for i in 0..<count {
    print("Person \(i + 1) is called \(names[i])")
}
// Person 1 is called Anna
// Person 2 is called Alex
// Person 3 is called Brian
// Person 4 is called Jack
```

例子中声明的数组包含四个元素，但由于使用半开区间运算符`0..<count`只会遍历到`3`。更多关于数组的信息，请参见[数组](0204-Collection-Types.md#array)

#####单侧区间
闭合区间有一种特殊形式，可以尽可能多的遍历区间的某一侧——例如，包含数组中所有索引大于2的区间。在这种情形下，可以省略闭合区间运算符一侧的值。由于只有运算符只有一侧有值，所以成为单侧区间。如下：

```Swift
for name in names[2...] {
    print(name)
}
// Brian
// Jack
 
for name in names[...2] {
    print(name)
}
// Anna
// Alex
// Brian
```

半开区间运算符也有一种单侧的写法（只写最后的值）。跟普通写法一样，最后的值并不会包含在区间中。如下：

```Swift
for name in names[..<2] {
    print(name)
}
// Anna
// Alex
```
单侧区间不只能够用在下标上。如果单侧区间没有首值，由于程序不知道开始位置，所以是无法遍历的。但是遍历去掉尾值得单侧区间就不会有这种问题。由于无尾单侧区间是无限的，所以在遍历的时候要有一个明确的结束遍历的操作，否则会死循环。可以通过下面的方式来判断单侧区间是否包含特定的值：

```Swift
let range = ...5
range.contains(7)   // false
range.contains(4)   // true
range.contains(-1)  // true
```
####逻辑运算符

逻辑运算符用来合并或改变逻辑值`true`和`false`。Swift支持三种基于C语言的语言所支持的逻辑运算符：

-逻辑非 (`!a`)
-逻辑与 (`a && b`)
-逻辑或 (`a || b`)

#####逻辑非运算符

逻辑非运算符(`!a`)用来对布尔值取反。`true`变为`false`，`false`变为`true`。

逻辑非是前置运算符，直接写在被操作数的前面，不允许有空格。可以读作"非`a`"，看下例：

```Swift
let allowedEntry = false
if !allowedEntry {
    print("ACCESS DENIED")
}
// Prints "ACCESS DENIED”
```

`if !allowedEntry`可以读为“如果不允许进入”。后面的语句只有在“不允许进入”为`true`的时候才会执行，也就是当`allowedEntry`为`false`的时候。

在给布尔常量或变量命名的时候要保证代码的可读性与简洁性。防止双重取反或者逻辑不明确。

#####逻辑与运算符
逻辑与运算符(`a && b`)，只有在两个被操作数都为`true`的时候才返回`true`。

如果有任何一个值为`false`，整个表达式的值就为`false`。事实上，如果第一个值为`false`的时候，由于第二个值不管是啥整个表达式都不会为`true`，所以第二个值会直接略掉。这种执行方式为短路求值。

下面例子中会判断两个布尔值，只有都为`true`的时候才能进入：

```Swift
let enteredDoorCode = true
let passedRetinaScan = false
if enteredDoorCode && passedRetinaScan {
    print("Welcome!")
} else {
    print("ACCESS DENIED")
}
// Prints "ACCESS DENIED”

```

#####逻辑或运算符

逻辑或运算符（`a || b`）是由两个相邻管道字符组成的中缀操作符。两个被操作数只要有一个为`true`整个表达式就会返回`true`。

和逻辑与运算符一样，逻辑或运算符也使用了短路求值的方式。如果左侧的值为true，那么右侧就不会执行，右侧不管为何值都不会改变最终结果。

在下面的例子中，第一个布尔值`hasDoorKey`为`false`，但是第二个值`knowsOverridePassword`为`true`，因为运算符两侧有一个值为`true`，所以整个表达式的结果为`true`，通过被允许：

```Swift
let hasDoorKey = false
let knowsOverridePassword = true
if hasDoorKey || knowsOverridePassword {
    print("Welcome!")
} else {
    print("ACCESS DENIED")
}
// Prints "Welcome!”
```

#####逻辑运算符合并使用
可以在一个表达式中使用多个逻辑运算符来实现复杂操作：

```Swift
if enteredDoorCode && passedRetinaScan || hasDoorKey || knowsOverridePassword {
    print("Welcome!")
} else {
    print("ACCESS DENIED")
}
// Prints "Welcome!”

```

例子中使用了多个`&&`和`||`运算符来创建一个长表达式。然而`&&`和`||`依然对两个值进行操作，所以这个长表达式只是多个表达式写在了一起。这个例子可以这样解读：

如果已经输入了正确的门编号并且通过了视网膜扫描，或者有门钥匙，或者知道紧急密码，都可以进入。

由于`enteredDoorCode`,`passedRetinaScan`,`hasDoorKey`的值都为`false`，前两个表达式的结果为`false`，但是知道紧急密码，所以整个表达式的值依然为`true`

>注意
>>由于Swift中的逻辑运算符为从左向右执行的，多个逻辑运算符同时使用的时候也遵循此规则。


####显式括号

有些时候通过在表达式中添加圆括号可以使得表达式可读性更强。在上面的例子中，通过在第一部分添加圆括号可以使得整个表达式的意图更明确：

```Swift
if (enteredDoorCode && passedRetinaScan) || hasDoorKey || knowsOverridePassword {
    print("Welcome!")
} else {
    print("ACCESS DENIED")
}
// Prints "Welcome!”
```

括号的使用表明了前两个值是作为整个逻辑表达式的一种情况存在的。整个逻辑表达式的结果并不会改变，但是整个表达式的意图更明确可读性更强。可读性永远要摆在简洁性之前。使用括号可以使得意图更明确。










