####枚举 结构体

可以通过`enum` 新建枚举。就像类或者其他提到过的类型，枚举可以设置与相关的方法。


```Swift
enum Rank: Int {
    case ace = 1
    case two, three, four, five, six, seven, eight, nine, ten
    case jack, queen, king
    func simpleDescription() -> String {
        switch self {
        case .ace:
            return "ace"
        case .jack:
            return "jack"
        case .queen:
            return "queen"
        case .king:
            return "king"
        default:
            return String(self.rawValue)
        }
    }
}
let ace = Rank.ace
let aceRawValue = ace.rawValue

```

>实验
>>定义一个方法通过比较两个枚举值的原始数值判断两个`Rank`枚举值的大小

在Swift中枚举的原始数值从0开始并以步长1递增，但是可以通过明确写出原始数值值来改变这一默认行为。在上面的例子中，`Ace` 指定为特定的值1，其他枚举项的原始数值将会按顺序递增。也可以设置枚举原始数值为字符串或者浮点类型。通过`rawValue`属性获取枚举的原始数值。

使用 `init?(rawValue:)` 初始化方法通过原始数值新建一个枚举。会返回一个对应原始数值的枚举，如果Rank中不包含该原始值则返回`nil`


```Swift

if let convertedRank = Rank(rawValue: 3) {
    let threeDescription = convertedRank.simpleDescription()
}

```
枚举中枚举项的值为实际值，并不是原始数值的另一种写法，如果原始数值并没有意义的话，可以完全省略掉。


```Swift

enum Suit {
    case spades, hearts, diamonds, clubs
    func simpleDescription() -> String {
        switch self {
        case .spades:
            return "spades"
        case .hearts:
            return "hearts"
        case .diamonds:
            return "diamonds"
        case .clubs:
            return "clubs"
        }
    }
}
let hearts = Suit.hearts
let heartsDescription = hearts.simpleDescription()

```

>试验
>>给 `Suit` 添加 `color()` 方法，`spades` 和 `clubs` 返回 `black`， `hearts` 和 `diamonds` 返回 `red`

