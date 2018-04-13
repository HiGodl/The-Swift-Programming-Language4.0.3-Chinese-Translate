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

######数组的遍历

可以通过`for-in`循环来完整遍历数组中的元素：

```Swift
for item in shoppingList {
    print(item)
}
// Six eggs
// Milk
// Flour
// Baking Powder
// Bananas
```

如果在遍历数组的时候同时需要使用元素的索引，可以使用数组的`enumerated()`方法来代替数组进行遍历。`enumerated()`方法会将数组的索引值及元素值放在元组中返回。索引从0开始，每个元素间的步长为1；如果需要遍历整个数组，那么元组中的整型值同元素的索引是相等的。可以将元组中的值分解为常量或者变量作为遍历的一部分来使用：

```Swift
for (index, value) in shoppingList.enumerated() {
    print("Item \(index + 1): \(value)")
}
// Item 1: Six eggs
// Item 2: Milk
// Item 3: Flour
// Item 4: Baking Powder
// Item 5: Bananas
```

更多关于`for-in`的信息，请参见[For-in循环](0205-Control-Flow.md#for-inLoops)




<span id="sets"></span>
####Sets

*set*用来存储同一类型的一组无序的值。如果元素的索引并不重要或者如要保证每个元素只出现一次，那么可以使用`Set`来代替`Array`。

>注意
>>Swift中的`Set`类型是从`NSSet`中桥接过来的。
>>更多关于Foundation和Cocoa中的`Set`信息，请参见*Using Swift with Cocoa and Objective-C (Swift 4).*中的 Working with Cocoa Data Types 章节

#####`Set`类型中的哈希值

存储在set中的值必须是*hashable*的——也就是该类型必须提供一种计算其哈希值的方法。哈希值是一个`Int`类型的值并且元素比较相同的话哈希值也应相同，例如，如果`a==b`，同样`a.hashValue == b.hashValue`。

所有Swift的基本类型（`String`,`Int`,`Double`,`Bool`）都是hashable的。枚举中无关联值的枚举值（如[枚举](0208-Enumerations.md)中所述）默认同样是hashable的

>注意
>>可以使用自定义并且实现`Hashable`协议的类来作为set值类型或者字典的键类型。实现`Hashable`协议必须提供一个只读并且类型为`Int`属性名为`hashValue`的属性。类型的`hashValue`值在同一程序的不同执行位置或者在不同程序中并不要求必须相同。
>>由于`Hashable`遵循`Equatable`，实现协议的类型必须实现判等运算符(`==`)。`Equatable`协议要求任何实现`==`的类都要是一个等价关系的实现。也就是，实现`==`必须满足以下三个条件，对于所有值`a`,`b`,`c`：
>> - a == a (自反性)
>> - a == b 意味着 b == a （交换性）
>> - a == b && b == c  （传递性）

>> 更多信息请参见[协议](0221-Protocols.md)章节

#####Set类型语法
Swift中set的类型写作`Set<Element>`，`Element`是set允许存储的类型。与Array不同的是Set没有简写形式。

#####创建并初始化一个空的Set

可以使用初始化语法来创建一个空的Set：

```Swift
var letters = Set<Character>()
print("letters is of type Set<Character> with \(letters.count) items.")
// Prints "letters is of type Set<Character> with 0 items."
```

>注意
>>`letter`的类型通过初始化语法可确定为`Set<Character>`。

或者，如果上下文中已经提供了类型的信息，例如方法的参数或者常量或变量已经指定类型，那么可以通过数组字面量来创建一个空的Set：

```Swift
letters.insert("a")
// letters now contains 1 value of type Character
letters = []
// letters is now an empty set, but is still of type Set<Character>
```

#####使用数组字面量来创建Set
可以使用数组字面量来作为简写形式实例化一个包含一个或多个值的Set。

下例中创建了一个名为`favoriteGenres`的储存`String`类型的Set：

```Swift
var favoriteGenres: Set<String> = ["Rock", "Classical", "Hip hop"]
// favoriteGenres has been initialized with three initial items
```

`favoriteGenres`变量声明为”存储`String`类型值的Set“，写作`Set<String>`。由于这个Set已知指定了存储的值得类型为`String`，所以它只允许存储`String`值。这里的`favoriteGenres`Set使用三个`String`值（`Rock`,`Classical`,`Hip hop`）通过数组字面量的方式进行初始化。

>注意
>>此处的`favoriteGenres`声明为变量（使用`var`关键字标识），而不是常量（使用`let`关键字标识）是由于在之后的例子中会对Set中的元素添加删除等操作。

set类型不能单独从数组字面量中推断出类型，所以需要指定为`Set`类型。然而，由于Swift的类型推断，在通过数组字面量来初始化set时不用明确写出set的具体类型。`favoriteGenres`的初始化可以简写为：

```Swift
var favoriteGenres: Set = ["Rock", "Classical", "Hip hop"]
```

由于数组字面量中的值都是同一类型，所以Swift可以推断出`Set<String>`就是`favoriteGenres`的正确类型。

#####Set的访问和操作

可以使用Set的属性和方法来访问和操作Set。

使用只读属性``来获取set中的元素个数：

```Swift
print("I have \(favoriteGenres.count) favorite music genres.")
// Prints "I have 3 favorite music genres." 
```

使用`isEmpty`属性作为检查set`count`属性是否为`0`的简写：

```Swift
if favoriteGenres.isEmpty {
    print("As far as music goes, I'm not picky.")
} else {
    print("I have particular music preferences.")
}
// Prints "I have particular music preferences."
```
使用`insert(_:)`方法来向Set中插入一个值：

```Swift
favoriteGenres.insert("Jazz")
// favoriteGenres now contains 4 items
```

使用`remove(_:)`方法来删除Set中的元素，如果删除的元素存在于Set中，则返回删除的元素，否则返回`nil`。可以使用` removeAll()`来清空Set：

```Swift
if let removedGenre = favoriteGenres.remove("Rock") {
    print("\(removedGenre)? I'm over it.")
} else {
    print("I never much cared for that.")
}
// Prints "Rock? I'm over it."
```

使用`contains(_:)`方法来判断set中是否含有某个特定的元素：

```Swift
if favoriteGenres.contains("Funk") {
    print("I get up on the good foot.")
} else {
    print("It's too funky in here.")
}
// Prints "It's too funky in here."
```

#####set的遍历

可以使用`for-in`循环对set进行完整遍历。

```Swift
for genre in favoriteGenres {
    print("\(genre)")
}
// Jazz
// Hip hop
// Classical
```
更多关于`for-in`的信息，请参见[For-in循环](0205-Control-Flow.md#for-inLoops)

Swift中`Set`类型是无序的，如果像使用特定的顺序遍历set，可以使用`sorted()`方法。该方法会返回一个包含set中元素的已经通过`<`运算符排过序的数组。

```swift
for genre in favoriteGenres.sorted() {
    print("\(genre)")
}
// Classical
// Hip hop
// Jazz
```

####执行Set的运算

通过基本的set运算可以更搞笑的对set进行操作，例如将两个set合并，检查两个set有哪些值相同，或者检查两个set是否包含所有、一些、或者没有相同的值。

#####基本的Set操作

下图描述了两个set`a`和`b`——用阴影区域表示的各种集合运算的结果。![](/assets/WX20180412-163219@2x.png)

- 使用`intersection(_:)`方法创建一个两个set的交集
- 使用`symmetricDifference(_:)`方法创建两个set的对等差分
- 使用`union(_:)`方法创建两个set的合集
- 使用`subtracting(_:)`方法创建`a`和`b`的差集

```Swift
let oddDigits: Set = [1, 3, 5, 7, 9]
let evenDigits: Set = [0, 2, 4, 6, 8]
let singleDigitPrimeNumbers: Set = [2, 3, 5, 7]
 
oddDigits.union(evenDigits).sorted()
// [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
oddDigits.intersection(evenDigits).sorted()
// []
oddDigits.subtracting(singleDigitPrimeNumbers).sorted()
// [1, 9]
oddDigits.symmetricDifference(singleDigitPrimeNumbers).sorted()
// [1, 2, 9]
```

#####Set的从属关系及判等

下图描述了三个set`a`和`b`——用阴影区域表示各个set公共的元素。Set`a`是set`b`的父集，因为set`a`包含`b`中所有的元素。相反的，set`b`是set`a`的子集，因为所有set`b`中的元素在`a`中都存在。由于set`b`与`a`没有任何相同的元素，所以`b`和`c`是不相交的。

![](/assets/WX20180413-172005@2x.png)

- 使用`==`运算符判断两个set是否包含相同的元素。
- 使用`isSubset(of:)`判断set是否为另一个set的子集
- 使用`isSuperset(of:)`判断set是否是另一个set的父集
- 使用`isStrictSubset(of:)`或`isStrictSuperset(of:)`判断一个set是否是另一个set的父集或子集，但两个set不能相等。
- 使用`isDisjoint(with:)`判断两个set是否不相交

```Swift
let houseAnimals: Set = ["🐶", "🐱"]
let farmAnimals: Set = ["🐮", "🐔", "🐑", "🐶", "🐱"]
let cityAnimals: Set = ["🐦", "🐭"]
 
houseAnimals.isSubset(of: farmAnimals)
// true
farmAnimals.isSuperset(of: houseAnimals)
// true
farmAnimals.isDisjoint(with: cityAnimals)
// true
```

<span id="dictionaries"></span>
####Dictionaries