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




<span id="sets"></span>
####Sets




<span id="dictionaries"></span>
####Dictionaries