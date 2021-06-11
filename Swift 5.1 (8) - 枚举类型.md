### Enumeration：枚举类型

一个枚举类型是为一组相关联的值定义的一个公共类型，使得这些关联值能够在代码中以类型安全的方式进行处理。 C语言中的枚举类型将相关的枚举项使用整数值表示。而Swift中的枚举更灵活，并且没有为枚举项提供值。如果为为枚举项提供值（则该值称为原始值`raw value`），该值可以是字符串，字符，任何整数或浮点类型的值。 另外，枚举项可以指定任何类型的关联值与枚举项的值一起存储。我们可以定义一组通用的相关项作为枚举的一部分，每个枚举都有一组比较合适的类型的不同值与之关联。同时Swift中的枚举类型采用了许多只有类才支持的特征，比如枚举：

*   能够提供计算属性，用于支持枚举当前值之外的额外的信息；
*   能够提供实例方法，用于支持与枚举所代表的值相关的功能；
*   能够定义初始化方法，提供初始枚举项的值；
*   能够支持扩展， 可以在原始实现的基础上扩展其功能；
*   能够遵守协议，用于提供一切标准的功能；

#### 枚举语法

使用enum关键字引入枚举，并将其整个定义放在`{}`中

```
enum <#name#> {
    case <#case#>
}
复制代码
```

枚举的定义与使用

```
enum CompassPoint {
    case north
    case west
    case east
    case south
}
//多个枚举写在一行中。
enum CompassPoint {
    case north,west,east,south
}
复制代码
```

每个枚举定义都定义了一个新类型。

```
var direction : CompassPoint = .north
var direction = CompassPoint.north
复制代码
```

#### 使用Switch语句匹配枚举值

```
let direction : CompassPoint = .north
switch direction {
case .east:
    print("ease")
case .north:
    print("north")
case .west:
    print("west")
case .south:
    print("south")
}
复制代码
```

#### 迭代枚举项

通过在枚举名称后使用`: CaseIterable`，可以使枚举，拥有一个关于所有枚举项的集合。调用枚举类型的`allCases`属性，可以获取这个集合。

```
enum CompassPoint : CaseIterable{
    case north,west,east,south
}
//输出allCases
/*
 log:[swift_basic.EnumerationPractice.CompassPoint.north, swift_basic.EnumerationPractice.CompassPoint.west, swift_basic.EnumerationPractice.CompassPoint.east, swift_basic.EnumerationPractice.CompassPoint.south]
 */
print(CompassPoint.allCases)
switch CompassPoint.allCases.first! {
case .north:
    print("输出正确")
default:
    print("输出失败")
}
//eachCase每一项都是枚举类型的示例
for eachCase in CompassPoint.allCases {
    /*north
     west
     east
     south*/
    print(eachCase)
}
复制代码
```

#### 枚举关联值

枚举类型中在枚举项的旁边存贮额外的其他类型的值，这些值被称为关联值。并且每次在代码中使用有关联值的枚举项时，该关联值都会有所不同。 Swift中可以定义枚举以存储任何给定类型的关联值，并且每个枚举项的值类型也可以不同。 例如：商品码有二维码和条形码两种形式。二维码的信息可以提取为`String`类型，条形码的信息是一串数字，按照：一位系统数字+五位制造商标识+五位产品标识+一位校验数字的格式，我们可以联想到`(Int,Int,Int,Int)`元组类型。所以我们使用关联值定义枚举类型如下： 通用商品条码

```
enum ProductCode {
    case upc(Int,Int,Int,Int)//通用商品条码
    case qrCode(String)//二维码
}
复制代码
```

上述代码解读：定义了一个枚举类型`ProductCode`，有两个枚举项`upc`和`qrCode`。这两个枚举项分别可以存储`(Int, Int, Int, Int)`类型和`String`类型的关联值。 `ProductCode`枚举类型的定义不提供任何实际意义的`Int`或`String`值。 它只定义`ProductCode`常量和变量在等于`ProductCode.upc`或`ProductCode.qrCode`时可以存储的关联值的类型。

```
var productCode = ProductCode.upc(1, 22, 333, 4444)
productCode = ProductCode.qrCode("二维码哈")
复制代码
```

使用`Switch`语句匹配枚举项并且提取枚举项的关联值。可以使用`let`和`var`将每个关联值提取为常量或变量，以在`case`的正文中使用。

```
var productCode = ProductCode.upc(1, 22, 333, 4444)
switch productCode {
case .upc(let x, let y, let z, let zz):
    print("从switch语句中提取的相匹配的枚举项的关联值为x:\(x) y:\(y) z:\(z) zz:\(zz)")
case ProductCode.qrCode(let str):
    print("从switch语句中提取的相匹配的枚举项的关联值为:\(str)")
}
productCode = ProductCode.qrCode("二维码哈")
switch productCode {
case let .upc(x, y, z, zz):
    print("从switch语句中提取的相匹配的枚举项的关联值为x:\(x) y:\(y) z:\(z) zz:\(zz)")
case let .qrCode(str):
    print("从switch语句中提取的相匹配的枚举项的关联值为:\(str)")
}
复制代码
```

#### 枚举原始值

关联值的示例中展示了枚举如何声明它们存储不同类型的关联值。作为关联值的替代，枚举也可以预先填充默认值（称为原始值），它们都是相同的类型。

```
enum NameType : String{
    case ZhangFei = "张飞"
    case GuanYu = "关羽"
    case LiuBei = "刘备"
}
let name = NameType.ZhangFei
print(name.rawValue)//!< log:张飞
复制代码
```

枚举`NameType`的原始值被定义为`String`类型，并被设置原始值。原始值可以是字符串，字符或任何整数或浮点数类型。`每个原始值在其枚举声明中必须是唯一的。` 原始值与关联值不同。原始值：预先填充的默认值，对于特定的枚举项，其原始值总是相同的。关联值：每次基于枚举情况之一创建一个常量或变量时，其关联值可以是不同的。

**隐式分配原始值**

使用原始值为整数或字符串类型的枚举时，可以不用为每个`case`显式分配原始值。因为Swift会自动为我们分配值。例如，当整数用于原始值时，每种情况的隐含值比前一种情况多一个。如果第一种情况没有设置值，则其值为0。可以使用`rawValue`属性访问枚举项的原始值。

```
enum Planet: Int,CaseIterable {
    case mercury = 1, venus, earth, mars, jupiter, saturn, uranus, neptune
}
//查看各项的`rawvalue`
var planetOutStr = "枚举类型Planet各项的原始值"
for item in Planet.allCases {
    planetOutStr += "\(item) : \(item.rawValue) "
}
print(planetOutStr)//!< 枚举类型Planet各项的原始值mercury : 1 venus : 2 earth : 3 mars : 4 jupiter : 5 saturn : 6 uranus : 7 neptune : 8
复制代码
```

原始值为字符串类型的枚举，每个枚举项隐式分配的原始值是该枚举项的名称。

```
enum CompassPoint :String,CaseIterable{
    case north,west,east,south
}
var directionOutStr = "枚举类型CompassPoint各项的原始值"
for item in CompassPoint.allCases {
    directionOutStr += "\(item) : '\(item.rawValue)' "
}
print(directionOutStr)//!< 枚举类型CompassPoint各项的原始值north : 'north' west : 'west' east : 'east' south : 'south' 
复制代码
```

**从原始值初始化**

如果使用原始值类型定义枚举，则枚举会自动接收一个参数名：`rawValue`参数类型：原始值类型的初始话方法，并返回枚举项或`nil`。我们可以使用此初始化方法尝试创建该枚举类型的新实例。

```
let possiblePalnet = Planet.init(rawValue: 7)
//!< Planet类型的可选项。Optional(swift_basic.EnumerationPractice.Planet.uranus)
//无法根据原始值匹配到枚举项的情况
let possiblePalnet = Planet.init(rawValue: 9)//!< Planet类型的可选项。9已经超出了枚举的所有项的范围。log:nil
//需要解包，可选绑定
if let possiblePlanet = possiblePalnet {
    print(possiblePlanet)
    switch possiblePlanet {
    case .earth:
        print("地球")
    default:
        print("其他行星")
    }
} else {
    print("没有找到合适的枚举项")
}
复制代码
```

#### 枚举的递归

**定义一个枚举时，若该枚举类型的某个`case`关联了一个或多个该枚举类型的值时，系统会自动提示，需要添加`indirect`关键字，因为此时的枚举类型已经被定义为了拥有递归结构的递归枚举。** 通过在枚举项的前面使用`indirect`关键字，来表示此枚举项是可递归的。 以下示例为存储了三个数学表达式递归枚举的定义。

```
//方式一
//递归枚举,存储了三个数学表达式 使用`indirect`来表示枚举项时可递归调用的。
enum ArithmeticExpression {
    case number(Int)
    indirect case addition(ArithmeticExpression, ArithmeticExpression)
    indirect case multiplication(ArithmeticExpression, ArithmeticExpression)
}
复制代码
```

在枚举开始之前使用`indirect`关键字，为具有关联值的所有枚举项启用递归：

```
//方式二
indirect enum ArithmeticExpression {
    case number(Int)
    case addition(ArithmeticExpression, ArithmeticExpression)
    case multiplication(ArithmeticExpression, ArithmeticExpression)
}
复制代码
```

`ArithmeticExpression`枚举类型的每一项都设置有相应的关联值，并且`addition`和`multiplication`都关联了可以存储`(ArithmeticExpression, ArithmeticExpression)`类型的值。即：分别关联了两个`ArithmeticExpression`枚举类型。

递归枚举的嵌套:

```
//存储了一个为5的关联值
let five = ArithmeticExpression.number(5)
//存储了一个为6的关联值
let six = ArithmeticExpression.number(6)
//存储了一个为3的关联值
let three = ArithmeticExpression.number(3)
//addition枚举项，关联了两个当前枚举类型的值。
let sum = ArithmeticExpression.addition(five, six)
//multiplication枚举项，关联了两个当前枚举类型的值。
let multiplication = ArithmeticExpression.multiplication(sum, three)//数学表达式的呈现形式。
复制代码
```

创建递归函数验证`multiplication`是否可以计算正确结果

```
//创建一个递归函数验证可递归性
func arithmeticOperation(_ expression : ArithmeticExpression) -> Int {

    switch expression {
    case let .number(x):
        return x
    case let .addition(x, y):
        //! 此处x和y仍旧是表达式，所以需要先进行递归运算得出`Int`类型的关联值
        return arithmeticOperation(x) + arithmeticOperation(y)
    case .multiplication(let x, let y):
        //! 此处x和y仍旧是`ArithmeticExpression`，所以需要先进行递归运算得出`Int`类型的关联值
        return arithmeticOperation(x) * arithmeticOperation(y)
    }
}
print("嵌套的数学表达式进行递归调用后的结果是：\(arithmeticOperation(multiplication))")
//!< log:嵌套的数学表达式进行递归调用后的结果是：33

复制代码
```

参考资料： [swift 5.1官方编程指南](https://docs.swift.org/swift-book)



收录于： [QiShare团队](https://www.jianshu.com/c/b3bd94559163)
