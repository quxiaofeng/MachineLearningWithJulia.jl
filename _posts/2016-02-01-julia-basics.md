---
layout: post
title: "Julia 基础"
date: 2016-02-01 21:15:18
backgrounds:
    - /assets/images/backgrounds/kazakhstan-korgalzhyn.jpg
thumb: /assets/images/thumbs/julia-logo.jpg
category: julia
tags: julia viarable type function REPL
---

## 目录 ##

1. [Julia 的安装与运行](#section-1)
2. Julia 语言基础
3. Jupyter 与 Juno 开发环境
3. [Julia 语言评价](#julia-)
4. [Julia 示例一](#section-8)
5. [Julia 示例二](#section-14)
6. [为什么要用 Julia（一篇翻译的文章）](#julia)

## 安装 ##

到[官网下载页面 (JuliaLang.org/downloads) ](http://julialang.org/downloads/)下载支持所用平台的版本，然后安装。

## 运行 （REPL） ##

执行 Julia 的控制台界面如下。

**Julia Version 0.3.7**
![]({{ "/assets/images/julia-repl.png" | prepend: site.url }})
**Julia Version 0.4.5**
![]({{ "/assets/images/julia-repl-045.png" | prepend: site.url }})

显示版本、平台和 `julia>` 提示符。在提示符后面可以运行 Julia 代码。根据版本不同，显示的版本号可能不一样。

## Julia 语言基础 ##

### 基本数据类型 ###

简单说，变量跟 MATLAB 使用方式一样，不需要声明，可以直接使用。 `#` 开始是注释。

```julia
julia> a = 3 # 默认数字是整形数 `Int64`
3

julia> typeof(a) # 查询变量类型可以使用 `typeof()` 函数
Int64

julia> b = a + 2.2 # 自动类型提升到浮点数 `Float64`
5.2

julia> typeof(b)
Float64
```

常用基本数据类型包括：`Int64` 整形数, `Float64` 浮点数, `Complex{Int64}` 复数, `Rational{Int64}` 有理数。

```julia
julia> 2 + 1im # Complex{Int64}
2 + 1im

julia> 2//3 # Rational{Int64}
2//3
```

### 基本运算 ###

基本运算：`+` 加, `-` 减, `*` 乘, `/` 除, `div()` 整除, `\` 左除, `^` 乘方, `%` 求余；调整优先级用 `(a + b)`。虽然运算符有优先级，但要清晰，不要依赖，才是最佳实践。 

```julia
julia> 24/6 # 除法默认是浮点数，哪怕能整除也是浮点数
4.0

julia> 5/6
0.8333333333333334

julia> div(7, 3) # 如果需要求整除结果，可以使用 `div()` 函数
2

julia> 3 ÷ 2 # 也可以使用 Unicode 除法符号 `÷`。这个符号在 REPL 中可以通过 `\div + <tab>` 来输入。
1

julia> 3 \ 8 # 左除就是左边是除数，右边是被除数
2.6666666666666665
```

### 变量 ###

变量的类型不是强制使用的。

额外的优点是：可以使用 unicode 字符作为变量名。包括数学常用的希腊字母和中文。前者方便直接使用数学语言写数学相关的程序；后者方便中文用户在日常脚本中使用。

### 控制逻辑 ###

支持基本的 if-else，for。但也可以完全不用 if-else。

### 函数 ###

函数的声明可以使用完整声明，也可以用类似隐函数的方式使用。

![]({{ "/assets/images/julia-function-example.jpg" | prepend: site.url }})


## GitHub 上 Julia 语言的学习代码 ##

+ [https://github.com/samuelcolvin/JuliaByExample](https://github.com/samuelcolvin/JuliaByExample)
+ [https://github.com/chrisvoncsefalvay/learn-julia-the-hard-way](https://github.com/chrisvoncsefalvay/learn-julia-the-hard-way)
+ [https://github.com/chezou/julia-100-exercises](https://github.com/chezou/julia-100-exercises)
+ [https://github.com/Aerlinger/JuliaExamples](https://github.com/Aerlinger/JuliaExamples)

## IJulia 及 Julia 变量、控制逻辑与函数 ##

### IJulia ###

#### 依赖 ####

1. Anaconda Python
2. IPython (Jupiter)

#### 安装 ####

```julia
Pkg.update()
Pkg.add("IJulia")
```

#### 运行 ####

```julia
using IJulia
notebook()
```

运行新建窗口如下

![]({{ "/assets/images/jupiter-new.png" | prepend: site.url }})


一个简单的例子

![]({{ "/assets/images/julia-viarable-example.jpg" | prepend: site.url }})

## Julia 语言的优点 ##

数学表达能力强，原生支持各种矩阵、向量运算。各种功能的正交组合甚至超过了 MATLAB。例如： MATLAB 矩阵运算中，可以和`.`搭配的运算符很有限，`.*` (Element-wise multiplication), `.^` (Element-wise power), `./` (Right array division), `.\` (Left array division), `.'` (Array transpose)。Julia 语言中，运算符与 `.` 的搭配就很正交，几乎所有运算符都可以加上 `.` 运算符，变成 elementwise （元素对元素的）运算符。

具有伟大的性能提升的潜力。性能极限接近 C 语言。原因很简单，对于变量的数据类型，可以不指定来自动推断，也可以手动指定。手动指定变量类型之后的速度，基本就等价于 C。当使用自动类型推断的时候，可以像 Python 或者 MATLAB 一样快速开发原型。当手动指定类型之后，可以用近乎 C 一般的速度去跑生产代码。

语言年轻，且去中心化。2015年4月9日的版本是 `0.3.7`，还没有到 `1.0`，各种语言特性都在剧烈变动中。比 C 语言还快的原因有两方面：A. 可以利用 C 语言发明以来最新的业界经验和科研成果。B. 整个 Julia 语言的基础是基于 GitHub 开源的，保证了语言的开放性。又由于有足够多学术界的关注，最新的学界成果得以引入 Julia 语言中。

直接调用 C， Python， 和 R。C 调用这个算是现代语言的基本功能，但 Julia 做得很舒服。无需配置，直接用ccall。格式如下，`ccall((：函数名，“指定C库文件”)，返回值类型，（输入参数数据类型），输入参数)`。[PyCall](https://github.com/stevengj/PyCall.jl) （stevengj/PyCall.jl · GitHub）得说是很流氓的。例如：绘图包 [PyPlot](https://github.com/stevengj/PyPlot.jl) （stevengj/PyPlot.jl · GitHub）。一连几年 julia 都一直在 PyCon 上做宣传。同样邪恶的还有 [RCall](https://github.com/JuliaStats/RCall.jl) (JuliaStats/RCall.jl · GitHub)。

[C++ REPL](https://github.com/Keno/Cxx.jl#user-content-the-c-repl)。使用 `Cxx.jl` 可以直接解释执行 `C++` 代码。例如：

```julia
# include headers
julia> using Cxx
julia> cxx""" #include<iostream> """  

# Declare the function
julia> cxx"""  
         void mycppfunction() {   
            int z = 0;
            int y = 5;
            int x = 10;
            z = x*y + 2;
            std::cout << "The number is " << z << std::endl;
         }
      """
# Convert C++ to Julia function
julia> julia_function() = @cxx mycppfunction()
julia_function (generic function with 1 method)

# Run the function
julia> julia_function()
The number is 52
```

PS.暂时还不支持 `windows` 平台。

对于 MATLAB 用户，Julia 也是极为友好。首先是 Julia 的语法本身就是面向数学的，与 MATLAB 极为相似，甚至可以一句对一句的翻译。JuliaLang 也有个包叫 [MATLAB.jl](https://github.com/JuliaLang/MATLAB.jl) (JuliaLang/MATLAB.jl · GitHub)，支持直接调用 MATLAB，最大限度的保护你的智力投资。脱离 MATLAB 之后，如果有依赖于 MATLAB 的历史数据，也可以使用 [`MAT.jl` 包](https://github.com/simonster/MAT.jl)来读写 `.mat` 文件。

原生的单元测试支持。默认程序包开发的格式中，就内置了测试架构。语言内置单元测试宏 `@test`。其实这里稍差一点，还没有对于行为驱动开发 （BDD）的原生支持。这一点可能在我看懂 [FactCheck.jl](https://github.com/julialang/factcheck.jl) （JuliaLang/FactCheck.jl · GitHub）之后再进一步修改。

方便自由的程序包开发。只要在 GitHub 上开一个 `.jl` 结尾的代码库，然后按照指定格式提交 `METADATA` 给 `JuliaLang`。就可以把自己开发的包提交到 Julia 官方库。很少有哪个语言的委员会这么亲民的，TeXLive 还得是每年升级呢。程序包是否受官方包管理器支持对于成果推广的价值是无法估量的。

有一个类似 IPython 的极为友好的基于 WEB 的 IDE - IJulia。而且 IPython 的下一版直接改名 Jupiter，原因就是对于 Julia、Python 和 R 的全面支持。

## 示例 一 ##

问题：打印1-100中可被2和3整除的数的總和。

### 数学计算法 ###

直接根据先验知识计算。可以把 Julia 直接当作科学计算器，类似 MATLAB 的语法，很友好。

```julia
sum(6:6:100)
```

### 循环 + 条件判断法 ###

+ version 1

循序渐进的循环、判断和计算。

```julia
Σ = 0
for x in 1:100 
  if x%2 == 0 && x%3 == 0
    Σ += x
  end
end
println("Σ: $Σ")
```

+ version 2

直接在循环体外，根据条件筛选循环变量。

```julia
Σ = 0
for x in filter(x -> x%2 == 0 && x%3 == 0, 1:100)
  Σ += x
end
println("Σ: $Σ")
```

+ version 3

一行流。其中 `filter` 与 `find` 是“等价”的函数。

```julia
println("Σ: $(sum(filter(x -> x%2 == 0 && x%3 == 0, 1:100)))")
```

or

```julia
println("Σ: $(sum(find(x -> x%2 == 0 && x%3 == 0, 1:100)))")
```

PS. 只是在这个例子中 `find` 与 `filter` 等价。根据 `julia` 的文档，[`find` 只用于 `Array`](http://docs.julialang.org/en/latest/stdlib/arrays/#Base.find)，按照 `Base.find (Julia function, in Arrays)` 格式调用；而 `filter` 则强大得多，作为函数式编程的一个常见元素，根据[文档](http://docs.julialang.org/en/latest/stdlib/collections/#Base.filter)，可以按照 `Base.filter (Julia function, in Collections and Data Structures)` 格式调用。

### 外调 Python 法 ###

他山之石可以攻玉。除 Python 外，Julia 也支持调用 C、R、Java、MATLAB 代码。

**Python 2**

```julia
using PyCall
pyeval("sum([x for x in xrange(101) if x%2==0 and x%3==0])")
```

**Python 3**

```julia
using PyCall
pyeval("sum([x for x in range(100) if x%2==0 and x%3==0])")
```

### 三元表达式 ###

三元表达式结合后置条件循环。

```julia
sum([x%2 == 0 && x%3 == 0 ? x : 0 for x = 1:100])
```

### 函数替换版 ###

Julia 可以使用各种 unicode 字符作为函数名。便于学术上数学公式与代码的一一对应。也可以在代码中写一些奇奇怪怪的东西。

```julia
Σ = sum
select = find
println("Σ: $(Σ(select(x -> x%2 == 0 && x%3 == 0, 1:100)))")
```

### MATLAB 语法版 ### 

可以对矩阵直接做矢量运算。但速度还是不如直接写循环。好处是可以简化建模时间。可以先以正确性为优先，直接使用数学语言写代码，接下来根据 `profile` 结果，有选择的优化。

```julia
testrange = 1:100
sum(testrange[(testrange % 2 .== 0) & (testrange % 3 .== 0)])
```

### 管道版 ###

可以轻松的使用管道来写链式的程序。

```julia
1:100 |> set -> filter(i -> i%2 == 0 && i%3 == 0, set) |> sum
```

PS. Julia 还没有实现 conditional list comprehension ([https://github.com/JuliaLang/julia/issues/550](https://github.com/JuliaLang/julia/issues/550))，实在是很遗憾啊。期待 1.0 版的发布。


## 示例 二 ##

一本书 168 页。问页码中 1、3、5、7、9 几个数字都出现多少次？

> 答案分别是：106、37、37、27、26。

完整统计

```julia
a=Dict()

for i in 1:168
    for j in bytestring("$i")
        a[j] = if haskey(a, j) a[j] + 1 else 1 end
    end
end

[a['1'], a['3'], a['5'], a['7'], a['9']]

5-element Array{Int64,1}:
 106
  37
  37
  27
  26
```

Python3

```python
from collections import Counter
cnt = Counter()
for num in range(169): cnt += Counter(str(num))
cnt

Counter({'0': 27,
         '1': 106,
         '2': 37,
         '3': 37,
         '4': 37,
         '5': 37,
         '6': 36,
         '7': 27,
         '8': 27,
         '9': 26})
```

一行流

Map + 管道

```julia
map('1':2:'9') do i filter(x->x==i, reduce(string, 1:168)) |> length end

5-element Array{Int64,1}:
 106
  37
  37
  27
  26
```

list comprehension

```julia
result = [i=>length(filter(x->x=='0'+i, reduce(string, 1:168))) for i in 1:2:9]

Dict{Int64,Any} with 5 entries:
  7 => 27
  9 => 26
  3 => 37
  5 => 37
  1 => 106

result[1]
106
```

字符串字典

```julia
result = [i=>length(filter(x->x==i, reduce(string, 1:168))) for i in '1':2:'9']

Dict{Char,Any} with 5 entries:
  '7' => 27
  '5' => 37
  '1' => 106
  '3' => 37
  '9' => 26

result['1']
106
```

并行版

```julia
@parallel vcat for i='1':2:'9' filter(x->x==i, reduce(string, 1:168)) |> length end

5-element Array{Int64,1}:
 106
  37
  37
  27
  26
```

C 语言版

```c
#include <stdio.h>

int main()
{
    unsigned count[10] = {0};
    unsigned temp = 0;
    for (unsigned i = 1; i <= 168; ++i) {
        temp = i;
        while (temp > 0) {
            ++count[temp % 10];
            temp /= 10;
        }
    }
    for (unsigned i = 0; i < 10; ++i)
        printf("%d occurs %d times\n", i, count[i]);
    return 0;
}
```

## 为什么要用 Julia

作者： [Micheal Murphy](https://mmstickman.wordpress.com/about/)

翻译： [曲晓峰](http://www.quxiaofeng.me/about)

原文见 [https://mmstickman.wordpress.com/programming/julia/](https://mmstickman.wordpress.com/programming/julia/)

Julia 是一个简洁高速，让我十分喜爱的编程语言。Julia 融合了脚本语言与编译语言。Julia 的代码按照脚本语言的方式编写，但运行时使用 Just In Time （JIT） LLVM 自动编译。使用这种方法，Julia 脚本可以像 C 一样快。

为什么要用 Julia

+ Julia 是教育初学者的完美编程语言

  + 语法甚至比 Python 还简单

  + 优良的函数式编程教学工具

  + 也是个完美的泛型编程的例子

  + 同时，完美的命令式编程

  + Julia 的元编程同样异常强大

  + 表达数学概念的完美语言

+ 与 C 一样快，甚至更快

  + Julia 包含最好的 Fortran 和 C 线性算法库、随机数生成、信号处理和字符串处理。

  + 使用 LLVM JIT 编译，拥有编译语言的性能

+ 专为技术（科学、数值）计算设计

  + 广泛的优化的高数值精度数学函数

  + 与 IPython （Jupiter，译者注）的集成提供了图形化的笔记本接口，以便绘制图表。

+ 像 Python 一样，支持 REPL，可以交互式编写代码

  + REPL 表示读入、执行、输出、循环

  + REPL 可以立即执行并即时显示

+ 泛型编程是头等公民

  + 很多标准库函数都充分利用了泛型编程，例如：

```julia
open(readall, "file.txt") # 在文件上运行一个函数
open("file.txt", "a") # 打开一个文件，在文件末尾追写
open("file.txt") # 只读方式打开一个文件
```

   + 灵活地类型推导

```julia
square(x) = x * x
square(5) # 可以用整形参数
25
square(5.5) # 也可以用浮点参数
30.25
```

   + 为新参数类型定义新函数

```julia
square(array::Array) = map(x->x*x, array)
square([1, 2, 3, 4, 5])
5-element Array{Int64,1}:
  1
  4
  9
 16
 25
```

+ 多重分发：鼓励重载函数

  + 接受不同参数的函数可以使用相同的函数名

  + 根据参数自动选择正确的函数

+ [针对元编程的优先支持](http://docs.julialang.org/en/latest/manual/metaprogramming/#macros)

+ [针对并行计算和分布式计算的设计；并支持协程](http://docs.julialang.org/en/latest/manual/parallel-computing/)

  + 编写并行代码相对简单

  + 如果线程太重，可以用协程

+ [强大的类似控制台的能力，可以读写外部程序](http://docs.julialang.org/en/latest/manual/running-external-programs/)

  + 可以操作其他程序的标准输出 stdout 和标准输入 stdin


+ 支持直接调用 [C](http://docs.julialang.org/en/latest/manual/calling-c-and-fortran-code/) 和 [Python](https://github.com/stevengj/PyCall.jl) 函数

  + 很多科学计算库是用 C 写的

  + 标准库充分利用了 C 和 Fortran 库

  + 让程序直接与 C 对话是水到渠成的

+ [采用模块式（module）的包管理系统](http://docs.julialang.org/en/latest/manual/modules/)

  + 包管理系统可以直接导入 Julia 模块

  + 使用包资源，赋予程序强大的能力

+ 充分详实的文档

  + 文档对于任何编程语言来说都是极为重要的

  + Julia 的文档涵盖所有主题，并深入细致

  + 对于没有编程经验的人也很容易理解

+ [一份关于 Map, Filter, and Reduce 的简明教程](https://mmstickman.wordpress.com/programming/julia/map-filter-and-reduce/)

+ [在线练习 Julia](http://www.tutorialspoint.com/)
