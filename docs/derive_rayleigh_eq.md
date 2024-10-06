---
title: Rayleigh方程式の導出
layout: default
nav_order: 10
parent: 非粘性・１次元速度分布の線形安定性解析
---

# Rayleigh方程式の導出

「**基本流 (base flow)**が与えられたとき、ある波長の擾乱を加えたら増幅（または減衰）されるか？」という、流体力学で定番の問題設定があります。
この問題を考えるのが安定性解析であり、一部の問題は**Rayleigh方程式**とよばれる常微分方程式の固有値問題を解くことに帰着します。
以下ではまず、Navier-Stokes方程式からRayleigh方程式への導出をまとめてみます。

## 出発点

{: .important-title}
> 基礎式：Navier-Stokes方程式 (非圧縮)
> 
> $$ \begin{gather}
& \pdv{u_i}{t} = -u_j \pdv{u_i}{x_j} - \pdv{p}{x_i} + \frac{1}{Re} \laplacian{u_i} \\
& \pdv{u_i}{x_i} = 0
\end{gather}$$
> ただし、 $u_i$ は速度 ($i=1,2,3$ をそれぞれ $x, y, z$軸方向とする)、 $p$ は圧力。
> 各値は代表速度 $U^\ast$ と代表長 $L^\ast$ で無次元化されているものとし、 $Re=U^\ast L^\ast / \nu^\ast$ はレイノルズ数 ($\nu^\ast$ は動粘性係数)。

いま、速度・圧力をそれぞれ　$u_i = U_i + u'_i, p = P + p'$ のように、「基本流成分＋擾乱成分」の形で書けるとします。
これをNavier-Stokes方程式に代入すれば、

$$\begin{gather*}
\pdv{t} \qty(U_i + u'_i) = - \qty(U_j + u'_j) \pdv{x_j} \qty(U_i + u'_i) - \pdv{x_i} \qty(P + p') + \frac{1}{Re} \laplacian{U_i + u'_i} \\
\pdv{x_i} \qty(U_i + u'_i) = 0
\end{gather*}$$

一方で、基本流成分 $U_i, P$ のみでもNavier-Stokes方程式

$$\begin{gather*}
& \pdv{U_i}{t} = - U_j \pdv{U_i}{x_j} - \pdv{P}{x_i} + \frac{1}{Re} \laplacian{U_i} \\
& \pdv{U_i}{x_i} = 0
\end{gather*}$$

が成り立つので、これを差し引きます。
また $(u'_i, p')$ を $(u_i, p)$ と書き直せば、

$$\begin{gather*}
\pdv{u_i}{t} = - u_j \pdv{U_i}{x_j} - U_j \pdv{u_i}{x_j} - u_j \pdv{u_i}{x_j} - \pdv{p}{x_i} + \frac{1}{Re} \laplacian{u_i} \\
\pdv{u_i}{x_i} = 0
\end{gather*}$$

となります。これが(非線形な)擾乱の支配方程式です。


## Rayleigh方程式導出のための仮定

Rayleigh方程式を導出では、以下の場合を考えます:
1. 非粘性 ($Re \to \infty$)
2. 無限小擾乱 (擾乱成分の2次以上の項を無視して線形化できる)
3. 平行流 (基本流の速度場は $U_1 = U(y), U_2=U_3 = 0$ の形をとる。ただし$i=1,2,3$ はそれぞれ $x, y, z$方向を表す)
4. 波状擾乱 (後述)

以下、これらの条件を順に適用して、式変形を進めます。

## 非粘性・無限小擾乱

非粘性 ($Re \to \infty$ の極限) の場合、前式の粘性項

$$\frac{1}{Re} \laplacian{u_i}$$

が消えます。
また無限小擾乱を考えると、擾乱成分の2次以上の項

$$u_j \pdv{u_i}{x_j}$$

も消えて、結局、

$$\begin{gather*}
\pdv{u_i}{t} = - u_j \pdv{U_i}{x_j} - U_j \pdv{u_i}{x_j} - \pdv{p}{x_i} \\
\pdv{u_i}{x_i} = 0
\end{gather*}$$

となります。


## 平行流

基本流の速度場が、 $U_1 = U(y), U_2 = U_3 = 0$ と書けるとします。
流れが $x$ 軸に平行であり、 $y$ 方向にのみ分布を持つ場合であり、境界層や混合層を単純化したものになっています〔TODO: 具体例 → mixing layer, jet, wake, Couette flow, Poiseuille flow, wall boundary layer, etc.〕

$u_1, u_2, u_3$ をそれぞれ $u, v, w$ として、前式を書き下すと、

$$\begin{align}
& \pdv{u}{t} = -v\dv{U}{y} - U\pdv{u}{x} - \pdv{p}{x} \label{eq:a1} \\
& \pdv{v}{t} = \phantom{-v\pdv{U}{y}} -U\pdv{v}{x} - \pdv{p}{y} \label{eq:a2} \\
& \pdv{w}{t} = \phantom{-v\pdv{U}{y}} -U\pdv{w}{x} - \pdv{p}{z} \label{eq:a3} \\
& \pdv{u}{x} + \pdv{v}{y} + \pdv{w}{z} = 0 \label{eq:a4}
\end{align}$$

となります。
この式は、未知の量 $u, v, w, p$ が入り混じっていて、そのままでは解析しづらいので、以下の3ステップで整理します。


### ステップ1: 圧力 $p$ の式

$\pdv{x}(\ref{eq:a1}) + \pdv{y}(\ref{eq:a2}) + \pdv{z}(\ref{eq:a3})$ を考えると、

$$\begin{equation*}
\pdv{t} \underbrace{\qty( \pdv{u}{x} + \pdv{v}{y} + \pdv{z}{z} )}_{=0 \ (\because \ (\ref{eq:a4}))} 
= -U' \pdv{v}{x} - U\pdv{x} \underbrace{\qty( \pdv{u}{x} + \pdv{v}{y} + \pdv{z}{z} )}_{=0 \ (\because \ (\ref{eq:a4}))}
-U' \pdv{v}{x}
-\underbrace{\qty(\pdv[2]{x} + \pdv[2]{y} + \pdv[2]{z})}_{\laplacian} p
\end{equation*}$$

$$\begin{equation*}
\therefore \quad \laplacian{p} = -2U' \pdv{v}{x}
\end{equation*}$$

が得られます。
ただし $$\dv*{U}{y}$$ を $U'$ と書いています。


### ステップ2: $y$方向速度 $v$ の式

$\laplacian{ (\ref{eq:a2}) }$ を考えると、

$$\begin{equation*}
\pdv{t}\laplacian{v} = -\pdv[2]{x} \qty(U\pdv{v}{x}) - \pdv[2]{y} \qty(U\pdv{v}{x}) - \pdv[2]{z} \qty(U\pdv{v}{x}) - \pdv{y} \laplacian{p} 
\end{equation*}$$

となります。
ここで、右辺の第2項は、

$$\begin{equation*}
\pdv[2]{y} \qty(U\pdv{v}{x}) = \pdv{y} \qty(U' \pdv{v}{x} + U \pdv{v}{x}{y}) = U'' \pdv{v}{x} + 2U' \pdv{v}{x}{y} + U \pdv{x} \pdv[2]{v}{y}
\end{equation*}$$

となります。
また、右辺の第4項は、ステップ1より

$$\begin{equation*}
-\pdv{y} \laplacian{p} = -\pdv{y} \qty(-2U' \pdv{v}{x}) = 2U'' \pdv{v}{x} + 2U' \pdv{v}{x}{y}
\end{equation*}$$

となります。したがって、

$$\begin{gather*}
\pdv{t} \laplacian{v} = - U \pdv{x} \laplacian{v} - U'' \pdv{v}{x} - \cancel{2U' \pdv{v}{x}{y}}  + 2U'' \pdv{v}{x} + \cancel{2U' \pdv{v}{x}{y}} \\
\therefore \quad \qty[ \qty(\pdv{t} + U \pdv{x}) \laplacian - U'' \pdv{x} ] v = 0
\end{gather*}$$

となります。
ただし $$\dv*[2]{U}{y}$$ を $U''$ と書いています。


### ステップ3: $y$方向渦度 $\eta$ の式

残る未知の量 $u, w$ を、 $y$方向渦度

$$\begin{equation*}
\eta = \pdv{u}{z} - \pdv{w}{x}
\end{equation*}$$

としてまとめます。
$\pdv{z}(\ref{eq:a1}) - \pdv{x}(\ref{eq:a3})$ とすると、

$$\begin{equation*}
\pdv{t} \pdv{u}{z} - \pdv{t} \pdv{w}{x} = -U' \pdv{v}{z} - U \pdv{x} \pdv{u}{z} - \cancel{\pdv{p}{x}{z}} + U \pdv{x} \pdv{w}{x} + \cancel{\pdv{p}{x}{z}}
\end{equation*}$$

$$\begin{equation*}
\therefore \quad \qty[ \pdv{t} + U \pdv{x} ] \eta = -U' \pdv{v}{z}
\end{equation*}$$

となります。


以上をまとめると、

{: .important-title}
> 線形化された、無限小擾乱の発展方程式 (非圧縮・非粘性・平行流)
> 
> 基本流の速度分布が $U_1 = U(y), U_2=U_3=0$ (添え字 1, 2, 3はそれぞれ $x, y, z$方向を表す) であるとき、式(\ref{eq:a1}) -- (\ref{eq:a4})は、次のように整理できる。
> $$ \begin{gather}
& \qty[ \qty(\pdv{t} + U \pdv{x}) \laplacian - U'' \pdv{x} ] v = 0 \label{eq:b1} \\
& \qty[ \pdv{t} + U \pdv{x} ] \eta = -U' \pdv{v}{z} \label{eq:b2} \\
& \laplacian{p} = -2U' \pdv{v}{x} \label{eq:b3}
\end{gather}$$

式(\ref{eq:b1})は $v$ のみの式となっています。
これを解いて $v$ が決まれば、式(\ref{eq:b2}), (\ref{eq:b3}) から $\eta, p$ も決まるはずです。

※ $$v, \eta$$ が求まれば、 $u, z$ も決まりそうです。
実際、$$\pdv{u}{x} + \pdv{v}{y} + \pdv{z}{w} = 0$$ と $$\eta = \pdv{u}{z} - \pdv{w}{x}$$ にそれぞれ $\pdv{x}, \pdv{z}$ をかけて差をとると、

$$\qty(\pdv[2]{x} + \pdv[2]{z}) u = \pdv{\eta}{z} - \pdv{v}{x}{y}$$

というポアソン方程式を解けば $u$ が決まります。
逆に $\pdv{z}, \pdv{x}$ をそれぞれかけて和をとると、

$$ \qty(\pdv[2]{x} + \pdv[2]{z}) w = - \pdv{\eta}{x} - \pdv{v}{y}{z}$$

となります。



## 波状擾乱

前節の式(\ref{eq:b1})の解として、次のような波状擾乱を仮定すると、Rayleigh方程式が得られます。

{: .new-title}
> (定義) 波状擾乱
> 
> $$\begin{equation} v(x, y, z, t) = \tilde{v}(y) e^{i \qty(\alpha x + \beta z - \alpha c t)} \label{eq:wave1} \end{equation}$$
> $\alpha \in \mathbb{R}$ は $x$ 方向波数、 $\beta \in \mathbb{R}$ は $z$ 方向波数、 $c = c_r + i c_i \in \mathbb{C}$ は(複素) 位相速度 ($c_r, c_i \in \mathbb{R}$)

$$\tilde{v}(y)  = \abs{\tilde{v} (y) } e^{i\phi (y)}$$

および、波数ベクトルと位置ベクトルを

$$\vb*{k} = \mqty(\alpha \\ \beta), \vb*{x} = \mqty(x \\ z)$$

とすれば、

$$\begin{align*}
\mathrm{Real}\qty(v)
& = \mathrm{Real}\qty{ \abs{\tilde{v}} e^{i\phi(y)} e^{i\qty[ \alpha x + \beta z - \alpha (c_r + i c_i) t]} } \\
& = \abs{\tilde{v} (y) } e^{\alpha c_i t} \cos( \vb*{k} \cdot \vb*{x} - \alpha c_r t + \phi(y) )
\end{align*}$$

と書けます。
これは、波数ベクトル $$\vb*{k}$$ に直交した波面を持っています(※ つまり、$t$ を固定すると、 $$\vb*{k}$$ に垂直な方向には $$\vb*{k} \cdot \vb*{x}$$ は変わらず $\cos$ の中身(位相) が一定となる)〔TODO: 具体例の図示〕

ここで重要なのが $e^{\alpha c_i t}$ の部分で、
- $\alpha c_i > 0$ ならば、時間とともに指数的に増幅
- $\alpha c_i < 0$ ならば、時間とともに指数的に減衰
をすることが分かります。
このとき、最初に述べた 「**基本流 (base flow)**が与えられたとき、ある波長の擾乱を加えたら増幅（または減衰）されるか？」 という問題は、「ある波数 $\alpha, \beta$ を与えたときに、式(\ref{eq:b1})を満たす $c$ の虚部 $c_i$ の符号は？」 という問題に帰着します。



## Rayleigh方程式

上述の波状擾乱(式(\ref{eq:wave1}))を、式(\ref{eq:b1})に代入します。
まず、

$$\begin{align*}
\laplacian{v}
& = \pdv{x} \qty( i\alpha \tilde{v} e^{i(\alpha x + \beta z - \alpha c t)}  ) + 
\pdv{y} \qty( \dv{\tilde{v}}{y} e^{i(\alpha x + \beta z - \alpha c t)} ) +
\pdv{z} \qty( i\beta \tilde{v} e^{i(\alpha x + \beta z - \alpha c t)}  ) \\
& = -\alpha^2 \tilde{v} e^{i(\alpha x + \beta z - \alpha c t)} +
\dv[2]{\tilde{v}}{y} e^{i(\alpha x + \beta z - \alpha c t)} -
\beta^2 \tilde{v} e^{i(\alpha x + \beta z - \alpha c t)}
\end{align*}$$

$\dv{y} = \mathcal{D}$ と書くこととし、 $\alpha^2 + \beta^2 = k^2$ とすると、

$$\begin{equation*}
\laplacian{v} = \qty[ \qty(\mathcal{D}^2 - k^2) \tilde{v} ] e^{i(\alpha x + \beta z - \alpha c t)}
\end{equation*}$$

これを式(\ref{eq:b1})に代入すると、

$$\begin{align*}
0 &= \qty[ \qty(\pdv{t} + U \pdv{x}) \laplacian - U'' \pdv{x} ] v \\
&= \qty(\pdv{t} + U \pdv{x}) \qty[ \qty(\mathcal{D}^2 - k^2) \tilde{v} ] e^{i(\alpha x + \beta z - \alpha c t)} -
   i\alpha U'' \tilde{v} e^{i(\alpha x + \beta z - \alpha c t)} \\
&= \qty{ \qty(-i\alpha c + i\alpha U) \qty(\mathcal{D}^2 - k^2) \tilde{v}  -i \alpha U'' \tilde{v}  } e^{i(\alpha x + \beta z - \alpha c t)}  \\
&= \qty{ \qty(U-c) \qty(\mathcal{D}^2 - k^2) \tilde{v} - U'' \tilde{v} } i\alpha e^{i(\alpha x + \beta z - \alpha c t)}
\end{align*}$$

これが $\alpha$ によらず成り立つには、

$$\begin{equation*}
\qty(U-c) \qty(\mathcal{D}^2 - k^2) \tilde{v} - U'' \tilde{v} = 0
\end{equation*}$$

これがRayleigh方程式とよばれる式です。
以上をまとめると、


{: .important-title}
> Rayleigh方程式
> 
> 式(\ref{eq:wave1})の波状擾乱
>
> $$\begin{equation*} v(x, y, z, t) = \tilde{v}(y) e^{i \qty(\alpha x + \beta z - \alpha c t)} \end{equation*}$$
>
> を仮定すると、式(\ref{eq:b1})の線形化された微小擾乱の発展方程式 (非圧縮・非粘性・基本流は１次元速度分布)
>
> $$\begin{equation*} \qty[ \qty(\pdv{t} + U \pdv{x}) \laplacian - U'' \pdv{x} ] v = 0 \end{equation*}$$
>
> から次の式が得られる：
>
> $$\begin{equation} \qty(U-c) \qty(\mathcal{D}^2 - k^2) \tilde{v} - U'' \tilde{v} = 0 \end{equation}$$
>
> ただし $$\mathcal{D} = \dv*{y}, U'' = \dv*[2]{U}{y}$$ である。
> この式は、 **Rayleigh方程式**とよばれる。





## 参考文献
1. P. Schmid and D. Henningson, "Stability and Transition in Shear FLows," Springer, 2001.
