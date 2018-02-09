字符串是一组字符的合集，例如`"hello, world"`或者`"albatross"` 。Swift中的字符串使用`String`类定义。`String`的内容可以通过多种方式访问，包括作为一组字符返回。

Swift的`String`和`Character`类型提供了一个快速，Unicode兼容的方式来处理代码中的文本。通过使用与C类似的字符串文字型语法，使得字符串的创建和处理更加轻便可读。字符串结合可以简单地通过使用`+`运算符连接两个字符串，字符串是否可变与Swift其他类型值一样仅取决于声明为常量（不可变）或变量（可变）。可以通过字符串插值操作很容易的将常量、变量、文本、表达式插入到一个长字符串中。这个使得创建用来显示、存储、打印的特定格式的字符串更容易。

Swift的`String`类尽管语法非常简单，但是它是一种快速、先进的文字处理的实现。每个字符串都由与编码无关的Unicode字符组成，并提供对各种Unicode表示形式访问这些字符的支持。

>注意
>>Swift的`String`类是通过Foundation的`NSString`类桥接过来的。Foundation框架也通过扩展`String`暴露了`NSString`的方法。也就是如果引用Foundation框架，那么无需转换`String`为`NSString`就可以访问`NSString`方法。
>>更多关于`String`在Foundation和Cocoa中的使用，请参考《Using Swift with Cocoa and Objective-C (Swift 4)》中的Cocoa数据类型的使用

####字符串字面量
可以在代码中预定义`String`值，作为字符串字面量。字符串字面量是被双引号包裹的一组字符。

可以使用字符串字面量作为常量或变量的初始值：

```Swift
let someString = "Some string literal value”
```
注意由于`someString`通过字符串字面量初始化，所以被自动定义为`String`类型

#####多行字符串字面量
如果需要将一个字符串分隔成多行，可以使用多行字符串字面量定义——通过三个双引号中的一组字符序列来定义：

```Swift
let quotation = """
The White Rabbit put on his spectacles.  "Where shall I begin,
please your Majesty?" he asked.
 
"Begin at the beginning," the King said gravely, "and go on
till you come to the end; then stop."
"""
```

多行字符串字面量包含三个双引号中间的所有行。字符串从起始双引号之后开始从结束双引号之前结束。也就是下面两种字符串写法中都不包含换行符：

```Swift
let singleLineString = "These are the same."
let multilineString = """
These are the same.
"""
```

如果多行字符串字面量中包含换行符，那么换行符也会显示在字符串值中。如果只是想通过换行符使得代码可读性更强，但并不需要在字符串中显示出来，那么在不需要显示换行符的行末添加反斜杠`(\)`。

```Swift
let softWrappedQuotation = """
The White Rabbit put on his spectacles.  "Where shall I begin, \
please your Majesty?" he asked.
 
"Begin at the beginning," the King said gravely, "and go on \
till you come to the end; then stop."
"""
```

如果想使得多行字符串字面量前后有空行，可以通过在字符串前后添加空行的方式实现。例如：

```Swift
let lineBreaks = """
 
This string starts with a line break.
It also ends with a line break.
 
"""
```

多行字符串会自动为其中的代码进行缩进。Swift会自动忽略结束双引号之前的包括其他行的空格。如果在自动缩进的基础上手动添加空格，那么这些空格就会包含在其中。

![](/assets/1518075269284.jpg)

在上面的例子中，虽然整个多行字符串是有缩进的，第一行和最后一行字符串也不会包含任何空格。因为第二行要比其他行缩进的多，所以会包含四个空格的缩进。


#####多行字符串字面量中的特殊字符

多行字符串字面量可以包含以下特殊字符：
- 转义特殊字符`\0`（空字符）， `\\`（反斜杠）, `\t`（z制表符），`\n`（换行符），`\r`（），`\"`（双引号），`\'`（单引号）
- 任意`Unicode`编码值，以`\u{n}`的格式书写，`n`是1-8位十六进制数组成的一个有意义的Unicode编码打印值（Unicode会在之后的[Unicode](0203-Strings-And-Characters.md#unicode)中介绍）


下面的例子展示了四种特殊字符的例子。`wiseWords`常量包含了两个转义双引号。`dollarSin`，`blackHeart`，和`sparklingHeart`常量展示了Unicode的格式：

```Swift
let wiseWords = "\"Imagination is more important than knowledge\" - Einstein"
// "Imagination is more important than knowledge" - Einstein
let dollarSign = "\u{24}"        // $,  Unicode scalar U+0024
let blackHeart = "\u{2665}"      // ♥,  Unicode scalar U+2665
let sparklingHeart = "\u{1F496}" // 💖, Unicode scalar U+1F496 
```

由于多行字符串字面量的定义是用三对双引号，所以可以在多行字符串字面两种直接加入非转义的单个双引号。如果要包含`"""`的话，至少要有一个双引号要进行转义。例如：

```Swift
let threeDoubleQuotationMarks = """
Escaping the first quotation mark \"""
Escaping all three quotation marks \"\"\"
"""
```

####初始化空字符串

可以通过给字符串变量赋值为空字符串或者使用`String`的初始化方法创建一个空字符串，以作为拼接一个长字符串的起点：

```Swift
var emptyString = ""               // empty string literal
var anotherEmptyString = String()  // initializer syntax
// these two strings are both empty, and are equivalent to each other
```

可以通过检查`isEmpty`属性来判断`String`value是否为空字符串：

```Swift
if emptyString.isEmpty {
    print("Nothing to see here")
}
// Prints "Nothing to see here”
```

####字符串可变性
可以通过表明字符串为常量（不可变）或变量（可变）来指定字符串是否可变：

```Swift
var variableString = "Horse"
variableString += " and carriage"
// variableString is now "Horse and carriage"
 
let constantString = "Highlander"
constantString += " and another Highlander"
// this reports a compile-time error - a constant string cannot be modified
```

>注意
>>Swift的字符串的可变性与`Objective-C`和`Cocoa`中的定义（通过两个类`NSString`、`NSMutableString`来定义字符串是否可变）是不同的


####字符串是值类型
Swift中的`String`是值类型。如果创建一个`String`类型的值，在作为参数传入函数或方法中或者给常量或变量赋值的时候实际上传递的是字符串的一个拷贝。在上边的情况中，都是从该值创建了一个新的拷贝，实际上传递的是这个拷贝，并不是该值。关于值类型请参考[结构体和枚举是值类型](0209-Classes-And-Structures.md#structuresandEnumerationsAreValueTypes)

Swift中`String`默认拷贝的特性，保证当字符串或者方法传给你一个`String`的值得时候，不管它从哪来你获取到的都是一个确确实实的`String`类型值。你可以确定你得到的字符串除了你自己谁都不能去修改。

在底层，Swift的编译器优化了字符串的使用，以便只有在必要时才进行实际的复制。 这意味着在字符串作为值类型时使用总能得到最好的结果。



####字符的使用

可以使用`for-in`表达式来通过遍历的方式获取`String`中的单个`Character`值：

```Swift
for character in "Dog!🐶" {
    print(character)
}
// D
// o
// g
// !
// 🐶
```

`for-in`循环请参见[For-in循环](0205-Control-Flow.md#for-inLoops)

或者也可以使用`Character`类型创建一个字符常量或变量并为其赋值：

```Swift
let exclamationMark: Character = "!"
```

`String`值可以通过在其构造函数中传入一个`Character`数组的方式进行初始化：

```Swift
et catCharacters: [Character] = ["C", "a", "t", "!", "🐱"]
let catString = String(catCharacters)
print(catString)
// Prints "Cat!🐱”
```

#####字符和字符串的串联
多个字符串值可以通过加法运算符`+`组合成一个新的字符串：

```Swift
let string1 = "hello"
let string2 = " there"
var welcome = string1 + string2
// welcome now equals "hello there”
```

也可以通过加法赋值运算符`+=`将一个字符串添加到另一个字符串之后：

```Swift
var instruction = "look over"
instruction += string2
// instruction now equals "look over there”
```

通过`String`类型的`append()`方法可以将字符类型的数据添加到字符串中：

```Swift
let exclamationMark: Character = "!"
welcome.append(exclamationMark)
// welcome now equals "hello there!”
```

>注意
>>由于`Character`只能包含一个字符，所以不能向字符变量中添加字符串

如果需要通过多行字符串字面量创建一个更长的字符串，并且每行之后都包含一个换行符，如下：

```Swift
let badStart = """
one
two
"""
let end = """
three
"""
print(badStart + end)
// Prints two lines:
// one
// twothree
 
let goodStart = """
one
two

"""
print(goodStart + end)
// Prints three lines:
// one
// two
// three
```

上例中，通过`badStart`和`end`结合生成了一个两行的字符串，这并不是我们想要的。因为在`badStart`的最后一行并没有换行符，所以这一行就会直接拼接上`end`的第一行。不同的是，`goodStart`的每一行末尾都包含换行符，所以当与`end`相加时就会返回预期的三行。


<span id="stringInterpolation"></span>

####字符串插值
字符串插值是在字符串字面量中通过插入常量、变量、字面量、或者表达式从而组成一个新的字符串的方法。字符串插值可以用在单行和多行字符串字面量中。每一个插入字符串字面量的元素都要写在前面带反斜杠的双括号中：

```Swift
let multiplier = 3
let message = "\(multiplier) times 2.5 is \(Double(multiplier) * 2.5)"
// message is "3 times 2.5 is 7.5”
```

上例中，通过`\(multiplier)`将`multiplier`的值插入到字符串字面量中。当字符串插值执行以创建一个字符串的时候，占位符会被`multiplier`的实际值替换掉。

同时`multiplier`也是字符串后边插入的一个表达式的一部分。表达式会计算出`Double(multiplier) * 2.5`的结果`7.5`并将其插入到字符串中。这个例子中，表达式在插入到字符串字面量中时应以`\(Double(multiplier) * 2.5)`的形式书写。

>注意
>>插入字符串中的表达式不能有非预期的反斜杠、换行符、回车符。可以包含其他字符串字面量








<span id="unicode"></span>