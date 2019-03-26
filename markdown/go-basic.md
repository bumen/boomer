
## go基础

### 语言结构
 * 包声明
 * 引入包
   + import "fmt" //使用双引号
   + import fm "fmt" // 使用fm别名
   ``` 
    // 组
    import (
       "fmt"
       "os"
    )
    // 组
    import ("fmt"; "os")
    // 一行引入
    import "fmt"; import "os"
    // 多行引入
    import "fmt"
    import "os"
    //当前路径
    import "./trans"
    // 系统搜索路径
    import "/tarns"
   ```
   
 * 函数
 * 变量
 * 语句&表达式
 * 注释
 * 运行 
   + go run hello.go
 * 可见性
   + 当标识符（包括常量、变量、类型、函数名、结构字段等等）以一个大写字母开头
   那么使用这种形式的标识符的对象就可以被外部包的代码所使用（客户端程序需要先导入这个包），这被称为导出（像面向对象语言中的 public）
   + 标识符如果以小写字母开头，则对包外是不可见的，但是他们在整个包的内部是可见并且可用的（像面向对象语言中的 private ）。

### 基础语法
 * go程序可以由多个标记组成
   + 关键字
   + 标识符
   + 常量
   + 字符串
   + 符号
 * 行分隔符
   + 一行代表一个语句结束
 * 注释
 
 * 标识符
   + 就是变量
 * 关键字
   + go已经定义的
 * 空格
   + Go 语言中变量的声明必须使用空格隔开
  

### 数据类型
 * Go 语言中不存在类型继承。
 * 类型可以是
   + 基本类型，如：int、float、bool、string；
   + 结构化的（复合的），如：struct、array、slice、map、channel；
      - 结构化的类型没有真正的值，它使用 nil 作为默认值
   + 只描述类型的行为的，如：interface。
 * 数据类型的出现是为了把数据分成所需内存大小不同的数据，编程的时候需要用大数据的时候才需要申请大内存，就可以充分利用内存。
 * 布尔型
   + true, false
 * 数字型
   + 整数，浮点，复数
   + uint8, uint16, uint32, uint64
   + int8, int16, int32, int64
   + float32, float64, complex64, complex128
      - float32 精确到小数点后 7 位
      - float64 精确到小数点后 15 位
      - 应该尽可能地使用 float64，因为 math 包中所有有关数学运算的函数都会要求接收这个类型
   + byte: 是 uint8 的别名
   + rune: 是int32的别名
   
 * 基于架构的类型
   + 在32 位操作系统上，它们均使用 32 位（4 个字节），在 64 位操作系统上，它们均使用 64 位（8 个字节）
   + uint: 32 或 64 位
   + int: 与 uint 一样大小
   + uintptr: 无符号整型，用于存放一个指针，长度被设定为足够存放一个指针即可
 * 字符串型
   + Go语言的字符串的字节使用UTF-8编码标识Unicode文本。
    ``` 
      var ch byte = 'A'
      var ch byte = 65 或 var ch byte = '\x41'
      （\x 总是紧跟着长度为 2 的 16 进制数, 长度为 3 的八进制数）
    ```
   + 在书写 Unicode 字符时，需要在 16 进制数之前加上前缀 \u 或者 \U。
   + 因为 Unicode 至少占用 2 个字节，所以我们使用 int16 或者 int 类型来表示。
   + 如果需要使用到 4 字节，则会加上 \U 前缀；前缀 \u 则总是紧跟着长度为 4 的 16 进制数，前缀 \U 紧跟着长度为 8 的 16 进制数。
 * 派生类型
   + (a) 指针类型（Pointer）
   + (b) 数组类型
   + (c) 结构化类型(struct)
   + (d) Channel 类型
   + (e) 函数类型
   + (f) 切片类型
   + (g) 接口类型（interface）
   + (h) Map 类型
   
 *  0 来表示 8 进制数， 0x 来表示 16 进制数
 * e 来表示 10 的连乘（如： 1e3 = 1000，或者 6.022e23 = 6.022 x 1e23）。
 * Go 中不允许不同类型之间的混合使用，但是对于常量的类型限制非常少，因此允许常量之间的混合使用
 * 类型别名
   + type TZ int， 使用TZ代表int类型
   
### 字符串
 * 字符串拼接符 +
 * 获取字符串中某个字节的地址的行为是非法的，例如：&str[i]
 * 在循环中使用加号 + 拼接字符串并不是最高效的做法，更好的办法是使用函数 strings.Join()，
 有没有更好地办法了？有！使用字节缓冲（bytes.Buffer）拼接更加给力
   
### 变量
 * 变量名由字母、数字、下划线组成，其中首个字符不能为数字。
 * 声明1
   + var identifier type
 * 声明2
   + var v_name = value
   + 自行判断类型
 * 声明3 
   + v_name := value：
   + 省略var 
   + 注意 := 左侧如果没有声明新的变量，就产生编译错误
   + 这种不带声明格式的只能在函数体中出现,而不可以用于全局变量的声明与赋值
   ``` 
    var intVal int 
    intVal :=1 // 这时候会产生编译错误
    intVal,intVal1 := 1,2 // 此时不会产生编译错误，因为有声明新的变量，因为 := 是一个声明语句
   ```
 * 声明4
   ``` 
    // 这种因式分解关键字的写法一般用于声明全局变量
    var (
        vname1 v_type1
        vname2 v_type2
    )
   ```
 * 如果你声明了一个局部变量却没有在相同的代码块中使用它，同样会得到编译错误
 * 但是全局变量是允许声明但不使用。 同一类型的多个变量可以声明在同一行
   + var a, b, c int
 * 多变量可以在同一行进行赋值
   + a, b, c := 5, 7, "abc"
   
 * 空白标识符**_**
   + 空白标识符 _ 也被用于抛弃值
   + 如: _, b = 5, 7中， 5被抛弃
   + _ 实际上是一个只写变量，你不能得到它的值
   + 这样做是因为 Go 语言中你必须使用所有被声明的变量，但有时你并不需要使用从一个函数得到的所有返回值。
   
   
### 常量
 * 在运行时不会被修改变量
 * 只可以是布尔型，数字型（整数，浮点，复数），字符串型
 * 定义
   + const identifier [type] = value
 * 可以使用常量表达式
   + 表达式中函数必须是内置函数
 * 常量组
   + const (
      a=1
      b=iota
      c
      d
   )
 * iota
   + iota，特殊常量，可以认为是一个可以被编译器修改的常量。
   + iota 在 const关键字出现时将被重置为 0(const 内部的第一行之前)，const 中每新增一行常量声明将使 iota 计数一次(iota 可理解为 const 语句块中的行索引)。
   + 在定义常量组时，如果不提供初始值，则表示将使用上行的表达式。
   + 每遇到一次 const 关键字，iota 就重置为 0 


### 运算符
 * 算术运算符  
 `+, -, *, /, %, ++, --`
 * 关系运算符  
 `==, !=, >, <, >=, <=`
 * 逻辑运算符  
 `&&, ||, !`
 * 位运算符  
 `&, |, ^, <<, >>`
 * 赋值运算符  
 `=, +=, -=, *=, /=, %=, <<=, >>=, &=, |=, ^=`
 * 其他运算符  
   + *: 定义指针，使用指针
   + &：取指针

### 条件语句
 * if
   ``` 
    if 布尔表达式 {
       /* 在布尔表达式为 true 时执行 */
    }
   ```
 * if...else
   ``` 
    if 布尔表达式 {
       /* 在布尔表达式为 true 时执行 */
    } else {
      /* 在布尔表达式为 false 时执行 */
    }
   ```
 * switch
   + 语句执行的过程从上至下，直到找到匹配项，匹配项后面也不需要再加 break。
   + 默认情况下 case 最后自带 break 语句，匹配成功后就不会执行其他 case，如果我们需要执行后面的 case，可以使用 fallthrough 。
   ``` 
    switch var1 {
        case val1:
            ...
        case val2:
            ...
        default:
            ...
    }
   ```
   + 变量 var1 可以是任何类型，而 val1 和 val2 则可以是同类型的任意值。类型不被局限于常量或整数，但必须是相同的类型；或者最终结果为相同类型的表达式。
 * Type Switch
   + switch 语句还可以被用于 type-switch 来判断某个 interface 变量中实际存储的变量类型。
   ``` 
    switch x.(type){
        case type:
           statement(s);      
        case type:
           statement(s); 
        /* 你可以定义任意个数的case */
        default: /* 可选 */
           statement(s);
    }
   ```
 * switch中的fallthrough
   + 使用 fallthrough 会强制执行后面的 case 语句，fallthrough 不会判断下一条 case 的表达式结果是否为 true。
   
 * select 
   + select是Go中的一个控制结构，类似于用于通信的switch语句。每个case必须是一个通信操作，要么是发送要么是接收。
   + select随机执行一个可运行的case。如果没有case可运行，它将阻塞，直到有case可运行。一个默认的子句应该总是可运行的。
   + 每个case都必须是一个通信
   + 所有channel表达式都会被求值
   + 所有被发送的表达式都会被求值
   + 如果任意某个通信可以进行，它就执行；其他被忽略。
   + 如果有多个case都可以运行，Select会随机公平地选出一个执行。其他不会执行。 
     否则：如果有default子句，则执行该语句。
     如果没有default字句，select将阻塞，直到某个通信可以运行；Go不会重新对channel或值进行求值。
   ``` 
    select {
        case communication clause  :
           statement(s);      
        case communication clause  :
           statement(s); 
        /* 你可以定义任意数量的 case */
        default : /* 可选 */
           statement(s);
    }
   ```

### 循环语句
 * go中没有while
 * for
   + for init; condition; post { }
   + for condition {}  -> while类似
   + for {} -> for(;;)类似
 * break, continue, 
 * goto
   + 尽量不使用
   ``` 
     LOOP: for a < 20 {
        goto LOOP   
     }
   ```

 * for 循环的 range 格式可以对 slice、map、数组、字符串等进行迭代循环。格式如下：
   ``` 
    for key, value := range oldMap {
        newMap[key] = value
    }
   ``` 



### 变量作用域
 * 全局变量
   + 定义在函数外
   + 全局变量可以在整个包甚至外部包（被导出后）使用
   + 全局变量与局部变量名称可以相同，但是函数内的局部变量会被优先考虑
 * 局部变量
   + 定义在函数内
 * 形式参数
   + 函数定义的参数

### 数组
 * 声明
   + var variable_name [SIZE] variable_type
   
 * 初始化
   + var balance = [5]float32{1000.0, 2.0, 3.4, 7.0, 50.0}
   + 初始化数组中 {} 中的元素个数不能大于 [] 中的数字。
   + var balance = [...]float32{1000.0, 2.0, 3.4, 7.0, 50.0}
 
 * 多维数组
   + var variable_name [SIZE1][SIZE2]...[SIZEN] variable_type
   
 * 初始化二维数组
    ``` 
      a = [3][4]int{  
       {0, 1, 2, 3} ,   /*  第一行索引为 0 */
       {4, 5, 6, 7} ,   /*  第二行索引为 1 */
       {8, 9, 10, 11},   /* 第三行索引为 2 */
      }
      以上代码中倒数第二行的 } 必须要有逗号，因为最后一行的 } 不能单独一行，也可以写成这样：
      a = [3][4]int{  
       {0, 1, 2, 3} ,   /*  第一行索引为 0 */
       {4, 5, 6, 7} ,   /*  第二行索引为 1 */
       {8, 9, 10, 11}}   /* 第三行索引为 2 */
    ```
 
 * 向函数传递数组
   + 方式一：设定大小  
   `void myFunction(param [10]int)`
   
   + 方式二：未设定大小  
   `void myFunction(param []int)`

### go中指针
 * 使用
   + 定义指针变量
   + 为指针变量赋值
   + 访问指针变量指向地址的值
 * 定义指针变量
   + var ipr *int 声明指针变量
 * 为指针变量赋值
   + var a int = 10
   + ipr = &a
 * 访问指针变量指向地址的值
   + fmt.Printf("a 变量的地址是：%x\n", &a)
   + fmt.Printf("ipr 变量存储的指针地址是：%x\n", ipr)
   + fmt.Printf("ipr 变量的值：%d", *ipr)
   
 * 空指针
   + 定义之后没有分配到变量时。为nil
   
 * 指针数组
   + var ptr [n]*int
 * 指向指针的指针
   + var pptr **int
   + 变量值为：**pptr
 * 向函数传递指针参数
 * 指针运算是不允许的
   + 因此 c = *p++ 在 Go 语言的代码中是不合法的
   + 未了避免C语言中内存泄露继而程序崩溃的指针运算
   
### range关键字
 * 用于for 循环中迭代数组，切片，通道，集合，字符串的元素
   + 数组与切片返回索引与值
   + 集合返回key
   
### Map集合
 * 定义
  ``` 
    /* 声明变量，默认 map 是 nil */
    var map_variable map[key_data_type]value_data_type
    /* 使用 make 函数 */
    map_variable := make(map[key_data_type]value_data_type)
  ```
 * 初始化
   +  countryMap := map[string]string{"France": "Paris"}
 * delete函数
   + delete(countryMap, "France")
   
### 类型转换
 * 用于将一种数据类型的变量转换为另外一种类型的变量
 * Go 语言不存在隐式类型转换，因此所有的转换都必须显式说明
 * 定义
   + type_name(expression)
   