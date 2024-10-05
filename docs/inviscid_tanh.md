---
title: tanh型速度分布の非粘性線形安定性解析
layout: default
nav_order: 10
---

# tanh型速度分布の非粘性線形安定性解析


Hydrodynamic stabilityの基本的な問題の一つですが、ちょっとややこしいのでまとめてみます。

## 準備

{: .new-title}
> 基礎式：Navier-Stokes方程式 (非圧縮)
> 
> $$ \begin{align}
& \pdv{u_i}{t} = -u_j \pdv{u_i}{x_j} - \pdv{p}{x_i} + \frac{1}{Re} \nabla^2 u_i \\
& \pdv{u_i}{x_i} = 0
\end{align}$$
> ただし、 $u_i$ は速度 ($i=1,2,3$ をそれぞれ $x, y, z$軸方向とする)、 $p$ は圧力。
> 各値は代表速度 $U^\ast$ と代表長 $L^\ast$ で無次元化されているものとし、 $Re=U^\ast L^\ast / \nu^\ast$ はレイノルズ数 ($\nu^\ast$ は動粘性係数)。

この基礎式を満たす基本流が存在するとします。
つまり、基本流の速度・圧力を $(U_i, P)$ とすると、以下が成り立ちます。
$$\begin{align*}
& \pdv{U_i}{t} = - U_j \pdv{U_i}{x_j} - \pdv{P}{x_i} + \frac{1}{Re} \nabla^2 U_i \\
& \pdv{U_i}{x_i} = 0
\end{align*}$$
〔※基本流は時間不変だとすることが多いのですが、必須ではない気がするのでひとまず時間変化を許しておきます〕

この基本流に擾乱が加わって、速度・圧力が $(U_i + u_i^\prime, P+p^\prime)$ になったとします。
基本流成分のみの項は前述の等式より消えて、基礎式は次のようになります。
$$\begin{align*}
& \cancel{\pdv{U_i}{t}} + \pdv{u_i^\prime}{t} = -
\cancel{U_j\pdv{U_i}{x_j}} - u_j^\prime \pdv{U_i}{x_j} - U_j \pdv{u_i^\prime}{x_j} - u_j^\prime \pdv{u_i^\prime}{x_j} -
\cancel{\pdv{P}{x_i}} - \pdv{p^\prime}{x_i} + \cancel{\frac{1}{Re} \nabla^2 U_i} + \frac{1}{Re} \nabla^2 u_i^\prime \\
& \cancel{\pdv{U_i}{x_i}} + \pdv{u_i^\prime}{x_i} = 0
\end{align*}$$
これが擾乱成分の(非線形)発展方程式です。

以下、擾乱成分 $(u_i^\prime, p^\prime)$ を $(u_i, p)$ と書きなおすことにします。
次の二つを仮定します。
1. 微小擾乱 (擾乱成分の2次以上の項は無視できるほど小さい)
2. 非粘性 ($Re \to \infty$)

このとき、

{: .new-title}
> 微小擾乱の線形化された発展方程式 (非圧縮・非粘性)
> 
> $$ \begin{align}
& \pdv{u_i}{t} = - u_j \pdv{U_i}{x_j} - U_j \pdv{u_i}{x_j} - \pdv{p}{x_i} \\
& \pdv{u_i}{x_i} = 0
\end{align}$$
> ただし $U_i$ は基本流の速度、 $(u_i, p)$ は微小な擾乱速度・圧力 (2次以上の項は無視)。



ここで、基本流 $U_i$ ($i=1,2,3$ はそれぞれ $x,y,z$ 成分) として、 $U_1 = U(y), U_2=U_3=0$ を考えます。 
$x$方向に流れがあり、$y$方向にのみ分布があるというもので、境界層や混合層を単純化したものになっています。〔※TODO: 詳しい説明の追加〕

$u_1, u_2, u_3$ をそれぞれ $u, v, w$ として、上述の式を書き下すと、

$$\begin{align}
& \pdv{u}{t} = -v\dv{U}{y} - U\pdv{u}{x} - \pdv{p}{x} \label{eq:a1} \\
& \pdv{v}{t} = \phantom{-v\pdv{U}{y}} -U\pdv{v}{x} - \pdv{p}{y} \label{eq:a2} \\
& \pdv{w}{t} = \phantom{-v\pdv{U}{y}} -U\pdv{w}{x} - \pdv{p}{z} \label{eq:a3}
& \pdv{u}{x} + \pdv{v}{y} + \pdv{w}{z} = 0 \label{eq:a4}
\end{align}$$

$\pdv{x}(\ref{eq:a1}) + \pdv{y}(\ref{eq:a2}) + \pdv{z}(\ref{eq:a3})$ とすると、

$$\begin{align*}
\pdv{t} \underbrace{\qty( \pdv{u}{x} + \pdv{v}{y} + \pdv{z}{z} )}_{=0 (\because \mathrm{Eq.} \ \ref{eq:a4})}
\end{align*}$$


## 参考文献
1. P. Schmid and D. Henningson, "Stability and Transition in Shear FLows," Springer, 2001.
