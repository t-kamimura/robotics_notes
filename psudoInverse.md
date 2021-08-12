# 擬似逆行列

ムーア-ペンローズの擬似逆行列と，冗長な自由度を持つ連立方程式の解法についてまとめる．

行列$A\in \mathbb{R}^{m\times n}$が存在する．
$A$に対して，以下の性質を満たす行列$X$を考える．

1. $AXA = A$
2. $XAX = X$
3. $(AX)^\top  = AX$
4. $(XA)^\top  = XA$

このような$X$のことを$A$の（ムーア-ペンローズの）**擬似逆行列**といい，$A^\dagger$（ダガー）あるいは$A^+$と表す．

## 擬似逆行列を作る

$A$の階数が$r$であるとき，行列の基本変形によって
$$
    PAQ = \begin{bmatrix}
    I_r & O_{r,n-r}\\
    O_{m-r, r}&O_{m-r,n-r}
    \end{bmatrix}
    =\begin{bmatrix}
    I_r\\
    O_{m-r, r}
    \end{bmatrix}
    \begin{bmatrix}
    I_r & O_{r,n-r}
    \end{bmatrix}
$$
となる．ここで，$I_r$は$r \times r$の単位行列，$O_{kl}$は$k \times l$のゼロ行列を表す．
ここで，
$$
    B=P^{-1}\begin{bmatrix}
    I_r\\
    O_{m-r, r}
    \end{bmatrix},\\
    C=\begin{bmatrix}
    I_r & O_{r,n-r}
    \end{bmatrix}Q^{-1}
$$
とおくと，
$$
    A=BC
$$
が成立する．この$B$と$C$を用いて
$$
D = C^\top (B^\top AC^\top )^{-1}B^\top  = C^\top (B^\top BCC^\top )^{-1}B^\top
$$
とおくと，$X=D$となる．

(証明)
まず，$B^\top B$と$CC^\top $は正則である（証明略）．このとき，
$$
    ADA = BC\{C^\top (CC^\top )^{-1}(B^\top B)^{-1}B^\top \}BC\\
    =B(CC^\top )(CC^\top )^{-1}(B^\top B)^{-1}(B^\top B)C\\
    =BC =A
$$
$$
    DAD = \{C^\top (CC^\top )^{-1}(B^\top B)^{-1}B^\top \}BC\{C^\top (CC^\top )^{-1}(B^\top B)^{-1}B^\top \}\\
    =C^\top (CC^\top )^{-1}(B^\top B)^{-1}(B^\top B)(CC^\top )(CC^\top )^{-1}(B^\top B)^{-1}B^\top \\
    =C^\top (CC^\top )^{-1}(B^\top B)^{-1}B^\top  = D
$$
が成立する．また，
$$
    (AD)^\top  = \{BC(C^\top (CC^\top )^{-1}(B^\top B)^{-1}B^\top )\}^\top \\
    = \{B(B^\top  B)^{-1}B^\top \}^\top  \\
    = (B^\top )^\top \{(B^\top B)^\top \}^{-1}B\\
    = B(BB^\top )B^\top  = AD
$$
である．$(DA)^\top =DA$についても同様．
したがって，$X=D$である．

## 擬似逆行列の一意性

擬似逆行列は一意で，
$$
A^{\dagger} = C^\top (B^\top BCC^\top )^{-1}B^\top
$$
のみである．

（証明）
$X$も$Y$も擬似逆行列であると仮定すると，$X=Y$が導かれる．

## 線形連立方程式を解く

線形連立方程式
$$
    A\boldsymbol{ x} = \boldsymbol{b}
$$
を解く．$A \in \mathbb{R}^{m\times n}$, $\boldsymbol{x}\in \mathbb{R}^n$, $\boldsymbol{b}\in \mathbb{R}^m$である．

### 正則な場合

$m=n$で，$A$が正則であれば$A^{-1}$が存在するため，
$$
    \boldsymbol{x} = A^{-1}\boldsymbol{b}
$$
が直ちに得られる．これは，線形連立方程式において未知数の数と式の数が一致している場合である．解は一意になる．

### 正則でない場合

もっと一般的な問題を考えよう．すなわち，未知数と式の数が一致しない場合，$A$は正則ではない．さらに場合分けをするなら，未知数に対して式が足りない場合($m<n$)と，未知数に対して式が多すぎる場合($n<m$)が存在する．

* 前者は，拘束条件が少ないため，無数に解を持つことができる．
* 後者は，拘束条件が多すぎるため，解が存在しない．

いずれの場合においても，解は$||A\boldsymbol{x}-\boldsymbol{b}||$を最小化するように探索する．前者では，原点から最も近い解を一つ選択し，そこから全ての解を表す．後者では，最も近くまで近づけるものを解として扱うことになる．

拘束条件が少ない場合，ラグランジュの未定乗数法によって
$$
\boldsymbol{x} = A^{\dagger}\boldsymbol{b} + (I_n-A^{\dagger}A)\boldsymbol{k}
$$
を得る．$\boldsymbol{k}\in\mathbb{R}^n$は任意のベクトルであり，解が無数に存在することを表す．

拘束条件が多すぎる場合，(二乗誤差の偏導関数)$=0$を解くことによって，
$$
\boldsymbol{x}^* = (A^\top A)^{-1}A^\top \boldsymbol{b}
$$
を得る．ただし，これは最適化の結果でしかなく，いかなる方程式の解でもないことに注意する必要がある．

### 例題

例えば冗長な自由度を持つロボットアームの逆運動学問題を考えてみよう．このとき，手先速度$\boldsymbol{v}$はヤコビ行列$J$と関節速度$\dot{\boldsymbol{q}}$を用いて
$$
    \boldsymbol{v} = J\dot{\boldsymbol{q}}
$$
で与えられる．$\boldsymbol{v}\in \mathbb{R}^6$であるのに対し，冗長自由度アームでは$\dot{\boldsymbol{q}}\in \mathbb{R}^n$ ($n>6$)である．このような場合，任意の手先速度は様々な関節角度の組み合わせによって得られる．すなわち，
$$
    \dot{\boldsymbol{q}} = J^\dagger\boldsymbol{v} + (I_n - J^\dagger J)\boldsymbol{k}
$$
となり，$\boldsymbol{k}$が任意性を表す．

逆に，自由度に対して制御系が不足している劣駆動システムの場合，入力の制約から任意の出力を達成することは不可能である．

## 参考文献

斎藤正彦，「線形代数演習」，東京大学出版会，1985．
吉川恒夫，「ロボット制御基礎論」，コロナ社，1988．