尽管Swift是 iOS, macOS, watchOS 及 tvOS 平台应用的新语言，但是如果你熟悉 C 或者 Objective-C 的话，用起来并不会感到陌生。

Swift 使用自己的方式实现了 C 和 Objective-C 中所有类型，包括`Int`(整型)，`Double`和`Float`（浮点数）， `Bool`(布尔值)，`String`（字符串）。Swift 也提供了三种主要的集合，`Array`,`Set`,`Dictionary`，在 [集合类型](0204-Collection-Types.md) 章节中有详细描述。

像C语言一样，Swift通过指定名称来存储关联变量。Swift中也大量使用了不可变的变量，也就是常量，并且在Swift中常量要比在 C 语言中要强大的多。在编码过程中如果有不需要改变的值的时候，可以通过常量使得代码更加安全、简洁，这种用法在Swift中随处可见。

除了我们所熟知的数据类型，Swift 中还提供了在 Objective-C 中并没有定义的数据类型，例如元组（tuples）。可以使用元组定义传递一组值。同时也可以通过元组在方法返回值中包含多个值。

Swift也提供了可选类型（optional types），用来处理一个值是否存在。可选类型可以告诉你“有一个等于x的值”或者“根本就没有值”。可选类型在Swift中的用法类似与在 Objective-C 中的空指针`nil`，但是可选类型并不是只能用与类对象，它可以给任何类型使用。可选类型不只比 Objective-C 中的空指针更安全和易理解， 它也是Swift许多强大特性的核心。

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
>>在实际工作中我们很少用到类型注解。在声明变量或常量的同时给变量或常量赋值，Swift 可以从赋值推断出变量或常量的实际类型，在[类型安全和类型推断](0201-The-Basics.md#typeSafetyAndTypeInference)中有详细讲解。在 `welcomeMessage` 例子中，由于在声明变量的时候没有给定初始化值，所以需要明确指明该变量的类型是什么。


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

`print(_:separator:terminator:)` 方法是全局方法，可以将常量或变量输出到合适的地方。例如在 Xcode 中，会将结果输出到 `console` 面板上。 `separator` 和 `terminator`参数有默认值，所以在调用该方法的时候可以忽略这两个参数。输出结束之后默认会添加换行符。如果想在输出完成之后不添加换行，则需要给 `terminator` 传入一个空字符串——例如 `print(someValue, terminator: "")` 。关于给参数设置默认值，请参考 [参数默认值](0206-Functions.md#defaultParameterValues) 章节

Swift 通过字符串插入操作符在长字符串中添加常量或变量，在执行时 Swift 会及时的将其转换为常量或变量此时的的值。将常量或变量的名称写在圆括号中，并在圆括号前加反斜杠：

```Swift

print("The current value of friendlyWelcome is \(friendlyWelcome)")
// Prints "The current value of friendlyWelcome is Bonjour!

```

>注意
>>所有可以使用的在字符串中插入值的操作，请参考 [字符串插值](0203-Strings-And-Characters.md#stringInterpolation) 章节


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

let minValue = UInt8.min // minValue is equal to 0, and is of type UInt8
let maxValue = UInt8.max // maxValue is equal to 255, and is of type UInt8

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
>> 除非使用到与运行平台同位宽的无符号整型值的情况下使用 `UInt` ，一般情况下就算只需要存储非负数也推荐使用 `Int`。使用`Int`是为了保证代码的通用性，不必在两种数值类型间进行转换。整型匹配推断，在 [类型安全和类型推断](0201-The-Basics.md#typeSafetyAndTypeInference) 中有详细介绍。


####浮点数

浮点数指包含小数位的数值，例如`3.14159`，`0.1`， `-273.15`。

浮点类型要比整数所表示的范围大得多，存储的最大值要比 `Int` 类型大得多，最小值也要比 `Int` 类型小得多。 Swift 有两种有符号的浮点数类型：

- `Double` 表示64位浮点数。
- `Float` 表示32位浮点数。

>注意
>>`Double`类型可以精确到小数点后15位，`Float`可以精确到小数点后6位。可以根据实际需要及取值范围来确定使用哪个浮点类型。当两种类型都可以满足时比较推荐使用`Double`。


<span id="typeSafetyAndTypeInference"></span>
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

3的字面值本身并没有明确的类型，因次 `Double` 作为正确的输出类型是从加法中的浮点数字面量推断出的。


####数字的书面表达方式

数字可以按以下方式书写：

- 十进制数字， 没有前缀
- 二进制数字，以0b为前缀
- 八进制数字，以0o为前缀
- 十六进制数字，以0x为前缀

十进制7的不同写法：

```Swift

let decimalInteger = 17
let binaryInteger = 0b10001 // 17 in binary notation
let octalInteger = 0o21 // 17 in octal notation
let hexadecimalInteger = 0x11 // 17 in hexadecimal notation

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

`SomeType(ofInitialValue)` 是 Swift 中默认的类型初始化并赋值的方法。在具体实现中，`UInt16`有一个接收`UInt8`的初始化方法，所以这个初始化方法用来将`UInt8`类型数转换为`UInt16`类型数。在通过初始化方法给`UInt16`类型传值时，传入的值并不是任意的，需要传入`UInt16`类型初始化方法中包含的类型。通过扩展已有的类型使得初始化方法接收新的数据类型（包括自定义数据类型）会在 [扩展](0220-Extensions.md) 章节中讲解。

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

`if`之类的条件语句在 [流程控制](0205-Control-Flow.md) 章节中有详细讲解

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

`i==1`比较结果为`Bool`类型，所以第二个例子可以通过类型检查。像`i == 1`这样的比较操作会在 [基础运算符](0202-Basic-Operators.md) 中详解。

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

元组在函数返回值包含多个数值的情况下非常有用。函数在返回网页访问情况的时候可能会返回一个`(Int, String)`类型的元组来描述返回是否成功。通过返回包含两个值与类型都不相同的元素的元组，比起只能返回一种类型的一个数值函数可以提供更多的返回值的信息。更多的信息可以参考 [多返回值函数](0206-Functions.md#functionsWithMultipleReturnValues) 章节。

>注意
>>元组在表达临时的一组有关系的数值是非常有用。并不适用于创建复杂的数据结构。如果需要的数据结构并不是作为临时使用，最好使用类或者结构体定义。更多信息请参考 [类和结构体](0209-Classes-And-Structures.md) 章节。


####可选类型
可选类型可以用在值可能不存在的情况下。可选值代表两种情况：如果值存在就可以解包可选类型并获取它的具体值，或者根本就没有值。

>注意
>>在 Objective-C 及 C 语言中并没有可选类型的定义。在 Objective-C 中返回值为对象的方法可以返回一个具体对象或者是 `nil`， `nil` 表示并没有对象返回。然而这种做法只能对返回值为对象的方法起作用，如果是结构体，基础C类型，或者枚举值，Objective-C 方法将返回一个特殊值（例如`NSNotFound`）来表达并没有具体值返回。Swift这种做法可以告诉方法调用者，方法的返回值是一个可选类型，使用之前需要检查是否有值。Swift可以用可选类型的方式表达任何类型的数值，并不需要特殊的常量来表达没有值返回的情况。

下例中说明可选类型如何处理值可能不存在的情况。Swift 中`Int` 的构造方法可以传入一个`String`并将`String`转为`Int`。 然而，并不是所有的字符串都能转为整型。字符串`123`可以转换为数值`123`，但是`Hello, world`并不能转换为整型。

下例中通过`Int`的构造方法尝试将`String`转为`Int`:

```Swift
let possibleNumber = "123"
let convertedNumber = Int(possibleNumber)
// convertedNumber is inferred to be of type "Int?", or "optional Int”

```

由于实例化可能失败，所以构造函数返回的是可选类型的`Int`，而不是`Int`。可选类型的 `Int` 写做 `Int?` 而不是 `Int` 。 问号表名其是一个可选类型的值，也就是可能包含一个`Int`值，也可能没有值。（不可能包含其他类型的值，例如`Bool`, `String`类型的值。只能是`Int`或者什么都没有。）


#####nil
通过设置可选类型变量的值为`nil`表明变量无值的状态：

```Swift

var serverResponseCode: Int? = 404
// serverResponseCode contains an actual Int value of 404
serverResponseCode = nil
// serverResponseCode now contains no value

```

>注意
>>不能够给非可选类型的常量或变量设置`nil`。一般使用指定类型的可选类型声明可能无值的常量或变量。

声明可选类型的变量如果没有设置初始值时，默认设置为`nil`：

```Swift

var surveyAnswer: String?
// surveyAnswer is automatically set to nil

```

>注意
>>Swift中与Objective-C中的`nil`是不同的。Objective-C中，`nil`代表空指针（指针不指向任何对象）。在Swift中，`nil`并不是指针——只是代表值不存在。任何类型的可选类型都可以设置为`nil`，并不只有对象能设置为`nil`。


#####if表达式与强制解包

可以通过`if`表达式与`nil`进行比较判断可选类型是否有具体值。通过使用“等于”操作符"==" 或者“不等”操作符"!="进行比较。

如果可选类型有值的话，就可以看做“不等于”`nil`：

```Swift

if convertedNumber != nil {
print("convertedNumber contains some integer value.")
}
// Prints "convertedNumber contains some integer value.”

```

如果能够确定可选类型有值，可以通过在可选类型后添加叹号"!"来访问可选类型的值。这个叹号表示：“我知道这个可选类型是有值的，我要使用这个值”，这叫做可选类型的强制解包：

```Swift

if convertedNumber != nil {
print("convertedNumber has an integer value of \(convertedNumber!).")
}
// Prints "convertedNumber has an integer value of 123.

```

更多关于`if`表达式的信息，请参考[流程控制](0205-Control-Flow.md)章节。

>注意
>>通过`!`强制解包无值的可选类型的时候会触发运行时错误。当使用`!`强制解包可选类型的时候要确定可选类型有具体值。


#####可选类型绑定

通过可选类型绑定可以判断一个可选类型是否有值，如果有的话会将该值保存到一个临时的常量或变量中。可选类型绑定可以使用`if`和`while`来检查可选类型中是否有值，并且将其解包到常量或变量中，作为一个操作的一部分。`if` 和 `while` 在[流程控制](0205-Control-Flow.md)章节中有详细说明。

通过 `if` 实现可选类型绑定：

```Swift

if let constantName = someOptional{
    statement
}

```

可以通过可选类型绑定的方式重写[可选类型](0201-The-Basics.md#optionals)章节的`possibleNumber`一例：

```Swift

if let actualNumber = Int(possibleNumber) {
    print("\"\(possibleNumber)\" has an integer value of \(actualNumber)")
} else {
    print("\"\(possibleNumber)\" could not be converted to an integer")
}
// Prints ""123" has an integer value of 123”

```

可以这样解读以上代码：

“如果 `Int(possibleNumber)` 返回的可选类型有值，则将可选类型中的值赋给 `actualNumber` 这个常量。”

如果转换成功，`actualNumber` 这个常量就可以在 `if` 的第一个分支语句中使用。因为该常量已经通过可选类型中的值进行了初始化，也就不必使用`!`强制解包来获取该值了。在上例中，`actualNumber`只是用来打印转换的结果。

在可选类型绑定中可以使用常量和变量。在`if`表达式的第一个分支中需要修改`actualNumber`的值，那就可以使用`if var actualNumber`来代替，这样就会通过可选类型的值初始化一个变量而不是常量。

在一个`if`表达式中可以包含多个以逗号分隔的可选类型绑定以及布尔条件。如果任何可选类型绑定为`nil`或者布尔条件为`false`则整个`if`表达式的条件被视为`false`。如下例：

```Swift
if let firstNumber = Int("4"), let secondNumber = Int("42"), firstNumber < secondNumber && secondNumber < 100 {
    print("\(firstNumber) < \(secondNumber) < 100")
}
// Prints "4 < 42 < 100"
 
if let firstNumber = Int("4") {
    if let secondNumber = Int("42") {
        if firstNumber < secondNumber && secondNumber < 100 {
            print("\(firstNumber) < \(secondNumber) < 100")
        }
    }
}
// Prints "4 < 42 < 100”
```

>注意
>>在`if`表达式中通过可选类型绑定创建的常量或者变量只能在`if`语句中使用。相反，在`guard`表达式中通过可选类型绑定创建的常量或者变量只能在`guard`表达式之后的语句中使用，请参考 [Early Exit](0205-Control-Flow.md#earlyExit) 章节


#####隐式解包可选类型

就像之前所描述的，可选类型指的是可以不存在任何值的常量或变量。可以通过`if`表达式判断可选类型是否有值，如果有值则可以通过可选类型绑定来访问可选类型的值。

有时通过程序结构我们可以清楚的知道一个可选类型在第一次赋值之后永远都是有值的。在这些案例中，当访问可选类型的值得时候并没有必要去检查是否有值再解包，因为它可以确定始终有一个值。

这种操作被成为隐式解包可选类型。通过在类型之后加一个感叹号`!`的方式来定义隐式解包可选类`(String!)`。

当可选类型在定义之后就有值并且在之后的任何时候都有值，使用隐式解包可选类型会更方便。在`Swift`中隐式解包可选类型主要用在类的初始化方法中，在 [非持有引用类型和隐式解包可选类型属性](0223-Automatic-Reference-Counting.md#unownedReferencesAndImplicitlyUnwrappedOptionalProperties) 章节中有详细说明。

隐式解包可选类型是一种无感知的常用可选类型，可以作为非可选类型值使用，在每次使用时不需要解包可选类型值。 下例中详细说明了在获取可选类型解包后的 `String` 类型值时可选字符串类型与隐式解包可选字符串类型在使用上的不同：

```Swift
let possibleString: String? = "An optional string."
let forcedString: String = possibleString! // requires an exclamation mark
 
let assumedString: String! = "An implicitly unwrapped optional string."
let implicitString: String = assumedString // no need for an exclamation mark

```

可以把隐式解包可选类型看做是赋予了可选类型在使用时自动解包的权限。同在每次使用可选类型的时候在其后追加 `!`  相比，隐式解包可选类型将这个操作提前到声明的时候。

>注意
>>如果隐式解包可选类型在为 `nil` 的时候想要获取其中的值会造成运行时错误。这个错误与可选类型值不包含值的时候使用 `!` 进行强制解包是相同的。

当然也可以将隐式解包可选类型看做是普通的可选类型使用，在使用之前判断是否有值：
```Swift

if assumedString != nil {
    print(assumedString)
}
// Prints "An implicitly unwrapped optional string.”

```

也可以使用可选类型绑定使用隐式解包可选类型，并在一个表达式中检查解包该值：

```Swift

if let definiteString = assumedString {
    print(definiteString)
}
// Prints "An implicitly unwrapped optional string.”

```

>注意
>>如果一个值在其整个生命周期中可能为`nil`，并且在之后的使用中要检查是否为`nil`的话，不要使用隐式解包可选类型而要用普通的可选类型。

####错误处理

使用错误处理可以在程序运行出错的时候做出响应。

不同于可选类型通过判断是否有值来表达方法的成功或失败，错误处理可以检查出潜在的错误，如果有需要还可以将错误传递到程序的其他部分。

在方法执行过程中如果出现不可预知的错误时，将会抛出错误。方法的调用者可以捕获这个错误并作出适当处理。

```Swift

func canThrowAnError() throws {
    // this function may or may not throw an error
}

```

函数可以通过 `throws` 关键字在声明的时候表明其可能抛出错误。在调用可能抛出错误的函数时需要在方法前加上`try`关键字来执行。

Swift会自动将错误传出到当前作用域，直到被`catch`分句处理。

```Swift

do {
    try canThrowAnError()
    // no error was thrown
} catch {
    // an error was thrown
}

``` 

`do`表达式创建了一个作用于，可与将错误传递给一个或多个`catch`分支。

下例中说明了错误处理如何响应多中错误：

```Swift

func makeASandwich() throws {
    // ...
}
 
do {
    try makeASandwich()
    eatASandwich()
} catch SandwichError.outOfCleanDishes {
    washDishes()
} catch SandwichError.missingIngredients(let ingredients) {
    buyGroceries(ingredients)
}

```

这个例子中，如果没有干净的盘子或者有原料缺失， `makeASandwich()` 就会抛出错误。 因为会抛出错误，`makeASandwich()` 在调用时需要使用`try`表达式包装。通过将方法包在`do`表达式中，使得任何抛出的错误都会传到之后提供的`catch`分支中。

如果没有错误抛出，就会调用`eatASandwich()`方法，如果抛出错误并且错误为`SandwichError.outOfCleanDishes`就会调用`washDishes()`方法，如果抛出错误并且错误为`SandwichError.missingIngredients`就会调用`buyGroceries(_:)`方法，并传入`catch`分支捕获的`[Srting]`参数

错误抛出、捕获、传递在[错误处理](0217-Error-Handling.md)章节有详细介绍

####断言与前置条件

断言与前置条件会在运行时进行判断。可以通过它们来判断当前环境是否满足程序后续运行的必要条件。如果断言与前置条件中的布尔表达式为`true`，程序会正常运行；否则程序的当前状态是不允许的，代码执行打断，程序退出。

可以通过断言与前置条件表达在编码过程中所作的假设和预期，所以可以作为代码的一部分。断言可以帮你查找错误及开发中错误的假设，前置条件可以定位生产环境中的问题。

除了定位运行时错误，断言与前置条件也是一种非常有用的代码文档的一种形式。与[错误处理](0217-Error-Handling.md)不同的是，断言与前置条件并不是用来处理可恢复的预期的错误。由于断言与前置条件是是一种非法的程序运行状态，所以没有办法捕获到失败的断言。

使用断言及前置条件不可能替代通过设计代码尽量减少非法状态的产生。但是使用它可以确保数据有效性程序运行状态正常，当可预料的非法状态产生时强制使程序退出，使排查程序问题更容易。当非法状态产生时立即停止程序运行也可以尽量减少程序非法运行状态产生的破坏。

断言和前置条件的不同之处在于：断言只能在debug环境中进行检查，而前置条件可以同时在debug环境和production环境中进行检查。 在production环境包中断言中的条件并不会执行。也就是说在开发过程中可以随意使用断言，且并不会对production环境的包产生影响。

#####使用断言调试

可以通过调用Swift标准函数库中的`assert(_:_:file:line:`方法来写断言。传入一个返回`true`或`false`的表达式，以及表达式返回`false`时需要展示的信息。例如：

```Swift
let age = -3
assert(age >= 0, "A person's age can't be less than zero.")
// This assertion fails because -3 is not >= 0.

```

在上面例子中，如果`age >= 0`为`true`的话，代码会继续执行，也就是`age`为非负数。如果`age`的值为负数的话，在上面的代码中，`age >= 0` 结果为`false`，断言失败，程序运行结束。

调用`precondition(_:_:file:line:)` 来写前置条件。传入一个返回`true`或`false`的表达式，以及表达式返回`false`时需要展示的信息。例如：

```Swift

// In the implementation of a subscript...
precondition(index > 0, "Index must be greater than zero.”)
```

也可以使用`preconditionFailure(_:file:line:)`方法指示错误的产生——例如，switch语句进入default分支中，但switch语句传入的值必须被非default分支执行。

>注意
>>如果编译器没有使用`-Ounchecked`模式，那么前置条件就不会检查，编译器认为前置条件永远都是`true`，并相应的组织代码。然而，`fatalError(_:file:line:)`方法会忽略优化设置任何情况下都会打断运行。
>>可以在原型或早期开发中还没有实现的方法中使用`fatalError(_:file:line:)`方法作标记。由于`fatalError`并没有在优化中忽略，所以在程序运行到`fatalError(_:file:line:)`标记的方法时会停止运行。


























