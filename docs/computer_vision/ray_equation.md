---
title: Ray Equation
layout: default
nav_order: 10
parent: Computer Vision
has_toc: true
---

# Ray Equation

光は，波動性 (回折など) を無視することで，１本の**光線** (ray) 上を伝わるとみなすことができる．
このような単純化は幾何光学近似とよばれ，光の屈折の計算などでよく使われる．

光線は，一様でない密度分布を通るとき，屈折のため曲線となる．
下図のような光線を考える．
光線上に基準点を１つとり，その位置ベクトルを $\vb\*{r}\_0$ とする．
基準点 $\vb\*{r}\_0$ から光線に沿って測った距離 (**弧長**, arc length) が $s$ となるような光線上の点の位置ベクトルを $\vb\*{r}(s)$ とかくことにする ($\vb\*{r}(0) = \vb\*{r}\_0$ である)．

<!-- ![弧長](figs/ray1.svg) -->
<img src="figs/ray1.svg" width="60%">

弧長が $\Delta s$ だけ離れた２点 $\vb\*{r}(s), \vb\*{r}(s\+\Delta s)$ に対し，
$$
\begin{equation}
\dv{ \vb*{r} }{s} = \lim_{\Delta s \to 0} \frac{ \vb*{r}(s+\Delta s) - \vb*{r}(s) }{\Delta s}
\end{equation}
$$
は，点 $\vb\*{r}(s)$ における光線方向の単位ベクトルを表している．
このベクトルと，屈折率 $n \qty(\= \frac{c\_0}{c})$ ($c\_0$ は真空中の光速， $c$ は物質中の各点での光速) との間には，次の**ray equation**が成り立つことが知られている:
$$
\begin{equation}
	\dv{s} \qty( n \dv{\vb*{r}}{s} ) = \grad n \label{eq:rayeq}
\end{equation}
$$

以下，このray equationの導出について説明する．
Maxwell方程式を出発点として，まず波動方程式を導出し，幾何光学近似を適用してeikonal方程式を求め，そこからray equationを得る．

### 前提: Maxwell方程式

電荷のない空間のMaxwell方程式を出発点とする:
$$
\begin{align}
& \curl{\vb*{E}}(\vb*{r}, t) = - \pdv{\vb*{B}(\vb*{r}, t)}{t} \label{eq:maxwell1}\\
& \curl{\vb*{H}}(\vb*{r}, t) = \pdv{\vb*{D}(\vb*{r}, t)}{t} + \vb*{j}(\vb*{r}, t) \label{eq:maxwell2} \\
& \div{\vb*{B}(\vb*{r}, t)} = \vb*{0} \label{eq:maxwell3} \\
& \div{\vb*{D}(\vb*{r}, t)} = \vb*{0} \label{eq:maxwell4}
\end{align}
$$
ただし $\vb\*{E}$ は電場 (electric vector), $\vb\*{H}$ は磁場 (magnetic vector), $\vb\*{D}$ は電束密度 (electric displacement), $\vb\*{B}$ は磁束密度 (magnetic induction), $\vb\*{j}$ は電流密度 (electric current density)である．

真空中では，次のような構成方程式が成り立つ:
$$
\begin{align}
&\vb*{D}(\vb*{r},t) = \epsilon_0 \vb*{E}(\vb*{r},t) \label{eq:vacuum1} \\
&\vb*{B}(\vb*{r},t) = \mu_0 \vb*{H}(\vb*{r},t) \label{eq:vacuum2}  \\
&\vb*{j}(\vb*{r},t) = \vb*{0} \label{eq:vacuum3} 
\end{align}
$$
ただし $\epsilon_0$ と $\mu_0$ はそれぞれ真空中の誘電率 (dielectric constant of vacuum) と透磁率 (magnetic permeability of vacuum) である．

物質中では (線形な等方性物質の場合)，次のような構成方程式が成り立つ:
$$
\begin{align}
&\vb*{D}(\vb*{r},t) = \epsilon(\vb*{r}) \epsilon_0 \vb*{E}(\vb*{r},t)  \label{eq:material1} \\
&\vb*{B}(\vb*{r},t) = \mu(\vb*{r}) \mu_0 \vb*{H}(\vb*{r},t) \label{eq:material2} \\
&\vb*{j}(\vb*{r},t) = \sigma(\vb*{r}) \vb*{E}(\vb*{r}, t) \label{eq:material3}
\end{align}
$$
ただし $\epsilon(\vb\*{r})$ と $\mu(\vb\*{r})$ はそれぞれ比誘電率 (dielectric function) と比透磁率 (magnetic permeability)， $\sigma(\vb\*{r})$ は比電導率 (specific conductivity)である．


### 波動方程式

前節のMaxwell方程式（と構成方程式）から，電磁場の波動方程式が得られる．

まず真空の場合を考える．
式\eqref{eq:maxwell1}の両辺に $\curl$ をかけると，
$$ \begin{align*}
&\curl(\curl{\vb*{E}}) 
= - \curl(\pdv{\vb*{B}}{t}) = -\pdv{}{t} \qty(\curl{\vb*{B}})
\overset{\mathrm{Eq. \ \eqref{eq:vacuum2}}}{=} - \mu_0 \pdv{}{t} \qty(\curl{\vb*{H}}) \\
& \overset{\mathrm{Eqs. \ \eqref{eq:maxwell2}, \eqref{eq:vacuum3}}}{=} - \mu_0 \pdv{}{t} \qty(\pdv{\vb*{D}}{t}) 
\overset{\mathrm{Eq. \ \eqref{eq:vacuum1}}}{=} - \epsilon_0 \mu_0 \pdv[2]{\vb*{E}}{t} 
\end{align*}$$

右辺の $\curl(\curl{\vb\*{E}})$ は，第 $i$ 成分を考えると，
$$ \begin{align*}
& \qty( \curl(\curl{\vb*{E}}) )_i = \epsilon_{ijk} \pdv{}{x_j} \qty( \epsilon_{klm} \pdv{E_m}{x_l} ) = \epsilon_{ijk} \epsilon_{lmk} \pdv{E_m}{x_j}{x_l} \\
&= \qty( \delta_{il}\delta_{jm} - \delta_{im} \delta_{jl} ) \pdv{E_m}{x_j}{x_l} 
= \pdv{E_j}{x_i}{x_j} - \pdv[2]{E_i}{x_j}
= \qty(\grad(\div{\vb*{E}}) - \laplacian{\vb*{E}})_i
\end{align*} $$

式\eqref{eq:maxwell4}と\eqref{eq:vacuum1}より， $\div{\vb\*{D}} = \epsilon_0 \div{\vb\*{E}} = 0$ となるので，結局
$$
\begin{align*}
\curl(\curl{\vb*{E}}) = -\laplacian{\vb*{E}}
\end{align*}
$$

以上をまとめると，
$$ 
\begin{align*}
\pdv[2]{\vb*{E}}{t} = \laplacian{\vb*{E}}
\end{align*}
$$

### 参考文献
- Träger, "Springer Handbook of Lasers and Optics," Springer, 2012. Sec. 2.1.