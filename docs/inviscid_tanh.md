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
> $$ \begin{gather}
& \pdv{u_i}{t} = -u_j \pdv{u_i}{x_j} - \pdv{p}{x_i} + \frac{1}{Re} \laplacian{u_i} \\
& \pdv{u_i}{x_i} = 0
\end{gather}$$
> ただし、 $u_i$ は速度 ($i=1,2,3$ をそれぞれ $x, y, z$軸方向とする)、 $p$ は圧力。
> 各値は代表速度 $U^\ast$ と代表長 $L^\ast$ で無次元化されているものとし、 $Re=U^\ast L^\ast / \nu^\ast$ はレイノルズ数 ($\nu^\ast$ は動粘性係数)。

この基礎式を満たす基本流が存在するとします。
つまり、基本流の速度・圧力を $(U_i, P)$ とすると、以下が成り立ちます。
$$\begin{align*}
& \pdv{U_i}{t} = - U_j \pdv{U_i}{x_j} - \pdv{P}{x_i} + \frac{1}{Re} \laplacian{U_i} \\
& \pdv{U_i}{x_i} = 0
\end{align*}$$
〔※基本流は時間不変だとすることが多いのですが、必須ではない気がするのでひとまず時間変化を許しておきます〕

この基本流に擾乱が加わって、速度・圧力が $(U_i + u'_i, P+p')$ になったとします。
基本流成分のみの項は前述の等式より消えて、基礎式は次のようになります。
$$\begin{align*}
& \cancel{\pdv{U_i}{t}} + \pdv{u'_i}{t} = -
\cancel{U_j\pdv{U_i}{x_j}} - u'_j \pdv{U_i}{x_j} - U_j \pdv{u'_i}{x_j} - u'_j \pdv{u'_i}{x_j} -
\cancel{\pdv{P}{x_i}} - \pdv{p'}{x_i} + \cancel{\frac{1}{Re} \laplacian{U_i}} + \frac{1}{Re} \laplacian{u'_i} \\
& \cancel{\pdv{U_i}{x_i}} + \pdv{u'_i}{x_i} = 0
\end{align*}$$
これが擾乱成分の(非線形)発展方程式です。

以下、擾乱成分 $(u'_i, p')$ を $(u_i, p)$ と書きなおすことにします。
次の二つを仮定します。
1. 微小擾乱 (擾乱成分の2次以上の項は無視できるほど小さい)
2. 非粘性 ($Re \to \infty$)

このとき、

{: .new-title}
> 微小擾乱についての、線形化された発展方程式 (非圧縮・非粘性)
> 
> $$ \begin{gather}
& \pdv{u_i}{t} = - u_j \pdv{U_i}{x_j} - U_j \pdv{u_i}{x_j} - \pdv{p}{x_i} \\
& \pdv{u_i}{x_i} = 0
\end{gather}$$
> ただし $U_i$ は基本流の速度、 $(u_i, p)$ は微小な擾乱速度・圧力 (2次以上の項は無視)。



ここで、基本流 $U_i$ ($i=1,2,3$ はそれぞれ $x,y,z$ 成分) として、 $U_1 = U(y), U_2=U_3=0$ を考えます。 
$x$方向に流れがあり、$y$方向にのみ分布があるというもので、境界層や混合層を単純化したものになっています。〔※TODO: もっと具体的な説明の追加〕

$u_1, u_2, u_3$ をそれぞれ $u, v, w$ として、上述の式を書き下すと、

$$\begin{align}
& \pdv{u}{t} = -v\dv{U}{y} - U\pdv{u}{x} - \pdv{p}{x} \label{eq:a1} \\
& \pdv{v}{t} = \phantom{-v\pdv{U}{y}} -U\pdv{v}{x} - \pdv{p}{y} \label{eq:a2} \\
& \pdv{w}{t} = \phantom{-v\pdv{U}{y}} -U\pdv{w}{x} - \pdv{p}{z} \label{eq:a3} \\
& \pdv{u}{x} + \pdv{v}{y} + \pdv{w}{z} = 0 \label{eq:a4}
\end{align}$$

以下、3つのステップに分けてこれらの式を整理します。
ただし、$\dv{U}{y}$ を $U'$ と書くことにします。

**(ステップ1)** $\pdv{x}(\ref{eq:a1}) + \pdv{y}(\ref{eq:a2}) + \pdv{z}(\ref{eq:a3})$ とすると、

$$\begin{equation*}
\pdv{t} \underbrace{\qty( \pdv{u}{x} + \pdv{v}{y} + \pdv{z}{z} )}_{=0 \ (\because \ (\ref{eq:a4}))} 
= -U' \pdv{v}{x} - U\pdv{x} \underbrace{\qty( \pdv{u}{x} + \pdv{v}{y} + \pdv{z}{z} )}_{=0 \ (\because \ (\ref{eq:a4}))}
-U' \pdv{v}{x}
-\underbrace{\qty(\pdv[2]{x} + \pdv[2]{y} + \pdv[2]{z})}_{\laplacian} p
\end{equation*}$$

$$\begin{equation*}
\therefore \quad \laplacian{p} = -2U' \pdv{v}{x}
\end{equation*}$$

**(ステップ2)** $\nabla^2 (\ref{eq:a2})$ とすると、

$$\begin{gather*}
\pdv{t}\laplacian{v} = -\pdv[2]{x} \qty(U\pdv{v}{x}) - \pdv[2]{y} \qty(U\pdv{v}{x}) - \pdv[2]{z} \qty(U\pdv{v}{x}) - \pdv{y} \laplacian{p} \\
\therefore \quad \pdv{t} \laplacian{v} = - U \pdv{x} \laplacian{v} - U'' \pdv{v}{x} - \cancel{2U' \pdv{v}{x}{y}}  + 2U'' \pdv{v}{x} + \cancel{2U' \pdv{v}{x}{y}} \\
\therefore \quad \qty[ \qty(\pdv{t} + U \pdv{x}) \laplacian - U'' \pdv{x} ] v = 0
\end{gather*}$$

ただし第１式から第２式への変形では、

$$\begin{equation*}
\pdv[2]{y} \qty(U\pdv{v}{x}) = \pdv{y} \qty(U' \pdv{v}{x} + U \pdv{v}{x}{y}) = U'' \pdv{v}{x} + 2U' \pdv{v}{x}{y} + U \pdv{x} \pdv[2]{v}{y}
\end{equation*}$$

と、ステップ1で得られた式による

$$\begin{equation*}
-\pdv{y} \laplacian{p} = -\pdv{y} \qty(-2U' \pdv{v}{x}) = 2U'' \pdv{v}{x} + 2U' \pdv{v}{x}{y}
\end{equation*}$$

を使っています。

**(ステップ3)**

$$\begin{equation*}
\eta = \pdv{u}{z} - \pdv{w}{x}
\end{equation*}$$
という値を考えて、 $u$と$w$をまとめます。〔$y$方向の渦度です〕。

$\pdv{z}(\ref{eq:a1}) - \pdv{x}(\ref{eq:a3})$ とすると、

$$\begin{equation*}
\pdv{t} \pdv{u}{z} - \pdv{t} \pdv{w}{x} = -U' \pdv{v}{z} - U \pdv{x} \pdv{u}{z} - \cancel{\pdv{p}{x}{z}} + U \pdv{x} \pdv{w}{x} + \cancel{\pdv{p}{x}{z}}
\end{equation*}$$

$$\begin{equation*}
\therefore \quad \qty[ \pdv{t} + U \pdv{x} ] \eta = -U' \pdv{v}{z}
\end{equation*}$$


以上をまとめると、

{: .new-title}
> 微小擾乱についての、線形化された発展方程式 (非圧縮・非粘性・1次元速度分布)
> 
> 基本流の速度分布が $U_1 = U(y), U_2=U_3=0$ (添え字 1, 2, 3はそれぞれ $x, y, z$方向を表す) であるとき、式(\ref{eq:a1}) -- (\ref{eq:a4})は、次のように整理できる。
> $$ \begin{gather}
& \qty[ \qty(\pdv{t} + U \pdv{x}) \laplacian - U'' \pdv{x} ] v = 0 \label{eq:b1} \\
& \qty[ \pdv{t} + U \pdv{x} ] \eta = -U' \pdv{v}{z} \label{eq:b2} \\
& \laplacian{p} = -2U' \pdv{v}{x} \label{eq:b3}
\end{gather}$$


TODO: モード解とRayleigh方程式、特異性、ラプラス変換に基づく積分経路の設定、数値

## 参考文献
1. P. Schmid and D. Henningson, "Stability and Transition in Shear FLows," Springer, 2001.
