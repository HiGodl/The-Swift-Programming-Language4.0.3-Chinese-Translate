运算符是用来检查、改变、结合值的特殊符号或表达。例如使用加法运算符（`+`） 使两个值相加 `let i = 1 + 2`， 通过逻辑与运算符（`&&`）结合两个布尔值 `if enteredDoorCode && passedRetinaScan`。

Swift 支持大部分 C 语言中的标准运算符并且加入了消除常见编码错误的能力。为了能够防止在使用判等(`==`)符号在使用时错写为赋值符号(`=`)，赋值符号在使用时并没有返回值。算数符号(`+, -, *, /, %`等等)为了避免在存储的数据超出当前类型所允许的范围是出现非预期结果，在使用时会进行检查以避免溢出。可以使用溢出运算符定义数据溢出时的操作，详细参见[溢出运算符]()章节。

Swift还提供了在 C 中并没有定义的范围运算符，例如`a..<b`，`a...b`，作为一定范围内一组值的简写表达方式。

本章节介绍了Swift中基础运算符。[高级运算符]() 章节讲解了高级运算符的使用，并且描述了如何自定义运算符以及如何重写运算符的默认实现方式。

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

与 C 和 Objective-C 不同的是，Swift算符运算符默认不允许有溢出。可以选择是否使用溢出运算符来进行操作(例如`a &+ b`)。参见[溢出运算符]()

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

更多Swift标准库提供的运算符的信息，请参考[运算符声明]()

####比较运算符
Swift提供所有C标准库的比较运算符：

- 等于 (a == b)
- 不等 (a != b)
- 大于 (a > b)
- 小于 (a < b)
- 大于等于 (a >= b)
- 小于等于 (a <= b)

>注意
>>Swift 也提供两种恒等运算符 (identity operator) (===和!==)，用来判断两个对象是否引用同一个实例。更多信息请参考[类和结构体]()

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

更多`if`表达式的信息，请参考[流程控制]() 章节

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







