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

函数可以有多个输入参数，参数写在函数名后的括号中，用逗号隔开。

下面函数中传入姓名及是否已经作为`greet`的参数传入过，并返回合适的欢迎语：

```Swift
func greet(person: String, alreadyGreeted: Bool) -> String {
    if alreadyGreeted {
        return greetAgain(person: person)
    } else {
        return greet(person: person)
    }
}
print(greet(person: "Tim", alreadyGreeted: true))
// Prints "Hello again, Tim!" 
```

通过传入一个叫做`person`的`String`参数以及一个叫做`alreadyGreeted`的`Bool`参数调用`greet(person:alreadyGreeted:)`函数。注意这个函数与之前的`greet(person:)`函数是不同的，虽然参数都以`greet`开头，但是`greet(person:alreadyGreeted:)`需要传入两个参数，而`greet(person:)`只需传入一个参数。

##### 无返回值的函数

函数并不一定要定义返回值类型。下例中的`greet(person:)`函数就在其内部打印而不是返回`String`值：

```Swift
func greet(person: String) {
    print("Hello, \(person)!")
}
greet(person: "Dave")
// Prints "Hello, Dave!" 
```

由于函数并不需要返回值，所以在定义时不需要添加返回箭头及返回值类型。

>注意
>> 严格来说，尽管`greet(person:)`函数没有定义返回值，但其仍然有返回值。没有定义返回值得函数默认返回`Void`类型，是一个简单的空元组，写作`()`

函数的返回值在调用的时候可以忽略：
```Swift
func printAndCount(string: String) -> Int {
    print(string)
    return string.count
}
func printWithoutCounting(string: String) {
    let _ = printAndCount(string: string)
}
printAndCount(string: "hello, world")
// prints "hello, world" and returns a value of 12
printWithoutCounting(string: "hello, world")
// prints "hello, world" but does not return a value 
```

第一个函数`printAndCount(string:)`打印一个字符串，并且返回字符串中字符个数`Int`类型。第二个函数`printWithoutCounting(string:)`，调用第一个函数但是忽略掉第一个函数的返回值。第二个函数调用的时候仍然打印字符串，但并没有使用其返回值。

>注意
>> 函数的返回值可以被忽略，但是如果一个函数声明了返回值，那么在函数体中必须要返回对应类型的返回值。如果不返回则会导致编译错误。

<span id="functionsWithMultipleReturnValues"></span>
##### 多返回值函数

可以通过元组作为函数的返回值以返回一个多返回值的组合类型。

下例中定义了一个叫做`minMax(array:)`的函数，用来查找一个`Int`数组中最大和最小值：

```Swift
func minMax(array: [Int]) -> (min: Int, max: Int) {
    var currentMin = array[0]
    var currentMax = array[0]
    for value in array[1..<array.count] {
        if value < currentMin {
            currentMin = value
        } else if value > currentMax {
            currentMax = value
        }
    }
    return (currentMin, currentMax)
} 
```

`minMax(array:)`函数返回一个包含两个`Int`值得元组。两个值的标签分别为`min`和`max`，我们可以通过返回值在元组中的名称获取对应的返回值。

函数体通过定义两个临时变量`currentMin`和`currentMax`开始，两个临时变量的初始值为数组中的第一个值。然后函数开始遍历数组中的其他值来和临时变量比较大小，并根据比较结果对两个临时变量重新赋值。最后最大值和最小值通过包含两个`Int`值的元组返回。

由于元组中元素在声明时定义了名称，所以可以通过点语法来获取元组中你的最大值及最小值：

```Swift
let bounds = minMax(array: [8, -6, 2, 109, 3, 71])
print("min is \(bounds.min) and max is \(bounds.max)")
// Prints "min is -6 and max is 109" 
```

注意，由于元组元素的名称在方法定义的时候就已经定义好了，所以在方法返回元组之后并不需要对元组中的元素重新命名。

##### 可选元组类型返回值



<span id="functionArgumentLablesAndParameterNames"></span>
函数参数标签及参数名



<span id="defaultParameterValues"></span>
参数默认值


