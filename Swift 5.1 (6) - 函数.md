### Functions：函数

函数是执行特定任务的独立代码块。为函数指定了一个标识其功能的名称，此名称可用于“调用”函数以在需要时执行其任务。Swift中的每个函数都有一个类型，由函数的参数类型和返回类型组成。可以像Swift中的任何其他类型一样使用此类型，这使得将函数作为参数传递给其他函数以及从函数返回函数变得很容易。函数也可以在其他函数中嵌套使用。

#### 定义和调用函数

*   定义函数：定义函数的名称+定义函数的参数+定义函数的返回值。
*   调用函数：使用其名称调用该函数，传递与函数参数类型匹配的值。

```
func greet(person: String) -> String {
    let greeting = "Hello, " + person + "!"
    return greeting
}
//上述方法也可以写为
func greetAgain(person: String) -> String {
    return "Hello again, " + person + "!"
}
print(greetAgain(person: "Anna")) //<! "Hello again, Anna!"
复制代码
```

#### 函数参数和返回值

**无参函数**

函数不要求必须定义输入参数。即使函数无参，在函数名称后仍需要括号。调用函数时，函数名后面还会有一对空括号。

```
func sayHelloWorld() -> String {
    return "hello, world"
}
print(sayHelloWorld())//<!  "hello, world"
复制代码
```

**有多个参数的函数**

```
func greet(person: String, alreadyGreeted: Bool) -> String {
    if alreadyGreeted {
        return greetAgain(person: person)
    } else {
        return greet(person: person)
    }
}
print(greet(person: "Tim", alreadyGreeted: true))//<! "Hello again, Tim!"
复制代码
```

**没有返回值的函数**

函数不要求必须定义返回值类型。

```
func greet(person: String) {
    print("Hello, \(person)!")
}
greet(person: "Dave") //<! "Hello, Dave!"
复制代码
```

没有定义返回类型的函数返回`Void`类型的特殊值。是一个空元组`()`。

**有多个返回值的函数**

使用元组类型作为函数的返回值类型，同时返回多个函数值。

```
//定义
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
//调用
let bounds = minMax(array: [8, -6, 2, 109, 3, 71])
print("min is \(bounds.min) and max is \(bounds.max)")//<! min is -6 and max is 109

复制代码
```

**返回值为可选的元组类型**

若函数返回的元组类型可能为空值时，则可以使用可选的元组返回类型。通过在元组类型的右括号后面放置一个`?`来编写一个可选的元组返回类型，例如`（Int，Int）？`或`（String，Int，Bool）？`

```
func minMax(array: [Int]) -> (min: Int, max: Int)? {
    if array.isEmpty { return nil }
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
复制代码
```

使用可选绑定来检查`minMax（array :)`函数是否返回`nil`

```
if let bounds = minMax(array: [8, -6, 2, 109, 3, 71]) {
    print("min is \(bounds.min) and max is \(bounds.max)")
}
复制代码
```

#### 函数的参数标签和参数名称

每个函数的参数都有参数标签和参数名称。调用函数时使用参数标签。参数名称用于函数的实现。默认情况下，函数的`参数名称`便是其`参数标签` **指定参数标签** 在参数名称前面编写参数标签，用空格分隔：

```
func someFunction(argumentLabel parameterName: Int) {
}
//调用
someFunction(argumentLabel: 6) // 参数名称 parameterName ： 6
//方式二，默认情况
func someFunction(parameterName: Int) {
}
someFunction(parameterName: 6)// 参数名称 parameterName ： 6
复制代码
```

**省略参数标签**

如果不想要参数的参数标签，请用下划线`_`替换明确的参数标签。

```
func someFunction(_ parameterName: Int) { 
}
//调用
someFunction(7)//参数忽略，parameterName：7
复制代码
```

**默认参数值**

通过在该参数的类型之后为参数赋值来为函数中的任何参数定义默认值。如果定义了默认值，则可以在调用函数时省略该参数。

```
func parameterContainDefaultValue(defaulValue1:Int,defaultValue2:Int=12) {
}
//调用，两者皆可以，
parameterContainDefaultValue(defaulValue1: 12, defaultValue2: 23)
//因为某个参数值定义了默认值，因而多出下面的方法。
parameterContainDefaultValue(defaulValue1: 12)
复制代码
```

**变量参数**

函数中使用可变参数，表示在函数调用时可以向该参数传递特定类型的不同数量的参数值。可变参数接受零或多个指定类型的值。 可变参数的表示：通过在参数的类型名称后插入`...`来表示可变参数。 传递给可变参数的值在函数体内可用作适当类型的数组。例如，一个`Double ...`类型的可变参数在函数体内可用作`[Double]`的常量数组。一个函数可能会有多个可变参数。

```
func arithmeticMean(_ numbers: Double...) -> Double {
    var total: Double = 0
    for number in numbers {//!< numbers 作为[Double]类型的数组存在
        total += number
    }
    return total / Double(numbers.count)
}
//调用
let average = arithmeticMean(1,2,3,4)
print("平均数\(average)")//!< 平均数2.5
复制代码
```

**输入输出参数`inout`**

默认情况下，函数参数是常量。如果尝试从该函数体内修改函数参数的值会导致编译时错误。 如果我们需要在函数体内修改参数的值，并且在函数调用结束后需要使用被修改过的参数的值。那么我们就需要定义该参数为输入输出参数。类似C与Object-C中的指针参数。 输入输出参数表示：通过将`inout`关键字放在参数类型之前来表示输入输出参数。 注意：`只能将变量作为输入输出参数的参数值进行传递，不能传递常量或文字值作为参数，因为不能修改常量和文字`。当我们将变量名称作为参数传递给输入输出参数时，可以在变量名称前面直接放置`＆`符号，以表示它可以由函数修改。

```
//根据内存地址交换两个整型数值
func changeTwoIntNumbers(_ a:inout Int,_ b:inout Int) {
    let temp = a
    a = b
    b = temp
}
//使用时需注意不能将类型为'Int'的不可变值作为inout参数传递，否则会报错
var a = 6
var b = 7
changeTwoIntNumbers(&a, &b)
print("b:\(b),a:\(a)")//!< b:6,a:7
复制代码
```

### 函数类型

每个函数都有一个特定的函数类型，由函数的参数类型和返回类型组成。函数类型不能带有参数标签。

```
func addTwoInts(_ a: Int, _ b: Int) -> Int {
    return a + b
}
func printHelloWorld() {
    print("hello, world")
}
复制代码
```

上述示例中的函数类型分别为：`(Int, Int) -> Int`和`() -> Void`。

**使用函数类型**

我们可以像使用Swift中的任何其他类型一样使用函数类型。可以将常量或变量定义为函数类型，并为该变量分配适当的函数。

```
var mathFunction:(Int,Int)->Int = addTwoInts
let addValue = mathFunction(a,b)
mathFunction = subTwoInts(_:_:)
let subValue = mathFunction(a,b)
print(subValue)//!< 1
print(addValue)//!< 13
//定义的函数
func addTwoInts(_ a: Int, _ b: Int) -> Int {
    return a + b
}
func subTwoInts(_ a:Int,_  b:Int)-> Int {
    return a - b
}
复制代码
```

**函数类型作为参数类型**

使用函数类型如`（Int，Int）- > Int`作为另一个函数的参数类型。

```
//定义
func mathResultFunction(_ mathCalculate:(Int,Int)->Int,_ a:Int, _ b:Int){
    print("函数计算的结果为：\(mathCalculate(a,b))")
}
//调用
var mathFunction:(Int,Int)->Int = addTwoInts
let addValue = mathFunction(a,b)
mathFunction = subTwoInts(_:_:)
let subValue = mathFunction(a,b)
mathResultFunction(mathFunction, a, b)//!< 函数计算的结果为：1
mathResultFunction(addTwoInts(a:_:), a, b)//!< 函数计算的结果为：13
复制代码
```

**函数类型作为返回类型**

使用函数类型作为另一个函数的返回类型。

```
//以下两个函数尽管具有不同的功能，但是都具有相同的函数类型，
func stepForward(_ input: Int) -> Int {
    return input + 1
}
func stepBackward(_ input: Int) -> Int {
    return input - 1
}
//定义返回值类型为函数类型的函数
func chooseStepFunction(backward: Bool) -> (Int) -> Int {
    return backward ? stepBackward : stepForward
}
//简单使用一下
var currentValue = 3
//! tempChooseStepFunction:stepBackward
let tempChooseStepFunction = chooseStepFunction(backward: currentValue > 0)
while currentValue > 0 {
    currentValue = tempChooseStepFunction(currentValue)
    print(currentValue)
}//!< 2 1 0
复制代码
```

#### 嵌套函数

```
func chooseStepFunction(backward: Bool) -> (Int) -> Int {
    func stepBackward(_ input: Int) -> Int {
        return input - 1
    }
    func stepForward(input: Int) -> Int {
        return input + 1
    }
    return backward ? stepBackward : stepForward
}
复制代码
```

参考资料： [swift 5.1官方编程指南](https://docs.swift.org/swift-book)



收录于： [QiShare团队](https://www.jianshu.com/c/b3bd94559163)
