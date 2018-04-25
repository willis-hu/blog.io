---
layout: post
title: softmax回归与逻辑斯蒂回归
date: 2018-04-25
categories: 机器学习
tags: [机器学习]
description: softmax回归与逻辑斯蒂回归
---

#### 一般应用场景

logistic回归一般用于二分类问题，对于多分类问题可以使用ovr的方法建立多个分类器进行分类，对输出结果进行投票，投票所属最高的类作为当前样本的类，另一种方法则是使用softmax回归，对于多个类别的概率值直接建立模型进行推到，并且由于softmax的概率计算公式可以同时缩减w倍而不改变概率值，因而sigmoid函数可以认为是softmax应用于二分类时的一种特殊书写方式。

#### softmax公式及其损失函数

对于样本 $x_i$以及它对应的类别 $y_i$，可以认为 $P(Y=j|X_i)$的计算公式为 $P(Y=j|X_i)= \frac{exp(\theta_j x_i)}{\sum_{l=1}^{n}exp(\theta_lx_i)}$ ，对于所有样本损失函数的极大似然估计即为![极大似然估计](http://deeplearning.stanford.edu/wiki/images/math/7/6/3/7634eb3b08dc003aa4591a95824d4fbd.png)。而对应的逻辑斯蒂回归的损失函数可以写成![逻辑斯谛回归损失](http://deeplearning.stanford.edu/wiki/images/math/5/4/9/5491271f19161f8ea6a6b2a82c83fc3a.png)，可以看出，logistic损失和softmax损失在形式上十分相似。对于softmax的计算公式，可以看出当所有类的参数 $\theta$都减去一个值 $\psi$，可以推导出![公式推导](http://deeplearning.stanford.edu/wiki/images/math/d/8/0/d8076908fb40b49db821dc410b03700f.png)，因而减去值$\psi$不影响概率公式的值，这表明softmax回归模型中存在冗余的参数。因而可以通过将 $\theta_0$替换为全0向量，进而使得概率公式中的第一项值为1，若应用于二分类，则转变为sigmoid函数。

#### softmax的圈中更新

可以使用迭代的优化算法，例如梯度下降法对softmax回归的损失函数进行求解，经过求导后得到的梯度公式为![梯度公式](http://deeplearning.stanford.edu/wiki/images/math/5/9/e/59ef406cef112eb75e54808b560587c9.png)，之后根据该梯度在负梯度方向进行更新。因为softmax中参数的冗余性，通常会添加一个权重衰减项来修改损失函数，使得损失函数求解时能得到唯一的最优解，将损失函数的公式修改为![损失函数](http://deeplearning.stanford.edu/wiki/images/math/4/7/1/471592d82c7f51526bb3876c6b0f868d.png)，对该公式求梯度并更新参数，则可以求得最优解。

#### softmax与logistic应用于多分类

softmax回归中，一般是假设多个类别是互斥的，样本在softmax中的概率公式中计算后得到的是样本属于各个类别的值，各个类别的概率之和一定为1，而采用logistic回归和ovr的思想进行多分类时，得到的是值是样本相对于其余类别而言属于该类别的概率，一个样本在多个分类器上计算后得到的结果不一定为1，因而当分类的目标类别是互斥时，常采用softmax回归进行预测，而目标类别不是互斥时，例如预测音乐是属于华语音乐、摇滚或者80年代音乐三个类别时，则采用逻辑斯蒂回归建立多个分类器。
