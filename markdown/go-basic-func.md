## go基础-函数

### 函数
 * 三种函数
   + 普通的带有名字的函数
   + 匿名函数或者lambda函数
   + 方法
 *  Go 里面函数重载是不被允许的
 * 定义：函数名称，返回类型（多个值），参数
   ``` 
    func function_name( [parameter list] ) [return_types] {
       函数体
    }
   ```
 * 左大括号 { 必须与方法的声明放在同一行，这是编译器的强制规定
 * 函数参数-值传递
   + 值传递是指在调用函数时将实际参数复制一份传递到函数中，这样在函数中如果对参数进行修改，将不会影响到实际参数
 * 函数参数-引用传递
   + 用传递是指在调用函数时将实际参数的地址传递到函数中，那么在函数中对参数所进行的修改，将影响到实际参数。
 * 默认情况下，Go 语言使用的是值传递，即在调用过程中不会影响到实际参数。
   + 在函数调用时，像切片（slice）、字典（map）、接口（interface）、通道（channel）这样的引用类型都是默认使用引用传递（即使没有显式的指出指针）。
 
 
 * 闭包
   + 匿名函数的优越性在于可以直接使用函数内的变量，不必申明
   ``` 
    func add(x1, x2 int) func()(int,int)  {
        i := 0
        return func() (int,int){
            i++
            return i,x1+x2
        }
    }
   ```
   + 一个返回值为另一个函数的函数可以被称之为工厂函数
 * 函数方法
   + 其实是为类定义方法
   + 一个方法就是一个包含了接受者的函数，接受者可以是命名类型或者结构体类型的一个值或者是一个指针。所有给定类型的方法属于该类型的方法集。
   ``` 
    func (variable_name variable_data_type) function_name() [return_type]{
       /* 函数体*/
    }
   ```
 * 命名的返回值
   ``` 
    // 未命名，需要return
    func getX2AndX3(input int) (int, int) {
        return 2 * input, 3 * input
    }
    // 命名返回值。不用return, 会自动return x2, x3
    func getX2AndX3_2(input int) (x2 int, x3 int) {
        x2 = 2 * input
        x3 = 3 * input
        // return x2, x3
        return
    }
   ```
 * 变长参数
   + 实参：slice...
   + 形参：func min(s ...int) int 
   
###  init 函数
 * 变量除了可以在全局声明中初始化，也可以在 init 函数中初始化。
 * 这是一类非常特殊的函数，它不能够被人为调用，而是在每个包完成初始化后自动执行，并且执行优先级比 main 函数高。
 * 每个源文件都只能包含一个 init 函数。初始化总是以单线程执行，并且按照包的依赖关系顺序执行
 * 一个可能的用途是在开始执行程序之前对数据进行检验或修复，以保证程序状态的正确性。
 * init 函数也经常被用在当一个程序开始之前调用后台执行的 goroutine
 
### defer
 * 相当于finally
 * 函数返回之前执行
 
### 内置函数
 * len 用于返回某个类型的长度或数量（字符串、数组、切片、map 和管道）；
 * cap 是容量的意思，用于返回某个类型的最大容量（只能用于切片和 map）
 * new 和 make 均是用于分配内存
   + new 用于值类型和用户定义的类型，如自定义结构
   + new(T) 分配类型 T 的零值并返回其地址，也就是指向类型 T 的指针
   + make 用于内置引用类型（切片、map 和管道）
   + make(T) 返回类型 T 的初始化之后的值
   
### 将函数作为参数
 ``` 
  func main() {
  	callback(1, Add)
  }
  
  func Add(a, b int) {
  	fmt.Printf("The sum of %d and %d is: %d\n", a, b, a+b)
  }
  
  func callback(y int, f func(int, int)) {
  	f(y, 2) // this becomes Add(1, 2)
  }
 ```
 
### 闭包
 * 当我们不希望给函数起名字的时候，可以使用匿名函数。例如：func(x, y int) int { return x + y }。
 * 可以被赋值于某个变量，即保存函数的地址到变量中：fplus := func(x, y int) int { return x + y }，
 然后通过变量名对函数进行调用：fplus(3,4)。
 * 可以直接对匿名函数进行调用：func(x, y int) int { return x + y }(3, 4)。