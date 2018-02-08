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



<span id="stringInterpolation"></span>