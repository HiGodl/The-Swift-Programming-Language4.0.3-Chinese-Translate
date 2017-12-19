作为编程语言学习的传统，我们来通过一个“Hello，World！”来开始我们的Swift教程。在Swift中，我们可以通过简单的一行来实现：

```
print("Hello, World!")
```

如果你写过C或者Objective-C， 这个语法看起来并不陌生——在Swift中，这行代码就是一个完整的程序。你不需要为了某些例如input/output操作或者字符串处理引入其他的库。写在顶级作用域的代码就可以作为程序的入口，所以不需要添加main\(\)函数。也不需要像其他语言一样在每个语句后边添加分号。

通过教程中如何完成多种编程任务的讲解，可以获得足够的用以开始Swift编程的信息。即使有些内容不是很清楚也无需担心——所有在此教程中提到的内容在本书后边内容中都会有详细的讲解。

```
NOTE

在Mac上可以下载Playground然后双击该文件在Xcode中打开：https://developer.apple.com/go/?id=swift-tour
```

#### 简单值

let 定义常量，var 定义变量。在编译时并不需要知道常量的值具体是多少，但是在定义常量的时候必须给常量赋值。这说明你可以通过常量来定义一个在多处使用的值。

```
var varmyVariable=42
myVaruable = 50
let myConstant = 42
```

在给常量或者变量赋值时，必须确保赋给常量或者变量的值类型必须同常量或变量的类型一致。但是并不是任何时候都需要明确的写出常量或者变量的类型。当定义常量或者变量的同时赋值，编译器会自动推断出常量或者变量的类型。在上面的例子中，编译器会根据赋予的整型值推断出“myVariable”是的类型是整型。

如果初始化并没有提供足够的信息（或者没有初始值），在变量后面写清该变量的类型，通过冒号隔开。

```Swift
let implicitInteger=70
let implicitDouble = 70.0
let explicitDouble: Double = 70
```

```
实验
通过写明数据类型定义一个初始值为4的Float常量
```

在Swift中不允许隐式的转换数据类型。如果需要进行数据类型转换，需要通过目标类型的转换方法来进行数据转换

```
let lable = "The width is "
let width = 94
let widthLable = lable + String(width)
```

```
实验
试着将最后一行的String转换语句删掉，直接+width，看看会出现什么错误
```

下面提供了更简单的在字符串中插入其他值的方法：将要插入字符串中的值写在圆括号中，在圆括号的最前面添加一个反斜杠"\"。如下：

```
let apples = 3
let oranges = 5
let appleSummary = "I have \(apples) apples."
let fruitSummary = "I have \(apples + oranges) pieces of fruit."
```

```
实验
在\()中添加一个浮点数计算表达式添加到字符串，并且完成在问候语中包含某个人的姓名
```

可以使用三个双引号定义多行字符串。默认三个双引号中的多行字符串不包含缩进，如下：

```
let quotation = """
I said "I have \(apples) apples."
And then I said "I have \(apples + oranges) pieces of fruit."
""”
```

使用方括号定义数组和字典”\[ \]“ ， 可以通过数组索引及字典键值获取集合中元素。最后一个元素后边可以有逗号。

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

给变量赋值或者作为方法参数传递时，如果能够推断出类型，空数组可以写成 \[\] ，空字典可以写成\[:\]。

```
shoppingList = []
occupations = [:]
```

#### 流程控制

使用if和switch实现条件控制，使用for-in，while，repreat-while实现循环。条件语句或者循环控制变量的圆括号是可以省略的，但是执行语句的花括号必须要写。

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

在if语句中，条件表达式结果必须为布尔值——也就是说在 if score {....}是错误的，并不包含与0的隐式的比较。

可以使用 if let 来判断某些值是否存在。这些值可以看做是可选值。可选值的值可以为具体值或者用nil表示没有值。在定义变量的值类型后边加问号”？“表示这个变量的值为可选值（可以为具体值或者为nil）。

```
var optionalString: String? = "Hello"
print(optionalString == nil)

var optionalName: String? = "John Appleseed"
var greeting = "Hello!"
if let name = optionalName {
    greeting = "Hello, \(name)"
}
```

```
试验

将optionalName的值设为nil，看看会得到什么结果？添加else分句当optionalName为nil时设置另外一个问候语
```

如果可选值为nil时，条件结果为false，在该分句中的代码就会跳过。如果可选值不为nil，就会将该值赋给let后边的常量，并执行分句中代码，分句代码中也可以正常使用该常量。

另一种操作可选值的方法是通过”??“操作符给可选值设置一个默认值。如果可选值的值没有设置就会使用默认值。

```
let nickName: String? = nil
let fullName: String = "John Appleseed"
let informalGreeting = "Hi \(nickName ?? fullName)”
```

Switch语句支持多种数据格式以及多种比较类表达式——不在限制于值支持整型和相等判断。

```
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

```
试验

去掉default条件看看会有什么错误？
```

注意上例中如何使用 let 将满足筛选条件的值赋给常量的

在swift中switch语句在执行完第一个满足条件的语句后并不会继续执行后边的语句而是直接跳出Swich表达式，因此在每个条件执行完之后并不需要明确写出break来跳出switch表达式。

可以通过for-in并提供两个名称接收字典的键值对来遍历字典。由于字典是无序集合，所以在遍历的时候输出顺序是随机的。

