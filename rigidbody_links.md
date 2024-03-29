# 剛体系の運動方程式

3つの回転自由度を持つ関節で結合された剛体リンク系の運動方程式を導く．

特徴

* 状態変数として，各リンクの**相対角速度**を用いる．一般に剛体の運動は，角速度を用いることで簡便に表現されるため．
* 系の運動エネルギーは，角速度ベクトルの2次形式として表される
  * 2次形式の係数行列は**リンクの質量中心の並進運動**と**質量中心周りの回転運動**に関する二つの行列に分離できる
  * それぞれの行列は三角行列の積の形で表される
* 各状態変数に対する運動方程式はLagrange方程式によって求める
  * 角速度は擬座標の微分なので，擬座標に対するLagrange方程式によって運動方程式が導出される
  * 得られた運動方程式は係数行列の構造を反映して，漸化形の方程式系となる．


## モデルの定義

3回転自由度を持つ関節で結合された$N$リンク系マニピュレータを考える．便宜上，一端のリンクをベース，他端のリンクをエンドエフェクタと呼ぶ．
ベース側からエンドエフェクタ側に向かって，各リンクに$1,2,\ldots,N$と番号をつける．慣性空間をリンク$0$とする．
リンク$i$に固定した座標系として，関節$C_i$に原点を持つ単位ベクトル系を$[{\bf a}_i]$ ($i=1,\ldots,N$)とする．

|記号|意味 |
|--|--|
| $A_{ii-1}$ | $[{\bf a}_{i-1}]$から$[{\bf a}_{i}]$への座標変換行列 |
|$\boldsymbol{\omega}_{ii-1}=[{\bf a}_i]^\top\omega_{ii-1}$|リンク$i$のリンク$(i-1)$に対する角速度ベクトル|
|${\bm R}_i = [{\bf a}_i]^\top R_i$|関節$C_i$からリンク$i$の中心までの距離ベクトル|
|${\boldsymbol{\rho}_i}=[{\bf a}_i]^\top \rho_i$|リンク$i$の質量中心からリンク$i$内の任意点への距離ベクトル|
|${\bm r}_i = [{\bf a}_i]^\top r_i$|$C_i$から$C_{i+1}$までの距離ベクトル|

リンク$i$の慣性空間に対する角速度ベクトル$\boldsymbol{\omega}_{i0} = [{\bf a}_i]^\top \omega_{i0}$は
$$
\boldsymbol{\omega}_{i0} = \sum_{j=1}^{i}\boldsymbol{\omega}_{jj-1}=\sum_{j=1}^{i}[{\bf a}_j]^\top{\omega}_{jj-1} = [{\bf a}_i]^\top \sum_{j=1}^i A_{ij}\omega_{jj-1}
$$
で与えられる．
