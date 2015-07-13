---
layout: post
title: "模式分类"
date: 2015-07-13 15:17:47
backgrounds:
    - /assets/images/backgrounds/color-blocks.jpg
thumb: /assets/images/thumbs/f76dd2d487fb31bb503714753e320d24-ld.jpg
category: julia
tags: pattern classification
---

## SVM

调用 Python 的 scikit-learn 包的 SVM 代码。

{% highlight julia %}
 # julia "svmtest.jl"
using PyCall

@pyimport sklearn.svm as svm

X = [[0 0], [0 1], [1 0], [1 1]]
y = [0, 1, 2, 3]

clf = svm.LinearSVC()
clf[:fit](X, y)
dec = clf[:decision_function]([1.2 0.8])
println("$(dec[1,2])")
{% endhighlight %}

## DPL

Projective Dictionary Pair Learning 投影字典对学习算法 [[Github]](https://github.com/quxiaofeng/ProjectiveDictionaryPairLearning.jl)。

<div>
$$\min_{P,D}{\sum_{k=1}^K\|X_k-D_kP_kX_k\|_F^2}$$
</div>

<div>
$${P^*,D^*} = \arg\min_{P,D}{\sum_{k=1}^K\|X_k-D_kP_kX_k\|_F^2 +\lambda\|P_k\bar{X}_k\|_F^2}$$
$$s.t.\ \|d_i\|_2^2\leq 1$$
</div>

### 安装

{% highlight julia %}
Pkg.update(); Pkg.add("ProjectiveDictionaryPariLearning")
{% endhighlight %}

### 使用

#### 训练

{% highlight julia %}
DictMat, EncoderMat = TrainDPL(TrData, TrLabel, DictSize, τ, λ, γ)
{% endhighlight %}

#### 分类

{% highlight julia %}
PredictLabel, Error, Distance = ClassificationDPL(TtData, DictMat, EncoderMat, DictSize)
{% endhighlight %}