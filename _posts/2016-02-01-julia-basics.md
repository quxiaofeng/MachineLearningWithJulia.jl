---
layout: post
title: "Julia 基础"
date: 2016-02-01 21:15:18
backgrounds:
    - /assets/images/backgrounds/mbmlbookcover.png
thumb: /assets/images/thumbs/julia-logo.png
category: julia
tags: julia viarable type function REPL
---

## 安装 ##

到[官网下载页面 (JuliaLang.org/downloads) ](http://julialang.org/downloads/)下载支持所用平台的版本，然后安装。

## 运行 （REPL） ##

执行 Julia 的控制台界面如下。

![]({{ "/assets/images/julia-repl.png" | prepend: site.baseurl | prepend: site.url }})

显示版本、平台和 `julia>` 提示符。在提示符后面可以运行 Julia 代码。

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

{% highlight julia %}
Pkg.update()
Pkg.add("IJulia")
{% endhighlight %}

#### 运行 ####

{% highlight julia %}
using IJulia
notebook()
{% endhighlight %}

运行新建窗口如下

![]({{ "/assets/images/jupiter-new.png" | prepend: site.baseurl | prepend: site.url }})

### 变量 ###

简单说，基本变量跟 MATLAB 使用方式一样。变量的类型不是强制使用的。

额外的优点是：可以使用 unicode 字符作为变量名。包括数学常用的希腊字母和中文。前者方便直接使用数学语言写数学相关的程序；后者方便中文读者日常使用。

![]({{ "/assets/images/julia-viarable-example.jpg" | prepend: site.baseurl | prepend: site.url }})

### 控制逻辑 ###

支持基本的 if-else，for。但也可以完全不用 if-else。

### 函数 ###

函数的声明可以使用完整声明，也可以用类似隐函数的方式使用。

![]({{ "/assets/images/julia-function-example.jpg" | prepend: site.baseurl | prepend: site.url }})

## Julia 语言的优点 ##

数学表达能力强，原生支持各种矩阵、向量运算。各种功能的正交组合甚至超过了 MATLAB。例如： MATLAB 矩阵运算中，可以和`.`搭配的运算符很有限，`.*` (Element-wise multiplication), `.^` (Element-wise power), `./` (Right array division), `.\` (Left array division), `.'` (Array transpose)。Julia 语言中，运算符与 `.` 的搭配就很正交，几乎所有运算符都可以加上 `.` 运算符，变成 elementwise （元素对元素的）运算符。

具有伟大的性能提升的潜力。性能极限接近 C 语言。原因很简单，对于变量的数据类型，可以不指定来自动推断，也可以手动指定。手动指定变量类型之后的速度，基本就等价于 C。当使用自动类型推断的时候，可以像 Python 或者 MATLAB 一样快速开发原型。当手动指定类型之后，可以用近乎 C 一般的速度去跑生产代码。

语言年轻，且去中心化。2015年4月9日的版本是 `0.3.7`，还没有到 `1.0`，各种语言特性都在剧烈变动中。比 C 语言还快的原因有两方面：A. 可以利用 C 语言发明以来最新的业界经验和科研成果。B. 整个 Julia 语言的基础是基于 GitHub 开源的，保证了语言的开放性。又由于有足够多学术界的关注，最新的学界成果得以引入 Julia 语言中。

直接调用 C， Python， 和 R。C 调用这个算是现代语言的基本功能，但 Julia 做得很舒服。无需配置，直接用ccall。格式如下，`ccall((：函数名，“指定C库文件”)，返回值类型，（输入参数数据类型），输入参数)`。[PyCall](https://github.com/stevengj/PyCall.jl) （stevengj/PyCall.jl · GitHub）得说是很流氓的。例如：绘图包 [PyPlot](https://github.com/stevengj/PyPlot.jl) （stevengj/PyPlot.jl · GitHub）。一连几年 julia 都一直在 PyCon 上做宣传。同样邪恶的还有 [RCall](https://github.com/JuliaStats/RCall.jl) (JuliaStats/RCall.jl · GitHub)。

对于 MATLAB 用户，Julia 也是极为友好。首先是 Julia 的语法本身就是面向数学的，与 MATLAB 极为相似，甚至可以一句对一句的翻译。JuliaLang 也有个包叫 [MATLAB.jl](https://github.com/JuliaLang/MATLAB.jl) (JuliaLang/MATLAB.jl · GitHub)，支持直接调用 MATLAB，最大限度的保护你的智力投资。脱离 MATLAB 之后，如果有依赖于 MATLAB 的历史数据，也可以使用 [`MAT.jl` 包](https://github.com/simonster/MAT.jl)来读写 `.mat` 文件。

原生的单元测试支持。默认程序包开发的格式中，就内置了测试架构。语言内置单元测试宏 `@test`。其实这里稍差一点，还没有对于行为驱动开发 （BDD）的原生支持。这一点可能在我看懂 [FactCheck.jl](https://github.com/julialang/factcheck.jl) （JuliaLang/FactCheck.jl · GitHub）之后再进一步修改。

方便自由的程序包开发。只要在 GitHub 上开一个 `.jl` 结尾的代码库，然后按照指定格式提交 `METADATA` 给 `JuliaLang`。就可以把自己开发的包提交到 Julia 官方库。很少有哪个语言的委员会这么亲民的，TeXLive 还得是每年升级呢。程序包是否受官方包管理器支持对于成果推广的价值是无法估量的。

有一个类似 IPython 的极为友好的基于 WEB 的 IDE - IJulia。而且 IPython 的下一版直接改名 Jupiter，原因就是对于 Julia、Python 和 R 的全面支持。

## 示例 ##

问题：打印1-100中可被2和3整除的数的總和

### 数学计算法 ###

直接根据先验知识计算。可以把 Julia 直接当作科学计算器，类似 MATLAB 的语法，很友好。

{% highlight julia %}
sum(6:6:100)
{% endhighlight %}

### 循环 + 条件判断法 ###

+ version 1

循序渐进的循环、判断和计算。

{% highlight julia %}
Σ = 0
for x in 1:100 
  if x%2 == 0 && x%3 == 0
    Σ += x
  end
end
println("Σ: $Σ")
{% endhighlight %}

+ version 2

直接在循环体外，根据条件筛选循环变量。

{% highlight julia %}
Σ = 0
for x in filter(x -> x%2 == 0 && x%3 == 0, 1:100)
  Σ += x
end
println("Σ: $Σ")
{% endhighlight %}

+ version 3

一行流。其中 `filter` 与 `find` 是等价的函数。

{% highlight julia %}
println("Σ: $(sum(filter(x -> x%2 == 0 && x%3 == 0, 1:100)))")
{% endhighlight %}

or

{% highlight julia %}
println("Σ: $(sum(find(x -> x%2 == 0 && x%3 == 0, 1:100)))")
{% endhighlight %}

### 外调 Python 法 ###

他山之石可以攻玉。除 Python 外，Julia 也支持调用 C、R、Java、MATLAB 代码。

{% highlight julia %}
using PyCall
pyeval("sum([x for x in xrange(101) if x%2==0 and x%3==0])")
{% endhighlight %}

### 三元表达式 ###

三元表达式结合后置条件循环。

{% highlight julia %}
sum([x%2 == 0 && x%3 == 0 ? x : 0 for x = 1:100])
{% endhighlight %}

### 函数替换版 ###

Julia 可以使用各种 unicode 字符作为函数名。便于学术上数学公式与代码的一一对应。也可以在代码中写一些奇奇怪怪的东西。

{% highlight julia %}
Σ = sum
select = find
println("Σ: $(Σ(select(x -> x%2 == 0 && x%3 == 0, 1:100)))")
{% endhighlight %}

### MATLAB 语法版 ### 

可以对矩阵直接做矢量运算。但速度还是不如直接写循环。好处是可以简化建模时间。可以先以正确性为优先，直接使用数学语言写代码，接下来根据 `profile` 结果，有选择的优化。

{% highlight julia %}
testrange = [1:100]
sum(testrange[(testrange % 2 .== 0) & (testrange % 3 .== 0)])
{% endhighlight %}

### 管道版 ###

可以轻松的使用管道来写链式的程序。

{% highlight julia %}
[1:100] |> set -> filter(i -> i%2 == 0 && i%3 == 0, set) |> sum
{% endhighlight %}

PS. Julia 还没有实现 conditional list comprehension ([https://github.com/JuliaLang/julia/issues/550](https://github.com/JuliaLang/julia/issues/550))，实在是很遗憾啊。期待 1.0 版的发布。


## 练习 ##

一本书 168 页 问页码中 1、3、5、7、9 共出现多少次？答案分别是：106、37、37、27、26。

完整统计

{% highlight julia %}
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
{% endhighlight %}

Python3

{% highlight python %}
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
{% endhighlight %}

一行流

Map + 管道

{% highlight julia %}
map('1':2:'9') do i filter(x->x==i, reduce(string, 1:168)) |> length end

5-element Array{Int64,1}:
 106
  37
  37
  27
  26
{% endhighlight %}

list comprehension

{% highlight julia %}
result = [i=>length(filter(x->x=='0'+i, reduce(string, 1:168))) for i in 1:2:9]

Dict{Int64,Any} with 5 entries:
  7 => 27
  9 => 26
  3 => 37
  5 => 37
  1 => 106

result[1]
106
{% endhighlight %}

字符串字典

{% highlight julia %}
result = [i=>length(filter(x->x==i, reduce(string, 1:168))) for i in '1':2:'9']

Dict{Char,Any} with 5 entries:
  '7' => 27
  '5' => 37
  '1' => 106
  '3' => 37
  '9' => 26

result['1']
106
{% endhighlight %}

并行版

{% highlight julia %}
@parallel vcat for i='1':2:'9' filter(x->x==i, reduce(string, 1:168)) |> length end

5-element Array{Int64,1}:
 106
  37
  37
  27
  26
{% endhighlight %}

C 语言版

{% highlight c %}
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
{% endhighlight %}

## 为什么要用 Julia

作者： Micheal Murphy

原链接见 https://mmstickman.wordpress.com/programming/julia/

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

{% highlight julia %}
open(readall, "file.txt") # 在文件上运行一个函数
open("file.txt", "a") # 打开一个文件，在文件末尾追写
open("file.txt") # 只读方式打开一个文件
{% endhighlight %}

   + 灵活地类型推导

{% highlight julia %}
square(x) = x * x
square(5) # 可以用整形参数
25
square(5.5) # 也可以用浮点参数
30.25
{% endhighlight %}

   + 为新参数类型定义新函数

{% highlight julia %}
square(array::Array) = map(x->x*x, array)
square([1, 2, 3, 4, 5])
5-element Array{Int64,1}:
  1
  4
  9
 16
 25
{% endhighlight %}

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
