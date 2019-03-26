## go基础-切片

### 切片
 * 语言切片是对数组的抽象
 *  数组的长度不可改变，在特定场景中这样的集合就不太适用。
 Go中提供了一种灵活，功能强悍的内置类型切片("动态数组"),与数组相比切片的长度是不固定的，可以追加元素，在追加时可能使切片的容量增大。
 
### 定义切片
 * var identifier []type
 * 切片不需要说明长度。
 * 使用make函数来创建切片
   + var slice1 []type = make([]type, len)
   + 简写为：slice1 := make([]type, len)
   + 也可以指定容量，其中capacity为可选参数。
     - make([]T, length, capacity)
     
### 切片初始化
 * s :=[] int {1,2,3 } 
   + 直接初始化切片，[]表示是切片类型，{1,2,3}初始化值依次是1,2,3.其cap=len=3
 * s := arr[:] 
   + 初始化切片s,是数组arr的引用
 * s := arr[startIndex:endIndex] 
   + 将arr中从下标startIndex到endIndex-1 下的元素创建为一个新的切片
 * s := arr[startIndex:] 
   + 缺省endIndex时将表示一直到arr的最后一个元素
 * s := arr[:endIndex] 
   + 缺省startIndex时将表示从arr的第一个元素开始
 * s1 := s[startIndex:endIndex] 
   + 过切片s初始化切片s1
 * s :=make([]int,len,cap) 
   + 通过内置函数make()初始化切片s,[]int 标识为其元素类型为int的切片
   
### len()与cap()函数
 * len
   + 获取切片长度
 * cap
   + 测量切片最长可以达到多少
   
### 空(nil)切片
 * 一个切片在未初始化之前默认为 nil，长度为 0
 
### 切片截取
 * 可以通过设置下限及上限来设置截取切片 [lower-bound:upper-bound]
   + 不包括upper-bound索引
   + number3 := numbers[2:5]
   
### append()与copy()函数
 * 如果想增加切片的容量，我们必须创建一个新的更大的切片并把原分片的内容都拷贝过来