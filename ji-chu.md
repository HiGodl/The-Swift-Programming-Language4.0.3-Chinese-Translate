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

####整型
整型是不包含小数部分的所有数值，例如 `42` 和 `-23`， 整型可以是有符号的(正数，零，负数)也可以是无符号的（正数和零）。

Swift 提供了 8,16,32,64位有符号和无符号的整型数。这些整型与 C 中的命名是一样的，8位无符号整型 `UInt8`， 32位有符号整型 `Int32`。像所有其他Swift中数据类型一样，整型类的命名也是以大写字母开头的。

#####整型范围
可以通过 `min` 和 `max` 属性获取整型的最小和最大值：

```Swift

let minValue = UInt8.min  // minValue is equal to 0, and is of type UInt8
let maxValue = UInt8.max  // maxValue is equal to 255, and is of type UInt8

```
这些属性值是适当大小的数字类型（例如上面的示例中的UInt8），因此可以在表达式中与其他相同类型的值一起使用。


#####Int

在实际使用过程中，并不需要使用特定大小的整型数。Swift提供了另外一种整型类型，Int，该类型的所占字节与当前操作系统平台的位宽相同：

- 在32位平台上，Int同Int32的所占字节相同
- 在64位平台上，Int同Int64的所占字节相同

除非需要指定特殊字节大小的整型值，在平时使用的时候直接用 `Int` 就可以了。可以保证代码的统一性和兼容性。就算是在32位的平台上，`Int` 也可以存储 `-2,147,483,648` 到 `2,147,483,647` 之间的整数， 就我们平时使用来说 `Int` 的范围已经足够大了。

#####UInt

Swift 也提供了无符号整型类型，`UInt` ， 与运行平台有相同的位宽：

- 32位平台， `UInt` 同 `UInt32`所占字节相同。
- 64位平台， `UInt` 同 `UInt64`所占字节相同。

>注意
>> 除非使用到与运行平台同位宽的无符号整型值的情况下使用 `UInt` ，一般情况下就算只需要存储非负数也推荐使用 `Int`。使用`Int`是为了保证代码的通用性，不必在两种数值类型间进行转换。整型匹配推断，在 [类型安全和类型推断]() 中有详细介绍。


####浮点数

浮点数指包含小数位的数值，例如`3.14159`，`0.1`， `-273.15`。

浮点类型要比整数所表示的范围大得多，存储的最大值要比 `Int` 类型大得多，最小值也要比 `Int` 类型小得多。 Swift 有两种有符号的浮点数类型：

- `Double` 表示64位浮点数。
- `Float` 表示32位浮点数。

>注意
>>`Double`类型可以精确到小数点后15位，`Float`可以精确到小数点后6位。可以根据实际需要及取值范围来确定使用哪个浮点类型。当两种类型都可以满足时比较推荐使用`Double`。


####类型安全和类型推断 

Swift是一种数据类型安全语言。数据类型安全要求在代码中表名需要具体使用哪种类型的数据。如果某段代码中需要一个 `String` 类型的数据， 则无法传入一个 `Int` 类型的值。

由于 Swift 是类型安全的，所以在编译代码的时候会将所有错误匹配的数据类型以错误形式标出。这个特性可以使得在开发过程中尽早的发现错误并改正。

类型检查机制可以帮助避免使用多种数据类型编码时可能发生的错误。但，这也不是说在声明常量或者变量的时候就必须写清常量或变量的数据类型。当在定义的时候没有指定具体的数据类型，Swift 会通过类型推断给其指定合适的数据类型。类型推断允许编译器在编译代码的时候通过特定的表达式推断出数据类型，简单的说就是通过检查你提供的值来判断数据类型。

因为有类型推断的存在，Swift会比 C 及 Objective-C 有更少的类型声明。常量和变量的类型仍是确定的，但是确定类型的工作我们基本上已经帮你做好了。

在声明有初始值的变量或常量时，类型推断及其有用。 声明变量或常量，在为其指定明确的初始值的同时，该变量或常量的类型就已经确定了。（明确的值就是直接写在代码中的值，例如下面例子中的 `42`和`3.14159`）。

例如，当你在声明一个未指定类型的常量的同时给它赋值为 `42`， Swift 会推断出你想要定义一个类型为 `Int` 的常量，因为你在声明的同事给其赋值为一个整型的值：

```Swift

let meaningOfLife = 42
// meaningOfLife is inferred to be of type Int

```

同样的，无需给一个指定浮点字面量的值指定类型，Swift 会推断出想要创建的类型为 `Double`:

```Swift
let pi = 3.14159
// pi is inferred to be of type Double

```

对于浮点数字面量的类型推断， Swift 通常选择 `Double` （而不是 `Float`）.

如果在一个表达式中包含整数和浮点数，得到的结果类型会推断为`Double`。

```Swift

let anotherPi = 3 + 0.14159
// anotherPi is also inferred to be of type Double

```

3的字面值本身并没有明确的类型，因次 `Double`  作为正确的输出类型是从加法中的浮点数字面量推断出的。


####数字的书面表达方式

数字可以按以下方式书写：

- 十进制数字， 没有前缀
- 二进制数字，以0b为前缀
- 八进制数字，以0o为前缀
- 十六进制数字，以0x为前缀

十进制7的不同写法：

```Swift

let decimalInteger = 17
let binaryInteger = 0b10001       // 17 in binary notation
let octalInteger = 0o21           // 17 in octal notation
let hexadecimalInteger = 0x11     // 17 in hexadecimal notation

```

浮点数可以写成十进制（无前缀）， 或者16进制（0x为前缀）。浮点数的小数点前后必须都要有数值（或者16进制数）。十进制数也可以有一个可选的指数，用大写或小写的e表示；16进制浮点数必须要有指数，用大写或小写p表示。

对于十进制浮点数，指数为`exp`的， 实际值为基础数值乘上 10^exp :

- `1.25e2`相当于`1.25*10^2` ，或者`125.0`
- `1.25e-2`相当于`1.25*10^-2` , 或者`0.0125`

对于十六进制指数为`exp`的数值，实际值为基础数值乘 2^exp :

- `0xFp2` 相当于 `15*2^2` ，或者`60`.
- `0xFp-2` 相当于 `15*2^-2` ，或`3.75`.

所有下面几种浮点数的写法值都为`12.1875` ：

```Swift

let decimalDouble = 12.1875
let exponentDouble = 1.21875e1
let hexadecimalDouble = 0xC.3p0

```

数字的书写可以添加其他格式化信息，以便于阅读。不管是整数或者浮点数，都可以通过以添加0或者下划线的方式为阅读提供便利。任何一种写法都不会影响数值的实际值。

```Swift

let paddedDouble = 000123.456
let oneMillion = 1_000_000
let justOverOneMillion = 1_000_000.000_000_1

```

####数值转换

通常情况下，就算用到的整数位非负数，我们在实际使用过程中声明的变量或常量依然是 `Int` 类型。在日常工作中使用默认的整型类型，可以自动匹配通过字面量推断出的值类型，并且最大程度的保证了程序的兼容性。

除非在显示外部资源的显示大小的数据，或者性能、内存使用情况或者其他必要的情况下，我们才会使用指定类型的整型数。在这些情况下使用指定大小的整型类型可以帮我们检测到内存意外泄漏并且隐含地记录了正在使用的数据的性质。

#####整型数值转换
每种数据数值数据类型使用常量或变量能够存储值的范围是不同的。`Int8`类型的常量或变量可以存储`-128`到`127`之间的数，`UInt8`类型可以存储 `0` 到 `255`之间的整数。如果使用常量或变量存储超出其类型范围的值代码编译过程中会报错：

```Swift

let cannotBeNegative: UInt8 = -1
// UInt8 cannot store negative numbers, and so this will report an error
let tooBig: Int8 = Int8.max + 1
// Int8 cannot store a number larger than its maximum value,
// and so this will also report an error

```

由于不同数值类型之间的存储范围不同，所以必须根据实际情况选择数据类型转换。这种选择可以防止隐式转换错误，并有助于在代码中明确类型转换的意图。

可以通过带转换值初始化一个新的目标类型的值来进行数值类型转换。在下例中，常量`twoThousand`是`UInt16`类型，而常量`one`是`UInt8`类型。由于值类型不同，这两个数值不能直接做加法。所以要通过`UInt16(one)`初始化一个新的`UInt16`类型的`one`， 并使用这个值来替换原来的值：

```Swift

let twoThousand: UInt16 = 2_000
let one: UInt8 = 1
let twoThousandAndOne = twoThousand + UInt16(one)

```

由于加号两侧都为`UInt16`类型的数值，所以可以进行加法操作。由于输出值是两个`UInt16`的值相加得来，所以输出值`twoThousandAndOne`也是`UInt16`类型。

`SomeType(ofInitialValue)` 是 Swift 中默认的类型初始化并赋值的方法。在具体实现中，`UInt16`有一个接收`UInt8`的初始化方法，所以这个初始化方法用来将`UInt8`类型数转换为`UInt16`类型数。在通过初始化方法给`UInt16`类型传值时，传入的值并不是任意的，需要传入`UInt16`类型初始化方法中包含的类型。通过扩展已有的类型使得初始化方法接收新的数据类型（包括自定义数据类型）会在 [扩展]() 章节中讲解。

#####整型和浮点数间的转换

整型数和浮点数之间的转换必须明确写出：

```Swift

let three = 3
let pointOneFourOneFiveNine = 0.14159
let pi = Double(three) + pointOneFourOneFiveNine
// pi equals 3.14159, and is inferred to be of type Double

```

例中，常量`three`用来创建一个新的`Double`值，用来保证加号两侧的类型相同。如果不做转换，两个数是无法相加的。

浮点数转换为整型也是需要明确写出的。整型可以通过`Double`和`Float`进行初始化：

```Swift

let integerPi = Int(pi)
// integerPi equals 3, and is inferred to be of type Int

```

通过这种方式转换，浮点数通常会去掉小数点后边的值而保留整数部分的值。也就是说`4.75`会转换为`4`，`-3.9`或转换为`-3`。

>注意
>>常量或变量相加的规则同数值的直接相加是不同的。数值`3`可以直接与数值`0.14159`相加，因为数值在其后并没有指定其类型是什么。它们的类型只有在编译器执行之后才会确定。


####类型别名

类型别名可以给已存在的类型起一个别名。可以使用`typealias`关键字定义。

类型别名可以使得已存在的类在更符合上下文语境，例如我们在对特定字节数据的外部资源进行处理的时候。

```Swift

typealias AudioSample = UInt16

```

定义完类型别名之后，可以任何地方将类型的原名用别名替换掉：

```Swift

var maxAmplitudeFound = AudioSample.min
// maxAmplitudeFound is now 0

```

例子中`AudioSample`被定义为`UInt16`的别名。由于是别名，`AudioSample.min`实际调用的是`UInt16.min`，并给`maxAmplitudeFound`提供了初始值`0`。


####布尔值

Swift中的布尔类型叫做`Bool`。由于值只能为真或假，布尔值被看做逻辑值。Swift有两个布尔常量，`true`和`false`：

```Swift

let orangesAreOrange = true
let turnipsAreDelicious = false

```

由于初始化的同时被赋值为布尔值，所以`orangesAreOrange`和`turnipsAreDelicious`被推断为布尔类型。就像`Double`和`Int`类型一样，如果在声明常量或变量的时候直接设置值为`true`或`false`，那么并不需要明确写出常量或变量的值类型为`Bool`。当常量或变量通过其他已经确定之类行的值进行初始化的时候，类型推断可以使得我们的代码更加简洁易读。

布尔值在使用`if`之类的条件语句时非常有用：

```Swift

if turnipsAreDelicious {
    print("Mmm, tasty turnips!")
} else {
    print("Eww, turnips are horrible.")
}
// Prints "Eww, turnips are horrible.”

```

`if`之类的条件语句在 [流程控制]() 章节中有详细讲解

Swift的类型安全机制确保非布尔值不能代替布尔值来执行操作。下例中会造成编译报错：

```Swift

let i = 1
if i {
    // this example will not compile, and will report an error
}

```

然而下面例子中的写法是允许的：

```Swift

let i = 1
if i == 1 {
    // this example will compile successfully
}

```

`i==1`比较结果为`Bool`类型，所以第二个例子可以通过类型检查。像`i == 1`这样的比较操作会在 [基础运算符]() 中详解。

就像在其他例子中提到的 Swift 的类型安全检查机制，这一进步可以避免某些意想不到的错误，同时可以使得特定代码的意图表达更清晰。


####元组

元组(Tuples)是由多个值组成的一个值。元组中的值可以是任何类型。

在下例中，`(404, "Not Found")` 是一个描述`HTTP`状态码的元组。我们在每次浏览网页的时候，服务器都会返回一个特殊的值作为`HTTP`状态码。当访问的网页不存在时会返回`404 Not Found`。

```Swift

let http404Error = (404, "Not Found")
// http404Error is of type (Int, String), and equals (404, "Not Found")

```

`(404, “Not Found”)` 将 `HTTP` 状态码由`Int`,`String`两种类型的值组成的元组来表示：数值和描述。它的类型可以描述为"`(Int, String)`类型的元组"。

在元组中可以包含任何数据类型的任何排列组合。可以实现`(Int, Int, Int)`或者`(String, Bool)`，或者特殊的需要使用的元组类型。

可以通过常量或者变量来接收元组中的数值，以便在后面的代码中使用：

```Swift

let (statusCode, statusMessage) = http404Error
print("The status code is \(statusCode)")
// Prints "The status code is 404"
print("The status message is \(statusMessage)")
// Prints "The status message is Not Found” 

```

在获取元组中的值的时候，如果有些值不需要，可以使用下划线“`_`”忽略掉该值：

```Swift

let (justTheStatusCode, _) = http404Error
print("The status code is \(justTheStatusCode)")
// Prints "The status code is 404”

```

或者，我们可以通过从0开始的索引值获取元组中的元素：

```Swift

print("The status code is \(http404Error.0)")
// Prints "The status code is 404"
print("The status message is \(http404Error.1)")
// Prints "The status message is Not Found”

```

我们可以在声明元组的时候给元组中的元素命名：

```Swift

let http200Status = (statusCode: 200, description: "OK")

```

命名元组中元素之后，可以通过元素名称获取元素值：

```Swift

print("The status code is \(http200Status.statusCode)")
// Prints "The status code is 200"
print("The status message is \(http200Status.description)")
// Prints "The status message is OK”

```

元组在函数返回值包含多个数值的情况下非常有用。函数在返回网页访问情况的时候可能会返回一个`(Int, String)`类型的元组来描述返回是否成功。通过返回包含两个值与类型都不相同的元素的元组，比起只能返回一种类型的一个数值函数可以提供更多的返回值的信息。更多的信息可以参考 [多返回值函数]() 章节。

>注意
>>元组在表达临时的一组有关系的数值是非常有用。并不适用于创建复杂的数据结构。如果需要的数据结构并不是作为临时使用，最好使用类或者结构体定义。更多信息请参考 [类和结构体]() 章节。


####可选值
可选值可以用在值可能不存在的情况下。可选值代表两种情况：如果值存在就可以解包可选值并获取它的具体值，或者根本就没有值。

>注意
>>在 Objective-C 及 C 语言中并没有可选值的定义。在 Objective-C 中返回值为对象的方法可以返回一个具体对象或者是 `nil`， `nil` 表示并没有对象返回。然而这种做法只能对返回值为对象的方法起作用，如果是结构体，基础C类型，或者枚举值，Objective-C 方法将返回一个特殊值（例如`NSNotFound`）来表达并没有具体值返回。Swift这种做法可以告诉方法调用者，方法的返回值是一个可选值，使用之前需要检查是否有值。Swift可以用可选值的方式表达任何类型的数值，并不需要特殊的常量来表达没有值返回的情况。


















