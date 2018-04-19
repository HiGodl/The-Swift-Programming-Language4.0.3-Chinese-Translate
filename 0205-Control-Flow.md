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






<span id="earlyExit"></span>