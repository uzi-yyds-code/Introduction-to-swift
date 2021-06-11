

* * *

**常量和变量**：常量的值一旦设置就不能更改，而变量可以在将来设置为不同的值。常量和变量必须在使用之前声明。常量声明使用`let`关键字。变量声明使用`var`关键字。

```
let num1 = 10 //!< 声明一个常量num1，并且赋初始值10
var num2 = 5  //!< 声明一个变量num2，并且赋初始值5
let a = 1, b = 3, c = 4 //!< 同时声明多个常量并赋初值
var aa = 1, bb = 3, cc = 4 //!< 同时声明多个变量并赋初值
复制代码
```

**类型注释**：声明常量或变量时，可以提供类型注释，以清楚常量或变量可以存储的值的类型。通过在常量或变量名称后面放置冒号，后跟空格，后跟要使用的类型的名称来编写类型注释。

```
let num3 : Int = 3 //!<声明一个常量num1，可以存储的值得类型是Int类型，并且赋初始值3
var str : String = "QS" //!< 声明一个变量str，可以存储的值得类型是String类型，并且赋初始值"QS"
let a : Int = 1, b : [Int] = [3,4,5], c : String = "constant" //!< < 同时声明，多个可以存储不同类型值的常量，并赋相应类型初值
var aa : Int = 1, bb : [Int] = [3,4,5], cc : String = "change" //!< < 同时声明，多个可以存储不同类型值的变量，并赋相应类型初值
复制代码
```

**命名规则**：常量和变量名称几乎可以包含任何字符，包括Unicode字符。但是常量和变量名称不能包含空格字符，数学符号，箭头，专用Unicode标量值或行和框绘制字符。也不能以数字开头，但可以包含在名称的其他地方。使用Swift关键字作为变量名称时，需要使用``包裹。如下例所示：

```
let π = 3.14159
let 你好 = "你好世界"
let 🐶🐮 = "dogcow"
let s2r = "s2r"
let `default` = "default"//!< 使用Swift关键字作为变量名称时，需要使用``包裹
复制代码
```

一旦声明了某个类型的常量或变量，就不能再使用相同的名称声明它，或者将其更改为存储不同类型的值。也不能将常量变为变量或变量变为常量。
**打印方法**：
`print(_:separator:terminator:)`它可以将一个或多个值输出到控制台。separator和terminator参数都有默认值分别是`" "`和`\n`，使用时可以忽略。

```
let word = "张翼德"
print(word)//!< 控制台输出:张翼德
let p1 = "HOW"
let p2 = "ARE"
let p3 = "YOU?"
print(p1,p2,p3,separator: "...")//!< 控制台输出:HOW...ARE...YOU?
print(p1,p2,p3,separator: ".",terminator: "FINE THANKS\n")//!<控制台输出:HOW.ARE.YOU?FINE THANKS
复制代码
```

`print(_ separator:terminator:to:)`它可以将一个或多个值输出到合适的输出。separator和terminator参数都有默认值分别是`" "`和`\n`，使用时可以忽略。

```
let p1 = "HOW"
let p2 = "ARE"
let p3 = "YOU?"
var  outputStream = ""
print(p1,p2,p3,separator: ".",terminator: "FINE THANKS\n",to:&outputStream)
print("打印的数据，写入了outputStream变量中最终输出为:\(outputStream)")//!< 控制台输出:打印的数据，写入了outputStream变量中最终输出为:HOW.ARE.YOU?FINE THANKS
复制代码
```

Swift使用字符串插值将常量或变量的名称包含在较长字符串中作为占位符，并提示Swift将其替换为该常量或变量的当前值。将名称括在括号中，并在左括号前用反斜杠转义它：

```
let word = "张翼德"
print("我乃燕人\(word)也!谁敢与我决一死战?")
复制代码
```

**代码注释**：单行注释以两个正斜杠开头`//`。多行注释以正斜杠开头后跟星号`/*`，以星号后跟正斜杠`*/`结束。Swift中的多行注释可以嵌套在其他多行注释中。

```
/* This is the start of the first multiline comment.
 /* This is the second, nested multiline comment. */
This is the end of the first multiline comment. */
复制代码
```

**分号**：Swift不要求代码中的每个语句之后都需要加分号`;`我们可以写也可以不写。如果一行代码中有多个语句，则必须要加分号`;`

**整型：**没有小数部分，整数有符号（正，零或负）或无符号（正或零）。Swift提供8，16，32和64位格式的有符号和无符号整数。这些整数遵循类似于C的命名约定，因为8位无符号整数属于类型UInt8，32位有符号整数属于类型Int32。

**整数边界：**

1.  不同位数格式的有符号和无符号整数，都会有最大值和最小值。

```
//无符号
let unsignedMinValue = UInt8.min  // UInt8类型最小值 0
let unsignedMaxValue = UInt8.max  // UInt8类型最大值 255
//有符号
let minValue = Int8.min  // Int8类型最小值 -128
let maxValue = Int8.max  // Int8类型最大值 127
复制代码
```

2.  Swift提供了一个额外的整数类型Int，它与当前平台机器的字节位数相同。即：大多数情况下，我们不需要选择该使用哪种大小的整数类型。除非我们需要使用特定大小的整数。每种整数类型存储不同的值范围，编译代码时，会检查是否在指定的整数类型范围内。在不同整数类型的数值间运算时，需要根据实际情况进行转换。
    *   在32位平台上，Int与Int32大小相同。
    *   在64位平台上，Int与Int64大小相同。
    *   在32位平台上，UInt与UInt32大小相同。
    *   在64位平台上，UInt与UInt64大小相同。

```
let cannotBeNegative: UInt8 = -1 //报错代码：无符号的8位整数类型不能表示有符号的-1
let tooBig: Int8 = Int8.max + 1 //报错代码:Int8表示范围0-255 不能表示256报错
复制代码
```

```
let twoThousand: UInt16 = 2000
let one: UInt8 = 1
let twoThousandAndOne = twoThousand + UInt16(one)
复制代码
```

**浮点数字：** 浮点数是具有小数部分的数字，浮点类型可以表示比整数类型更宽范围的值。例如3.14159，0.1，和-273.15。Swift提供了两种带符号的浮点数类型：Double 表示64位浮点数。 Float 表示32位浮点数。 整数与浮点数之间的转换： 整数转浮点数

```
let three = 3 //需要类型转换，使用常量three创建一个double类型的新值：Double(three)，否则这种相加操作不被允许会报错
let pointOneFourOneFiveNine = 0.14159
let pi = Double(three) + pointOneFourOneFiveNine
复制代码
```

浮点数转整数

```
let pi = 3.14159
let integerPi = Int(pi)//采用这种形式则浮点数总是被截断，这意味着4.76->4 ，3.9->3
复制代码
```

**类型安全和类型判断：**
Swift是一种类型安全的语言，编译代码时执行类型检查，并将任何不匹配的类型标记为错误，让我们在开发过程中尽早捕获并修复错误。比如：定义的变量或常量是`String`类型的，那么我们就不能使用`Int`类型赋值。所以Swift鼓励我们在使用变量或常量时，能够清楚的知道所需的值的类型。但并不意味着我们必须指定声明的变量或常量的类型。如果未指定所需的值类型，Swift将使用类型推断来匹配适当的类型。类型推断使编译器能够在编译代码时自动推断出特定表达式的类型，只需检查我们提供的值即可。类型推断有助于使Swift代码在使用其类型已知的其他值初始化常量或变量时简洁性和可读性更高。
使用初始值声明常量或变量时，类型推断特别有用。推断浮点数的类型时，Swift总是选择`Double`（而不是`Float`）。如`let π = 3.14159`，π 将会推断为`Double`类型。`let π = 3 + 0.14159`，`Double`类型作为加法的一部分，所以也会推断为`Double`类型 **数值（浮点，整数）类型表达式：**

> 一个十进制数(decimal)，无前缀 一个二进制数(binary)，有0b前缀

一个八进制数(octal)，有0o前缀 一个十六进制数(hexadecimal)，有0x前缀

一个整数17，使用不同进制数进行表示

```
let decimalInteger = 17
let binaryInteger = 0b10001       // 二进制数表示17
let octalInteger = 0o21           // 八进制数表示17 
let hexadecimalInteger = 0x11     // 16进制数表示17
复制代码
```

浮点数可以是没有前缀的十进制数，或者带有`0x`前缀的十六进制数，不管是无前缀的十进制数还是有前缀的十六进制数它们必须始终在小数点的两边都有一个数字。（基于此我们可能会用到表达式去实现）十进制数有一个可选的指数，可以使用大写或小写的e来表示，即：`en = 10ⁿ`，十六进制数也必须会有一个可选的指数，可以使用大写或小写的p来表示，即：`pn = 2ⁿ`.
浮点数十进制数表示：

> 1.25e2表示1.25 * 10^2，或125.0。

1.25e-2表示1.25 * 10^ -2，或0.0125。

浮点数十六进制数表示：

> 0xFp2指15 * 2^2，或60.0。

0xFp-2表示15 * 2^-2，或3.75。

一个浮点数12.1875，可以使用如下表达式：

```
let decimalDouble = 12.1875
let exponentDouble = 1.21875e1
let hexadecimalDouble = 0xC.3p0
复制代码
```

数字文字可以包含额外的格式以使其更易于阅读。整数和浮点数都可以用额外的零填充，并且可以包含下划线以帮助提高可读性。这两种格式都不会影响文字的基础值：

```
let paddedDouble = 000123.456
let oneMillion = 1_000_000
let justOverOneMillion = 1_000_000.000_000_1
复制代码
```

**定义别名：**使用关键字：`typealias`为现有类型定义别名。

```
typealias MyString = String
var my :MyString?
my = "我"
print(my!)
复制代码
```

**布尔**：Swift有一个基本的布尔类型，叫做`Bool`。Swift只提供了两个布尔常量值：`true`和`false`。

**元组：** 元组中的值可以是任何类型，并且不必彼此具有相同的类型。我们可以创建任意数量，任何类型，任意顺序的组合，作为一个元组。元组作为函数的返回值特别有用。

```
let someGrop =  ("元组",401,"未授权",[1,3],true,["name" : "张三"])
print(someGrop)
复制代码
```

分解元组中的常量或者变量单独去使用。

```
let  httpError = (401,"未授权")//!< httpError可以被描述为(Int,String)类型的元组
let (code,error) = httpError
print(code,error)//code:401   error 未授权
复制代码
```

元组中包含许多项不同类型的常量或者变量，我们需要有针对性的分解出某一个元素。

```
let someGrop =  ("元组",401,"未授权",[1,3],true,["name" : "张三"])
let (name,_,_,_,_,_) = someGrop
print(name)
复制代码
```

使用从零开始的索引访问元组中的各个元素值

```
let someGrop =  ("元组",401,"未授权",[1,3],true,["name" : "张三"])
let name = someGrop.0
let num =  someGrop.1
let des = someGrop.2
let array = someGrop.3
print(name,num,des,array)
复制代码
```

定义元组时可以命名元组中各个元素。

```
let httpError = (code:401,error:"未授权")
//元素单独使用
print(httpError.code,httpError.error)
复制代码
```

定义元组时不赋初值

```
let httpSubError : (Int,String)?
httpSubError = (401,"未授权")
print(httpSubError!)
//也可以
let httpSubError : (code:Int,error:String)?
httpSubError = (401,"未授权")
print(httpSubError!.code)
复制代码
```

**可选项(Optionals)：**
当某个类型变量的值可能为空的场景，我们需要使用Optionals（可选项）。一个可选代表两种可能：有值并且你可以解开可选项（optional）的包获取到这个值，否则没有值。

> 选项的概念在C或Objective-C中不存在。Objective-C中最接近的是一个具备返回值的方法在缺少有效对象的情况下可以返回nil，否则返回此对象。但是这种场景只适用于对象 ，而对于结构体，基本C类型或枚举值这些类型，Objective-C的方法是返回特殊值（例如NSNotFound）来表示这些类型不存在的情况。Swift的选项可以让我们表示任何类型都没有值的情况，而不需要特殊的常量。

对于非可选类型的常量或变量我们不能使用nil，如果我们的代码需要在变量或常量缺少值的情况下正常运行，那么我们就应该始终声明变量或变量为相应类型的可选值 在不提供默认值的情况下定义可选变量`var str: String?`系统将会自动为变量设置`nil`，Swift中的nil与Objective-C不同。在Objective-C中，`nil`是一个指向不存在的对象的指针。在Swift中，`nil`不是指针，而是一个确定的类型的变量或常量的一个缺省值。任何类型的可选值都能设置`nil`，不仅仅只是对象类型
**if语句和强制解包：**
使用if语句通过“等于”运算符（`==`）或“不等于”运算符（`!=`）比较可选项,来确定可选项是否包含值`nil`。

```
let possibleNumber = "123"
let convertedNumber : Int? = Int(possibleNumber)
if convertedNumber != nil {
//! 当我们确定了convertedNumber的值不可能为nil便可以使用！进行强制解包获取可选包中的值
print(convertedNumber!)
复制代码
```

强制解包可选的值:一旦确定可选项确实包含值，就可以通过在可选项名称的末尾添加感叹号`!`来访问其基础值。

**可选绑定：** 使用`可选绑定`来确定可选项是否包含值，如果包含值，则这个值可用于临时常量或变量的值。`可选绑定`可与if和while语句一起使用，以检查可选内部的值，并将该值提取为常量或变量，作为单个操作的一部分。 可选绑定，if语句示例

```
let possibleNumber = "1234"
let convertedNumber : Int? = Int(possibleNumber)
if let tempValue = convertedNumber {
    print(tempValue);
} else {
    print("没有值")
}
if var tempVar = convertedNumber {
     tempVar = tempVar + 1
     print(tempVar);
} else {
     print("没有值")
}
复制代码
```

代码解读：如果Int类型的可选项convertedNumber ，通过Int(possibleNumber)返回了一个值，则使用此值设置一个新的常量tempValue。条件成立时，tempValue是被一个没有可选包的确定的值初始化的，因此没有必要使用`!`后缀来访问它的值。
单个if语句中可以包含尽可能多的`可选绑定`和`布尔条件`，并以逗号分隔。如果`可选绑定`中的任何值是nil，或任何布尔条件求值为false，则整个语句的条件是false。示例：

```
if let firstNumber = Int("4"), let secondNumber = Int("42"), firstNumber < secondNumber && secondNumber < 100 {
    print("\(firstNumber) < \(secondNumber) < 100")
} else {
    print("不成立")
}
//等效的表达形式
if let firstNumber = Int("4") {
    if let secondNumber = Int("42") {
        if firstNumber < secondNumber && secondNumber < 100 {
            print("\(firstNumber) < \(secondNumber) < 100")
        }
    }
}
复制代码
```

**隐式解包(未包装)的可选项**：
可选项：允许我们的常量或变量不存在，使用时，可以使用if 语句检查是否`nil`或者使用`可选绑定`进行解包，以保证可选项在有值得情况下正确的访问值。
隐式解包(未包装)的可选项：我们从程序的结构可以得出，在我们首次设置可选项的值以后，这个可选项将总是会有值，每次调用都不可能是`nil`。基于此我们可能会想，那么我们就没必要每次访问值时，都检查和解包可选的值。那么上述场景中可选项，便可以被定义为隐式解包(未包装)的可选项。 可选类型的定义是类型后加`?`：(String?)，而隐式解包的可选项是在类型后加`!`：(String!)
隐式解包的可选项幕后其实是一个正常的可选项，但是我们可以像非可选值那样去使用，而不用每次访问都要先对可选项的值解包。
当使用一个字符串类型的可选项和一个隐式解包的字符串类型的可选项去访问它们字符串类型可选包（wrapped）中的确定值会有差异。
1.定义了字符串类型的可选项，并赋初值。在使用时需要针对可选的字符串，进行强制解包，以获取其中的确定值。需要加`！`。

```
 //! 1.定义了字符串类型的可选项，并赋初值。
let possibleString: String? = "An optional string."
let forcedString: String = possibleString! // 使用时需要针对可选的字符串，进行强制解包，以获取其中的确定值。
复制代码
```

2.定义了隐式解包的字符串类型的可选项，并赋初始值。使用时，不在需要针对隐式解包的字符串类型的可选项，进行解包。不再需要!

```
 //! 2.定义了隐式解包的字符串类型的可选项，并赋初始值。
let assumedString: String! = "An implicitly unwrapped optional string."
let implicitString: String = assumedString // 使用时，不在需要针对隐式解包的字符串类型的可选项，进行解包 即：不再需要!
复制代码
```

3.如果隐式解包的可选项是`nil`并且尝试访问其包装值，则会触发运行时错误。结果与在不包含值的普通可选项之后放置感叹号完全相同。同时也可以将隐式解包的可选项视为普通可选项，以检查它是否包含值：`if`或`可选绑定`。

```
let assumedString: String! = nil
let implicitString: String = assumedString
print(implicitString)//!< 崩溃：隐式解包一个可选项的值时发现了nil。Fatal error: Unexpectedly found nil while implicitly unwrapping an Optional value
复制代码
```

**错误处理：** 响应程序在执行期间可能遇到的错误情况。 定义可以抛出错误的函数

```
func canThrowAnError() throws {
    // this function may or may not throw an error
}
复制代码
```

函数声明时在参数与返回值之间使用关键字`throws` ，代表这个函数可能抛出错误。在调用这个可能抛出错误函数时需要在表达式前放置`try`关键字。
当使用catch分句处理错误时，Swift会自动把函数抛出的错误，自动传播出当前的函数作用域。

```
do {
    try canThrowAnError()
    // no error was thrown
} catch {
    // an error was thrown
}
复制代码
```

以下是如何使用错误处理来响应不同错误条件的示例：
1.定义错误
`Error`类型：表示一个能够被抛出（thrown）的错误。声明的任何类型只要遵守了 `Error`的协议都能够在Swift的错误处理系统中表示一个错误。因为`Error`协议没有要求自身必须实现，我们可以在创建的任何自定义类型中声明遵守这个协议即可。

```
public protocol Error {
}
extension Error {
}
extension Error where Self : RawRepresentable, Self.RawValue : FixedWidthInteger {
}
复制代码
```

`Error`枚举：Swift的枚举很适合表示简单的错误。我们可以创建一个遵守`Error` 协议的枚举类型，并在枚举中定义每一种可能的错误事例。

```
enum HttpError: Error {
    case authError
    case netWorkError
    case serviceError
}
复制代码
```

2.定义方法

```
func requestWebData(status: String) throws -> Void {

    let status = status
    if status == "401" {
        throw HttpError.authError
    } else if status == "500" {
        throw HttpError.serviceError
    } else if status == "404"{
        throw HttpError.netWorkError
    } else {
        print("一切正常");
    }

}
func noThrowErrorCanDoSomeThing () {
    print("没有错误抛出，可以做我们要做的事情")
}

func handleServiceError() {
    print("服务器错误，需要重新连接")
}
func handleAuthError () throws {
    print("授权失败了，选择重新登录")
    //! 网络请求
    do {
        try requestWebData(status: "404")
    } catch let error as HttpError  {
        throw error
    }
}
func handleNetWorkError(){
    print("网络错误了，检查网络")
}
复制代码
```

3.使用`do try catch`方法调用并处理异常。

```
do {
    try requestWebData(status:"400")
    //没有出现错误，做事情
    noThrowErrorCanDoSomeThing()
} catch HttpError.authError {

    do {
        try handleAuthError()
    } catch HttpError.netWorkError {
        print("授权登录时出现网络错误")
    } catch {
        print("授权登录时出现其他错误")
    }

} catch HttpError.netWorkError {
    handleNetWorkError()
} catch HttpError.serviceError {
    handleServiceError()
} catch {
    print("其他错误")//!< 这个catch就是在补全错误的处理，否则编译器指示错误
}
复制代码
```

**断言和前置条件：**
在执行任何进一步的代码之前，使用它们来确保代码满足基本条件。如果断言或前置条件中的布尔条件求值为true，则代码执行将照常继续。如果条件评估为false，则程序的当前状态无效，代码执行结束，程序终止。 断言：只有`debug`环境下才可以生效。 1.代码未进行条件检查

```
let num = -1        
assert(num > 0, "num不能为负数")
复制代码
```

2.代码进行了条件检查

```
let num = -1
if num > 10 {
} else if num >= 0 {
} else {
    assertionFailure("num不能为负数")//!< 陈述条件的信息
}
复制代码
```

前置条件:在`release`环境下也可以生效。

```
let num = -1
precondition(num > 0, "num不能为负数")
复制代码
```

注意：

*   如果代码中存储不会更改的值，需要始终使用`let`关键字将其声明为常量。存储需要更改的值需要始终使用`var`关键字将其声明为变量。
*   如果我们为定义的常量或变量提供了初始值，则不需要编写类型注释，Swift可以进行类型推断得出该常量或变量的类型 。若只是声明并未赋初值，如`var str1 : String`则需要提供类型注释
*   常量或变量命名使用与Swift关键字相同的名称时，需要使用``包裹该关键字名称。尽量避免使用关键字作为名称。
*   除非我们需要与平台机器的位数一致的无符号整型时使用`UInt`。其他情况`Int`则优选，即使已知要存储的值是非负的。`Int`对整数值的一致使用有助于代码互操作性，避免在不同数字类型之间进行转换，有利于整数类型推断。
*   `Double`至少可以精确到小数点后15位，`Float`的精度可以少至6位小数。任何一种类型适当的情况下，`Double`是首选。代码中也可以根据使用的值的性质和范围选择适当浮点类型。
*   元组对于简单的不同类型值的组合很有用。它们不适合创建复杂的数据结构。如果我们的数据结构可能更复杂，应当使用构建为类或结构，而不是元组。
*   尝试使用`!`访问不存在的可选值会触发运行时错误。在使用`!`强制解包可选变量或常量的值之前，请务必确保可选项包含的值非`nil`。
*   在if语句中使用`可选绑定`创建的常量和变量仅在if语句的主体中可用。相反，使用guard语句创建的常量和变量在主体语句后面的代码行中仍然可用。

```
let possibleNumber = "1234"
let convertedNumber : Int? = Int(possibleNumber)
guard let tempValue = convertedNumber else {
   print("没有值")
   //只是跳出方法体
   return
}
print("guard\(tempValue)")
复制代码
```

*   当变量在后面使用时可能变为nil，不要使用隐式解包的可选项。如果需要在变量的生命周期内检查值是否为`nil`，请始终使用普通的可选类型。

```
var assumedString: String! = "俺是张飞"
assumedString = nil;
let implicitString: String = assumedString //< 崩溃：隐式解包一个可选项的值时发现了nil。Fatal error: Unexpectedly found nil while implicitly unwrapping an Optional value
复制代码
```

*   使用throws关键字表明这个方法会抛出异常，所以需要try catch 语句进行错误处理，否则方法直接调用不会被允许，会报错。同时对于错误的处理（catch）必须是全面的（穷尽所有可能出现的错误），否则此处的错误不会被执行，编译器会指示错误。

参考资料： [swift 5.1官方编程指南](https://docs.swift.org/swift-book)

收录原文： [QiShare团队](https://www.jianshu.com/c/b3bd94559163)
