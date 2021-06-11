### Closures：闭包

闭包是独立的函数块，可以在代码中传递和使用。Swift中的闭包类似于C和Objective-C中的`block`以及其他编程语言中的`lambdas(匿名函数)`。闭包可以捕获和存储上下文中定义的任何常量和变量的引用。 全局函数和嵌套函数实际上是闭包的特例。闭包采用以下三种形式之一：

*   全局函数是具有名称但不捕获任何值的闭包。
*   嵌套函数是具有名称并且可以从其封闭函数中捕获值的闭包。
*   Closure表达式是一种未命名的可以从周围的上下文中捕获值的闭包，用轻量级语法编写。

Swift的闭包表达式鼓励简洁，因此闭包具备：

*   从上下文中推断参数和返回值类型
*   单表达式闭包的隐式返回
*   简洁的参数名称
*   尾随闭包语法

#### 闭包表达式

嵌套函数可以将独立的函数命名和定义为更大函数的一部分。Closure表达式优化了其中函数的构造，而不用对于函数进行完整声明和命名。Closure表达式是一种以简短，集中的语法编写内联闭包的方法。下面将通过`sort（by :)`方法来阐述Closure表达式所做出的优化。

**排序方法**

`sorted（by :)`方法，可以根据我们提供的排序闭包对已知类型的数组进行排序。该`sorted(by:)`方法返回一个与旧数组相同类型和大小的新数组，新数组按正确的顺序排列。`sorted（by :)`方法接受一个闭包，该闭包接受与数组中元素相同类型的两个参数，并返回一个`Bool`值，若返回是`true`说明第一个值是出现在第二个值之前。若返回是`false`说明第一个值是出现在第二个值之后。

```
//排序数组
let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
//定义递减的排序函数
func backward(_ s1: String, _ s2: String) -> Bool {
    return s1 > s2//表示从大到小 递减的顺序
}
let newArray = names.sorted(by: backward)
print(newArray)//!< ["Ewa", "Daniella", "Chris", "Barry", "Alex"]
复制代码
```

**闭包表达式语法**

闭包表达式语法具有以下一般形式：

```
{ (<#parameters#>) -> <#returnType#> in
    <#statements#> 
}
复制代码
```

闭包表达式语法中的参数可以是输入输出参数，但不能具有默认值。可以使用变量(variadic)参数。元组也可以用作参数类型和返回类型。 上述示例使用闭包表达式语法内联编写排序闭包:

```
//排序数组
let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
let newArray = names.sorted(by: {(s1:String,s2:String)->Bool in
    return s1 > s2
})
print(newArray)//!< ["Ewa", "Daniella", "Chris", "Barry", "Alex"]
复制代码
```

对于内联闭包表达式，参数和返回类型写在花括号内，而不是在花括号外。闭包的方法体的开头由`in`关键字引入。这个关键字表示闭包的参数和返回类型的定义已经完成，闭包的方法体即将开始。

**从上下文中推断类型**

因为排序闭包(函数类型)作为参数传递给方法，所以Swift可以推断出它的参数类型以及它返回的值的类型。同时`sort（by :)`方法是在字符串数组上调用的，因此排序闭包是`（String，String） - > Bool`的函数类型。因为可以推断出所有类型，所以排序的闭包表达式`（String，String）`和`Bool`类型的返回值也可以不用出现，这意味着可以省略 `- >`，返回值类型和参数名称周围的括号：

```
let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
let newArray = names.sorted(by: {s1,s2 in return s1 > s2})
//也可以这样写
names.sorted { (s1, s2) -> Bool in
    return s1 > s2
}
print(newArray)//!< ["Ewa", "Daniella", "Chris", "Barry", "Alex"]
print(names)//!< ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
复制代码
```

在将闭包作为内联闭包表达式传递给函数或方法时，始终可以推断出参数类型和返回类型。因此，当闭包用作函数或方法参数时，永远不需要以最完整的形式编写内联闭包 **单表达式闭包的隐式返回** 单表达式(s1>s2)闭包可以通过从闭包的声明中省略`return`关键字来隐式返回单个表达式的结果，故上述示例也可写为：

```
let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
let newArray = names.sorted(by: {s1,s2 in s1 > s2})
复制代码
```

示例说明：`sorted（by :)`方法的函数类型的参数，清楚地表明了闭包必须返回一个`Bool`值。因为闭包的方法体中包含了一个返回`Bool`值的表达式`s1> s2`，所以没有歧义，并且可以省略`return`关键字。

**简写参数名称**

简写参数名称，可通过名称`$ 0`，`$ 1`，`$ 2`等引用闭包参数的值。如果在闭包表达式中使用这些简写参数名称，则可以从闭包表达式中省略闭包的参数列表，并将通过函数类型推断简写的参数名称的数量和类型。`in`关键字也可以省略。

```
let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
let newArray = names.sorted(by: {$0 > $1})
复制代码
```

**操作符方法** 上面的闭包表达式实际上有一种更简短的方式来编写。Swift的`String`类型将其大于运算符`>`的实现，定义为具有两个`String`类型参数的方法，并返回`Bool`类型的值。这与`sorted（by :)`方法所需的方法类型完全匹配。因此，可以简单地传入运算符`>`。

```
let newArray = names.sorted(by: >)
复制代码
```

#### 尾随闭包

如果需要将闭包表达式作为函数的最终参数传递给函数，并且闭包表达式很长，则可以将其写为尾随闭包。写法：尾随闭包写在函数调用的圆括号之后，即使它是函数的最终参数。如果尾随闭包作为函数的最终参数，并且定义了相应的参数标签，在使用尾随闭包语法时，不能将闭包的参数标签写为函数调用的一部分。

```
//定义一个闭包表达式为函数最终参数的函数
func trailingClosures(parameter:String,block:(_:String)->Void) -> Void {
    block(parameter + " 期待下：trailingClosures")
}
//可以有非尾随闭包的调用形式
func blockFunction(_ paramter:String)->Void {
    print(paramter)
}
trailingClosures(parameter: "不是尾随闭包写法1", block: blockFunction)
trailingClosures(parameter: "不是尾随闭包写法2", block: {(parameter:String)->Void in print(parameter)})
trailingClosures(parameter: "不是尾随闭包写法3", block: {(parameter)in print(parameter)})//!< 参数类型和返回值可以根据函数类型得知，故可以省略
//尾随闭包写法的调用形式，block函数标签不能出现在圆括号内
trailingClosures(parameter: "尾随闭包的写法") { (parameter) in
 print(parameter)
}
复制代码
```

`sorted（by :)`的尾随闭包的写法。

```
let newArray = names.sorted(){s1,s2 in s1 > s2}
let newArray = names.sorted(){$0>$1}
复制代码
```

若闭包表达式是函数的唯一参数，在调用该函数时，若采用尾随闭包的写法，则不需要再函数名称之后写一对圆括号`()`

```
let newArray = names.sorted{s1,s2 in s1 > s2}
let newArray = names.sorted{$0>$1}
复制代码
```

#### 值的捕获

闭包可以从定义它的周围上下文中捕获常量和变量。闭包可以在其方法体中引用并修改常量和变量的值，即使定义常量和变量的原始作用域不存在。 在Swift中，一个闭包可以捕获值的最简单形式就是嵌套函数。一个嵌套函数可以捕获任何它外围函数的参数也可以捕获定义在外围函数里的常量和变量。

```
//阐述闭包捕获值的函数方法。
func createIncrementer(forIncrese amount:Int) -> ()->Int {
    //定义嵌套函数外部的变量
    var total = 0
    //定义一个嵌套函数
    func increase()->Int {
        total += amount
        return total
    }
    //返回此嵌套函数
    return increase
}
复制代码
```

闭包捕获值的表现分析

```
let increaseByTen = createIncrementer(forIncrese: 10)//increaseByTen其实是内部的嵌套函数（闭包的一种），捕获了`createIncrementer`方法的参数`amount`与方法体中定义的`total`变量。
print(increaseByTen())//!< log:10
print(increaseByTen())//!< log:20
print(increaseByTen())//!< log:30 综上述`increaseByTen`函数捕获了捕获了`createIncrementer`方法的参数`amount`与方法体中定义的`total`变量，并在其内部持有了外部变量`total`和外部方法参数`amount`的副本。以至于`increaseByTen`可以每次调用都能基于`amount`的值，对变量`total`进行递增，并且返回结果。
let increaseBySix = createIncrementer(forIncrese: 6)
print(increaseBySix())//!< log:6
print(increaseBySix())//!< log:12
print(increaseBySix())//!< log:18 综上述：`increaseBySix`是调用了`createIncrementer`生成的一个`()->Int`类型的常量。在生成的过程中，内部的闭包（嵌套函数）`increase`重新捕获了外部变量`total`和外部方法参数`amount`，并返回此方法赋值给了`increaseBySix`，以至于`increaseBySix`和`increaseByTen`具备不同的递增系数。本质上这是两个不同的函数类型的常量。
复制代码
```

上述示例中，`increaseByTen`其实是内部的嵌套函数（闭包的一种）`increase` 。`increaseByTen`函数捕获了`createIncrementer`方法的参数`amount`与方法体中定义的`total`变量，并在其内部持有了`increaseByTen`函数捕获的值的副本。以至于`increaseByTen`可以每次调用都能基于`amount`的值，对变量`total`进行递增，并且返回结果。`increaseBySix`是调用了`createIncrementer`生成的另一个`()->Void`类型的常量。在生成的过程中，内部的闭包（嵌套函数）`increase`重新捕获了外部变量`total`和外部方法参数`amount`，并返回此方法赋值给了`increaseBySix`，以至于`increaseBySix`和`increaseByTen`具备不同的递增系数，并且分别进行多次调用。本质上这是两个不同的函数类型的常量。

注意：如果值不会被闭包改变，并且闭包创建以后值也不会被改变。Swift可以代替闭包捕获和存储值的一个副本。Swift也会参与处理所有不再需要的变量的内存管理。

#### 闭包是引用类型

函数和闭包是引用类型。无论何时将函数或闭包赋值给常量或变量，实际上都是将该常量或变量设置为对函数或闭包的引用。意味着如果为两个不同的常量或变量分配同一个闭包，那么这两个常量或变量都将引用的是相同的闭包。

```
let alsoIncreaseByTen = increaseByTen //!< 引用传递
print(alsoIncreaseByTen())//!< log:40
let alsoIncreaseByTen1 = increaseByTen
print(alsoIncreaseByTen1())//!< log:50
复制代码
```

上述示例中可以看出，函数或闭包是引用类型，常量之间的赋值，其实是引用的传递，不管是`alsoIncreaseByTen` 还是`alsoIncreaseByTen1` 都引用的是同一个函数指针。因此调用结果会持续递增。

#### 逃逸闭包

闭包作为函数参数进行传递，但是该闭包并未在函数返回前调用，而是在函数返回后才被调用，则这个闭包被称为逃逸了。当我们声明一个以闭包作为参数之一的函数时，我们可以在该闭包参数的类型之前书写`@escaping`来表示该闭包允许逃逸。即：允许该闭包在函数结束后仍然可以被调用。 当一个函数需要用到异步操作回调的时候需要使用逃逸闭包。 实现闭包逃逸的一种途径是通过将该闭包存储到定义在函数外面的变量中，稍后再去调用。我们将使用这种方式，描述闭包逃逸的场景。

```
class escapeClosure: NSObject {
    //声明一个闭包类型的数组
    var closureArray : [(String)->Void] = []
    override init() {
        super.init()

    }
    //模仿闭包逃逸:写完 closureArray.append编译器检测到时逃逸闭包提示添加@escaping
    func escapeClosures(title:String,handle:@escaping (String)->Void){
        closureArray.append(handle)
    }
    //类方法
    static func startEscape(){
       let escapeObject = escapeClosure()
       escapeObject.escapeClosures(title: "场景1") { (s1) in
            print("场景1"+s1)//!< 场景1逃逸闭包1被调用了
        }
        escapeObject.escapeClosures(title: "场景2") { (s1) in
            print("场景2"+s1)//!< 场景2逃逸闭包2被调用了
        }
        //使用迭代器进行下标和元素的同时遍历
        for (index,obj) in  escapeObject.closureArray.enumerated() {
            obj("逃逸闭包\(index+1)被调用了")
        }
    }
}
//调用
escapeClosure.startEscape()//!< 场景1逃逸闭包1被调用了 场景2逃逸闭包2被调用了
复制代码
```

#### 自动闭包：Autoclosures

`autoclosure`是一个被自动创建的闭包，用于包装作为参数传递给函数的表达式。该表达式被自动创建为：不含参数，返回值省略（根据表达式的返回值决定）`in`关键字省略，方法体中只含表达式的闭包。 当该函数被调用时，自动闭包会返回表达式的值。我们可以通过在函数类型前使用关键字`@autoclosure`把自动闭包外围的花括号`{}`都给去掉。但是**重点是使用`@autoclosure`关键字只限于修饰参数中的闭包，并且该闭包的类型可以有返回值，但绝对不能有参数。**若对`@autoclosure`关键字搞点事情修饰下不是参数的闭包，会发现报错：`'@autoclosure' may only be used on parameters`。修饰下带有参数的闭包，会发现报错：`Argument type of @autoclosure parameter must be '()'`。

```
var nameArray = ["赵云","关羽","张飞","刘备"]
//闭包参数为空 被省略 返回值是String类型由`nameArray.remove(at: 0)`的返回值决定 故省略，同时省略了`in`关键字
let removeClosure = {
    nameArray.remove(at: 0)
}
print("调用`removeClosure`移除之前，数组`nameArray`的个数：\(nameArray.count)。调用`removeClosure`之后移除了字符串：\(removeClosure()) ，数组`nameArray`的个数变为：\(nameArray.count)。综上述可以看出自动闭包允许延迟调用，因为在调用闭包之前，内部代码不会运行")
复制代码
```

上述示例中，调用`removeClosure`移除数组首元素之前，数组`nameArray`的个数：4。调用`removeClosure`之后移除了字符串：赵云 ，数组`nameArray`的个数变为：3。综上述可以看出自动闭包允许延迟调用，因为在调用闭包之前，内部代码不会运行。

```
//延迟调用的另一种形式，定义个拟合自动闭包的函数类型作为参数的函数。先定义闭包，随后在函数体内调用获取值。
static func unknownOperate(operation:()->String) -> Void {
    print("闭包作为参数,输出的删除的数组的字符串:\(operation())")//<!闭包作为参数,输出的删除的数组的字符串:赵云
}
//将闭包作为参数传递给函数时，在函数中进行数据元素移除的操作
escapeClosure.unknownOperate { () -> String in
    nameArray.remove(at: 0)
}
//更简化的形式
escapeClosure.unknownOperate {nameArray.remove(at: 0)}
复制代码
```

使用关键字`@autoclosure`标记闭包参数为自动闭包类型的。调用函数时，传递闭包的实参时，可以像传`String`类型的参数一样而不是闭包那样传递。

```
//定义一个自动闭包的形式
static func autoClosure(operation: @autoclosure ()->String){
    print("自动闭包作为参数,输出的删除的数组的字符串:\(operation())")
}
//调用很神奇啊，但也会让人很蒙 有木有
 escapeClosure.autoClosure(operation: nameArray.remove(at: 0))
复制代码
```

注意：过度使用`autoclosures`会使我们的代码难以理解。上下文和函数名称应该明确表示该闭包的调用被推迟了。 自动闭包同时也允许逃逸。需要同时使用`@autoclosure`和`@escaping`属性。

```
//定义存储自动闭包类型的数组变量
var autoclosureArray : [()->String] = []
//自动闭包实现逃逸
func autoclosureAndEscape(handle: @autoclosure @escaping ()->String) -> Void {
    autoclosureArray.append(handle)
}
//执行自动闭包逃逸操作
static func doAutoclosureAndEscape(){
    var nameArray = ["我是来自数组的可逃逸的自动闭包"]
    //实例化对象
    let escapeObj = escapeClosure()
    escapeObj.autoclosureAndEscape(handle: "我是可逃逸的自动闭包")
    escapeObj.autoclosureAndEscape(handle: nameArray.remove(at: 0))
    //逃逸闭包的调用，在函数返回后
    for (index,handle) in escapeObj.autoclosureArray.enumerated() {
        print("\(handle()):\(index)号")
    }
}
//调用
escapeClosure.doAutoclosureAndEscape()//!< 自动闭包逃逸
/*控制台输出：
我是可逃逸的自动闭包：0号
我是来自数组的可逃逸的自动闭包：1号
*/
复制代码
```

参考资料： [swift 5.1官方编程指南](https://docs.swift.org/swift-book)


收录于： [QiShare团队](https://www.jianshu.com/c/b3bd94559163)
