# Optimizer

2021-12-27
深度学习里面的优化器，这个问题被多次问到。一直答不好，归结一下原因是没有正儿八经做过深度的模型，没有用过TF。
今天稍微看了一下陈攀的模型代码，发现随处可见的Adam优化器，这个很难说不知道这个东西。只能说明没做过深度模型。

其实回想一下，这个当时看吴恩达的课程，都是学到的，可是如今全忘了，还是印证了那个说法，只有动手做才是做好的
学习方法，记忆深刻，只看书只看视频，记忆都不深刻，很容易忘记。没有在具体问题中遇到困难，就无法有深刻的印象
知道为什么需要这些概念，这些工具。


优化器可以分为两大类
- 第一类 优化过程中 学习率delta不受梯度影响，全程不变或者按照一定的learning schedule随时间变化，常见的有
SGD 随机梯度下降， 带Momentum的SGD， 带Nesterov的SGD，
- 第二类 优化过程中，学习率随着梯度自适应的改变，并尽可能去消除给定的全局学习率的影响，如Adagrad, Adam等，
可以称之为自适应学习率随

梯度下降三种常见变形

## BGD Batch Gradient Descent
每次使用整个训练集来计算cost function对参数的梯度

## SGD Stochastic Gradient Descent
和GD一次用所有的数据计算梯度相比不同，SGD每次更新时对每个样本进行梯度更新。
SGD更新频繁，造成cost function严重震荡，包含随机性，但从期望上来看，它是等于正确的导数的

## MBGD Mini-Batch Gradient Descent
每次利用一小批样本，即n个样本，可以降低参数更新时的方差，收敛更稳定。和SGD的区别是每一次循环不是作用于每个样本，而是具有
n个样本的批次
更新频繁，造成cost function严重震荡，包含随机性，但从期望上来看，它是等于正确的导数的

## Momentum
SGD在某些情况下容易卡住，加入一个超参数gamma * Vt-1，可以加速SGD且抑制震荡。可以理解为一个小球从山上滚下来，没有阻力的时候
动量越来越大，遇到阻力的时候的时候速度变小

自适应的优化器，就是学习率也会跟着变化
## Adam

## Adagrad


