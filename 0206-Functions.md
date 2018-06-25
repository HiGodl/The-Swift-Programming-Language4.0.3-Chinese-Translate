*函数*是一个独立的实现特殊任务的代码块。通过一个用来说明方法功能的名字来定义函数，并且可以在需要的时候通过这个名字来调用函数。

Swift有着统一灵活的函数定义方法，几乎可以表达一切包括C风格的无参的函数以及复杂的Objective-C风格的每个参数都带有名称和参数标签的函数。参数可以提供默认值以简化函数调用，并且可以作为输入参数传递，这些参数在函数完成其执行后修改传递的变量。

函数的参数及返回值类型组成Swift中的函数的类型。函数的类型可以像其他任何类型一样在Swift中使用，这一特性使得函数可以作为其他函数的参数及返回值。函数还可以作为其他函数的子函数存在，用以在函数内部提供特定的功能。

#### 函数的定义及调用

当定义函数使可以选择性的定义一个或多个带有名称及类型的参数。也可以选择行的定义一个类型作为函数执行完返回并输出的值，也就是返回值类型。

每个函数都有函数名，用来描述函数的实现功能。通过函数名加复合函数参数类型的参数来调用函数。函数的参数顺序必须要与函数定义的参数列表中一致。

下例中的方法叫做`greet(person:)`，因为它的功能就是输入一个人的姓名然后输入对这个人的欢迎语。为了完成该功能，需要声明一个输入参数——一个叫做`person`的`String`——并且返回一个包含对这个人的欢迎语的`String`：

```Swift
func greet(person: String) -> String {
    let greeting = "Hello, " + person + "!"
    return greeting
} 
```

所有这些信息展示了如何定义函数，使用`func`关键字开头。使用->来声明返回值，箭头加返回值类型。

函数的定义描述了函数的功能，需要接受什么参数，执行完之后返回什么。函数的定义使得其在代码的其他部分更明确的调用：

```Swift
print(greet(person: "Anna"))
// Prints "Hello, Anna!"
print(greet(person: "Brian"))
// Prints "Hello, Brian!" 
```

可以通过在`person`参数标签之后传入`String`类型的参数来调用`greet(person:)`，例如`greet(person: "Anna")`。由于方法返回`String`值，`greet(person:)`可以在`print(_:separator:terminator:)`中解包并且将返回字符串传入该函数，像例子中一样将返回值打印出来。

>注意
>> `print(_:separator:terminator:)`并没有参数标签，并且由于其他参数有默认值所以是可选的。这些语法差异会在[函数参数标签及参数名](0206-Functions.md#functionArgumentLablesAndParameterNames)和[参数默认值](0206-Functions.md#defaultParameterValues)中提及

`greet(person:)`的函数体通过定义一个新的叫做`greeting`字符串常量并设置一个简单的欢迎信息来开始。这个欢迎信息通过`return`关键字传出。在`return greeting`这行代码处，函数结束执行，并将`greeting`的当前值返回。

可以使用不同的参数多次调用`greet(person:)`。在上面的例子中表明了当传入`Anna`、`Brian`时将会发生什么事情。函数会为每一个名字返回一个特定的欢迎语。

为了使函数体更短，可以将信息的创建及返回语句写到一行：

```Swift
func greetAgain(person: String) -> String {
    return "Hello again, " + person + "!"
}
print(greetAgain(person: "Anna"))
// Prints "Hello again, Anna!"
```

#### 函数的参数和返回值

函数的参数和返回值在Swift中的使用非常灵活。可以定义任何简单实用的只包含一个未命名的参数的函数，或者复杂的包含多个有特殊意义的参数名的参数及多种不同的参数选项。

##### 无参函数

函数并不一定要有传入参数。下例中就是无参的函数，调用时会返回一个简单的字符串信息：

```Swift
func sayHelloWorld() -> String {
    return "hello, world"
}
print(sayHelloWorld())
// Prints "hello, world" 
```

即使不需要参数在函数定义时也需要在函数名后加圆括号。在函数调用的时候同样需要在函数名后加圆括号来调用。

##### 多参函数

<span id="functionArgumentLablesAndParameterNames"></span>
函数参数标签及参数名

<span id="functionsWithMultipleReturnValues"></span>
多返回值函数

<span id="defaultParameterValues"></span>
参数默认值


