作为编程语言学习的传统，我们来通过一个`Hello，World！`来开始我们的Swift教程。在Swift中，我们可以通过简单的一行来实现：

```
print("Hello, World!")
```

如果你写过C或者Objective-C， 这个语法看起来并不陌生——在Swift中，这行代码就是一个完整的程序。你不需要为了某些例如`input/output`操作或者字符串处理引入其他的库。写在顶级作用域的代码就可以作为程序的入口，所以不需要添加`main()`函数。也不需要像其他语言一样在每个语句后边添加分号。

通过教程中如何完成多种编程任务的讲解，可以获得足够的用以开始Swift编程的信息。即使有些内容不是很清楚也无需担心——所有在此教程中提到的内容在本书后边内容中都会有详细的讲解。

> NOTE
>
> > 在Mac上可以下载Playground然后双击该文件在Xcode中打开：[swift-tour](https://developer.apple.com/go/?id=swift-tour)

#### 简单值

`let` 定义常量，`var` 定义变量。在编译时并不需要知道常量的值具体是多少，但是在定义常量的时候必须给常量赋值。这说明你可以通过常量来定义一个在多处使用的值。

```Swift
var varmyVariable=42
myVaruable = 50
let myConstant = 42
```

在给常量或者变量赋值时，必须确保赋给常量或者变量的值类型必须同常量或变量的类型一致。但是并不是任何时候都需要明确的写出常量或者变量的类型。当定义常量或者变量的同时赋值，编译器会自动推断出常量或者变量的类型。在上面的例子中，编译器会根据赋予的整型值推断出`myVariable`是的类型是整型。

如果初始化并没有提供足够的信息（或者没有初始值），在变量后面写清该变量的类型，通过冒号隔开。

```Swift
let implicitInteger=70
let implicitDouble = 70.0
let explicitDouble: Double = 70
```

> 实验
>
> > 通过写明数据类型定义一个初始值为4的`Float`常量

在Swift中不允许隐式的转换数据类型。如果需要进行数据类型转换，需要通过目标类型的转换方法来进行数据转换

```
let lable = "The width is "
let width = 94
let widthLable = lable + String(width)
```

> 实验
>
> > 试着将最后一行的`String`转换语句删掉，直接+width，看看会出现什么错误

下面提供了更简单的在字符串中插入其他值的方法：将要插入字符串中的值写在圆括号中，在圆括号的最前面添加一个反斜杠`\`。如下：

```
let apples = 3
let oranges = 5
let appleSummary = "I have \(apples) apples."
let fruitSummary = "I have \(apples + oranges) pieces of fruit."
```

> 实验
>
> > 在\(\)中添加一个浮点数计算表达式添加到字符串，并且完成在问候语中包含某个人的姓名

可以使用三个双引号定义多行字符串。默认三个双引号中的多行字符串不包含缩进，如下：

```
let quotation = """
I said "I have \(apples) apples."
And then I said "I have \(apples + oranges) pieces of fruit."
"""
```

使用方括号定义数组和字典`[]` ， 可以通过数组索引及字典键值获取集合中元素。最后一个元素后边可以有逗号。

```
var shoppingList = ["catfish", "water", "tulips", "blue paint"]
shoppingList[1] = "bottle of water"

var occupations = [
    "Malcolm": "Captain",
    "Kaylee": "Mechanic",
]
occupations["Jayne"] = "Public Relations”
```

可以通过初始化方法新建空数组或字典。

```
let emptyArray = [String]()
let emptyDictionary = [String: Float]()
```

给变量赋值或者作为方法参数传递时，如果能够推断出类型，空数组可以写成`[]` ，空字典可以写成`[:]`。

```
shoppingList = []
occupations = [:]
```

#### 流程控制

使用`if`和`switch`实现条件控制，使用`for-in，while，repreat-while`实现循环。条件语句或者循环控制变量的圆括号是可以省略的，但是执行语句的花括号必须要写。

```
let individualScores = [75, 43, 103, 87, 12]
var teamScore = 0
for score in individualScores {
    if score > 50 {
        teamScore += 3
    } else {
        teamScore += 1
    }
}
print(teamScore)
```

在`if`语句中，条件表达式结果必须为布尔值——也就是说在 `if score {....}`是错误的，并不包含与0的隐式的比较。

可以使用 `if let` 来判断某些值是否存在。这些值可以看做是可选值。可选值的值可以为具体值或者用nil表示没有值。在定义变量的值类型后边加问号`？`表示这个变量的值为可选值（可以为具体值或者为nil）。

```
var optionalString: String? = "Hello"
print(optionalString == nil)

var optionalName: String? = "John Appleseed"
var greeting = "Hello!"
if let name = optionalName {
    greeting = "Hello, \(name)"
}
```

> 试验
>
> > 将optionalName的值设为`nil`，看看会得到什么结果？添加`else`分句当`optionalName`为`nil`时设置另外一个问候语

如果可选值为`nil`时，条件结果为`false`，在该分句中的代码就会跳过。如果可选值不为`nil`，就会将该值赋给`let`后边的常量，并执行分句中代码，分句代码中也可以正常使用该常量。

另一种操作可选值的方法是通过`??`操作符给可选值设置一个默认值。如果可选值的值没有设置就会使用默认值。

```
let nickName: String? = nil
let fullName: String = "John Appleseed"
let informalGreeting = "Hi \(nickName ?? fullName)”
```

`Switch`语句支持多种数据格式以及多种比较类表达式——不在限制于值支持整型和相等判断。

```Swift
let vegetable = "red pepper"
switch vegetable {
case "celery":
    print("Add some raisins and make ants on a log.")
case "cucumber", "watercress":
    print("That would make a good tea sandwich.")
case let x where x.hasSuffix("pepper"):
    print("Is it a spicy \(x)?")
default:
    print("Everything tastes good in soup.")
}
```

> 试验
>
> > 去掉`default`条件看看会有什么错误？

注意上例中如何使用 `let` 将满足筛选条件的值赋给常量的

在Swift中`switch`语句在执行完第一个满足条件的语句后并不会继续执行后边的语句而是直接跳出`switch`表达式，因此在每个条件执行完之后并不需要明确写出`break`来跳出`switch`表达式。

可以通过`for-in`并提供两个名称接收字典的键值对来遍历字典。由于字典是无序集合，所以在遍历的时候输出顺序是随机的。

```
let interestingNumbers = [
    "Prime": [2, 3, 5, 7, 11, 13],
    "Fibonacci": [1, 1, 2, 3, 5, 8],
    "Square": [1, 4, 9, 16, 25],
]
var largest = 0
for (kind, numbers) in interestingNumbers {
    for number in numbers {
        if number > largest {
            largest = number
        }
    }
}
print(largest)
```

> 试验
>
> > 添加另外一个变量来确定最大的值是哪个类型的，最打的值是多少

使用`while`语句来循环执行一段代码，指到不满足条件为止。如果要确保该循环最少执行一次，需要将条件放到最后

```Swift
var n = 2
while n < 100 {
    n *= 2
}
print(n)

var m = 2
repeat {
    m *= 2
} while m < 100
print(m)
```

可以使用`..<`来确保循环在某一索引范围内执行。

```Swift
var total = 0
for i in 0..<4 {
    total += i
}
print(total)
```

`..<`操作符不包含索引中的最大值，如果要包含最大值需要使用 `...<`

#### 

#### 方法和闭包

使用func定义方法。通过方法名调用方法，方法参数写在方法名后的圆括号中。使用`->`将参数名及参数类型与返回值类型隔开



```Swift
func greet(person: String, day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet(person: "Bob", day: "Tuesday")

```

>试验
>>将`day`这个参数移除。在问候中添加一个包含午餐的参数

通常情况下，参数名默认为方法参数标签，可以在参数名前添加自定义参数标签，或者使用`_`来代表无参数标签

```Swift
func greet(_ person: String, on day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet("John", on: "Wednesday")

```









