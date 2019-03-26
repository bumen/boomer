
## go基础-结构体
 * 类似class

### struct
 * 定义
  ``` 
    type struct_variable_type struct {
       member definition;
       member definition;
       ...
       member definition;
    }
  ```
 * 变量的声明
 ``` 
  variable_name := structure_variable_type {value1, value2...valuen}
  或
  variable_name := structure_variable_type { key1: value1, key2: value2..., keyn: valuen}
 ```
 
### 访问结构成员
 * 结构体.成员名
 
### 结构体作为函数参数
 * 结构体是作为参数是值传递
   + 所以修改结构体中的变量值，不会影响调用结构体
   + 如果要改变需要使用传递结构体指针
 
### 结构体指针
 * var struct_pointer *Books
 * struct_pointer = &Books
 * 访问结构体成员
   + struct_pointer.title
   
### 接口
 * Go 语言提供了另外一种数据类型即接口，它把所有的具有共性的方法定义在一起，
 任何其他类型只要实现了这些方法就是实现了这个接口。
 * 定义
   ``` 
   type interface_name interface {
      method_name1 [return_type]
      method_name2 [return_type]
      ...
      method_namen [return_type]
   }
   /* 定义结构体 */
   type struct_name struct {
      /* variables */
   }
   /* 实现接口方法 */
   func (struct_name_variable struct_name) method_name1() [return_type] {
      /* 方法实现 */
   }
   ```
 * 例子
   ``` 
   type Phone interface {
       call()
   }
   type NokiaPhone struct {
   }
   func (nokiaPhone NokiaPhone) call() {
       fmt.Println("I am Nokia, I can call you!")
   }
    var phone Phone
    phone = new(NokiaPhone)
    phone.call()
   ```