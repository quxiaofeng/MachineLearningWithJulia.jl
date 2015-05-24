---
layout: post
title: "Julia 基础"
date: 2015-01-09
backgrounds:
    - /assets/images/gadfly-demo.png
thumb: /assets/images/julia-logo.png
category: julia
tags: julia viarable type function REPL
---

## 安装 ##

到[官网下载页面 (JuliaLang.org/downloads) ](http://julialang.org/downloads/)下载支持所用平台的版本，然后安装。

## 运行 （REPL） ##

执行 Julia 的控制台界面如下。

![](/assets/images/julia-repl.png)

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

{% highlight julia%}

Pkg.update()

Pkg.add("IJulia")

{% endhighlight %}

#### 运行 ####

{% highlight julia %}

using IJulia

notebook()

{% endhighlight %}

运行新建窗口如下

![](/assets/images/jupiter-new.png)

### 变量 ###

### 控制逻辑 ###

### 函数 ###

![](/assets/images/julia-function-example.jpg)

## Julia 语言的优点 ##

数学表达能力强，原生支持各种矩阵、向量运算。各种功能的正交组合甚至超过了 MATLAB。例如： MATLAB 矩阵运算中，可以和`.`搭配的运算符很有限，`.*` (Element-wise multiplication), `.^` (Element-wise power), `./` (Right array division), `.\` (Left array division), `.'` (Array transpose)。Julia 语言中，运算符与 `.` 的搭配就很正交，几乎所有运算符都可以加上 `.` 运算符，变成 elementwise （元素对元素的）运算符。

具有伟大的性能提升的潜力。性能极限接近 C 语言。原因很简单，对于变量的数据类型，可以不指定来自动推断，也可以手动指定。手动指定变量类型之后的速度，基本就等价于 C。当使用自动类型推断的时候，可以像 Python 或者 MATLAB 一样快速开发原型。当手动指定类型之后，可以用近乎 C 一般的速度去跑生产代码。

语言年轻，且去中心化。2015年4月9日的版本是 `0.3.7`，还没有到 `1.0`，各种语言特性都在剧烈变动中。比 C 语言还快的原因有两方面：A. 可以利用 C 语言发明以来最新的业界经验和科研成果。B. 整个 Julia 语言的基础是基于 GitHub 开源的，保证了语言的开放性。又由于有足够多学术界的关注，最新的学界成果得以引入 Julia 语言中。

直接调用 C， Python， 和 R。C 调用这个算是现代语言的基本功能，但 Julia 做得很舒服。无需配置，直接用ccall。格式如下，`ccall((：函数名，“指定C库文件”)，返回值类型，（输入参数数据类型），输入参数)`。[PyCall](https://github.com/stevengj/PyCall.jl) （stevengj/PyCall.jl · GitHub）得说是很流氓的。例如：绘图包 [PyPlot](https://github.com/stevengj/PyPlot.jl) （stevengj/PyPlot.jl · GitHub）。一连几年 julia 都一直在 PyCon 上做宣传。同样邪恶的还有 [RCall](https://github.com/JuliaStats/RCall.jl) (JuliaStats/RCall.jl · GitHub)。

对于 MATLAB 用户，Julia 也是极为友好。首先是 Julia 的语法本身就是面向数学的，与 MATLAB 极为相似，甚至可以一句对一句的翻译。JuliaLang 也有个包叫 [MATLAB.jl](https://github.com/JuliaLang/MATLAB.jl) (JuliaLang/MATLAB.jl · GitHub)，支持直接调用 MATLAB，最大限度的保护你的智力投资。脱离 MATLAB 之后，如果有依赖于 MATLAB 的历史数据，也可以使用 [`MAT.jl` 包](https://github.com/simonster/MAT.jl)来读写 `.mat` 文件。

原生的单元测试支持。默认程序包开发的格式中，就内置了测试架构。语言内置单元测试宏 `@test`。其实这里稍差一点，还没有对于行为驱动开发 （BDD）的原生支持。这一点可能在我看懂 [FactCheck.jl](https://github.com/julialang/factcheck.jl) （JuliaLang/FactCheck.jl · GitHub）之后再进一步修改。

方便自由的程序包开发。只要在 GitHub 上开一个 `.jl` 结尾的代码库，然后按照指定格式提交 `METADATA` 给 `JuliaLang`。就可以把自己开发的包提交到 Julia 官方库。很少有哪个语言的委员会这么亲民的，TeXLive 还得是每年升级呢。程序包是否受官方包管理器支持对于成果推广的价值是无法估量的。

有一个类似 IPython 的极为友好的基于 WEB 的 IDE - IJulia。而且 IPython 的下一版直接改名 Jupiter，原因就是对于 Julia、Python 和 R 的全面支持。