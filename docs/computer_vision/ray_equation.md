---
title: Ray Equation
layout: default
nav_order: 10
parent: Computer Vision
---

# Ray Equation

## Ray Equationとは

光は，波動性 (回折など) を無視することで，１本の**光線** (ray) 上を伝わるとみなすことができる．
このような単純化は幾何光学近似とよばれ，光の屈折の計算などでよく使われる．

<!-- ![弧長](figs/ray1.svg) -->
<img src="figs/ray1.svg" width="60%">

屈折した光線は，一般に，上図のように曲線となる．
光線上に基準点を１つとり，その位置ベクトルを $$\vb*{r}_0$$ とする．
基準点 $$\vb*{r}_0$$ から光線に沿って測った距離 (**弧長**, arc length) が $$s$$ となるような光線上の点の位置ベクトルを $$\vb*{r}(s)$$ と書くこととする ($$\vb*{r}(0) = \vb*{r}_0$$ である)．
このとき，
$$
\begin{equation}
\dv{ \vb*{r} }{s} = \lim_{\Delta s \to 0} \frac{ \vb*{r}(s+\Delta s) - \vb*{r}(s) }{\Delta s}
\end{equation}
$$
は，点 $$\vb*{r}(s)$$ における(単位)光線方向ベクトルを表す．


この光線方向ベクトルの変化量は，次式のように，屈折率 $$n$$ (真空中の光速 $$c_0$$ と物質中の光速 $$c$$ の比: $$n \equiv c_0 / c$$) の空間勾配で決まる:
$$
\begin{equation}
	\dv{s} \qty( n \dv{\vb*{r}}{s} ) = \grad n \label{eq:rayeq}
\end{equation}
$$
この式を**ray equation**とよび，以下で導出する．

## 導出

### 前提

光は電磁波であり，Maxwell方程式で記述される．

{: .note-title }
> 電荷のない空間のMaxwell方程式
> $$
\begin{align}
& \curl{\vb*{E}}(\vb*{r}, t) = - \pdv{\vb*{B}(\vb*{r}, t)}{t} \label{eq:maxwell1}\\
& \curl{\vb*{H}}(\vb*{r}, t) = \pdv{\vb*{D}(\vb*{r}, t)}{t} + \vb*{j}(\vb*{r}, t) \label{eq:maxwell2} \\
& \div{\vb*{B}(\vb*{r}, t)} = \vb*{0} \label{eq:maxwell3} \\
& \div{\vb*{D}(\vb*{r}, t)} = \vb*{0} \label{eq:maxwell4}
\end{align}
$$

ただし,
- $\vb\*{E}$, 電場 (electric vector);
- $\vb\*{H}$, 磁場 (magnetic vector);
- $\vb\*{D}$, 電束密度 (electric displacement);
- $\vb\*{B}$, 磁束密度 (magnetic induction);
- $\vb\*{j}$, 電流密度 (electric current density).

これに加えて真空中と物質中で，それぞれ以下の構成方程式が成り立つ．

**真空中の構成方程式**
$$
\begin{align}
&\vb*{D}(\vb*{r},t) = \epsilon_0 \vb*{E}(\vb*{r},t) \label{eq:vacuum1} \\
&\vb*{B}(\vb*{r},t) = \mu_0 \vb*{H}(\vb*{r},t) \label{eq:vacuum2}  \\
&\vb*{j}(\vb*{r},t) = \vb*{0} \label{eq:vacuum3} 
\end{align}
$$
ただし，
- $\epsilon_0$, 真空中の誘電率 (dielectric constant of vacuum); 
- $\mu_0$, 真空中の透磁率 (magnetic permeability of vacuum).


**(線形な等方性の) 物質中の構成方程式**
$$
\begin{align}
&\vb*{D}(\vb*{r},t) = \epsilon(\vb*{r}) \epsilon_0 \vb*{E}(\vb*{r},t)  \label{eq:material1} \\
&\vb*{B}(\vb*{r},t) = \mu(\vb*{r}) \mu_0 \vb*{H}(\vb*{r},t) \label{eq:material2} \\
&\vb*{j}(\vb*{r},t) = \sigma(\vb*{r}) \vb*{E}(\vb*{r}, t) \label{eq:material3}
\end{align}
$$
ただし，
- $\epsilon(\vb\*{r})$, 比誘電率 (dielectric function);
- $\mu(\vb\*{r})$, 比透磁率 (magnetic permeability);
- $\sigma(\vb\*{r})$, 比電導率 (specific conductivity).



### 定常波解





## 参考文献
- Träger, "Springer Handbook of Lasers and Optics," Springer, 2012. Sec. 2.1.



<!-- 
## 前提: Maxwell方程式

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


## 波動方程式

前節のMaxwell方程式（と構成方程式）から，以下のようにして波動方程式が得られる．

まず真空の場合を考える．
式\eqref{eq:maxwell1}の両辺に $\curl$ をかけると，
$$ \begin{align*}
&\curl(\curl{\vb*{E}}) 
= - \curl(\pdv{\vb*{B}}{t}) = -\pdv{}{t} \qty(\curl{\vb*{B}})
\overset{\mathrm{Eq. \ \eqref{eq:vacuum2}}}{=} - \mu_0 \pdv{}{t} \qty(\curl{\vb*{H}}) \\
& \overset{\mathrm{Eqs. \ \eqref{eq:maxwell2}, \eqref{eq:vacuum3}}}{=} - \mu_0 \pdv{}{t} \qty(\pdv{\vb*{D}}{t}) 
\overset{\mathrm{Eq. \ \eqref{eq:vacuum1}}}{=} - \epsilon_0 \mu_0 \pdv[2]{\vb*{E}}{t} 
\end{align*}$$

左辺の $\curl(\curl{\vb\*{E}})$ は，第 $i$ 成分を考えると，
$$ \begin{align*}
& \qty( \curl(\curl{\vb*{E}}) )_i = \epsilon_{ijk} \pdv{}{x_j} \qty( \epsilon_{klm} \pdv{E_m}{x_l} ) = \epsilon_{ijk} \epsilon_{lmk} \pdv{E_m}{x_j}{x_l} \\
&= \qty( \delta_{il}\delta_{jm} - \delta_{im} \delta_{jl} ) \pdv{E_m}{x_j}{x_l} 
= \pdv{E_j}{x_i}{x_j} - \pdv[2]{E_i}{x_j}
= \qty(\grad(\div{\vb*{E}}) - \laplacian{\vb*{E}})_i
\end{align*} $$

ただし
$$\begin{align*}
\delta_{ij} = \begin{cases} 1 \quad & (i=j) \\ 0 & (i\neq j) \end{cases}, \quad
\epsilon_{ijk} = \begin{cases} 
1 \quad & (i,j,k) \in \{ (1,2,3), (2,3,1), (3,1,2) \} \\
-1 & (i,j,k) \in \{(3,2,1), (2,1,3), (1,3,2)\} \\
0 & \mathrm{otherwise}
\end{cases}
\end{align*}$$

式\eqref{eq:maxwell4}と\eqref{eq:vacuum1}より， $\div{\vb\*{D}} = \epsilon_0 \div{\vb\*{E}} = 0$ となるので，結局
$$
\begin{align*}
\curl(\curl{\vb*{E}}) = -\laplacian{\vb*{E}}
\end{align*}
$$

以上をまとめれば，
$$ 
\begin{align*}
\pdv[2]{\vb*{E}}{t} = \frac{1}{\epsilon_0 \mu_0} \laplacian{\vb*{E}}
\end{align*}
$$



同様に，式\eqref{eq:maxwell2} (ただし式\eqref{eq:vacuum3}より $\vb\*{j}=\vb\*{0}$) の両辺に $\curl$ をかけると，
$$
\begin{align*}
& \curl(\curl{\vb*{H}}) = \pdv{}{t} \qty(\curl{\vb*{D}})
\overset{\mathrm{Eq. \ \eqref{eq:vacuum1}}}{=} \epsilon_0 \pdv{}{t} \qty(\curl{\vb*{E}}) \\
& \overset{\mathrm{Eq. \ \eqref{eq:maxwell1}}}{=} \epsilon_0 \pdv{}{t} \qty(\pdv{\vb*{B}}{t}) 
\overset{\mathrm{Eq. \ \eqref{eq:vacuum2}}}{=} \epsilon_0 \mu_0 \pdv[2]{\vb*{H}}{t} 
\end{align*}
$$

左辺も同様に 
$$
\begin{align*}
\curl(\curl{\vb*{H}}) = \grad(\div{\vb*{H}}) - \laplacian{\vb*{H}}
\end{align*}
$$
となり，式\eqref{eq:maxwell3}と\eqref{eq:vacuum2}より， $\div{\vb\*{B}} = \mu_0 \div{\vb\*{H}} = 0$ となるので，結局
$$
\begin{align*}
\curl(\curl{\vb*{H}}) = -\laplacian{\vb*{H}}
\end{align*}
$$

したがって，
$$ 
\begin{align*}
\pdv[2]{\vb*{H}}{t} = \frac{1}{\epsilon_0 \mu_0} \laplacian{\vb*{H}}
\end{align*}
$$

以上から，
$$
\begin{align}
\pdv[2]{\vb*{E}}{t} = \frac{1}{\epsilon_0 \mu_0} \laplacian{\vb*{E}}, \quad \pdv[2]{\vb*{H}}{t} = \frac{1}{\epsilon_0 \mu_0} \laplacian{\vb*{H}} \label{eq:wave-vacuum}
\end{align}
$$
が得られた．
真空中の電磁波の位相速度 (真空中の光速) は $c_0 = \frac{1}{\epsilon_0 \mu_0}$ だとわかる．


真空中ではなく物質中の場合，構成方程式が変わる．
ただ，電流が無い場合 ($\vb\*{j} = \vb\*{0}$) には，真空中の構成方程式 (式\eqref{eq:vacuum1}, \eqref{eq:vacuum2}) と物質中の構成方程式 (式\eqref{eq:material1}, \eqref{eq:material2}) が，右辺の係数のみ異なる<sub>(電流があるとどうなる...?)</sub>．
それ以外は真空中と物質中で等しいので，得られる波動方程式は  $\epsilon_0 \to \epsilon\epsilon_0, \mu_0 \to \mu \mu_0$ と置き換えたもの，つまり
$$
\begin{align}
\pdv[2]{\vb*{E}}{t} = \frac{1}{\epsilon \epsilon_0 \mu \mu_0} \laplacian{\vb*{E}}, \quad \pdv[2]{\vb*{H}}{t} = \frac{1}{\epsilon \epsilon_0 \mu \mu_0} \laplacian{\vb*{H}} \label{eq:wave-material}
\end{align}
$$
となる．
ここで $n = \sqrt{\epsilon \mu}$ とおけば，物質中の光速は 
$$c = \frac{1}{\sqrt{\epsilon \mu \epsilon_0 \mu_0}} = \frac{c_0}{n}$$
である．この $n$ を屈折率 (refractive index) とよぶ．
 -->