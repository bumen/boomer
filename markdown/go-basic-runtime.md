## go基础-执行

### main调用过程
 1. 按顺序导入所有被 main 包引用的其它包，然后在每个包中执行如下流程：
 2. 如果该包又导入了其它的包，则从第一步开始递归执行，但是每个包只会被导入一次。
 3. 然后以相反的顺序在每个包中初始化常量和变量，如果该包含有 init 函数的话，则调用该函数。
 4. 在完成这一切之后，main 也执行同样的过程，最后调用 main 函数开始执行程序。