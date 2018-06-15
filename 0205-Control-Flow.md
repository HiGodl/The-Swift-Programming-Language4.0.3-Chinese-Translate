Swift提供了多种流程控制语句。包括`while`用来多次执行某一任务；`if`,`guard`和`switch`语句通过特定的条件执行不同的分支；`break`和`continue`打断代码流程执行并转到其他位置。

Swift也提供了``循环使得对数组，字典，范围，字符串和其他序列的遍历更加简便。

Swift的`switch`语句要比其他C类的语言等更强大。case 还可以匹配很多不同的模式，包括间隔匹配（interval match），元组（tuple）和转换到特定类型。`switch`的case中匹配的值可以包装成临时的常量或者变量以供case体使用，并且可以使用`where`来描述更复杂的匹配条件。


<span id="for-inLoops"></span>
#### For-In 循环

可以使用`for-in`循环来遍历序列，例如数组中的元素，一定范围的数字，或者字符串中的字符。

下面例子中使用`for-in`来遍历数组中的元素：

```Swift
let names = ["Anna", "Alex", "Brian", "Jack"]
for name in names {
    print("Hello, \(name)!")
}
// Hello, Anna!
// Hello, Alex!
// Hello, Brian!
// Hello, Jack! 
```

也可以用来遍历字典中的键值对。字典中的每个元素在遍历的时候都会返回一个`(key, value)`格式的元组，可以将元祖拆分成指定名称的常量以供`for-in`的方法体使用。在下面例子中，字典的键被拆分为名为`animalName`的常量，值被拆分为名为`legCount`的常量：

```Swift
let numberOfLegs = ["spider": 8, "ant": 6, "cat": 4]
for (animalName, legCount) in numberOfLegs {
    print("\(animalName)s have \(legCount) legs")
}
// ants have 6 legs
// spiders have 8 legs
// cats have 4 legs 
```

`Dictionary`的内容并不是有序的，所以在遍历的时候并不能保证取回某个元素的顺序。更多关于数组和字典的介绍，请参见[集合类型](0204-Collection-Types.md)

也可以使用`for-in`循环来遍历数值范围。下面的例子用来输出乘 5 乘法表前面一部分内容：

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

例子中用来进行遍历的元素是使用闭区间操作符（...）表示的从1到5的数字区间。`index`被赋值为闭区间中的字一个数字`1`，然后循环中的语句执行一次。在这个例子中，循环体中只包含一个语句，用来输出当前`index`的值对应的乘`5`的乘法表的结果。执行完语句之后，`index`的值就变为闭区间的第二个值`2`，然后`print(_:separator:terminator:)`方法再次执行。该过程会一直运行到闭区间结尾。

上例中，`index`常量会在每次遍历开始时自动赋予新的值。所以，`index`并不需要在使用之前声明。无序使用`let`关键字，循环语句的声明会对其进行隐式声明。

如果在遍历中并不需要序列中的值，那么可以使用`_`代替变量名：

```Swift
let base = 3
let power = 10
var answer = 1
for _ in 1...power {
    answer *= base
}
print("\(base) to the power of \(power) is \(answer)")
// Prints "3 to the power of 10 is 59049" 
```

上面的例子用来计算base的power次幂（在例子中是`3`的`10`次幂），使用`1`到`10`的闭区间来代表10次。在这个计算中，每一次循环并不需要知道计数器的具体值——该循环只需要执行指定的次数就好了。使用`_`可以忽略掉当前的值，并且在每次循环中不提供对当前值得访问。

在某些情景下，可能并不需要使用闭合区间（包含区间两端的值）。例如我们画表盘上的分钟标记。从`0`分钟开始你需要画`60`个分钟标记。半开闭区间`..<`运算符只包含开始值不包含结束值。更多关于区间的说明，请参见[](0202-Basic-Operators.md#rangeOperators)。

```Swift
let minutes = 60
for tickMark in 0..<minutes {
    // render the tick mark each minute (60 times)
} 
```

某些用户并不需要在UI上有那么多的分钟标记。他们可能希望每五分钟一个。那么使用`stride(from:to:by:)`可以跳过不需要的标记。

```Swift
let minuteInterval = 5
for tickMark in stride(from: 0, to: minutes, by: minuteInterval) {
    // render the tick mark every 5 minutes (0, 5, 10, 15 ... 45, 50, 55)
} 
```

闭合区间和有类似的方法，只是参数名略有不同`stride(from:through:by:)`：

```Swift
let hours = 12
let hourInterval = 3
for tickMark in stride(from: 3, through: hours, by: hourInterval) {
    // render the tick mark every 3 hours (3, 6, 9, 12)
} 
```
#### While 循环

`while`循环用来循环执行一组语句，直到条件为`false`。这类循环适合使用在第一次迭代前，迭代次数未知的情况下。Swift 提供两种while循环形式：

- `while`每次在循环开始时计算条件是否符合；
- `repeat-while`每次在循环结束时计算条件是否符合

##### while
`while`循环有单一的判断条件开始。如果条件为`true`，将会循环执行一段语句，直到条件变为`false`

下面我们来看一个叫做*Snakes and Ladders* （也叫做*Chutes and Ladders*）：

![](/assets/WX20180419-154131@2x.png)

游戏的规则如下：

- 游戏板上有25个方格，目标就是到达或者越过标号为25的方格
- 玩家从游戏板的左下角开始，开始值为0
- 每轮开始会掷骰子，并根据骰子的数字按照上图中的轨迹移动。
- 如果最后一步恰好在梯子的底部，那么就可以直接跳到梯子的顶部。
- 如果最后一步恰好在蛇头所在的格子中，那么就跳回到蛇尾所在的格子。

游戏板由一组`Int`值表示。大小由常量`finalSquare`表示，该常量用来数组的初始化以及作为胜利的标志位。由于玩家是从游戏板之外开始的，也就是所谓的”0号方格“，所以游戏板会以26个从0开始的`Int`值进行初始化，而不是25个。

```Swift
let finalSquare = 25
var board = [Int](repeating: 0, count: finalSquare + 1)
```

同时一些方格也会设置一些特殊的值来表明蛇和梯子所在的方格。梯子底部的方格会有一个正数来表明要前进的步数。蛇头所在的位置会设置一个负数表明要回退的步数。

```Swift
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08 
```

3号方格包含了一个梯子底部，该梯子可以让你跳到11号方格。我们用`board[3]`等于`+08`来表示。也就是整数`8`（`3`和`11`的差值）。为了使代码看起来更整齐，我们使用一元加法运算符`+`与一元减法运算符`-`一同使用，小于10的整数由0补齐（虽然代码格式并不是严格要求统一，但是这样做会使得代码更整洁。）

```Swift
var square = 0
var diceRoll = 0
while square < finalSquare {
    // roll the dice
    diceRoll += 1
    if diceRoll == 7 { diceRoll = 1 }
    // move by the rolled amount
    square += diceRoll
    if square < board.count {
        // if we're still on the board, move up or down for a snake or a ladder
        square += board[square]
    }
}
print("Game over!")
```

上面的例子中使用了非常简单地掷骰子的方式。`diceRoll`没有有使用获取随机数的方式，而是从`0`开始，每次加`1`的方式（超过6之后赋值为1）来代表掷骰子的结果。所以`diceRoll`的值为`1,2,3,4,5,6,1,2.....`。
掷骰子之后玩家会根据`diceRoll`来移动所在位置。当移动完之后超过或等于25，则游戏结束。为了实现游戏场景，代码会检查`square`是否小于`board`的`count`。如果`square`存在，那么就会将其与`board[square]`相加来实现梯子底部上，移蛇头下移

>注意
>> 如果不检查的话，`board[square]`可能会造成数组越界的运行时错误。

当`while`体中的语句执行结束之后，会判断循环条件来决定是否执行下次循环。当玩家移动到25号方格或者大于25，那么循环条件置为`false`游戏结束。

`while`循环比较适合这种场景。因为在`while`循环开始的时候并不知道该游戏的执行次数。而且，该循环一直到某一特定条件才结束。

#####Repeat-While

另一种 `while` 循环也就是 `repeat-while` 循环， 在判断条件之前先执行一次循环体。 然后在继续进行循环直到条件变为 `false`。

>注意
>> `repeat-while` 同其他语言中的 `do-while` 类似。

下面是 `repeat-while` 表达形式：

```Swift
repeat {
    <statements>
} while <condition>
``` 

让我们再次使用`repeat-while`而不是`while`来写*蛇和梯子*这个游戏。`finalSquare`, `board`, `square` 和 `diceRoll` 还是使用 `while` 中相同的方法来初始化。

```Swift
let finalSquare = 25
var board = [Int](repeating: 0, count: finalSquare + 1)
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
var square = 0
var diceRoll = 0
```

在这个版本的游戏中，循环中的第一步是检查梯子或者蛇。没有梯子可以直接把玩家带到25号块，也不会通过梯子直接获胜。但是，将检查蛇或梯子放在循环的第一步会更安全。

在游戏开始前，玩家在"0号块"。`board[0]` y永远等于`0`并且没有任何影响。

```Swift
repeat {
    // move up or down for a snake or ladder
    square += board[square]
    // roll the dice
    diceRoll += 1
    if diceRoll == 7 { diceRoll = 1 }
    // move by the rolled amount
    square += diceRoll
} while square < finalSquare
print("Game over!") 
```
检查完梯子和蛇之后，掷骰子并根据骰子数向前移动。当前循环结束。

循环条件（`while square < finalSquare`）跟之前的相同。但是在第一次执行结束之前循环条件判断语句并不会执行。对于这款游戏来说 `repeat-while` 比 `while` 循环更合适。 在 `repeat-while` 循环中当 `while` 循环判断条件确认 `square` 在游戏板上时会立即执行 `square += bord[square]`。 这样就可以将 `while` 中的数组越界检查操作移除掉了。

####条件控制语句

我们在开发中会经常用到根据不同的条件来执行不同代码块的场景。当发生错误的时候你可能需要执行某一段代码，或者当一个值变得太高或者太低时需要有消息提示。 要满足这样的需求就需要将某些代码放在特定的条件来执行。

Swift提供两种方式给你的代码添加条件分支： `if` 语句和 `switch` 语句。 一般的我们使用 `if` 语句来执行简单的只有少数条件分支的情境。 `switch` 推荐用来处理条件复杂分支过多的情况，对于使用正则表达式来作为判断条件是，`switch`更有优势。

##### if

最简单的形式，`if` 只有一个 `if` 条件。 当条件为 `true` 时执行一段代码。

```Swift
var temperatureInFahrenheit = 30
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
}
// Prints "It's very cold. Consider wearing a scarf." 
```

例子中检查温度是否低于32华氏温度（冰点）。 如果是，将会打印信息。否则的话不会打印任何信息，并继续执行 `if` 语句之后的代码。

`if` 语句可以提供另外一组表达，也就是*else子句*，当 `if` 条件为 `false` 的时候执行。 这部分表达通过 `else` 关键字标识。

```Swift
temperatureInFahrenheit = 40
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
} else {
    print("It's not that cold. Wear a t-shirt.")
}
// Prints "It's not that cold. Wear a t-shirt."
```

这两个分支总有一个会被执行。 由于温度已经升到 `40` 华氏度以上了，所以当前的温度并不需要提示围上围巾，因此会执行 `else`分支。

可以在 `if` 表达式中添加更多的条件来适应更多的场景。

```Swift
temperatureInFahrenheit = 90
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
} else if temperatureInFahrenheit >= 86 {
    print("It's really warm. Don't forget to wear sunscreen.")
} else {
    print("It's not that cold. Wear a t-shirt.")
}
// Prints "It's really warm. Don't forget to wear sunscreen."
```

这里我们添加了一个 `if` 条件来对特定的温度条件做出回应。 最后的 `else` 字句仍然保留， 对于不是特别冷也不是特别热的情况做出回应。

最后的 `else` 字句是可选的，并且如果并不需要考虑所有条件的话我们并不非要完成所有条件的判断。

```Swift
temperatureInFahrenheit = 72
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
} else if temperatureInFahrenheit >= 86 {
    print("It's really warm. Don't forget to wear sunscreen.")
} 
```

当温度不是特别高或特别低的时候 `if` 和 `else if` 都不会执行，也不会有信息打印。


#####Switch
`switch` 表达式通过比较的方式来判断值是否符合一定的形式或者是否同某些值相等。匹配成功后会基于最近的匹配成功值执行一段代码。对于多种情况的判断语句 `swift` 为 `if` 提供了另一种表达形式。

在它的表达格式中，`switch` 会将一个特定的值与一个或多个相同类型的值的比较。

```Swift
switch some value to consider {
case value 1:
    respond to value 1
case value 2,
     value 3:
    respond to value 2 or 3
default:
    otherwise, do something else
} 
```

每个 `switch` 表达式都包括多个可能的 *case*，每个 *case* 都会以 `case` 关键字开头。为了更好的与某一特定值进行比较，Swift提供了多种满足复杂匹配条件的表达方式。这些选项会在本章稍后进行讲解

同 `if` 一样，每个 `case` 都会执行特定的代码分支。`switch` 表达式会决定要执行哪个分支。这个过程就是根据具体需要考虑的值来进行切换。

每个 `switch` 表达式必须是详尽的。也就是每种可能的值都要对应一种 `case`。如果不能提供详尽的 `case` 来覆盖所有情况的话，可以定义一个默认的 `case` 来覆盖没有被具体表述的情况。默认的 `case` 使用 `default` 关键字标识，并且要写在最后。

下面例子中使用`switch` 表达式来检查一个单个小写字符`someCharacter`。

```Swift
let someCharacter: Character = "z"
switch someCharacter {
case "a":
    print("The first letter of the alphabet")
case "z":
    print("The last letter of the alphabet")
default:
    print("Some other character")
}
// Prints "The last letter of the alphabet" 
```



`switch`表达式第一个`case`匹配字母表中的第一个字母`a`，第二个`case` 匹配最后一个字母`z`，由于`switch`必须匹配所有可能的字符，但是除了字母表中的字符之外还有很多，所以为了覆盖所有`case` `switch` 表达式在此处使用`default` 来代表所有除了`a`和`z`的所有字符。这保证了`switch`条件的完整性。

######不包含隐式贯穿
不同于C和Objective-C，Swift中的`switch`表达式并不会在执行完一个case之后继续执行之后的case。在得到第一个匹配的case之后`switch`在执行完case中的语句之后会立即退出并且不需要`break`来控制。这一点使得Swift中的`switch`表达式更加安全，并且不会像C中可能会由于误操作一次执行多个case。

>注意
>> 尽管`break`在Swift中并不会起什么作用，但是依然可以在case中使用`break`来忽略特定的case以及条件性的提前退出某个case。详细信息请参见 [Switch表达式中的break](0205-Control-Flow.md#breakInASwitchStatement)

每个case体中都必须包含至少一行表达式。下面的写法是错误的：

```Swift
let anotherCharacter: Character = "a"
switch anotherCharacter {
case "a": // Invalid, the case has an empty body
case "A":
    print("The letter A")
default:
    print("Not the letter A")
}
// This will report a compile-time error.

```

不同于C语言中的`switch`，这样写的话并不会匹配到`a`和`A`，并且由于`case "a"`中并没有包含任何可执行的表达式，会报运行时错误。这项改进可以避免意外的隐式贯穿并且使得意图更加明确。

如果想要使得一个case同事匹配`a`和`A`，需要将两个值包含在一个case中，通过逗号分隔两个值。

```Swift
let anotherCharacter: Character = "a"
switch anotherCharacter {
case "a", "A":
    print("The letter A")
default:
    print("Not the letter A")
}
// Prints "The letter A" 
```

为了使表达更清晰，可以将case分多行书写。更多信息请参见[复合case](0205-Control-Flow.md#compoundCases)

######区间匹配

`switch`的case可以检查值是否在某个区间。下面例子中通过数值区间来为任何大小的值来提供自然语言描述：

```Swift
let approximateCount = 62
let countedThings = "moons orbiting Saturn"
let naturalCount: String
switch approximateCount {
case 0:
    naturalCount = "no"
case 1..<5:
    naturalCount = "a few"
case 5..<12:
    naturalCount = "several"
case 12..<100:
    naturalCount = "dozens of"
case 100..<1000:
    naturalCount = "hundreds of"
default:
    naturalCount = "many"
}
print("There are \(naturalCount) \(countedThings).")
// Prints "There are dozens of moons orbiting Saturn."
```

在上面例子中，`approximateCount`通过`switch`表达式来进行评估。每个`case`会将该值于一个区间进行对比。由于该值在12到100之间，`naturalCount`被赋值为`"dozens of"`，执行完之后直接跳出`switch`表达式。

######元组
可以使用元组在一个`switch`表达式中比较多个值。每个元组中的元素都可以与某一个值或者一个区间进行对比。并且可以通过下划线字符`(_)`（作为通配符），匹配任何可能的值。

下面例子中使用一个简单类型`(Int, Int)`的元组来定义一个`(x, y)`的点，并使用`switch`将点按坐标位置归类：

```Swift
let somePoint = (1, 1)
switch somePoint {
case (0, 0):
    print("\(somePoint) is at the origin")
case (_, 0):
    print("\(somePoint) is on the x-axis")
case (0, _):
    print("\(somePoint) is on the y-axis")
case (-2...2, -2...2):
    print("\(somePoint) is inside the box")
default:
    print("\(somePoint) is outside of the box")
}
// Prints "(1, 1) is inside the box" 
```

![](/assets/WX20180615-110756@2x.png)

`switch`表达式阐明了这个点是在原点（0，0），x轴，y轴，在蓝色方框中还是蓝色方框外。

与C语言不同的是，Switch中的`switch`允许多个case中包含相同的值。事实上，（0，0）可以匹配该表达式中所有的case，但是，如果多有多个匹配的话，永远会执行第一个匹配的case。（0，0）将会匹配`case (0, 0)`，并且会忽略掉之后的所有case

######值绑定
如果在case的执行语句中使用匹配的值的话，`switch`可以将值赋给某一临时常量或变量。由于值被绑定到作用域为case体的临时常量或变量，所以这个行为被称作值绑定。

下面例子中使用一个简单类型`(Int, Int)`的元组来定义一个`(x, y)`的点，并使用`switch`将点按坐标位置归类：

```Swift
let anotherPoint = (2, 0)
switch anotherPoint {
case (let x, 0):
    print("on the x-axis with an x value of \(x)")
case (0, let y):
    print("on the y-axis with a y value of \(y)")
case let (x, y):
    print("somewhere else at (\(x), \(y))")
}
// Prints "on the x-axis with an x value of 2" 
```

![](/assets/WX20180615-133526@2x.png)

该`switch`表达式判断点是在红色的x轴，橙色的y轴或是其他地方。

`switch`的case中声明了`x`和`y`占位符来临时表示元组`anotherPoint`中的一个或两个值。第一个case`case (let x, 0)`，用来匹配`y`值为`0`的元组，并且将`x`的值临时赋给`x`常量。同样的在第二个case中，`case (0, let y)`匹配`x`为`0`的元组，并将`y`赋给临时常量`y`。

当临时常量声明之后，它们可以在case的代码块中使用。这里用来给point分类。

这个例子中没有`default`的case。最后一个case `case let (x, y)` 声明了一个可以匹配任意值的元组，元组中包含两个占位符。由于`anotherPoint`永远是两个值得元组，所以这个case可以匹配所有可能的未匹配的值，因此`default`在这里并不需要。

######Where

`switch`还可以使用`where`从句来添加附加条件。
下例中将（x, y）按下图中的划分分类：

```Swift
let yetAnotherPoint = (1, -1)
switch yetAnotherPoint {
case let (x, y) where x == y:
    print("(\(x), \(y)) is on the line x == y")
case let (x, y) where x == -y:
    print("(\(x), \(y)) is on the line x == -y")
case let (x, y):
    print("(\(x), \(y)) is just some arbitrary point")
}
// Prints "(1, -1) is on the line x == -y" 
```
![](/assets/WX20180615-134959@2x.png)

`switch`表达式用来判断一个点是否在绿色线上也就是`x == y`， 是否在紫色线上`x == -y`， 或者在其他地方。

`switch`中的左右case都使用占位符`x`和`y`来临时绑定`yetAnotherPoint`中的值。这些常量用来组成`where`从句中的动态筛选条件。`switch`中所有case只有在`where`从句中的判断条件为`true`时才算匹配该case。

像之前的例子一样，最后一个case用来匹配其他所有情况，所以并不需要`default`case，`switch`就是合法的。





<span id="breakInASwitchStatement"></span>
######Switch表达式中的break


<span id="compoundCases"></span>


<span id="earlyExit"></span>

