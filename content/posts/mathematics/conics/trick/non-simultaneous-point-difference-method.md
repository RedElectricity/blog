+++
title = '圆锥曲线 方法 / 不联立: 点差法'
date = 2025-03-07T22:40:13+08:00
draft = true

+++

> 圆锥曲线版的设而不求

## 回归教材

我们先来看教材上的例子

---

(人教版A版 选择性必修一 P128 拓广 第13题) 已知双曲线$x^2 - \frac{y^2}{2} = 1$, 过$P(1, 1)$的直线$l$与双曲线交于$AB$两点, $P$是否能为$l_{AB}$中点?

Prove. 设$A(x_1, y_1) B(x_2, y_2)$, 代入双曲线得
$$
\left\{ {\begin{array}{*{20}{c}}
{{x_1} - \frac{{y_1^2}}{2} = 1}\\
{{x_2} - \frac{{y_2^2}}{2} = 1}
\end{array}} \right.
$$
两式作差得
$$
x_1 ^2 - x_2 ^2 = \frac{{y_1^2 - y_2^2}}{2}
$$
变形可得
$$
\frac{{{y_1} - {y_2}}}{{{x_1} - {x_2}}} = 2 \cdot \frac{{{x_1} + {x_2}}}{{{y_1} + {y_2}}}
$$
若$P(1, 1)$为$AB$中点, 则有$x_1 + x_2 = 2, y_1 + y_2 = 2$. 所以有$k_{AB} = \frac{{{y_1} - {y_2}}}{{{x_1} - {x_2}}} = 2$, $l: y=2x-1$
$$
\left\{ {\begin{array}{*{20}{c}}
{{x^2} - \frac{{{y^2}}}{2} = 1}\\
{y = 2x - 1}
\end{array} \Rightarrow 2{x^2} - 4x + 3 = 0} \right.
$$
因为$\Delta < 0$, 故无焦点. 因此不能$Q.E.D$

---

如果直线与圆锥曲线有两个交点$AB$将两交点坐标代进曲线方程, 得到两个式子, 并对两式作差化简发现, 直线$l_{AB}$的斜率与线段$AB$中点$E$的坐标之间存在一定的数量关系.

## 推广

