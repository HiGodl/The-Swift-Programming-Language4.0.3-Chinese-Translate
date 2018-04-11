Swift提供了三种集合类型用以存储一组数值，包括数组（`Array`），集合（`Set`），字典（`Dictonary`）。数组是一组有序值，集合是一组无序唯一值，字典存储的为一组无序键值对。

![](/assets/WX20180211-132830@2x.png)

Swift中数组，集合，字典会明确的知道它们能存储什么类型的键和值。这就意味着我们不会误把错误类型的值存入集合类。当我们从集合中取值得时候也可以明确的知道我们取出的是什么类型。

>注意
>>Swift中的数组，集合，字典是泛型集合的实现。更多关于泛型和集合请参考[泛型](0222-Generics.md)章节


####可变集合类型

当我们以变量形式创建数组，集合，字典类的时候，它们就是可变的。这就意味着我们在创建完之后可以通过添加、删除、改变集合类中存储的值来对其进行操作。如果以常量形式创建，那就是不可变的，它的大小及内容都不能改变。

>注意
>>在任何不需要改变集合的情况下都尽量创建不可变集合。这样做会使代码更清晰也能够使Swift编译器更好的处理你创建的集合


<span id="arrays"></span>
####Array

数组可以存储一组有序同类型的值。同一个值可以在数组中的不同位置出现多次。

>注意
>>Swift中的`Array`类是从Foundation的`NSArray`类中桥接过来的。
>>更多关于`Array`在Foundation和Cocoa的使用请参考《Using Swift with Cocoa and Objective-C (Swift 4)》中的`Working with Cocoa Data Types`章节。

#####数组类型的简写语法

Swift中数组定义的完整写法为`Array<Element>`，`Element`是数组允许存储的类型。可以简写为`[Element]`。尽管两种写法在功能上是一样的，但是更推荐简写形式，并且在本书中涉及到数组的地方几乎都是简写形式。

#####创建空数组

使用实例化语法创建特定类型的空数组：

```Swift
var someInts = [Int]()
print("someInts is of type [Int] with \(someInts.count) items.")
// Prints "someInts is of type [Int] with 0 items."
```

注意`someInts`变量可以从实例化方法中推断为`[Int]`类型。

如果上下文中（方法参数或者声明常量或变量时已经指定类型）已经知道数组存储的类型，那么可以通过数组字面量来创建空数组，这样写`[]`（一对空方括号）：

```Swift
someInts.append(3)
// someInts now contains 1 value of type Int
someInts = []
// someInts is now an empty array, but is still of type [Int]”
```

##### 创建有默认值的数组

Swift中的`Array`类型提供了一种创建指定长度且元素都为默认值的构造方法。为该构造方法传入两个参数，一个为合适类型的默认值，参数名为`repeating`；并且传入该默认值在数组中重复的次数，也就是数组的size，参数名为`count`：

```Swift
var threeDoubles = Array(repeating: 0.0, count: 3)
// threeDoubles is of type [Double], and equals [0.0, 0.0, 0.0]
```

#####通过两个已知数组创建一个新数组

可以通过加法运算符（`+`）将两个已知的并且包含类型相同的数组合并为一个新的数组。新数组的类型可以通过相加的两个数组推断出来：

```Swift
var anotherThreeDoubles = Array(repeating: 2.5, count: 3)
// anotherThreeDoubles is of type [Double], and equals [2.5, 2.5, 2.5]
 
var sixDoubles = threeDoubles + anotherThreeDoubles
// sixDoubles is inferred as [Double], and equals [0.0, 0.0, 0.0, 2.5, 2.5, 2.5]
```

#####通过数组字面量创建数组

可以通过数组的字面量来创建数组，一种通过写明一个或者更多的值作为数组元素的简单表达方式。数组字面量由一组逗号分隔、方括号包裹的值组成：

```Swift
[value1, value2, value3]
```

下面的例子创建了一个名为`shoppingList`的数组来存储`String`类型的数据：

```Swift
var shoppingList: [String] = ["Eggs", "Milk"]
// shoppingList has been initialized with two initial items
```

`shoppingList`变量声明为“字符串数组”，写作`[String]`。 由于这个特殊的数组指明了特定的存储类型`String`，所以只允许存储`String`类型的值。在该例中，`shoppingList`由包含两个字符串的数组字面量进行实例化（`Eggs`和`Milk`）， 

>注意
>>由于之后的例子中回向`ShoppingList`添加更多的元素，所以此处`ShoppingList`数组为变量（使用`var`关键字修饰），而不是常量（使用`let`关键字修饰）

在该例子中，数组字面量只包含两个`String`值。符合`shoppingList`声明的类型（只能存储`String`类型的数组），所以该赋值运算作为包含两个元素的`shoppingList`的实例化方法是合法的。

由于类型推断的存在，Swift在使用只包含一种类型的数组字面量来初始化时，不需要在数组名后指定类型。所以`shoppingList`的初始化方法可以简写为：

```Swift
var shoppingList = ["Eggs", "Milk"]
```

因为数组字面量中所有值都为相同类型，Swift可以通过该类型推断出`[String]`为`shoppingList`的正确存储类型。


#####数组的访问和修改

可以使用数组的方法和属性或者下标来访问或者修改数组。

使用只读属性`count`来获取数组元素个数：
```Swift
print("The shopping list contains \(shoppingList.count) items.")
// Prints "The shopping list contains 2 items."
```

使用`isEmpty`属性作为检查数组`count`属性是否为`0`的简写：

```Swift
if shoppingList.isEmpty {
    print("The shopping list is empty.")
} else {
    print("The shopping list is not empty.")
}
// Prints "The shopping list is not empty."
```

使用`append(_:)`方法向数组末尾添加一个元素：

```Swift
hoppingList.append("Flour")
// shoppingList now contains 3 items, and someone is making pancakes
```

使用加等（`+=`）运算符添加一个或更多的类型符合的元素到数组中：

```Swift
shoppingList += ["Baking Powder"]
// shoppingList now contains 4 items
shoppingList += ["Chocolate Spread", "Cheese", "Butter"]
// shoppingList now contains 7 items
```

通过下标取出数组中元素。在数组名之后的方括号中传入要取出的元素的索引值：

```Swift
var firstItem = shoppingList[0]
// firstItem is equal to "Eggs"
```

>注意
>>数组中第一个元素的索引为`0`，而不是`1`，Swift中的数组索引都是0开始的。

可以通过下标来改变特定索引位置元素的值：

```Swift
shoppingList[0] = "Six eggs"
// the first item in the list is now equal to "Six eggs" rather than "Eggs"
```

在使用数组下标时，要确保指定的索引值存在，如果尝试使用`shoppingList[shoppingList.count] = "Salt"`这种方式在数组末尾添加一个元素会导致运行时错误。

可以通过下标的方式一次性改变数组中多个元素值，甚至可以使用不同长度的数组来替换指定索引范围的值。下例中使用"Bananas","Apples"来替换数组中的"Chocolate Spread","Cheese","Butter"三个元素：

```Swift
shoppingList[4...6] = ["Bananas", "Apples"]
// shoppingList now contains 6 items
```

使用`insert(_:at:)`方法来向数组特定索引位置插入一个值：

```Swift
shoppingList.insert("Maple Syrup", at: 0)
// shoppingList now contains 7 items
// "Maple Syrup" is now the first item in the list
```

使用索引值`0`作为`insert(_:at:)`的参数，将“Maple Syrup”插入到数组的开头也就是第一个元素的位置

同样的可以使用`remove(at:)`方法来将数组中特定索引位置的值删除，该方法将元素从数组中删除并返回删除的元素（当然如果你并不需要被删除的值可以忽略掉这个方法的返回值）

```Swift
let mapleSyrup = shoppingList.remove(at: 0)
// the item that was at index 0 has just been removed
// shoppingList now contains 6 items, and no Maple Syrup
// the mapleSyrup constant is now equal to the removed "Maple Syrup" string
```

>注意
>>如果你尝试访问超出数组所包含的索引位置，会导致运行时错误。可以通过`count`属性来检查索引是否合法。由于数字的索引为0开始所以最大的合法索引值是`count-1`，但是当`count`为0时（数组为空），没有合法的索引值。

当元素被移除时会自动重新计算索引值，所以此时索引值为`0`的元素为`Six eggs`：

```Swift
firstItem = shoppingList[0]
// firstItem is now equal to "Six eggs"
```

移除数组中最后一个元素，可以用`removeLast()`方法替换`remove(at:)`这样的话就避免使用`count`属性来查询数组中元素个数。同`remove(at:)`方法一样，`removeLast()`方法也会返回移除的元素值：

```Swift
let apples = shoppingList.removeLast()
// the last item in the array has just been removed
// shoppingList now contains 5 items, and no apples
// the apples constant is now equal to the removed "Apples" string
```






<span id="sets"></span>
####Sets




<span id="dictionaries"></span>
####Dictionaries