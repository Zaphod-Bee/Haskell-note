### Haskell-1 基础与基本数据类型

[TOC]



#### 概述

- 函数式程序语言

- 论坛：Freenode IRC #Haskell、StackOverflow #Haskell

- 打开cmd，输入ghci，出现提示语Prelude


#### ghci下的操作

##### 普通操作

1. 计算时用到负数请用括号括起来
2. 运算符：&&、||、not、==、/=
3. 整数可以被看成浮点数，反过来不行。
4. 用let定义常量，例：>let a = 1与在脚本中编写a=1等价

##### 运行操作

1. ghci
2. :l title.hs
3. 运行函数

#### 函数

1. 前缀函数：如succ(successor后继)

```haskell
>succ 8
9
```

2. 中缀函数：如*

3. Haskell中用空格将函数/参数分割

4. 函数调用有最高优先级：succ 9*10 先调用的是succ 9。

5. 声明函数：

   ```haskell
   doubleMe x = x + x
   ```


6. 函数里可以包含自己写的函数
7. 函数不分顺序，可以打乱次序声明
8. 函数名不允许首字母大写

#### if-else语句

else不可省略

#### 数组

##### 数组拼接

数组与数组 使用++
元素与数组 使用：

```haskell
 >5:[1,2,3]
 [5,1,2,3]
```
- 如果++前数组很长，遍历就需要较长时间。建议往数组前端插入元素。

##### 数组索引！！

```haskell
>"Steve Rogers" !! 6
'R'
```

初始下标为1

##### 数组的比较> < ==

如果可以比较，则比较

##### 数组首元素、末元素与尾部、头部。数组自由截取

```haskell
>head [1,2,3]
1
>tail [1,2,3]
[2,3]
>last [1,2,3]
3
>init [1,2,3]
[1,2]
>take 2 [1,2,3]
[1,2]
>drop 2 [1,2,3]
3
```

不允许用于空数组

##### 其余操作

```haskell
>length [1,2,3]
3
>null [1,2,3]
False
>reverse [1,2,3]
[3,2,1]
>maximum [1,2,3]
3
>minimum [1,2,3]
1
>sum [1,2,3]
6
>product [1,2,3]
6
>4 `elem` [1,2,3]
False
```

注：elem判断一个元素是否存在于某数组。

#### 数组的构造

##### 使用let定义

```haskell
>let lostNumbers=[1,2,3]
```

##### RANGE/REPEAT

```haskell
>[1..4]
[1,2,3,4]
>['A'..'D']
[A,B,C,D]
>[1,4..10]
[1,4,7,10]
```

注：

- RANGE可以构造步长，需要写出前两位。

- RANGE避免使用浮点数。

- 无限LIST

  ```haskell
  >take 5 [12,24..]
  [12,24,36,48,60]
  ```

```haskell
>take 10(repeat 5)
[5,5,5,5,5]
>replicate 3 10
[10,10,10]
```

##### LIST COMPREHENSION，过滤

说明：
$$
S = \{2\cdot x\quad|\quad x\in N, \quad x\leq 10\}
$$

```haskell
>[x*2|x<-[1..10],x*2<=14]
[2,4,6,8,10,12,14]
```

###### 练习1：取50到100之间所有除以7余数为3的元素

```haskell
>[x|x<-[50..100],x `mod` 7 ==3]
[52,59,66,73,80,87,94]]
```

注：mod需要引起来。

###### 练习2：使LIST中大于10的奇数变为‘BANG'，小于10的奇数变为’BOOM'，其他扔掉。

```haskell
boomBangs xs = [if x < 10 then "BOOM!" else "BANG" | x <- xs, odd x]
>boomBangs [9,11]
["BOOM!","BANG!"]
```

###### 练习3：取一个包含形容词+名词的LIST COMPREHENSION

```haskell
>let adj = ["calm","lucky","purple"]
>let noun = ["Keanu Reeves","nuts","UN"]
>[x++" "++y|x<-adj,y<-noun]
["calm Keanu Reeves","calm nuts","calm UN","lucky Keanu Reeves","lucky nuts","lucky UN","purple Keanu Reeves","purple nuts","purple UN"]
```

###### 练习4：嵌套LIST——除去所有奇数

```haskell
>let xxs = [[1,2,3],[3,4,5],[4,5,6]]
>[[x|x<-xs,even x]|xs<-xxs]
[[2],[4],[4,6]]
```



##### 编写函数

###### 练习1：编写一个除去字符串中所有非大写字母的函数

```haskell
removeNonUp st = [x|x<-st,x `elem` ['A'..'Z']]
>removeNonUp "Cycle Per Instruction"
"CPI"
```

#### 元组Tuple

##### 区分于数组

- 元组固定了元素个数
- 元组中的项不必为同一类型
- 元组用( )括起
- 二元元组可以理解为序对

##### 元组的操作

###### fst与snd（仅用于序对）

```haskell
>fst (8,11)
8
>snd (8,11)
11
```

###### zip——生成序对

```haskell
>zip [1,2,3] [2,3,4]
[(1,2),(2,3),(3,4)]
```

###### 练习1：取所有边长为整数且小于等于10，周长为24的直角三角形。

```haskell
>let tri = [(a,b,c)|a<-[1..10],b<-[1..a],c<-[1..b],b^2+c^2==a^2,a+b+c==24]
>tri
[(10,8,6)]
```

