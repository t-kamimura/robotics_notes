# ラグランジュの運動方程式

ラグランジュの運動方程式は，運動エネルギー$T$とポテンシャルエネルギー$U$から導かれるラグランジアン$L=T-U$を用いて
$$
    \frac{{\rm d}}{{\rm d}t}\left(\frac{\partial L}{\partial \dot{q}_i}\right) - \frac{\partial L}{\partial q_i} = Q_i
$$
である．

## ダランベールの原理からの導出

質点系の運動を考える．剛体の場合は，質点系に拘束条件が加えられた特別な場合として，後に考えることにする．

質点系の運動を考えよう．
質点$m_i$に対して，仮想変位$\delta {\bm r}_i$の方向に力${\bm F}_i$が加えられるとする．
このとき，ダランベールの原理から
$$
	\sum_i ({\bm F}_i-\dot{{\bm p}}_i)\cdot\delta {\bm r}_i = 0
$$
となる．ここで，${\bm p}_i$は質量$m_i$が持つ運動量で，$-\dot{{\bm p}}_i$は慣性力を表す．

外力の仮想仕事を一般化座標を用いた表式に変更する．
$$
	{\bm r}_i = {\bm r}_i(q_1, q_2, \ldots, q_n, t)
$$
と座標変換できるとき，**一般化力**$Q_i$を用いて
$$
	\sum_i {\bm F}_i\cdot\delta {\bm r}_i = \sum_j Q_j\delta q_j
$$
となる（**どのような座標系から測っても，仕事というスカラー量は同じ**であるから）．
ここで一般化力$Q_i$は，チェインルールを用いて
$$
    Q_j = \sum_i {\bm F}_i\cdot\frac{\partial {\bm r}_i}{\partial q_j}
$$
である．

次に，慣性項の仮想仕事
$$
	\sum_i \dot{{\bm p}}_i\cdot\delta {\bm r}_i = \sum_i m_i\ddot{{\bm r}}_i\cdot\delta {\bm r}_i = \sum_{i,j} m_i\ddot{{\bm r}}_i\cdot\frac{\partial {\bm r}_i}{\partial q_j}\delta q_j
$$
は，運動エネルギー$T=\sum_i\frac{1}{2}m_iv_i^2$を用いて，
$$
\sum_{i,j} m_i\ddot{{\bm r}}_i\cdot\frac{\partial {\bm r}_i}{\partial q_j}\delta q_j = \sum_j \left\lbrace \frac{{\rm d}}{{\rm d}t}\left(\frac{\partial T}{\partial q_j}\right) - \frac{\partial T}{\partial q_j} \right\rbrace \delta q_j
$$
となる（ここの導出は長くなるので後述）．

以上をまとめると，ダランベールの原理は一般化座標と一般化力を用いて
$$
    \sum_j \left\lbrace\frac{{\rm d}}{{\rm d}t}\left(\frac{\partial T}{\partial \dot{q}_j}\right) + \frac{\partial T}{\partial q_j} - Q_j \right\rbrace \delta q_j=0

$$
となる．

今回は拘束条件を考えていないので，仮想変位$\delta q_j$はそれぞれ独立であり，$\delta q_j$がそれぞれどのような値を取ろうともダランベールの原理は成立する．
このためには，それぞれの$j$に対して
$$
\frac{{\rm d}}{{\rm d}t}\left(\frac{\partial T}{\partial \dot{q}_j}\right) + \frac{\partial T}{\partial q_j} - Q_j =0
$$
が成立する必要がある．

外力の一部が，あるスカラーポテンシャル関数$U$から以下のように導出できる場合を考えよう．
$$
F_i = F_i^{\rm e} - \nabla_i U
$$
ただし，
$$
    \nabla U = \left[\frac{\partial U}{\partial r_1}, \cdots,\frac{\partial U}{\partial r_i},\cdots \frac{\partial U}{\partial r_n}\right]^\top
$$
このとき，一般化力は
$$
    Q_j = \sum_i {\bm F}_i^{\rm e}\cdot\frac{\partial {\bm r}_i}{\partial q_j} - \sum_i \nabla_i U\cdot\frac{\partial {\bm r}_i}{\partial q_j}\\
    = Q_j^{\rm e} + \frac{\partial U}{\partial q_j}
$$
となることから，
$$
\frac{{\rm d}}{{\rm d}t}\left(\frac{\partial T}{\partial \dot{q}_j}\right) + \frac{\partial T}{\partial q_j} - \frac{\partial U}{\partial q_j} =Q_j^{\rm e}
$$
が得られる．
ポテンシャルが一般化速度に依存しないとき，さらに変形できて
$$
\frac{{\rm d}}{{\rm d}t}\left(\frac{\partial (T-U)}{\partial \dot{q}_j}\right) + \frac{\partial (T-U)}{\partial q_j} = Q_j^{\rm e}
$$
ラグランジアン$L=T-U$を用いると，
$$
\frac{{\rm d}}{{\rm d}t}\left(\frac{\partial L}{\partial \dot{q}_j}\right) + \frac{\partial L}{\partial q_j} = Q_j^{\rm e}
$$
となる．これを**ラグランジュの運動方程式**と呼ぶ．

### 慣性力項の計算

上で導出を省略した部分の補足を行う．
$$
    \sum_{i} m_i\ddot{{\bm r}}_i\cdot\frac{\partial {\bm r}_i}{\partial q_j} = \sum_i \left\lbrace \frac{{\rm d}}{{\rm d}t}\left( m_i \dot{\bm r}_i \cdot \frac{\partial {\bm r}_i}{\partial q_j} \right) - m_i \dot{\bm r}_i \cdot \frac{{\rm d}}{{\rm d}t} \left(\frac{\partial {\bm r}_i}{\partial q_j}\right) \right\rbrace
$$
について，チェインルールを用いて
$$
    \frac{{\rm d}}{{\rm d}t}\left(\frac{\partial {\bm r}_i}{\partial q_j}\right) = \sum_k \frac{\partial}{\partial q_k}\left(\frac{\partial {\bm r}_i}{\partial q_j}\right)\frac{{\rm d}q_k}{{\rm d}t} + \frac{\partial}{\partial t}\left(\frac{\partial {\bm r}_i}{\partial q_j}\right)\\
    = \sum_j \frac{\partial}{\partial q_j}\left(\frac{\partial {\bm r}_i}{\partial q_k}\right)\frac{{\rm d}q_k}{{\rm d}t} + \frac{\partial}{\partial q_j}\left(\frac{\partial {\bm r}_i}{\partial t}\right)
    =\frac{\partial \dot{\bm r}_i}{\partial q_j}
    =\frac{\partial {\bm v}_i}{\partial q_j}
$$
であることと，
$$
\frac{\partial {\bm v}_i}{\partial \dot{q}_j} = \frac{\partial {\bm r}_i}{\partial q_j}
$$
であることを用いると，
$$
    \sum_{i} m_i\ddot{{\bm r}}_i\cdot\frac{\partial {\bm r}_i}{\partial q_j}
    = \sum_i \left\lbrace \frac{{\rm d}}{{\rm d}t}\left( m_i {\bm v}_i \cdot \frac{\partial {\bm v}_i}{\partial \dot{q}_j} \right) - m_i {\bm v}_i \cdot \frac{\partial {\bm v}_i}{\partial q_j} \right\rbrace\\
    = \sum_i \left\lbrace \frac{{\rm d}}{{\rm d}t}\left( \frac{\partial (\frac{1}{2}m_i v_i^2)}{\partial \dot{q}_j} \right) - \frac{\partial (\frac{1}{2}m_i v_i^2)}{\partial q_j} \right\rbrace\\
    =\frac{{\rm d}}{{\rm d}t}\left( \frac{\partial T}{\partial \dot{q}_j} \right) - \frac{\partial T}{\partial q_j}
$$
が得られる．

## 特別な場合のラグランジュの運動方程式

ロボティクスや機械力学の問題では，ポテンシャルエネルギーは速度を用いず位置だけで表せる場合がほとんどである．
また，直交座標系を用いる限り，運動エネルギーは位置を用いず速度だけで表せる（円筒座標系など，座標が屈曲しているとその限りではない）．
このような場合においては，$\partial T/ \partial q_i =0$, $\partial U /\partial \dot{q}_i = 0$であることから，ラグランジュの運動方程式はラグランジアンを用いずに
$$
    \frac{{\rm d}}{{\rm d}t}\left(\frac{\partial T}{\partial \dot{q}_i}\right) + \frac{\partial U}{\partial q_i} = Q_i
$$
と表せる．
さらに，外力がすべて保存力であった場合，
$$
    \frac{{\rm d}}{{\rm d}t}\left(\frac{\partial T}{\partial \dot{q}_i}\right) + \frac{\partial U}{\partial q_i} = 0
$$
となる．これを公式として用いると計算が楽になるので，**適用条件に配慮した上で**活用しよう．

## Reference

ゴールドスタイン，ポール，サーフコ，「古典力学（上）　原著第3版」，吉岡書店，2006.