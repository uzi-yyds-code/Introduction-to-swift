
**字符串**
字符串是一系列字符组成的。Swift字符串由String类型表示。 1.使用字符串文字作为常量或变量的初始值：

```
let str = "I am zhangfei"//str 系统使用类型推断为String类型
复制代码
```

2.多行字符串：由三个双引号`"""`括起来的字符序列。注意：多行字符串文字的正文开始以及结束时，分隔符`"""`必须独占一行。

```
let quotation = """
The White Rabbit put on his spectacles.  "Where shall I begin,
please your Majesty?" he asked.

"Begin at the beginning," the King said gravely, "and go on
till you come to the end; then stop."
"""
let multilineString = """
These are the same.
"""
复制代码
```

多行字符串文字中包含换行符时，该换行符也会出现在字符串的值中。 如果只想使用换行符来简化代码的读取，而不希望换行符成为字符串值的一部分，请在这些行的末尾写一个反斜杠`\`。

```
/*
 不加反斜杠\打印：
 The White Rabbit put on his spectacles.  "Where shall I begin,
 please your Majesty?" he asked.

 "Begin at the beginning," the King said gravely, "and go on
 till you come to the end; then stop."
 加反斜杠\打印：
 The White Rabbit put on his spectacles.  "Where shall I begin,please your Majesty?" he asked.

 "Begin at the beginning," the King said gravely, "and go ontill you come to the end; then stop."
 */
 let softWrappedQuotation = """
The White Rabbit put on his spectacles.  "Where shall I begin,\
please your Majesty?" he asked.

"Begin at the beginning," the King said gravely, "and go on \
till you come to the end; then stop."
"""
print(softWrappedQuotation)
复制代码
```

**字符串中的特殊字符**
字符串中可以包含以下特殊字符：

*   转义的特殊字符 `\ 0`（空字符），`\\`（反斜杠），`\ t`（水平制表符），`\ n`（换行符），`\ r \ n`（回车符），`\"`（双引号）和`\'`（单

引号）。

*   一个任意的Unicode标量值，写为`\ u {n}`，其中`n`是1-8位十六进制数。

特殊字符示例：

```
let name = "i am \"张飞\""
let dollarSign = "\u{24}"        // $,  Unicode标量 U+0024
let blackHeart = "\u{2665}"      // ♥,  Unicode标量 U+2665
let sparklingHeart = "\u{1F496}" // 💖, Unicode标量 U+1F496
print(name+dollarSign+blackHeart+sparklingHeart)//!<i am "张飞"$♥💖
复制代码
```

因为多行字符串文字使用三个双引号`"""`而不是一个`"`，故多行字符串文字中包含双引号`"`可以不用转义它。但是要在多行字符串中包含`"""` ，需要至少转义一个引号。

```
let threeDoubleQuotationMarks = """
Escaping the first quotation mark \"""
Escaping all three quotation marks \"\"\"
"""
复制代码
```

**扩展字符串分隔符：** 我们可以将包含特殊字符的字符串放在`扩展分隔符`中，让所包含的特殊字符（如：转义符）不生效。使用时将字符串放在引号`"`中并用数字符号`＃`括起来。`#`的个数不限制，但是数量需要保持一致性。形式：`let str = #"Line 1\nLine 2"#`，`str`输出换行符`\n`而不是输出两行的字符串。
如果需要字符串中特殊字符的特殊效果，则需要在转义字符`\`后面使用数字符号`#`，但要注意匹配`#` 的个数。例如，字符串：`let str = #"Line 1\nLine 2"#`，我们需要让换行符`\n`生效，则可以使用`let str = #"Line 1\#nLine 2"#`来代替。同样，`let str = ##"Line 1\##nLine 2"##`或`let str = ###"Line 1\###nLine 2"###`也能让换行符生效。
多行字符串使用扩展分隔符而不需要使用转义符`\`，例如：

```
let threeQuotationMarks = #"""
Here are three more double quotes: """
"""#
print(threeQuotationMarks)//!< log:Here are three more double quotes: """
复制代码
```

**初始化一个空的字符串：** 可以使用将空字符串指定给变量，或使用初始化字符串的语法初始化一个`String`实例：

```
// 一下两个字符串都是空的，并且彼此都是相等的
var emptyString = ""        
var anotherEmptyString = String() 
复制代码
```

字符串判空：

```
if emptyString.isEmpty {
    print("空字符串")
}
复制代码
```

**可变字符串：**将特定字符串赋值给变量或常量，来表示字符串是否可以被修改。 将特定字符串赋值给变量：在这种情况下可以对其进行修改。

```
var variableString = "Horse"
variableString += " and carriage"
print(variableString)
复制代码
```

将特定字符串赋值给常量：在这种情况下无法对其进行修改。

```
let constantString = "Highlander"
constantString += " and another Highlander"//!< 编译器报错：constantString是常量不可变
复制代码
```

这种方法与Objective-C和Cocoa中的字符串可变不同，您可以在两个类`NSString和NSMutableString`之间进行选择，区分可变字符串。

**字符串是值类型：** Swift的`String`类型是一种值类型。如果我们创建一个新的字符串`a`，在将`a`传递给函数或方法时，或将其赋值给常量或变量时，将复制字符串`a`的值。在以上每种情况下，都会创建现有字符串的新副本，并传递或分配新副本，而不是原始字符串。
Swift默认复制字符串的行为，确保了在函数或方法中传递字符串时，该字符串的值不会被改变，无论它来自何处，除非我们自己修改。
同时Swift的编译器对字符串的默认复制行为做了优化：只有在绝对必要的情况下才会进行实际的复制，保证了性能。

**字符使用**：我们可以通过使用`for-in`循环遍历字符串来访问字符串中各个字符。

```
let str = "Dog!"
for character in str {
    print(character)
}
复制代码
```

创建一个`Character` 类型的常量或变量

```
//创建常量
let character : Character = ""
print(character)
//创建变量
var character : Character = ""
character = ""
print(character)
复制代码
```

通过字符数组，生成一个字符串

```
let catCharacters : [Character] = ["c","a","t","i","s",""]
let catString = String(catCharacters)
print(catString)
复制代码
```

**连接字符串和字符：**
字符串可以使用加法运算符`+`连接到一起以创建新的字符串：

```
let string1 = "hello"
let string2 = " there"
let welcome = string1 + string2
print(welcome)
复制代码
```

使用加号赋值运算符`+=`：

```
var instruction = "look over"
let string2 = " there"
instruction += string2 //!< log:look over there
复制代码
```

使用`String`类型的`append()`方法将`Character`类型的值添加到`String`类型的变量。

```
var character : Character = ""
character = ""
var instruction = "look over"
let string2 = " there"
instruction += string2
instruction.append(character) //!< look over there
复制代码
```

使用多行字符串文字来构建更多行的字符串，则希望字符串中的每一行都以换行符结束，包括最后一行。

```
let badStart = """
one
two
"""
let end = """
three
"""
/*输出两行：badStart的最后一行不以换行符结束，所以该行与end的第一行结合
one
twothree
*/
print(badStart + end)

let goodStart = """
one
two

"""
/*输出三行：goodStart最后一行以换行符结束。
one
two
three
*/
print(goodStart + end)
复制代码
```

**字符串插值**：字符串插值是一种通过在字符串中混合常量，变量，文字和表达式并可以构造出新字符串的方法。
作用：将常量或变量的名称包含在较长字符串中作为占位符，并提示Swift将其替换为该常量或变量的当前值。使用形式：将名称括在括号中，并在左括号前用反斜杠转义它`\(变量或常量)`。单行和多行字符串都可以使用字符串插值。

```
let multiplier = 3
let message = "\(multiplier) times 2.5 is \(Double(multiplier) * 2.5)"
print(message)//!< 3 times 2.5 is 7.5
复制代码
```

上例中`\(multiplier)`和`\(Double(multiplier) * 2.5)`属于字符串插值。

```
print(#"Write an interpolated string in Swift using \(multiplier)."#)//!<Write an interpolated string in Swift using \(multiplier).
复制代码
```

上例中使用`扩展字符串分隔符`来创建包含特殊字符`\`的字符串，否则这些字符将被视为字符串插值。
若要在使用`扩展分隔符`的字符串中使用字符串插值，需将`\`后面的数字符号`#`的个数与字符串开头和结尾处`#`的个数相匹配。

```
print(#"Write an interpolated string in Swift using \#(multiplier)."#)//!<Write an interpolated string in Swift using 3.
复制代码
```

**Unicode：**又名：统一码、万国码、单一码。它是跨语言、跨平台进行文本转换、处理的国际标准。Swift中的字符串和字符类型完全符合Unicode。

1.  `Unicode标量`：Swift的原生`String`类型是根据Unicode标量构建的。Unicode标量：使用21个二进制位表示的字符或修饰符，（注解：目前Unicode的编码范围达到了21位，Unicode标量范围 0x0000 - 0x10ffff 的范围，二进制位为 1 0000 1111 1111 1111 1111，总共21位）例如：`U+0061`表示`a`,U+1F425表示`🐥`。需要注意的是，Unicode标量值并不需要把所有21个二进制位都分配给字符或修饰符 ，某些多出来的Unicode标量会保留下来，用于将来分配或用于UTF-16编码(注解：UTF-16是Unicode的其中一个使用方式，即把Unicode字符集的抽象码位映射为16位的序列，用于数据存储或传递)。

2.  扩展字形集群：Swift的`Character`类型的每个实例，代表一个扩展的字形集群。扩展字形集群是一个或多个可组合的Unicode标量（组合时，产生单个人类可读字符）的序列。字母`é`可以表示为单个Unicode标量`\u{00E9}`。字母`é`也可以表示为一对标量 ：标准字母`e`:`\u{0065}`和尖音符`\u{301}`组合的形式。（音调符标量以图形方式应用于其前面的标量，当它由具有Unicode感知的文本渲染系统渲染时将e转换为é）

在这两种情况下，字母`é`表示为单个Swift中的`Character`值，表示可扩展的字形簇。在第一种情况下，集群中的单个标量;在第二种情况下，它是两个标量的集群：

```
let eAcute: Character = "\u{E9}"                         // é
let combinedEAcute: Character = "\u{65}\u{301}" //é
print(String(eAcute)+String(combinedEAcute))
复制代码
```

可扩展的字形集群是一种将许多复杂脚本字符表示为单个字符值的灵活方式。

```
let precomposed: Character = "\u{D55C}"                  // 한
let decomposed: Character = "\u{1112}\u{1161}\u{11AB}"   // \u{1112}:ᄒ, \u{1161}:ᅡ,\u{11AB}: ᆫ ->한
print(String(precomposed)+String(decomposed))
复制代码
```

区域指示符号的Unicode标量可以成对组合以生成单个字符值，例如区域指示符符号U（U + 1F1FA）和区域指示符符号字母S（U + 1F1F8）的组合：

```
let regionalIndicatorForUS: Character = "\u{1F1FA}\u{1F1F8}"
print(String(regionalIndicatorForUS))//log:🇺🇸
复制代码
```

**字符计数：**检索字符串中字符的数目，可以使用字符串的count属性：

```
let title = "Koala 🐨, Snail 🐌, Penguin 🐧, Dromedary 🐪"
print("title中有\(title.count)个字符")//!< 40个字符
复制代码
```

需要注意的是：Swift中对字符串拼接扩展字形集群可能并不会影响字符串的字符数目。如：

```
var x = "thing" //!< x.count = 5
x += "\u{301}" //!< x:thinǵ
print(x) //!< x.count 依旧是5
复制代码
```

扩展的字形集群可以由多个Unicode标量组成。这意味着相同字符的不同表示可能需要不同的内存量来存储。因此，在Swift中，字符串的每个字符在内存中所占的大小可能不相同。需要注意的是如果字符串特别长，使用`count`属性获取字符串中字符数量时，是会遍历整个字符串中的Unicode标量的。`count`属性可能与包含相同字符的NSString的`length`属性返回的字符数量不相同。因为两者的计算基准不一样。NSString的长度基于字符串的`UTF-16`表示中的16位码元的数量，而不是基于字符串中Unicode可扩展的字形集群的数量。

```
//OC中计算的字符数。
NSString *str = @"Koala 🐨, Snail 🐌, Penguin 🐧, Dromedary 🐪";
NSLog(@"%ld",str.length);//!< 44个字符
复制代码
```

**访问和修改字符串：**通过相应方法和属性或使用下标语法来访问和修改字符串。 字符串索引：每个String值都有一个关联的索引类型`String.Index`，它对应于字符串中每个字符的位置。
如上所述，Swift中不同的字符可能需要不同的内存量来存储，因为Swift的字符串中字符数是基于`Unicode标量的`来计算的：a.集群中的单个标量，b.多个标量的可扩展集群。因此Swift字符串不能用整数值索引，为了确定某个特定的字符位于哪个位置，我们必须从该字符串的开头或结尾遍历每个`Unicode标量`。
使用`startIndex`属性可以访问字符串的第一个字符的位置。**`endIndex`属性是字符串最后一个字符之后的位置**。因此，`endIndex`属性不是字符串下标的有效参数。如果字符串为空，则`startIndex`和`endIndex`相等。可以使用字符串的索引`index(before: )`和`index(after:)`方法访问给定索引之前和之后的索引。要访问远离给定索引的索引，可以使用索引`index(_:, offsetBy: )`方法，而不是多次调用其中一种方法。字符串`title`根据字符索引获取字符：`title[String.Index(必须是索引类型)]`

```
let title = "Koala 🐨, Snail 🐌, Penguin 🐧, Dromedary 🐪"
let subStr = title[title.index(after: title.startIndex)]//!< startIndex之后的位置 输出o
let subStr1 = title[title.index(before: title.endIndex)]//!< 🐪

let subStr2 = title[title.index(title.endIndex, offsetBy: -1)] //!< log:🐪
let subStr3 = title[title.index(title.startIndex, offsetBy: 6)]//!< log: 🐨

let index = title.index(title.startIndex, offsetBy: 15)
let subStr4 = title[index] //!< log:🐌

复制代码
```

尝试访问字符串范围之外的索引或字符时将触发运行时错误。

```
//! 所得索引超越了字符串的有效范围，触发运行时错误：Thread 1: Fatal error: String index is out of bounds
let outsideIndex = title.index(after: title.endIndex)
//！索引超越了有效范围，触发运行时错误：Thread 1: Fatal error: String index is out of bounds
let subStr5 = title[title.endIndex]
复制代码
```

使用`indices`属性可以获取字符串中所有字符的索引。

```
let indices = title.indices;//!DefaultIndices<String>(_elements: "Koala , Snail , Penguin , Dromedary ", _startIndex: Swift.String.Index(_rawBits: 0), _endIndex: Swift.String.Index(_rawBits: 3407872))
var tempStr:String = ""
for index in indices {
    print("\(title[index])","",separator: "_", terminator: "", to: &tempStr)
}
////!< 最终合成的新字符串:K_o_a_l_a_ __,_ _S_n_a_i_l_ __,_ _P_e_n_g_u_i_n_ __,_ _D_r_o_m_e_d_a_r_y_ __
print("最终合成的新字符串:\(tempStr)")
复制代码
```

重点：我们可以在符合Collection协议的任何类型上使用`startIndex`和`endIndex`属性以及索引`index(before: )`和`index(after:)`和`index(_:, offsetBy: )`方法。这包括字符串以及集合类型，如Array，Dictionary和Set。 **字符串插入和删除：** `插入：`字符串指定索引处插入单个字符使用`insert(_:at:)`方法;在指定索引处插入另一个字符串使用`insert(contentsOf:at:)`方法。

```
var inserStr = "hello"
//! 插入单个字符：unicode标量
inserStr.insert("\u{1F1F7}", at: inserStr.startIndex)//!< log:🇷hello
//! 插入单个字符：普通字符
inserStr.insert("!", at: inserStr.endIndex)//!< log:🇷hello! 插入时可以使用endIndex
//!< 插入字符串：由字符：unicode标量组成的字符串
let scalarStr = "\u{1F1F6}\u{1F496}"//!< 🇶💖
inserStr.insert(contentsOf: scalarStr, at: inserStr.startIndex)//!< 🇶💖🇷hello!
//! 插入普通字符串：
let normalStr = "_word"
inserStr.insert(contentsOf: normalStr, at: inserStr.index(before: inserStr.endIndex))//!< 🇶💖🇷hello_word!
复制代码
```

`删除：`字符串删除指定索引处的单个字符使用`remove(at:)`方法;删除指定范围内的子字符串使用`removeSubrange(_:)`方法：

```
//复杂组成的字符串
var removeStr = "\u{1F1F6}\u{1E67F}\u{1F496}\u{1F1F7}hello_word!eye\u{301}"//!< log:🇶💖🇷hello_word!eyé
//移除unicode标量字符：💖
removeStr.remove(at: removeStr.index(removeStr.startIndex, offsetBy: 2))//!< log:🇶🇷hello_word!eyé
//移除普通字符：y 为啥-2因为endIndex属性表示字符串最后一个字符之后的位置
removeStr.remove(at: removeStr.index(removeStr.endIndex, offsetBy: -2))//!< log:🇶🇷hello_word!eé
//!< 删除子0-1范围内的字符串：由字符：unicode标量组成的子字符串：🇶
//*range
//    let range = removeStr.startIndex..<removeStr.index(removeStr.startIndex, offsetBy: 2)
//或
let range = removeStr.startIndex...removeStr.index(removeStr.startIndex, offsetBy: 1)
removeStr.removeSubrange(range) //!< 🇷hello_word!eé
复制代码
```

注意：`String`类型实现了`RangeReplaceableCollection` 协议，其他实现了`RangeReplaceableCollection` 协议的任何类型都可以使用`insert(_:at:)`，`insert(contentsOf:at:)`，`remove(at:)`和`removeSubrange(_:)`方法。如：Array，Dictionary和Set。
**子字符串：**
从字符串中获取子字符串时 - 例如，使用索引或类似`prefix(_:)`的方法 ，结果是`Substring`的实例，而不是另一个字符串。Swift中的子字符串与字符串具有多数相同的方法，这意味着我们可以像处理字符串一样使用子字符串。但是与字符串不同，我们在对字符串执行操作时只会使用子字符串很短的时间。当我们需要将子字符串存储更长时间时，则需要将子字符串转换为`String`实例。

```
var myString = "\u{1F1F6}\u{1E67F}\u{1F496}\u{1F1F7}hello_word!eye\u{301}"//!< log:𞙿hello_word!eyé
//从字符串中取出hello子字符串
//1.获取hello在字符中的范围
//Returns the last index where the specified value appears in the collection.
let subStart = myString.lastIndex(of:"🇷" ) ?? myString.startIndex //!< 字符🇷的位置
//Returns the first index where the specified value appears in the collection.
let subEnd = myString.firstIndex(of: "_") ?? myString.endIndex//!< 字符_的位置
//2.获取子字符串
let subString = myString[subStart..<subEnd]//!<log: 🇷hello
print(subString)
//3.若需要长时间使用子字符串则需要类型转换
let longSubStr = String(subString) //!< or:String.init(subString)
复制代码
```

**重点知识：**
字符串和子字符串之间的区别：与字符串一样，每个子字符串都有一个内存区域，用于存储构成子字符串的字符。但是作为性能优化，子字符串可以重用用于存储原始字符串的部分内存，或者用于存储另一个子字符串的内存的一部分。`字符串具有类似的优化，但如果两个字符串共享内存，则它们是相等的`此性能优化意味着在修改字符串或子字符串之前，不会增加复制内存的性能成本。如上所述，`子字符串不适合长期存储 因为它们重用原始字符串的存储，只要使用任何子字符串，整个原始字符串就必须保存在内存中`。
示例描述：myString是一个字符串，这意味着它有一个内存区域，用于存储构成字符串的字符。因为subString是myString的子字符串，所以它重用了myString使用的内存。相比之下，longSubStr是一个字符串 ，从子字符串创建时，它有自己的存储空间。![image.png](https://upload-images.jianshu.io/upload_images/19704571-8bd12ca82042e020.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


**字符串比较：**
字符串和字符是否相等的比较：使用“等于”运算符`==`和“不等于”运算符`!=`检查字符串和字符相等性。

```
let testStr1 = "i have a cat\u{E9}?"//!< i have a caté?
let testStr2 = "i have a cat\u{65}\u{301}?"//!< i have a caté?
if testStr1 == testStr2 {
    print("这两个字符串是相等的")
}
复制代码
```

如果两个字符串值（或两个字符值）的扩展字形集群在规范上等效，则它们被认为是相等的。如果扩展的字形集群具有相同的语言含义和外观，则它们在规范上是等效的，即使它们是不同`Unicode标量`组成的。
举个反例：英语中大写字母A:`\u{0041}`不等同于俄语中的A:`\u{0410}`。字符在视觉上相同，但却不具有相同的语言含义，因此也是不相等的。

```
let englishA = "\u{0041}"//!< A
let RussianA = "\u{0410}"//!< A
if englishA == RussianA {
    print("这两个字符串是相等的")
} else {
    print("这两个字符串是不相等的")//!< log:这两个字符串是不相等的
}
复制代码
```

字符串的前缀与后缀的比较：要检查字符串是否具有特定的字符串前缀或后缀，调用字符串的`hasPrefix（_ :)`和`hasSuffix（_ :)`方法，返回值都为布尔值。

```
let testStr1 = "i have a cat\u{E9}?"//!< i have a caté?
let testStr2 = "i have a cat\u{65}\u{301}?"//!< i have a caté?
let array = [testStr1,testStr2]
for item in array[...] {
    if item.hasPrefix("i") {
        print(item + "*")
    }
}
/*注意：hasPrefix（_ :)和hasSuffix（_ :)方法在每个字符串中的扩展字形集群之间执行逐个字符的规范等效比较。*/
for item in array[...] {
    if item.hasSuffix("\u{E9}?") {
        print(item + "*")//!<输出两次： i have a caté?*
    }
}
复制代码
```

注意：在每个字符串中调用`hasPrefix（_ :)`和`hasSuffix（_ :)`方法，会在字符串的扩展字形集群之间逐个字符进行规范的相等比较
**字符串的Unicode表示：**
将Unicode字符串写入文本文件或其他存储时，字符串中的`Unicode标量`将以多种Unicode定义的编码方式之一进行编码。每种编码方式都是以码元(二进制位)为单位对字符串进行编码。
Unicode定义的编码方式：1.`UTF-8`编码格式：将字符串编码为多个8个二进制位的码元。2.`UTF-16`编码格式：将字符串编码为多个16个二进制位的码元。3.`UTF-32`编码格式：将字符串编码为多个32个二进制位的码元。
Swift提供了几种访问字符串的Unicode的方法。
a. 使用`for-in`语句迭代字符串，将其各个字符值作为Unicode扩展字符集群进行访问。
b. 访问字符串的值依据兼容Unicode的三种编码方式之一。

*   UTF-8码元的集合，使用字符串的`utf8`属性访问
*   UTF-16码元的集合，使用字符串的`utf16`属性访问
*   21位的Unicode标量值的集合，相当于字符串的UTF-32编码格式，使用字符串的`unicodeScalars`属性访问。

**1.UTF-8表示：** 通过迭代字符串的`utf8`属性来访问字符串的UTF-8编码格式的表示形式。`utf8`属性的类型为`String.UTF8View`。
关于`String.UTF8View`结构体：将字符串内容作为UTF-8码元的集合进行展示。我们可以使用字符串`utf8`属性访问字符串的UTF-8码元表示形式。`String.UTF8View`将字符串的`Unicode标量值`编码为无符号的8位整数，故：`String.UTF8View`是无符号的8位整数`UInt8`值的集合 。字符串中`Unicode标量`值最长可达21位。要使用8位整数表示这些标量值，通常需要多个UTF-8代码单元。

```
let flowers = "Flowers 💐"
for v in flowers.utf8 {
    print(v,"",separator: " ", terminator: "")//替换换行符
}
//!< 控制台最终输出：70 108 111 119 101 114 115 32 240 159 146 144
/*一个💐的字符是unicode标量：\u{1F490}
flowermoji.unicodeScalars ：32位的0001F490 表示字符为\u{1F490} 打印值为：128144
*/
let flowermoji = "💐" 
let flowermojiUnicodeScalars = flowermoji.unicodeScalars //!< log:"\u{0001F490}" 这个是封包了
for v in flowermojiUnicodeScalars {
    print(v,v.value)//!< v.value = 128144  9*16 + 4*256 +15 * 256 *16 + 256 *256 = 128144
}
//将💐unicode标量：\u{128144}，转为UTF-8编码集合，会发现需要多个
var count = 0
var value = ""
for v in flowermoji.utf8 {
    count += 1
    value += "\(v) "
}
//!console.log：💐unicode标量转换成了4个utf8码元集合分别是：240 159 146 144
print("\u{1F490}unicode标量转换成了\(count)个utf8码元集合分别是：\(value)")
复制代码
```

比如`let dogString = "Dog‼🐶"`转换`UTF-8`集合`"68 111 103 226 128 188 240 159 144 182 "`![image.png](https://upload-images.jianshu.io/upload_images/19704571-87b605fe64e0ddec.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**2.UTF-16表示：**
通过迭代字符串的`utf16`属性来访问字符串的UTF-16编码格式的表示形式。`utf16`属性的类型为`String.UTF16View`，与`String.UTF8View`同理。区别：`String.UTF16View`是无符号的16位整数`UInt16`值的集合 。字符串中`Unicode标量`值最长可达21位。要使用16位整数表示这些标量值，可能需要两个UTF-16代码单元。

```
let dogString = "Dog‼🐶"
var count = 0
var value = ""
for v in dogString.utf16 {
    count += 1
    value += "\(v) "
}
//控制台输出： 🐶 unicode标量转换成了6个utf16码元集合分别是：68 111 103 8252 55357 56374
print("\u{1F436}unicode标量转换成了\(count)个utf16码元集合分别是：\(value)")// 🐶 :\u{1F436}
复制代码
```

![image.png](https://upload-images.jianshu.io/upload_images/19704571-a356ba84f5dfe2bb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



**3.Unicode Scalar 表示：**
通过迭代字符串的`unicodeScalars`属性来访问字符串的Unicode标量表示形式（集合）。`unicodeScalars` 属性的类型为`String.UnicodeScalarView`。每个`UnicodeScalar`都有一个value属性： Unicode.Scalar的实例对象，会使用无符号的32位整数`UInt32` ，返回标量的值。

```
for scalar in dogString.unicodeScalars {
    print("\(scalar.value) ", terminator: "")// log "68 111 103 8252 128054 "
}
复制代码
```

![image.png](https://upload-images.jianshu.io/upload_images/19704571-cc85b1d7e65d7e79.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


参考资料： [swift 5.1官方编程指南](https://docs.swift.org/swift-book)



收录于： [QiShare团队](https://www.jianshu.com/c/b3bd94559163)
