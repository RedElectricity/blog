+++
title = 'Physics Principle: 动量'
date = 2024-07-06T22:22:17+08:00
draft = false
categories = ['Physics', 'Course']
+++

## 质点的动量定理

{{< quote author="牛顿" source="自然哲学的数学原理" >}}
运动的变化与所加的动力成正比, 并且发生在这个动力所沿的直线的方向上.
{{< /quote >}}

牛顿在第二定律中所提出的**运动**有严格的定义, 其实就是我们现在所说的**动量**, 使用$\vec{p}$表示
$$
\vec{p} = m\vec{v}
$$
并且**运动的变化**指的就是动量的变化量, 因此有
$$
\frac{d \vec{p}}{dt} = \vec{F}
$$
式等价于我们通常所看到的公式$\vec{F} = m\vec{a}$

接下来我们讨论力的时间累计效应, 考虑将$dt$移项变成
$$
\vec{F}dt=d(m\vec{v})
$$
其中$\vec{F}dt$即为力$\vec{F}$的**原冲量**. 考虑将式从$t_1$到$t_2$积分可得
$$
\int_{t_1}^{t_2} \vec{F}dt = m\vec{v}_2 - m\vec{v}_1 = \vec{p}_2 - \vec{p}_1
$$
我们称上式为力$\vec{F}$在$t_1$到$t_2$内**力的冲量**. 常用$\vec{I}$表示
$$
\vec{I} = \int_{t_1}^{t_2} \vec{F}dt
$$
