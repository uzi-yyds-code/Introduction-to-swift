### 结构体和类

结构体和类是多功能的，灵活的结构，是程序中代码的构建块。我们可以使用与定义常量，变量和函数相同的语法来定义属性和方法，为我们的结构体和类添加功能。 Swift中我们为自定义的结构体和类不需要创建单独的.h和.m文件。而是在单个文件中定义结构体或类即可，并且Swift会提供额外的接口，自动让类或结构体在其他代码中可用。

#### 比较结构体和类

在Swift中，结构体和类有许多相像的地方。

*   定义存储值的属性
*   定义提供功能的方法
*   定义下标以使用下标语法提供对其值进行访问
*   定义初始化方法以设置其初始状态
*   可以被扩展 `extend`，在函数的默认实现的基础上可以扩展其功能。
*   可以遵守协议以提供某种标准功能

同时，类具有结构体所没有的附加功能：

*   继承：一个类能够继承另一个类的特性。
*   类型转换：在运行时检查和解释类的实例对象所属类型。
*   析构函数（Deinitializers）：允许类的实例对象释放它已分配的任何资源。
*   引用计数：允许对类实例进行多个引用。

**语法定义**

结构和类具有相似的定义语法。使用`struct`关键字定义一个结构体。使用`class`关键字定义类。

```
struct SomeStructure {
}
class SomeClass {
}
复制代码
```

**结构体和类的实例**

结构和类构建新实例的最简单的初始化语法：使用类或结构体的类型名称，后跟空括号。

```
struct Resolution {
    var width = 0
    var height = 0

}
class VideoMode {
    var resolution = Resolution()
    var interlaced = false
    var frameRate = 0.0
    var name: String?
}
let someResolution = Resolution()
let someVideoMode = VideoMode()
复制代码
```

**属性访问**

使用**`.`**语法进行结构体和类的属性的访问

```
let width = someResolution.width
let width = someVideoMode.resolution.width 
复制代码
```

使用**`.`**语法为属性赋新值

```
someResolution.width = 250
someVideoMode.resolution.width  = 255
复制代码
```

**结构体类型的成员初始化方法**

所有结构体都有一个自动生成的初始化方法。我们可以使用这个自动生成的初始化方法初始化一个新的实例对象，并根据初始化方法的参数（结构体中定义的属性名称），设置成员的属性。

```
let someResolution = Resolution(width: 33, height: 77)
复制代码
```

与结构体不同，类没有默认的成员初始化方法。

#### 结构体和枚举是值类型

类似Swift中的整数，浮点数，布尔值，字符串，数组和字典，都是值类型的，并且这些类型在Swift中的实现都是基于结构体的。故所有结构体和枚举值类型都是值类型。这意味着我们创建的任何结构体和枚举实例以及作为它们属性的任何值类型，在代码中传递时始终会被复制。 注意：标准库定义的集合，如：数组，字典和字符串使用优化来降低复制的性能成本。这些集合类型不是立即复制，而是共享内存，其元素存储在原始实例和任何副本之间。如果需要修改集合的其中一个副本，则会在修改之前复制集合中的所有元素。但是我们在代码中看到的好像总是立即发生了复制。

```
let someResolution = Resolution(width: 33, height: 77)
var myResolution = someResolution
复制代码
```

在这个赋值的过程中，由于`Resolution`是值类型的，所以首先会生成`someResolution`实例的副本并将此副本赋值给`myResolution`。此时`someResolution`和`myResolution`具有相同的宽度和高度，但是却是两个不同的实例。

```
myResolution.width = 255
复制代码
```

`someResolution`和`myResolution`是两个单独的实例，所以修改副本`myResolution`的属性`width`，并不会影响`someResolution` 的`width`。 枚举类型也是值类型，具有和结构体一样的赋值特性：`复制`

```
enum CompassPoint {
    case north, south, east, west
     mutating func turnNorth() -> Void {
        self = .north
    }
}
var currentDirection = CompassPoint.west
let rememberedDirection = currentDirection
currentDirection.turnNorth()

print("当前的方向，被改变后 \(currentDirection)")//!< 当前的方向，被改变后 north
print("保存的方向 \(rememberedDirection)")//!< 保存的方向 west
复制代码
```

使用`mutating`关键字放在枚举或结构体中所定义方法的`func`关键字之前，使得该方法可以在方法中修改枚举或结构体的属性。 当`currentDirection`赋值给`rememberedDirection`时，`rememberedDirection`拥有的是`currentDirection`实例的副本。此后更改`currentDirection`的值不会影响存储在`rememberedDirection`中值。因为彼此独立。

#### 类是引用类型的

与值类型不同，引用类型在分配给变量或常量时或者传递给函数时不会被复制，而是使用对同一实例的引用。

```
let tenEighty = VideoMode()
tenEighty.resolution = someResolution
tenEighty.interlaced = true
tenEighty.name = "视频模式"
tenEighty.frameRate = 25.0
//赋值给新的实例对象
let alsoTenEighty = tenEighty
alsoTenEighty.frameRate = 30.0
print(tenEighty.frameRate,alsoTenEighty.frameRate)
//!< tenEighty.frameRate：30.0 alsoTenEighty.frameRate：30
复制代码
```

**身份运算符**

参考[swift 5.1基础（二）运算符](https://www.jianshu.com/p/99c971f2e240)讲解。

**指针**

Swift中引用某个引用类型的实例作为常量或变量时，类似于C中的指针，但它不是指向内存中地址的直接指针（不是直接寻址），并且不需要编写星号`*`来指示你正在创建一个引用对象。相反，这些引用的定义与Swift中的任何其他常量或变量一样。 另：Swift标准库提供指针和缓冲类型，如果需要直接与指针交互，可以使用它们 [手动内存管理](https://developer.apple.com/documentation/swift/swift_standard_library/manual_memory_management)。

参考资料： [swift 5.1官方编程指南](https://docs.swift.org/swift-book)



收录于： [QiShare团队](https://www.jianshu.com/c/b3bd94559163)
