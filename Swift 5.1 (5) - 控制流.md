### 控制流

##### For-In循环

使用`for-in`循环迭代数组

```
let names = ["Anna", "Alex", "Brian", "Jack"]
for name in names {
    print("Hello, \(name)!")
}
复制代码
```

使用`for-in`循环迭代字典

```
let airports = ["job": "将军", "age": "16", "name": "zhangfei"]
for (key,value) in airports {
print("\(key)")
print("\(value)")
}
复制代码
```

使用`for-in`循环迭代数值范围

```
for index in 1...5 {
    print("\(index) times 5 is \(index * 5)")
}
复制代码
```

使用`for-in`循环迭代数值范围之使用`stride（from：to：by :)`函数：返回从起始值到结束值（不包括），跳过指定量的序列。从开始值起序列中的每个连续值都会增加相同范围的幅度，直到下一个值等于或超过结束值。（以指定间隔迭代特定数值时的序列）。符合`Strideable`协议的任何类型的值都可以使用此函数，例如整数或浮点类型。

```
for item in stride(from: 0, to: 60, by: 5) {
    print(item, separator: "", terminator: " ")//!< 0 5 10 15 20 25 30 35 40 45 50 55
}
for item in stride(from: 0, to: Double.pi * 2, by: .pi/2) {
     print(item, separator: "", terminator: " ")//!<0.0 1.5707963267948966 3.141592653589793 4.71238898038469
}
复制代码
```

使用`for-in`循环迭代数值范围之使用`stride(from:through:by:)`函数：返回从起始值到结束值（可能包括），跳过指定量的序列。（以指定间隔迭代特定数值时的序列）与`stride（from：to：by :)`函数区别于它可能会包括结束值。

```
for item in stride(from: 0, through: 60, by: 5) {
    print(item, separator: "", terminator: " ")//!< 0 5 10 15 20 25 30 35 40 45 50 55 60
}
for item in stride(from: 0, through: Double.pi * 2, by: .pi/2) {
     print(item, separator: "", terminator: " ")//!<0.0 1.5707963267948966 3.141592653589793 4.71238898038469 6.283185307179586 
}
复制代码
```

##### While循环

Swift提供了两种`while`循环：

*   while：在每次循环开始时判断条件。
*   repeat-while：在每次循环结束时判断条件。

**While** `while`循环开始时判断条件是否成立，若`true`立即执行方法体，直到条件变为`false`时停止执行。

```
let adc = 10
var apc = 0;
while apc < adc {
    apc += 1 //!< 必须要有终止的条件 若 apc < adc 恒成立则程序陷入死循环
    print("条件成立") //10
}
复制代码
```

**Repeat-While** `repeat-while`循环：`while`循环的变体，类似于其他语言中的`do-while`，先执行单个循环，再考虑循环条件，若为`true`继续重复循环，直到条件为`false`停止执行。

```
let adc = 10
var apc = 0;
repeat {
    apc += 1
    print("条件成立") //!< 10次
}while apc < adc
复制代码
```

##### 条件语句

**If**

```
let adc = 20
if adc <= 32 {
    print("adc <= 32")
} else if adc >= 86 {
    print("adc >= 86")
} else {
    print("32 <adc< 86")
}
复制代码
```

**Switch**

```
let someCharacter: Character = "z"
switch someCharacter {
case "a":
    print("The first letter of the alphabet")
case "z":
    print("The last letter of the alphabet")
default:
    print("Some other character")
}
复制代码
```

**不隐式贯穿** Swift中的`switch`语句执行时不会贯穿每个case。而C和Objective-C中的`switch`语句需要显式的`break`语句，若不添加则会向下贯穿到所匹配项下面的每个`case`，并执行。

```
MyEnumType type = MyEnumType2;
switch (type) {
    case MyEnumType1:
        NSLog(@"MyEnumType1");
    case MyEnumType2:
        NSLog(@"MyEnumType2");
    case MyEnumType3:
        NSLog(@"MyEnumType3");

}
/*
 MyEnumType2
 MyEnumType3
 */
复制代码
```

Swift中的`switch`语句只要第一个匹配的`switch`的`case`完成，整个switch语句就会完成执行，而不需要显式的`break`语句。

```
let anotherCharacter: Character = "a"
switch anotherCharacter {
case "a", "A":
    print("The letter A")
default:
    print("Not the letter A")
}
复制代码
```

**Range匹配**
`switch`语句可以检测其判断的值，是否包含在某个case的范围内。

```
let adc = 20
var apc = 0;
var result = ""

switch adc {
case 0...10:
   result = "0...10"
case 11..<20:
    result = "11..<20"
case 20...30:
    result = "20...30"
default:
    result = "beyond of range"
}
print(result)//!< 20...30
复制代码
```

**元组**
`switch`语句可以判断元组的值，是否符合某个case。可以针对元组不同的值或值的间隔范围来测试元组的每个元素。或者，使用下划线字符(通配符)`_`来匹配任何可能的值。

```
let tuples : (Int,String,Int) = (404,"not found",-1)
switch tuples {
case (300,"精准匹配1",0):
    print("精准匹配1")
case (0...200,"范围匹配1",-2...10):
    print("范围匹配1")
case (_,_,-2...2):
    print("通配符匹配元组前两个,范围匹配最后一项")
default:
    print("没有匹配到")
}

复制代码
```

**值绑定**
`switch`中`case`可以命名它所匹配到的临时的常量或变量， 以便在`case`对应的方法中使用。这种行为称为值绑定。

```
let anotherPoint = (2, 0)
switch anotherPoint {
case (let x, 0):
    print("横坐标\(x)")
case (0, let y):
    print("纵坐标 \(y)")
case let (x, y):
    print("任何点 (\(x), \(y))")
}
复制代码
```

上述switch语句中`case（let x，0）`匹配`y`值为0的任何点，并将点的`x`值赋给临时常量`x`。`case（0，let y）`匹配`x`值为0的任何点，并将点的`y`值赋给临时常量`y`。`let（x，y）`，声明了一个可以匹配任何值的含有两个占位符常量的元组。因为匹配所有可能的剩余值，所以不需要`default case`来使switch语句穷举。
**Where**
switch语句中case可以使用`where`子句来检查其他条件。

```
let yetAnotherPoint = (1, -1)
switch yetAnotherPoint {
case let (x, y) where x==y:
    print("匹配到x与y相同的情况")
case let(x,y) where x == -y:
    print("匹配到x与y为相反数的情况")//!<匹配到x与y为相反数的情况
default:
    print("没有匹配的结果")
}
复制代码
```

上述示例中switch语句中的case声明占位符常量`x`和`y`，它们暂时从`yetAnotherPoint`获取元组值。这些常量用作`where`子句的一部分，用于创建动态过滤器。仅当`where`子句的条件对占位符常量`x`和`y`的计算结果为`true`时，switch语句的case才会成功匹配当前值。

**复合使用**

`switch`语句中若有多个case共享的相同方法体，可以通过在`case`之后组合多个模式，每个模式之间用逗号隔开来表示。多个模式中任一个匹配，则认为这个`case`是匹配的。同时`case`之后的多个模式也可以多行表示。

```
let someCharater = "e"
switch someCharater {
case "a","o","e","f":
    print("事例1，匹配成功")//!< log
case "b","v","r","h":
    print("事例2，匹配成功")
default:
    print("未匹配")
}
//复合事例中的值绑定，绑定的值类型必须匹配。case (let x, let y), (0, let x)这种是不被允许的 因为方法体中使用x，y时，若匹配的是 (0, let x)则y 无效。因为相同的值绑定应该存在于所有`case`之后的模式中。
let stillAnotherPoint = (9, 0)
switch stillAnotherPoint {
case (let x, 0), (0, let x)://!< 'x' must be bound in every pattern:'x'必须绑定在每个模式中
    print("匹配成功")
default:
    print("未匹配")
}
复制代码
```

switch的`case`后对应多个模式的复合事例中，每个模式对应的绑定的值类型必须匹配，并且相同的一组值绑定，如`(let x, let y)`其中`x`，`y`称为一组值绑定，应该存在于所有`case`之后的模式中。

##### 控制转移语句

控制转移语句通过将控制从一段代码转移到另一段代码来改变代码执行的顺序。Swift有五个控制转移语句：

*   continue
*   break
*   fallthrough
*   return
*   throw

**continue**

`continue`语句：跳出正在执行的循环语句，立即开始执行下一次循环。

```
let puzzleInput = "great minds think alike"
var puzzleOutput = ""
let charactersToRemove: [Character] = ["a", "e", "i", "o", "u", " "]
for character in puzzleInput {
    if charactersToRemove.contains(character) {
        continue
    }
    puzzleOutput.append(character)
}
print(puzzleOutput) //!< break下跳出循环,立即开始下一次迭代，输出为：grtmndsthnklk
复制代码
```

**break**

`break`语句：立即结束所有控制流语句的执行。
循环语句中的`break`：循环语句中使用break，会立即结束循环的执行，并在循环方法体`}`之后将控制权转移给后续的代码。

```
let puzzleInput = "great minds think alike"
var puzzleOutput = ""
let charactersToRemove: [Character] = ["a", "e", "i", "o", "u", " "]
for character in puzzleInput {
    if charactersToRemove.contains(character) {
        break
    }
    puzzleOutput.append(character)
}
print(puzzleOutput) //!< break下跳出循环不在开始，输出为gr
复制代码
```

switch语句中的`break`：在switch语句中使用`break`，会使switch语句立即结束其执行，并移交控制权。

```
let stillAnotherPoint = (9, 0)
switch stillAnotherPoint {
case (let x, 0), (0, let x):
    print("匹配成功")
default:
    break
}
复制代码
```

**贯穿（Fallthrough）**

如果需要C或Objective-C的贯穿行为，则可以使用`fallthrough`关键字。

```
let describe = 5
var description = ""
switch describe {
case 2, 3, 5, 7, 11, 13, 17, 19:
    description += "I am"
    fallthrough
case 18:
    description += " bob" //!< case 去掉fallthrough 则输出I am bob
    fallthrough
default:
    description += " and you?"
}
print(description)//!< I am bob and you?
复制代码
```

**标签语句**

在Swift中，其他循环和条件语句中可以嵌套循环和条件语句，从而创建复杂的控制流结构。但是，循环和条件语句都可以使用`break`语句过早地结束执行。因此，需要明确`break`语句终止的循环或条件语句，或明确`continue`语句应该影响哪个循环是非常必要的，故会用到标签语句。

```
var result = ""
let adc = 30
forLabel : for item in 9...adc {
   switchLabel :switch item {
    case 0...10:
        result += " 0...10"
        break switchLabel //!<swift中break是默认的
    case 11..<20: //!<  若是11..<20区间则跳出for循环，开始下次迭代
        continue forLabel
    case 20://!< 若是20 则立即终止for循环
        result += " 终止for循环"
        break forLabel
    default:
        result += "beyond of range"
    }
}
print(result) //!< 0...10 0...10 终止for循环
复制代码
```

**提前退出（throw,return）**
与`if`语句一样，`guard`语句根据表达式的布尔值执行语句。使用guard语句要求条件必须为`true`才能执行`guard`语句之后的代码。与`if`语句不同，`guard`语句总是有一个`else`子句 如果条件为`false`，则执行`else`子句中的代码。`guard`的`else`子句不能向下贯穿，必须使用转移控制的语句`return`或`throw`才能退出作用域。

```
//return
let adc = 30
//! guard方法体不能向下贯穿，需要使用`return`或`throw`退出作用域
guard adc > 30 else {
    print("条件不成立")
    return //!< 提前结束了
}
//throw退出作用域
guard adc > 30 else {
    print("条件不成立")
    throw HttpError.authError
}
复制代码
```

**检查API可用性**
Swift支持检查API可用性：编译器使用SDK中的可用性信息来验证使用的API是否在指定部署目标上可用。确保我们不会在给定部署目标上使用不可用的API。可以在`if`或`guard`语句中使用可用性条件进行判断。

```
if #available(iOS 10, macOS 10.12, *) {
    // Use iOS 10 APIs on iOS, and use macOS 10.12 APIs on macOS
} else {
    // Fall back to earlier iOS and macOS APIs
}
复制代码
```

参考资料： [swift 5.1官方编程指南](https://docs.swift.org/swift-book)



收录于： [QiShare团队](https://www.jianshu.com/c/b3bd94559163)
