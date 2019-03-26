## go基础-错误处理

### 错误接口
 * Go 语言通过内置的错误接口提供了非常简单的错误处理机制
   ``` 
    type error interface {
        Error() string
    }
   ```
 * 函数通常在最后的返回值中返回错误信息。使用errors.New 可返回一个错误信息
   ``` 
    func Sqrt(f float64) (float64, error) {
        if f < 0 {
            return 0, errors.New("math: square root of negative number")
        }
        // 实现
    }
   ```
 * struct实现Error函数
 
### panic, recover

#### panic
 * 用于主动抛出错误
 * 触发panic
   + 一是程序主动调用
   + 二是程序产生运行时错误，由运行时检测并退出
   
 * 发生panic后，程序会从调用panic的函数位置或发生panic的地方立即返回，逐层向上执行函数的defer语句。
 然后逐层打印函数调用堆栈，直到被recover捕获或运行到最外层函数。
 
 * panic不但可以在函数正常流程中抛出，在defer逻辑里也可以再次调用panic或抛出panic。
 defer里面的panic能够被后续执行的defer捕获。
 
 * recover用来捕获panic，阻止panic继续向上传递。recover()和defer一起使用，
 但是defer只有在后面的函数体内直接被掉用才能捕获panic来终止异常，否则返回nil，异常继续向外传递。
 
#### recover
 * 用于捕获panic抛出的错误