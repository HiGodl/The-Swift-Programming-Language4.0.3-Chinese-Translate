作为编程语言学习的传统，我们来通过一个`Hello，World！`来开始我们的Swift教程。在Swift中，我们可以通过简单的一行来实现：

```Swift

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

```Swift
let lable = "The width is "
let width = 94
let widthLable = lable + String(width)
```

> 实验
>
> > 试着将最后一行的`String`转换语句删掉，直接+width，看看会出现什么错误

下面提供了更简单的在字符串中插入其他值的方法：将要插入字符串中的值写在圆括号中，在圆括号的最前面添加一个反斜杠`\`。如下：

```Swift
let apples = 3
let oranges = 5
let appleSummary = "I have \(apples) apples."
let fruitSummary = "I have \(apples + oranges) pieces of fruit."
```

> 实验
>
> > 在\(\)中添加一个浮点数计算表达式添加到字符串，并且完成在问候语中包含某个人的姓名

可以使用三个双引号定义多行字符串。默认三个双引号中的多行字符串不包含缩进，如下：

```Swift
let quotation = """
I said "I have \(apples) apples."
And then I said "I have \(apples + oranges) pieces of fruit."
"""
```

使用方括号定义数组和字典`[]` ， 可以通过数组索引及字典键值获取集合中元素。最后一个元素后边可以有逗号。

```Swift
var shoppingList = ["catfish", "water", "tulips", "blue paint"]
shoppingList[1] = "bottle of water"

var occupations = [
    "Malcolm": "Captain",
    "Kaylee": "Mechanic",
]
occupations["Jayne"] = "Public Relations”
```

可以通过初始化方法新建空数组或字典。

```Swift
let emptyArray = [String]()
let emptyDictionary = [String: Float]()
```

给变量赋值或者作为方法参数传递时，如果能够推断出类型，空数组可以写成`[]` ，空字典可以写成`[:]`。

```Swift

shoppingList = []
occupations = [:]
```

#### 流程控制

使用`if`和`switch`实现条件控制，使用`for-in，while，repreat-while`实现循环。条件语句或者循环控制变量的圆括号是可以省略的，但是执行语句的花括号必须要写。

```Swift

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

```Swift

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

```Swift

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

```Swift

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

> 试验
>
> > 将`day`这个参数移除。在问候中添加一个包含午餐的参数

通常情况下，参数名默认为方法参数标签，可以在参数名前添加自定义参数标签，或者使用`_`来代表无参数标签

```Swift
func greet(_ person: String, on day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet("John", on: "Wednesday")
```

通过元组`(tuple)`来定义一个复合值——例如，方法返回多个值。元组中的值可以通过名称或者索引获取。

```Swift

func calculateStatistics(scores: [Int]) -> (min: Int, max: Int, sum: Int) {
    var min = scores[0]
    var max = scores[0]
    var sum = 0
    for score in scores {
        if score > max {
            max = score
        } else if score < min {
            min = score
        }
        sum += score
    }

    return (min, max, sum)
}
let statistics = calculateStatistics(scores: [5, 3, 100, 3, 9])
print(statistics.sum)
print(statistics.2)
```

Swift中方法可以嵌套，嵌套的方法可以访问上层方法中定义的变量。可以通过方法嵌套来组织过于长过于复杂的方法中的代码。

```Swift
func returnFifteen() -> Int {
    var y = 10
    func add() {
        y += 5
    }
    add()
    return y
}
returnFifteen()
```

方法是基础数据类型（first-class type 不太清楚这个咋翻译）。也就是说方法可以作为另一个方法的返回值。

```Swift
func makeIncrementer() -> ((Int) -> Int) {
    func addOne(number: Int) -> Int {
        return 1 + number
    }
    return addOne
}
var increment = makeIncrementer()
increment(7)
```

方法同样可以作为其他方法的参数。

```Swift
func hasAnyMatches(list: [Int], condition: (Int) -> Bool) -> Bool {
    for item in list {
        if condition(item) {
            return true
        }
    }
    return false
}
func lessThanTen(number: Int) -> Bool {
    return number < 10
}
var numbers = [20, 19, 7, 12]
hasAnyMatches(list: numbers, condition: lessThanTen)
```

方法其实是一种特殊类型的闭包：一个可以先定义后调用的代码块。不管闭包在哪里执行，都可以访问其定义作用域中的变量、方法等——其实在方法嵌套中就已经展示了这个特性。可以通过 `{()}` 来定义闭包，通过 `in` 来分割参数及闭包返回值类型。

```Swift
numbers.map({ (number: Int) -> Int in
    let result = 3 * number
    return result
})
```

> 试验
>
> > 重写闭包，使所有奇数返回值为0

通过一些可选项可以更简洁的书写闭包。当闭包的类型确定的时候，例如作为代理的回调方法，可以删掉参数的类型，返回值的类型，或者同时删掉。单语句闭包隐式的返回他们唯一语句的值

```Swift
let mappedNumbers = numbers.map({ number in 3 * number })
print(mappedNumbers)
```

我们可能更喜欢使用数字来代替名称来作为参数——这种操作对于短小的闭包来说非常实用。作为函数的最后一个参数传递的闭包可以直接写在圆括号后。当闭包作为方法的唯一参数时，可以将圆括号省略。

```Swift
let sortedNumbers = numbers.sorted { $0 > $1 }
print(sortedNumbers)
```

#### 

#### 类和对象

通过在 `class` 后添加类名来定义类。类属性的声明与常量变量的声明式一样的，唯一不同的是属性实在类中的。同样的，方法和函数的声明也是一样的。

```Swift
class Shape {
    var numberOfSides = 0
    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
```

> 试验
>
> > 通过`let`声明一个不可变的属性，声明一个含参的方法

通过`<class>()`的方法来创建类的对象。使用点 `.` 访问对象的属性及方法。

```Swift
var shape = Shape()
shape.numberOfSides = 7
var shapeDescription = shape.simpleDescription()
```

这个版本的`Shape`有一些重要的事情没有做：在初始化的时候给对象设置一些初始值的构造方法。使用 `init` 来定义构造方法。

```Swift
class NamedShape {
    var numberOfSides: Int = 0
    var name: String

    init(name: String) {
        self.name = name
    }

    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
```

注意如何使用 `self` 区分 `name` 属性和 `name` 参数，类初始化的时候初始化方法的参数传递与方法调用的参数传递基本相同。每个属性都需要赋值——定义的时候直接赋值`(numberOfSides)` 或者在类的初始化方法中赋值 `(name)`

如果在对象销毁之前需要做一些操作可以使用 `deinit` 来创建对象销毁方法

使用`class` 加类名加父类名来创建的子类，父类与类名间用冒号隔开。创建新的类的时候并不需要继承任何基类，按需确定是否要添加父类。子类中重写父类的方法时需要在前面加 `override` 修饰符 —— 如果在未加 `override` 的情况下重写了父类的方法，编译器会报错。同时编译器也会检查写明 `override` 的子类方法是否在父类中有定义。所以使用 `override` 的时候要注意。

```Swift
class Square: NamedShape {
    var sideLength: Double

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 4
    }

    func area() -> Double {
        return sideLength * sideLength
    }
    override func simpleDescription() -> String {
        return "A square with sides of length \(sideLength)."
    }
}
let test = Square(sideLength: 5.2, name: "my test square")
test.area()
test.simpleDescription()
```

>试验
>>新建一个命名为`Circle`继承于`NameShape`的子类，并且将`name`和半径作为初始化方法的参数。实现`area()`和`simpleDescription()`方法

类属性除了可以存储值意外，还可以给属性添加`get`和`set`方法。


```Swift

class EquilateralTriangle: NamedShape {
    var sideLength: Double = 0.0
    
    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 3
    }
    
    var perimeter: Double {
        get {
            return 3.0 * sideLength
        }
        set {
            sideLength = newValue / 3.0
        }
    }
    
    override func simpleDescription() -> String {
        return "An equilateral triangle with sides of length \(sideLength)."
    }
}
var triangle = EquilateralTriangle(sideLength: 3.1, name: "a triangle")
print(triangle.perimeter)
triangle.perimeter = 9.9
print(triangle.sideLength)

```

在`perimeter`的set方法中，新值的默认名称为`newValue`，当然可以通过在set方法后的圆括号中写明来指定特定的名称。

注意在`EquilateralTriangle`的初始化方法中，一共做了三件事：
    1. 给子类的属性设置初始化值
    2. 调用父类初始化方法
    3. 修改父类中初始化属性的值。所有初始化的工作包括方法调用，获取设置属性值都可以在这一步完成。

在实际开发中如果并不需要对赋给属性的值做任何处理，但是在属性赋值前后要执行特定的方法或者代码，可以使用`willSet`和`didSet`方法实现。写在这两个方法中的代码会在除了在类初始化方法中的任何给属性设置方法的时候执行。例如下例中，该类可以确保三角形的边长永远与正方形的边长相等。


```Swift

class TriangleAndSquare {
    var triangle: EquilateralTriangle {
        willSet {
            square.sideLength = newValue.sideLength
        }
    }
    var square: Square {
        willSet {
            triangle.sideLength = newValue.sideLength
        }
    }
    init(size: Double, name: String) {
        square = Square(sideLength: size, name: name)
        “triangle = EquilateralTriangle(sideLength: size, name: name)
    }
}
var triangleAndSquare = TriangleAndSquare(size: 10, name: "another test shape")
print(triangleAndSquare.square.sideLength)
print(triangleAndSquare.triangle.sideLength)
triangleAndSquare.square = Square(sideLength: 50, name: "larger square")
print(triangleAndSquare.triangle.sideLength)

```
当使用可选值的时候，可以在执行操作（方法、属性、索引取值）之前添加 `?` 。当值为 `nil` 的时候，`？` 后边的内容不会执行，整个表达式的值都为 `nil` 。 如果不是 `nil` 那么`？` 后边的内容就会正常执行。无论哪种情况，整个表达式返回的都是可选值


```Swift

let optionalSquare: Square? = Square(sideLength: 2.5, name: "optional square")
let sideLength = optionalSquare?.sideLength

```

####枚举 结构体

可以通过`enum` 新建枚举。就像类或者其他提到过的类型，枚举可以设置与相关的方法。


```Swift
enum Rank: Int {
    case ace = 1
    case two, three, four, five, six, seven, eight, nine, ten
    case jack, queen, king
    func simpleDescription() -> String {
        switch self {
        case .ace:
            return "ace"
        case .jack:
            return "jack"
        case .queen:
            return "queen"
        case .king:
            return "king"
        default:
            return String(self.rawValue)
        }
    }
}
let ace = Rank.ace
let aceRawValue = ace.rawValue

```

>实验
>>定义一个方法通过比较两个枚举值的原始数值判断两个`Rank`枚举值的大小

在Swift中枚举的原始数值从0开始并以步长1递增，但是可以通过明确写出原始数值值来改变这一默认行为。在上面的例子中，`Ace` 指定为特定的值1，其他枚举项的原始数值将会按顺序递增。也可以设置枚举原始数值为字符串或者浮点类型。通过`rawValue`属性获取枚举的原始数值。

使用 `init?(rawValue:)` 构造方法通过原始数值新建一个枚举。会返回一个对应原始数值的枚举，如果Rank中不包含该原始值则返回`nil`


```Swift

if let convertedRank = Rank(rawValue: 3) {
    let threeDescription = convertedRank.simpleDescription()
}

```
枚举中枚举项的值为实际值，并不是原始数值的另一种写法，如果原始数值并没有意义的话，可以完全省略掉。


```Swift

enum Suit {
    case spades, hearts, diamonds, clubs
    func simpleDescription() -> String {
        switch self {
        case .spades:
            return "spades"
        case .hearts:
            return "hearts"
        case .diamonds:
            return "diamonds"
        case .clubs:
            return "clubs"
        }
    }
}
let hearts = Suit.hearts
let heartsDescription = hearts.simpleDescription()

```

>试验
>>给 `Suit` 添加 `color()` 方法，`spades` 和 `clubs` 返回 `black`， `hearts` 和 `diamonds` 返回 `red`

注意上面用到 `hearts` 枚举项的两个地方：由于 `heart`常量在定义的时候并没有指定类型，所以在赋值的时候是通过`Suit.hearts`这种方式获取枚举项赋值。在`switch`语句中，因为已知`self`的类型，所以可以通过简写的方式(`.hearts`)获取枚举项。当值类型可以确认的时候可以通过简写获取枚举项。

如果枚举有原始数值，那么原始数值会作为声明的一部分存在，也就是在任何时候同一枚举项的原始数值都相同。同事我们有另外一种将枚举项与原始数值关联的方法——原始数值可以在实例化枚举的时候指定，这样在同一枚举的同一枚举项就可以设置为不同的原始数值。你可以将其看做给枚举项的属性赋值。例如，从服务器获取太阳升起落下的时间。服务器可能返回正确的信息，或者返回错误信息。

```Swift
enum ServerResponse {
    case result(String, String)
    case failure(String)
}
 
let success = ServerResponse.result("6:00 am", "8:09 pm")
let failure = ServerResponse.failure("Out of cheese.")
 
switch success {
case let .result(sunrise, sunset):
    print("Sunrise is at \(sunrise) and sunset is at \(sunset).")
case let .failure(message):
    print("Failure...  \(message)")
}
```

>试验
>>在`switch`语句及`ServerResponse`中添加第三个枚举项。

注意在`switch`语句中如何获取枚举项中服务器返回的太阳升起落下的时间。

使用`struct`定义结构体。结构体支持大部分类的操作，包括方法、构造方法。类和结构体最大的不同是传值时类对象是引用传递，结构体是值传递。

```Swift

struct Card {
    var rank: Rank
    var suit: Suit
    func simpleDescription() -> String {
        return "The \(rank.simpleDescription()) of \(suit.simpleDescription())"
    }
}
let threeOfSpades = Card(rank: .three, suit: .spades)
let threeOfSpadesDescription = threeOfSpades.simpleDescription()

```

>试验
>>为卡片添加一个创建一副完整的卡片组合方法的，每张卡片组合一个等级和套装


####协议和扩展

使用`protocol`声明代理

```Swift

protocol ExampleProtocol {
    var simpleDescription: String { get }
    mutating func adjust()
}

```

类、枚举和结构体都可以实现协议。

```Swift

class SimpleClass: ExampleProtocol {
    var simpleDescription: String = "A very simple class."
    var anotherProperty: Int = 69105
    func adjust() {
        simpleDescription += "  Now 100% adjusted."
    }
}
var a = SimpleClass()
a.adjust()
let aDescription = a.simpleDescription
 
struct SimpleStructure: ExampleProtocol {
    var simpleDescription: String = "A simple structure"
    mutating func adjust() {
        simpleDescription += " (adjusted)"
    }
}
var b = SimpleStructure()
b.adjust()
let bDescription = b.simpleDescription

```

>试验
>>定义一个实现该协议的枚举

注意在 `SimpleStructure` 中需要通过 `mutating`关键字来声明一个用来管理结构体属性的方法。但是由于类方法任何时候都对类对象有管理权，所以在`SimpleClass`中的方法不需要添加任何关键字以实现对类对象的管理

通过 `extension` 给已存在的类添加扩展功能， 例如添加新的方法或者可计算属性。可以通过扩展给定义在其他地方的类甚至是引用库中的类实现扩展。

```Swift

extension Int: ExampleProtocol {
    var simpleDescription: String {
        return "The number \(self)"
    }
    mutating func adjust() {
        self += 42
    }
}
print(7.simpleDescription)

```

>试验
>>通过扩展给`Double`类添加一个`absoluteValue`属性

我们可以像其他类型一样使用协议的名称——例如，创建一个指定协议的集合对象，集合中添加的对象必须要实现指定的协议。当使用一个协议类型的值的时候，我们只能调用协议中定义的方法，任何协议方法之外的方法我们都无法调用。

```Swift

let protocolValue: ExampleProtocol = a
print(protocolValue.simpleDescription)
// print(protocolValue.anotherProperty)  // Uncomment to see the error

```

尽管`protocolValue`的运行时类型是`SimpleClass`，编译器也会按照指定的类型（`ExampleProtocol`）处理。也就是除了协议中的方法我们无法掉用类定义的其他属性及方法。