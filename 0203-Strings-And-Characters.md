字符串是一组字符的合集，例如`"hello, world"`或者`"albatross"` 。Swift中的字符串使用`String`类定义。`String`的内容可以通过多种方式访问，包括作为一组字符返回。

Swift的`String`和`Character`类型提供了一个快速，Unicode兼容的方式来处理代码中的文本。通过使用与C类似的字符串文字型语法，使得字符串的创建和处理更加轻便可读。字符串结合可以简单地通过使用`+`运算符连接两个字符串，字符串是否可变与Swift其他类型值一样仅取决于声明为常量（不可变）或变量（可变）。可以通过字符串插值操作很容易的将常量、变量、文本、表达式插入到一个长字符串中。这个使得创建用来显示、存储、打印的特定格式的字符串更容易。

Swift的`String`类尽管语法非常简单，但是它是一种快速、先进的文字处理的实现。每个字符串都由与编码无关的Unicode字符组成，并提供对各种Unicode表示形式访问这些字符的支持。

>注意
>>Swift的`String`类是通过Foundation的`NSString`类桥接过来的。Foundation框架也通过扩展`String`暴露了`NSString`的方法。也就是如果引用Foundation框架，那么无需转换`String`为`NSString`就可以访问`NSString`方法。








<span id="stringInterpolation"></span>