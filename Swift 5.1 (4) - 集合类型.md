### 集合类型

Swift提供三种主要的集合类型，称为`Array`，`Set`和`Dictionary`，用于存储值的集合。`Array`是有序的值的集合。`Set`是唯一值的无序集合。`Dictionary`是键值关联的无序集合。
**可变集合：**
如果创建数组，集合或字典，并将其分配给变量，则创建的集合将是可变的。我们可以通过添加，删除或更改集合中的项目来更改集合。如果将数组，集合或字典分配给常量，则该集合是不可变的，并且其大小和内容不能更改。
**数组：**
数组可以存储相同类型的值，并且相同的值可以在数组不同位置多次出现。

1.  数组类型的简写语法：a. `Array <Element>` b. `[Element]`其中`Element`是允许数组存储的值的类型。其中`[Element]`简写形式优选。

2.  创建一个空的数组：

使用初始化语法创建某个类型的空数组：

```
//方式一
let intArray = Array<Int>()
print("intArray中有\(intArray.count)个元素")
//方式二
let intArray = [Int]()
print("intArray中有\(intArray.count)个元素")
复制代码
```

如果上下文已经提供了数组中的类型信息，则数组存储的值得类型就是确定的。

3.  创建带有初始值得数组：

Swift的`Array`类型提供了一个初始化方法，用于创建一个特定大小的数组，并将其所有值设置为相同的默认值。

```
let defaultValueArray = Array.init(repeating: "你好", count: 3)
print(defaultValueArray)//!< ["你好", "你好", "你好"]
复制代码
```

4.  两个数组相加：

使用加法运算符`+`将两个具有兼容类型的现有数组相加来创建新数组。新数组的类型是从我们添加的两个数组的类型推断出来的。这两个相加的数组的类型必须要可以兼容，否则编译器会报错。

```
let defaultValueArray = Array.init(repeating: "你好", count: 3)
let secondValueArray = Array.init(repeating: "大佬", count: 2)
let thirdValueArray = defaultValueArray + secondValueArray
print(thirdValueArray)//!< ["你好", "你好", "你好", "大佬", "大佬"]
复制代码
```

5.  使用字面量元素初始化数组：

使用数组字面量元素初始化数组，语法：`[value 1, value 2, value 3]`

```
let literalArray = ["逗哥","刀哥"] //!< ["逗哥", "刀哥"] 有初值，可以类型推断，不必声明数组的类型
let literalArray1 : [Int] = [6,7]//!< [6, 7] 声明了类型
复制代码
```

6.  数组的访问和修改：

`count`属性：访问数组元素的个数。`isEmpty` 属性值`Bool`类型数组判空，相较`Array.count == 0`更高效。

```
if intArray.isEmpty {
   print("intArray:\(intArray)中有\(intArray.count)个元素")//!< intArray:[]中有0个元素
}
复制代码
```

使用`append(_:)`方法拼接新项到数组的末尾

```
var appendArray = ["飞哥","强哥"]
appendArray.append("大哥")//!< ["飞哥", "强哥", "大哥"]
复制代码
```

使用加法赋值运算符`+=`追加一个或多个兼容项的数组：

```
var appendArray = ["飞哥","强哥"]
let array1 = ["finally","ok"]
let array2 = ["拯救","静","\u{65}"]
appendArray += array1 //!< ["飞哥", "强哥", "finally", "ok"]
appendArray += array2 //!< ["飞哥", "强哥", "finally", "ok", "拯救", "静", "e"]
复制代码
```

使用下标从数组中取值：

```
let literalArray = ["逗哥","刀哥"] //!< ["逗哥", "刀哥"]
let firstStr = literalArray[0]
print(firstStr) //!< 逗哥
复制代码
```

使用下标更改给定索引处的值：

```
var literalArray = ["逗哥","刀哥"] //!< ["逗哥", "刀哥"]
literalArray[0] = "加油"
print(literalArray) //!< ["加油", "刀哥"]
复制代码
```

使用范围下标一次性更改值，即使替换值的数组长度与要替换的范围不同。但是必须不能越界：下标范围必须在当前数组的有效范围内。

```
var totalArray = ["飞哥", "强哥", "finally", "ok", "拯救", "静", "e"]
totalArray[...3] = ["","","","❌"]//!< ["", "", "", "❌", "拯救", "静", "e"]
totalArray[5..<7] = ["融合了"]//!< 5..<7有两个元素 被替换成了一个 log：["", "", "", "❌", "拯救", "融合了"]
print(totalArray)
复制代码
```

使用`insert（_：at :)`方法在指定索引处将指定项插入数组：

```
var literalArray = ["逗哥","刀哥"] //!< ["逗哥", "刀哥"]
literalArray.insert("妄言", at: 1)//!< ["逗哥", "妄言", "刀哥"]
print(literalArray)
复制代码
```

使用`remove（at :)`方法从数组中删除指定项并返回删除项

```
var literalArray = ["逗哥","刀哥"] //!< ["逗哥", "刀哥"]
literalArray.insert("妄言", at: 1)//!< ["逗哥", "妄言", "刀哥"]
let deleteStr = literalArray.remove(at: 0)//!< ["妄言", "刀哥"]
print(literalArray,"删除了:\(deleteStr)")//!< ["妄言", "刀哥"] 删除了:逗哥
复制代码
```

使用`removeLast()`从数组中删除最终项并返回删除项。以避免需要查询数组的`count`属性.

```
var literalArray = ["逗哥","刀哥"] //!< ["逗哥", "刀哥"]
literalArray.removeLast()
//!< 也可以removeFirst()
literalArray.removeFirst()
复制代码
```

7.  数组的遍历

使用`for-in`循环遍历

```
var literalArray = ["逗哥","刀哥"] //!< ["逗哥", "刀哥"]
for item in literalArray {
    print(item,"", separator: " ", terminator: "")//!< 逗哥 刀哥
}
复制代码
```

使用enumerated（）方法迭代数组:同时遍历各项的整数索引及其值。 返回由整数和各项的值组成的元组。

```
for item in literalArray.enumerated() {
    print(item.1) //!< 逗哥 刀哥
    print(item.0) //!< 0 1
    print(item) //!< (offset: 0, element: "逗哥") (offset: 1, element: "刀哥")
}
复制代码
```

**集合：**

`Set`是唯一值的无序集合，这个特性可以让我们在适当的场景下去使用。

1.  集合类型的值（散列，哈希）

必须是可散列的类型才能存储在集合中。 即：集合中存储的类型必须提供能够计算自身散列值的方法。哈希值是一个`Int`值，对于所有相互比较相等的对象都是相同的，例如`a == b`，则遵循`a.hashValue == b.hashValue`。
默认情况下，Swift的所有基本类型，如`String`，`Int`，`Double`和`Bool`都是可哈希的，并且可以用作集合中的值类型或字典的key类型。默认情况下，没有关联值的枚举类型也是可以哈希的。

> 注意点：我们可以使用自定义符合`Hashable`协议的类型作为集合中的值类型或字典的key类型。符合`Hashable`协议的类型必须提供名为`hashValue`的`Int`类型的可访问的属性。该自定义类型的`hashValue`属性在同一程序的不同执行或不同程序中执行时返回的值不需要相同。因为`Hashable`协议继承`Equatable`协议，所以符合`Hashable`协议的类型还必须提供运算符`==`的实现。

`Equatable`协议要求任何符合`==`实现的，都是相等关系。`==`的实现必须要满足三个条件：反身性，对称性，及物性。
比如实现`Equatable`协议的类型的值a，b，c：
•`反身性`表示：a == a
•`对称性`表示：a == b则b == a
•`及物性`表示：a == b && b == c则 a == c

2.  集合类型语法：`Set <Element>`，其中Element是允许集合存储的类型。与数组不同，集合没有等效的简写形式。

3.  创建空集合：

```
let emptySet = Set<Int>()
let emptyCharacterSet = Set<Character>()
复制代码
```

如果上下文已经提供了集合中的类型信息，则集合中存储的值得类型就是确定的。

4.  使用数组创建集合

使用数组初始化集合，将一个或多个值写入集合中。

```
var favoriteGenres :Set<String> = ["可是","怎么","能够","如此"]
//! 由于Swift的类型推断的存在，在上下文提供了类型信息后，可以简写为
var favoriteGenres :Set = ["可是","怎么","能够","如此"]
复制代码
```

5.  集合的访问和修改

`count`属性：访问集合中元素的个数。`isEmpty`Bool类型的属性值用于集合判空。

```
if favoriteGenres.isEmpty {
    print("favoriteGenres集合中没有元素")

} else {
    print("favoriteGenres集合有 \(favoriteGenres.count)个元素")

}
复制代码
```

使用`insert(_:)`方法添加一个新项到集合中：

```
favoriteGenres.insert("聪明")//!< ["聪明", "能够", "可是", "怎么", "如此"]
复制代码
```

使用`remove（_ :)`方法从集合中删除指定项并返回删除项：如果该项目是该集合的成员，则删除该项目，并返回已删除的值，如果该集合不包含该项目，则返回nil

```
if let removeItem = favoriteGenres.remove("聪明") {
    print("\(removeItem)此项已被移除")
} else {
    print("favoriteGenres集合中没有该项")
}
复制代码
```

使用`contains(_:)`方法，判断集合中是否包含某一项。

```
if favoriteGenres.contains("好的") {
    print("包含")
} else {
    print("不包含")
}
复制代码
```

6.  集合的遍历

使用`for-in`循环遍历

```
var favoriteGenres :Set = ["可是","怎么","能够","如此"]
for item in favoriteGenres {
    print(item,"",separator: " ", terminator: "")//!< 能够 怎么 如此 可是
}
复制代码
```

使用`sorted()`方法，以特定顺序遍历集合的值，该方法将集合的元素使用`<`运算符排序后的元素作为数组返回。

```
for item in favoriteGenres.sorted() {
    print(item)
}
复制代码
```

7.  集合的操作

两组集合a和b以阴影区域表示的各种集合操作的结果。
![image.png](https://upload-images.jianshu.io/upload_images/19704571-3375e1925d3d5526.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


*   使用`intersection（_ :)`方法创建一个只包含两个集合共有的值的新集合。
*   使用`symmetricDifference（_ :)`方法创建一个新集合，其中包含任一集合中的值，但不包含两个集合共同的部分。
*   使用`union（_ :)`方法创建一个包含两个集合中所有值的新集合。
*   使用`subtracting(_:)`方法创建一个值不在指定集中的新集。

```
let set1 : Set<Int> = Set.init(arrayLiteral: 1,5,7,2)
let set2 : Set<Int> = [2,4,6,8]
let set3 = set1.intersection(set2)//!< 预期：[2] 实际 [2]
//除了相同以外的其他元素
let set4 = set1.symmetricDifference(set2)//!< 预期：[1,5,7,4,6,8] 实际: [6, 4, 5, 7, 8, 1]
let set5 = set1.union(set2)//!< 预期[6, 4, 5, 7, 8, 1,2] 实际 [4, 5, 2, 8, 1, 7, 6]
//从set1中去除与set2有关的所有元素
let set6 = set1.subtracting(set2)//!< 预期[1,5,7] 实际[1, 7, 5]
复制代码
```

7.  集合之间的关系与相等判断：三个集合a，b和c，集合a包含集合b中的所有元素，则称集合a是集合b的超集，相反，集合b是集合a的子集。集合b和集合c没有共同的元素。集合a和集合c有共同的元素，则集合a和集合c相交。

• 使用运算符`==`确定两个集合是否包含所有相同的值。
• 使用`isSubset（of :)`方法确定集合的所有值是否包含在指定集合中。
• 使用`isSuperset（of :)`方法确定集合是否包含指定集合中的所有值。
• 使用`isStrictSubset（of :`)或`isStrictSuperset（of :)`方法来确定集合是否是指定集合的​​子集或超集，但不能判断相等。
• 使用`isDisjoint（with :)`方法确定两个集合是否没有有共同的值。

```
let set : Set<Int> = [1,5,2,7]
let set1 : Set<Int> = Set.init(arrayLiteral: 1,5,7,2,8)
//! 判断相等
if set == set1 {
    print("相等")
} else {
    print("不相等")
}
//！判断子集与超集
if set.isStrictSubset(of: set1){//!< set是否是set1的子集
    print("set是set1的子集")
}
if set1.isStrictSubset(of: set){//!< set1是否是set的超集
    print("set1是set的超集")
}
//!< 判断是否不相交
if set1.isDisjoint(with: set) {//!< `true`元素不相交 否则`false`
    print("set1和set不相交")
} else {
    print("set1和set相交")
}
复制代码
```

**字典：**

1.  字典类型的简写语法：

a.`Dictionary <Key，Value>`。b. `[Key：Value]`。其中`Key`表示字典中键的值的类型，`Value`表示存储的值的类型。 字典`Key`类型必须符合`Hashable`协议，就像集合的值类型一样。 2\. 创建一个空的字典：

```
//方式一
let namesOfIntegers :Dictionary<Int,String> = Dictionary<Int,String>.init()
let namesOfIntegers  = Dictionary<Int,String>.init()
let namesOfIntegers  = Dictionary<Int,String>()

//方式二
let namesOfIntegers  = [Int:String].init() //!< [:]
let namesOfIntegers = [Int:String]()
//方式三：提供类型信息
let namesOfIntegers : [Int:String] = [:]
复制代码
```

如果上下文已经提供了字典中的类型信息，则字典中的类型信息就是确定的。

3.  创建带初始值的字典：

```
let airports : [String:String] = [String:String].init(dictionaryLiteral: ("name","zhangfei"),("age","16"),("职业","将军"))//!< ["职业": "将军", "age": "16", "name": "zhangfei"]
复制代码
```

简写语法：`[key 1: value 1, key 2: value 2, key 3: value 3]`

```
//键值类型都相同，swift乐行推断，故省略字典类型
let airports = ["职业": "将军", "age": "16", "name": "zhangfei"]
//以下类型的字典就不能类型推断，必须声明字典的键值类型
 let airports : [String : Any] = ["职业": "将军", "age": 16, "name": "zhangfei"]
复制代码
```

4.  字典的访问和修改

`count`属性：访问字典键值对的个数。`isEmpty`属性值Bool类型，字典判空

```
if airports.isEmpty {
    print("airports是空的")
} else {
    print("airports:\(airports)中有\(airports.count)个元素")//!< airports:["name": "zhangfei", "职业": "将军", "age": "16"]中有3个元素
}
复制代码
```

添加新项到字典中

```
//方式一.使用下标语法
var airports = ["job": "将军", "age": "16", "name": "zhangfei"]
airports["sex"] = "男"
//方式二
var airports = ["job": "将军", "age": "16", "name": "zhangfei"]
airports.updateValue("男", forKey: "sex")
print(airports)//!< ["sex": "男", "job": "将军", "age": "16", "name": "zhangfei"]
复制代码
```

更改与特定键关联的值

```
//方式一.使用下标语法
var airports = ["job": "将军", "age": "16", "name": "zhangfei"]
airports["job"] = "主公"
//方式二
var airports = ["job": "将军", "age": "16", "name": "zhangfei"]
airports.updateValue("主公", forKey: "job")
print(airports)//!< ["age": "16", "job": "主公", "name": "zhangfei"]
复制代码
```

上述示例中`updateValue(_:forKey:)`方法，若是`key`在字典中已存在，则更改其对应的值为新值，并且返回其对应的旧值。若`key`在字典中不存在，则返回`nil`，并且添加这个新的键值对到字典中，因为返回值可`nil`故此方法的返回值是可选类型。

```
if let oldValue =  airports.updateValue("男", forKey: "sex") {
    print("key早就已经存在了，并且旧值为\(oldValue)")
} else {
    print("key不存在，需添加到字典中")//!< log:key不存在，需添加到字典中
}
复制代码
```

删除字典中键值对：

```
//方式一.使用下标语法
var airports = ["job": "将军", "age": "16", "name": "zhangfei"]
airports["job"] = nil
//方式二
if let value = airports.removeValue(forKey: "job") {
     print("The value \(value) was removed.")//!< The value 将军 was removed.
}
print(airports)//!< ["age": "16", "name": "zhangfei"]
复制代码
```

上述示例中`removeValue(_:forKey:)`方法，若是key在字典中已存在，则移除，并且返回该移除项的值。若key在字典中不存在，则返回nil，（不存在键值对，无法做移除）因为返回值可nil故此方法的返回值是可选类型。

5.  字典的遍历：

使用`for-in`循环遍历字典中的键值对。字典中的每项都会作为 `(key, value)`这样的元组类型返回，并且我们可以再迭代的过程中将元组的成员分解为临时常量或变量。

```
//! 方式一
for item in airports {
print("\(item.key)")
print("\(item.value)")
}
//! 方式二
for (key,value) in airports {
print("\(key)")
print("\(value)")
}
复制代码
```

单独遍历其键或值

```
for key in airports.keys {
    print(key)
}
for value in airports.values {
    print(value)
}
复制代码
```

`keys`或`values`的类型转换为数组。不可强转，类型不一致，需要重新初始化为`Array`类型

```
let keysArray = [String](airports.keys)
let valuesArray = Array<String>.init(airports.values)
复制代码
```

Swift的`Dictionary`类型是无序的。要按特定顺序遍历字典的键或值，需要在字典的 `keys` 或 `values` 属性的基础上使用`sorted()`方法(升序)，得到有序的keys或values。

参考资料： [swift 5.1官方编程指南](https://docs.swift.org/swift-book)



收录于： [QiShare团队](https://www.jianshu.com/c/b3bd94559163)
