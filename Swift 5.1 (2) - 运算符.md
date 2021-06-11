**运算符的术语：** 操作符分为一元，二元，三元。

*   一元运算符主要操作一个单一的目标(比如：-a)。一元前缀运算符可以直接出现在它们的目标前面(比如：!b)，一元后缀运算符直接出现在它们目标之后（比如：c!）。
*   二元运算符在两个目标（例如2 + 3）上运行，并且是中缀，因为它们出现在两个目标之间。
*   三元运算符在三个目标上进行运算。与C一样，Swift只有一个三元运算符，即三元条件运算符（a？b：c）

**赋值运算符：** 赋值运算符（a = b）使用b值初始化或更新a的值。

```
let b = 10
var a = 5
a = b //a的值变为了10
复制代码
```

如果赋值的右侧是具有多个值的元组，则元组的元素可以一次分解为多个常量或变量。

```
let (x, y) = (1, 2)//!< x = 1 , y = 2
复制代码
```

与C和Objective-C中的赋值运算符不同，Swift中的赋值运算符本身不返回值。以下声明无效

```
 if x = y {//!< '='运算符在swift中没有返回值，所以此处这样写是无效的，同时会报错。
        }
复制代码
```

此功能可防止在实际使用等于运算符`==`时意外使用赋值运算符`=`，通过使`x = y`无效，Swift可以帮助我们避免代码中的这类错误。

**算数运算符**

*   加 `+`
*   减 `-`
*   乘 `*`
*   除 `/`

```
1 + 2       // equals 3
5 - 3       // equals 2
2 * 3       // equals 6
10.0 / 2.5  // equals 4.0
复制代码
```

与C和Objective-C中的算术运算符不同，Swift算术运算符默认情况下不允许值溢出。我们可以通过使用Swift的溢出运算符（例如＆+ b）来选择值溢出行为。请参阅[溢出运算符](https://docs.swift.org/swift-book/LanguageGuide/AdvancedOperators.html#ID37) 字符串连接也支持加法运算符：

```
"hello, " + "world"  // equals "hello, world"
复制代码
```

**求余运算符：** 余数运算符（a％b）计算出a中将包含多少个b，并返回剩余的值（称为余数)

```
9 % 4    // equals 1
-9 % 4   // equals -1
复制代码
```

**一元`-`和`+`运算符：** 可以使用`-`（称为一元减运算符）直接添加于运行的值之前，没有任何空格，切换数值的符号。使用`+`（称为一元加运算符）直接添加于运行的值之前，没有任何空格，一元加运算符`+`只返回它操作的值，没有任何变化。
一元减运算符

```
let three = 3
let minusThree = -three       // minusThree equals -3
let plusThree = -minusThree   // plusThree equals 3, or "minus minus three"
复制代码
```

一元加运算符

```
let minusSix = -6
let alsoMinusSix = +minusSix  // alsoMinusSix equals -6
复制代码
```

即使一元加运算符实际上没有做任何事情，但是当使用一元减运算符作为负数时，我们可以使用它来为代码提供正数的对称性。
**复合赋值运算符：**
与C一样，Swift提供了将赋值`=`与另一个操作符相结合的复合赋值运算符。比如加法赋值运算符`+ =`：

```
var a = 1
a += 2// a is now equal to 3
复制代码
```

表达式`a += 2`是`a = a + 2`的简写。实际上，加法和赋值操作符被组合成一个同时执行两个任务的运算符。 需要注意的是：复合赋值运算符不返回值。例如：不能写`let b = a += 2`。 **比较运算符：** Swift支持所有标准C比较运算符。

*   等于 `==` , 如：(a == b)
*   不等于`!=`, 如： (a != b)
*   大于`>`, 如： (a > b)
*   小于`<`, 如： (a < b)
*   大于等于`>=`, 如： (a >= b)
*   小于等于`!=`, 如： (a <= b)

```
1 == 1   // true because 1 is equal to 1
2 != 1   // true because 2 is not equal to 1
2 > 1    // true because 2 is greater than 1
1 < 2    // true because 1 is less than 2
1 >= 1   // true because 1 is greater than or equal to 1
2 <= 1   // false because 2 is not less than or equal to 1
复制代码
```

比较运算符通常用于条件语句，例如if语句：

```
let name = "world"
if name == "world" {
    print("hello, world")
} else {
    print("I'm sorry \(name), but I don't recognize you")
}
// Prints "hello, world", because name is indeed equal to "world".
复制代码
```

比较元组：如果它们具有相同的类型和相同的数值，则可以比较两个元组。元组从左到右进行比较，一次一个值，直到比较发现两个不相等的值。比较这两个值，并且该比较的结果确定元组比较的总体结果。如果所有元素都相等，则元组本身是相等的。即：在可以比较的前提下，只要按顺序比较找到两个元组中不相同的两个值，则进行比较并且返回，作为元组的比较结果，后面的值将不再进行比较例如：

```
(1, "zebra") < (2, "apple")   //返回 true 因为1 小于2  "zebra" 和 "apple" 将不比较：“ zebra”不小于“apple”并不重要，因为比较已经由元组的第一个元素决定，当元组的第一个元素相同时，它们的第二个元素会被比较。
但是，当元组的第一个元素相同时，它们的第二个元素会被比较，下面就是这种情况
(3, "apple") < (3, "bird")    // 返回 true 因为 3 等于 3, "apple"小于"bird"
(4, "dog") == (4, "dog")      //返回 true 因为 4 等于 4, "dog" 等于"dog"
复制代码
```

另：`只有当给定运算符可以应用于相应元组中的每个值时，才能将元组运用给定运算符进行比较。` 例如，如下面的代码所示，您可以比较两个类型`（String，Int）`的元组，因为可以使用`<`运算符比较`String`和`Int`值。相反，两个类型`（String，Bool）`的元组不能与`<`运算符进行比较，因为`<`运算符不能应用于`Bool`值。

```
if ("blue", -1) < ("purple", 1)  {
    print("结果成立，返回了true")
}
if ("blue", false) < ("purple", true) {//!< 编译器直接会报错
    print("Binary operator '<' cannot be applied to two '(String, Bool)' operands")
}
复制代码
```

> Swift标准库包含的比较元组时，只限于元组少于7个元素。要将元组与七个或更多元素进行比较，我们必须自己实现比较运算符。

另外：Swift还提供了两个标识运算符（===和!==），用于测试两个对象引用是否都引用同一个对象实例
**身份运算符：** 因为类是引用类型，所以多个常量和变量可能引用同一个类的单个实例。（对于结构体和枚举，情况也是如此，因为它们在分配给常量或变量或传递给函数时总是被复制）Swift 提供了两个身份运算符来找出两个常量或变量是否完全引用类的相同实例。

*   相同 (===)
*   不相同 (!==)

注意：相同`===`并不意味着等于`==`。`===`意味着类类型（class type）的两个常量或变量引用了完全相同的类实例。等于意味着两个实例在值上被认为是相等的。

1.  obj1和obj2常量都是类类型，两者引用了不相同的类的实例对象

```
let obj1 = UIView.init()
let obj2 = UIView.init()
let (x,y) = (obj1,obj2)
if x === y {
   print("obj1和obj2常量都是类类型，并且两者引用了完全相同的类的实例对象")
} else{
   print("obj1和obj2常量都是类类型，两者引用了不相同的类的实例对象")//!< 打印结果
}
复制代码
```

2.  obj1和obj2常量都是类类型，并且两者引用了完全相同的类的实例对象

```
let obj1 = UIView.init()
let obj2 = obj1
let (x,y) = (obj1,obj2)
if x !== y {
    print("obj1和obj2常量都是类类型，两者引用了不相同的类的实例对象")
} else{
    print("obj1和obj2常量都是类类型，并且两者引用了完全相同的类的实例对象")//!< 打印结果
}
复制代码
```

**三元条件运算符：**三元条件运算符是一个特殊的运算符，有三个部分，使用用形式：`question ? answer1 :<br/> answer2`。如果问题为真，则返回answer1；否则返回answer2。
三元条件运算符是以下代码的简写：

```
if question {
    answer1
} else {
    answer2
}
复制代码
```

**可Nil合并(Nil-Coalescing)运算符**：nil-coalescing运算符`??`解包一个可选的`a`使用形式：`a ?? b`。解读为：解包可选`a`；如果`a`为`nil`，则返回默认值`b`，否则返回`a`。表达式中`a`始终是可选类型。并且`b`必须与`a`的类型匹配。 nil-coalescing运算符是下面代码的简写：

```
a! =  nil  ?  a!  :  b //<! 使用三元条件运算符和强制解包（a！）来访问包含在a不是nil时的值，否则返回b
复制代码
```

上面的代码使用三元条件运算符和强制解包`a！`来访问包含在可选的`a`中的值，若不是nil时，则不去管`b`的值，并返回`a`中的值，否则返回`b`。

```
let defaultColorName = "red"
var userDefinedColorName: String?   // defaults to nil
var colorNameToUse = userDefinedColorName ?? defaultColorName
复制代码
```

**返回运算符：** Swift包含多个范围运算符。 1.`封闭范围运算符（Close Range Operator）`：封闭范围运算符`...`，使用形式`（a ... b）`定义从`a`到`b`的范围，并包括值`a`和`b`并且`a`的值不得大于`b`。 当我们希望在所有值的全部范围内进行遍历时，闭合范围运算符非常有用，例如使用for-in循环：

```
for item in 1...8 {
    print(item)//!< 打印 12345678
}
复制代码
```

2.`半开范围运算符（Half-Open Range Operator）`：半开范围运算符`..<`使用形式：`a .. <b`定义从`a`到`b`的范围，但不包括`b`，它被认为是半开放的，因为只包含它的第一个值却没有它的最终值。与封闭范围运算符一样，`a`的值不得大于`b`。如果`a`的值等于`b`，则最终有效范围将为空。
当我们遍历基于零的列表（如数组），因为数组的长度需要计算，此时根据定义，使用半开范围运算符是最合适的。

```
/*打印结果：
 索引:0,对应字符串：i
 索引:1,对应字符串：am
 索引:2,对应字符串：zhangfei
*/
let array = ["i","am","zhangfei"]
for index in 0 ..< array.count { //!< 遍历数组
    print("索引:\(index),对应字符串：\(array[index])")
}
//直接输出字符串,形式
let array = ["i","am","zhangfei"]
for str in array[0..<array.count] {
    print(str)
}
复制代码
```

3.局部（单面/侧）范围(One-Sided Ranges)：`封闭范围运算符（Close Range Operator）`和`半开范围运算符（Half-Open Range Operator）`的使用延伸。
`封闭范围运算符`有一个替代形式，用于使范围在一个方向上尽可能继续。例如：一个数组从索引位置2到数组末尾的所有元素的范围。这种情况下我们可以省略运算符一侧的值。具体使用：

```
let array = ["i","am","zhangfei"]
//直接输出字符串 形式1
for str in array[...]{
    print(str)
}
//直接输出字符串 形式2 此处`1`可以是数组范围内小于`array.count-1`的任意值
for str in array[1...] {
    print(str)
}
//直接输出字符串 形式3 此处`(array.count-1)`可以是数组范围内大于0的任意值
for str in array[...(array.count-1)] {
    print(str)
}
复制代码
```

`半开放范围操作符`也具有单侧形式，仅使用其最终值编写，最终值不是范围的一部分，因为是小于`<`。具体使用

```
//直接输出字符串 形式4 
for str in array[..<array.count] {
    print(str)
}
复制代码
```

局部（单面/侧）范围(One-Sided Ranges)可以在其他上下文中使用，而不仅仅在下标中使用。在需要遍历的情况下不能忽略了单侧范围的第一个值，因为遍历需要清楚的知道应该从哪里开始。我们却可以使用忽略了最终值单侧范围，但是范围可以无限期的继续，所以需要确保为我们的循环添加显式结束条件，我们还可以检查单侧范围是否包含特定的值。具体示例如下：

```
let range = ...5
range.contains(7)   // false
range.contains(4)   // true
range.contains(-1)  // true
复制代码
```

关于范围可以无限期的继续，所以需要确保为我们的循环添加显式结束条件举例如下：

```
let range =  0...
for i in range {//!< 代码无限期的执行
    print(i)
}
复制代码
```

**逻辑运算符：** 逻辑运算符修改`Boolean` 逻辑值为`true`和`false`。 Swift支持基于C语言的三个标准逻辑运算符。

*   逻辑非 `!` 如：`!a`
*   逻辑与 `&&`如：`a && b`
*   逻辑或 `||`如：`a || b`

参考资料： [swift 5.1官方编程指南](https://docs.swift.org/swift-book)



收录原文： [QiShare团队](https://www.jianshu.com/c/b3bd94559163)
