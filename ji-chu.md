尽管Swift是一个用来写 iOS, macOS, watchOS 及 tvOS 应用的新语言，但是如果你以前写过C以及 Objective-C 的话，用起来并不会感到陌生。

Swift 使用自己的方式实现了 C 和 Objective-C 中所有类型，包括`Int`(整型)，`Double`和`Float`（浮点数）， `Bool`(布尔值)，`String`（字符串）。Swift 也提供了三种主要的集合，`Array`,`Set`,`Dictionary`，在 [集合类型]() 章节中有详细描述。

像C语言一样，Swift通过指定名称来存储关联变量。Swift中也大量使用了不可变的变量，也就是常量，并且在Swift中常量要比在 C 语言中要强大的多。在编码过程中如果有不需要改变的值的时候，可以通过常量使得代码更加安全、简洁，这种用法在Swift中随处可见。

除了我们所熟知的数据类型，Swift 中还提供了在 Objective-C 中并没有定义的数据类型，例如元组（tuples）。可以使用元组定义传递一组值。同时也可以通过元组在方法返回值中包含多个值。

Swift也提供了可选值类型（optional types），用来处理一个值是否存在。可选值可以告诉你“有一个等于x的值”或者“根本就没有值”。可选值在Swift中的用法类似与在 Objective-C 中的空指针`nil`，但是可选类型并不是只能用与类对象，它可以给任何类型使用。可选值不只比 Objective-C 中的空指针更安全和易理解， 它也是Swift许多强大特性的核心。

Swift 是类型安全的语言，也就是Swift可以帮你确定你在编码过程中可以使用的类型。如果代码某一部分需要传入一个`String`类型的值，类型安全检查机制会阻止你传入除`String`之外的其他类型。同样的，如果一段代码需要传入一个费可选类型的`String`， 类型安全检查机制会阻止你传入一个可选类型的`String`。类型安全检查机制可以最大限度的提早告知编码过程中的错误。

####常量和变量

常量或变量通过自定义名称表示（例如`maximumNumberOfLoginAttempts`和`welcomeMessage`）指定为特定类型的值（例如数字`10`或字符串`Hello`）。常量的值设置之后不可变，变量的值在设置之后是可以修改的。

#####声明常量和变量

常量和变量在使用之前必须声明。使用`let`声明常量，`var`声明变量。下面的例子中说明了如何使用常量和变量记录用户登录尝试次数：

```Swift

let maximumNumberOfLoginAttempts = 10
var currentLoginAttempt = 0

```

代码解读：
“声明一个名为`maximumNumberOfLoginAttempts`的常量，赋值为10；声明一个名为`currentLoginAttempt`的变量，赋值为0。”

在上例中，因为最大尝试次数是一个固定值，并不会改变，所以声明为常量。而登录尝试次数在每次登陆失败之后都需要加一，所以用声明为变量。

可以在一行代码中声明多个常量或变量：

```Swift
var x = 0.0, y = 0.0, z = 0.0
```

>注意
>>通常使用`let`声明常量，也就是在代码执行过程中不需要改变的值。变量用来存储在程序运行过程中需要改变的值。


#####类型注解

在声明常量或变量的时候可以通过添加注解的方式确定常量或变量可以存储的值类型。通过常量或变量名加冒号加空格加类型的方式定义。

我们通过下例中给`welcomeMessage`的变量指定为`String`的方式说明一下如何定义：

```Swift

var welcomeMessage: String

```

该句中的分号意义是“...的类型为...”，所以我们可以这样来解读这句代码：

"声明一个类型为`String`的变量`welcomeMessage`"。

类型为`String`也就是可以且只能存储任何`String`类型的值。

`welcomeMessage`可以设置任何字符串的值

```Swift

welcomeMessage = "Hello"

```

可以在一行中定义多个同类型的变量，变量间用逗号隔开，在最后添加数据类型，用分号将数据类型与变量名隔开：

```Swift

var red, green, blue: Double

```

>注意
>>在实际工作中我们很少用到类型注解。在声明变量或常量的同时给变量或常量赋值，Swift 可以从赋值推断出变量或常量的实际类型，在[类型安全和类型推断]()中有详细讲解。在 `welcomeMessage` 例子中，由于在声明变量的时候没有给定初始化值，所以需要明确指明该变量的类型是什么。


#####变量和常量的命名

变量和常量的命名几乎可以包含任何字符，包括 Unicode 字符：

```Swift

let π = 3.14159
let 你好 = "你好世界"
let 🐶🐮 = "dogcow”

```

常量和变量名称不能包含空白字符，数学运算符，箭头，私有（或无效）的Unicode字符，或者线条 "-"和框图字符。可以在名称中包含数字，但数字不能放在最前。

只要声明过确定类型的变量或常量，就不能再其他地方再次声明，也不允许用该变量存储其他类型的值。常量和变量也不能互相转换。

>注意
>>如果需要将常量或变量以 Swift 保留关键字命名时，需要使用将关键字写在 " `` " 中。除非没有其他选择否则尽量不要使用关键字作为常量或变量的名称。

可以将变量的值替换为该类型的其他值，下例中就将 `friendlyWelcome` 的值由 `Hello!` 改为 `Bonjour!` :

```Swift

var friendlyWelcome = "Hello!"
friendlyWelcome = "Bonjour!"
// friendlyWelcome is now "Bonjour!

```

但是常量就不一样了，一旦声明并赋值，常量的值就不能再改变。如果非要这样做的话，在代码编译的时候编译器会报错：

```Swift

let languageName = "Swift"
languageName = "Swift++"
// This is a compile-time error: languageName cannot be changed.

```


#####输出常量和变量

可以使用 `print(_:separator:terminator:)` 方法输出常量或变量：

```Swift

print(friendlyWelcome)
// Prints "Bonjour!"

```

`print(_:separator:terminator:)` 方法是全局方法，可以将常量或变量输出到合适的地方。例如在 Xcode 中，会将结果输出到 `console` 面板上。 `separator` 和 `terminator`参数有默认值，所以在调用该方法的时候可以忽略这两个参数。输出结束之后默认会添加换行符。如果想在输出完成之后不添加换行，则需要给 `terminator` 传入一个空字符串——例如 `print(someValue, terminator: "")` 。关于给参数设置默认值，请参考 [参数默认值]() 章节

Swift 通过字符串插入操作符在长字符串中添加常量或变量，在执行时 Swift 会及时的将其转换为常量或变量此时的的值。将常量或变量的名称写在圆括号中，并在圆括号前加反斜杠：

```Swift

print("The current value of friendlyWelcome is \(friendlyWelcome)")
// Prints "The current value of friendlyWelcome is Bonjour!

```

>注意
>>所有可以使用的在字符串中插入值的操作，请参考 [字符串插值]() 章节


####注释

可以通过注释写一些笔记或者提醒，注释并不会执行。当 Swift 编译器编译时会自动跳过注释内容。

Swift 中的注释几乎和 C 中一样。 单行注释以双斜杠开头：

```Swift

// This is a comment.

```

多行注释以 "`/*`" 开头 "`*/`" 结尾

```Swift

/* This is also a comment
 but is written over multiple lines. */

```

在Swift中，多行注释是可以嵌套的，这一点有别与 C 语言。

```Swift

“/* This is the start of the first multiline comment.
 /* This is the second, nested multiline comment. */
 This is the end of the first multiline comment. */

```

Swift 中的嵌套注释可以很轻松的注释掉一大段包含多行注释的代码。


####分号

不像其他语言一样，Swift可以省略掉每行代码之后的分号，当然如果愿意的话是可以写上的。但是如果一行中有多个操作的话，则需要使用分号将每个操作隔开。

```Swift

let cat = "🐱"; print(cat)
// Prints "🐱”

```



