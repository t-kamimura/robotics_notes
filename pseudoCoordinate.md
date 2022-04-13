# 角速度と擬座標

3次元空間内の角速度$\omega$は，3次元ベクトルで表せる．これを積分してもオイラー角にはならない．そもそも，角速度は積分できない．これはなぜか，そしてそのような場合にラグランジュの運動方程式はどのように表されるのか考えてみよう．

## 全微分型の微分方程式

角速度の議論を行う前にまず，積分関数が簡単に求められる微分方程式について考えるところから始めよう．
$$
F(x,y)dx + G(x,y)dy=0
$$
という形の微分方程式を全微分型の方程式と呼び，解は$\phi(x,y) = c$の形で与えられる．この方程式について詳しく見ていく．

### ポテンシャル関数が存在すること

ある関数$P, Q$がスカラーポテンシャル関数$\phi(x,y)$の偏微分で表されるとしよう．すなわち，
$$
P(x,y) = \frac{\partial \phi(x,y)}{\partial x}\\
Q(x,y) = \frac{\partial \phi(x,y)}{\partial y}
$$
とする．このとき，
$$
\frac{\partial P}{\partial y} = \frac{\partial Q}{\partial x}
$$
が成立する．$(x,y)$空間内にポテンシャル$\phi$に由来するベクトル場$(P,Q)$が存在すると考えるとイメージがつきやすい．

逆に，$\partial P/\partial y = \partial Q /\partial x$が成立するとしよう．このとき，
$$
\phi(x,y) = \int_{\pi_0}^x P(x,y)dx + \int_{y_0}^y Q(\pi_0,y)dy
$$
と定義すると，
$$
\frac{\partial \phi}{\partial x} = P(x,y)
$$
と
$$
\frac{\partial \phi}{\partial y}=\int_{\pi_0}^x \frac{\partial P}{\partial y}dx + Q(\pi_0,y)\\
=\int_{\pi_0}^x \frac{\partial Q}{\partial x}dx + Q(\pi_0,y)\\
= Q(x,y) - Q(\pi_0, y) + Q(\pi_0,y)\\
= Q(x,y)
$$
となり，$\phi$が確かにポテンシャル関数になっていることが確認される．

以上から，2次元ベクトル場$(P,Q)$がポテンシャル$\phi(x,y)$を持つための必要十分条件は$\partial P/\partial y - \partial Q /\partial x=0$が成立することである．
(ベクトル解析の言葉を使って，${\rm rot(P,Q)=0}$としてもよい)

言い換えると，偏微分が入れ替え可能すなわち
$$
\frac{\partial}{\partial y}\frac{\partial \phi}{\partial x}=\frac{\partial}{\partial x}\frac{\partial \phi}{\partial y}
$$
が成立することが，ポテンシャル関数が存在することの必要十分条件である（積分が経路に依存しない）．

以上から，全微分型の方程式
$$
P(x,y)dx+Q(x,y)dy=0
$$
の解は，ポテンシャル関数$\phi(x,y)=c$となる．$c$は任意定数．

### 一般化した全微分型の方程式

$k,l=1,...,n$のすべての値に対して
$$
\frac{\partial P_k}{\partial q_l} = \frac{\partial P_l}{\partial q_k}
$$
が成立するとき，ポテンシャル関数$\phi(q_1,...q_n)$が存在する．

全微分型の方程式
$$
P_1dq_1+P_2dq_2+\cdots+P_ndq_n=0
$$
の解はポテンシャル関数$\phi(q_1,...q_n)=c$で与えられる．$c$は任意定数．

## 真の座標と擬座標

力学の問題を考えよう．一般化座標$q_1,...q_n$で表される系におけるラグランジュの運動方程式は
$$
\frac{d}{dt}\left(\frac{\partial T}{\partial q_i}\right)-\frac{\partial T}{\partial q_i}=Q_i
$$
で与えられる．ここで，$T$は運動エネルギー，$Q_i$は一般化力である．

速度$\omega_1,...,\omega_n$を，一般化座標$\dot{q}_1,...\dot{q}_n$の一次結合で定義する：
$$
\omega_i = a_{i1}\dot{q}_1 + a_{i2}\dot{q}_2+\cdots+a_{in}\dot{q}_n
$$
ただし，$a_{ki}$は$q_1,...,q_n$の与えられた関数である．

上記の定義では，$\omega_i$は何らかの位置の時間微分としては定義されていない．この速度に対応する「位置」と呼べる関数$\pi_i$が存在するとしよう．このとき，$d\pi_i$を微分$dq_1,...dq_n$の一次結合で
$$
d\pi_i = a_{i1}d q_1 + a_{i2}d q_2 + \cdots + a_{in}d q_n
$$
と表す．$a_{ki}$は先ほどと同じ関数である．

ある$i$について，もし
$$
\frac{\partial a_{ki}}{\partial q_l}=\frac{\partial a_{li}}{\partial q_k}
$$
が成立するならば，$d\pi_i$の式は全微分型の方程式であり，その解$\pi_i$は簡単に求められる（ポテンシャル関数を求めればよい）ことになる．このような$\pi_i$を**真の座標**と呼ぶ．
この場合，$\omega_i$は正しく$\pi_i$の時間微分として与えられることになる．
【注意】「ポテンシャル関数」と書いたが，エネルギーを求めるわけではない．速度を積分して位置を求める問題であることを失念してはならない．

ここで，$\partial a_{ki}/{\partial q_l}\neq\partial a_{li}/{\partial q_k}$となる場合を考えてみる．積分の順番によって結果が変わる場合である．
この場合には，$d\pi_1,...,d\pi_n$は$\pi_1,...,\pi_n$の微分にはならない．このような量$d\pi_1,...d\pi_n$を**擬座標の微分**と呼ぶ．
すなわち，速度を積分した量としての位置を定義できない．

## 擬座標でのラグランジュ方程式

### 座標変換

#### 一般化力の変換
一般化速度$\dot{q}_k$を速度$\omega_1,...,\omega_n$で表すと
$$
q_k=b_{k1}\omega_1+\cdots+b_{kn}\omega_n
$$
となる．ラグランジュ方程式にそれぞれ$b_{kr}$をかけて，$k=1,2,...,n$について和をとると
$$
\sum_{k=1}^n b_{kr}\left\lbrace \frac{d}{dt}\left(\frac{\partial T}{\partial \dot{q}_k}\right)-\frac{\partial T}{\partial q_k}\right\rbrace = \sum_{k=1}^n b_{kr}Q_k
$$
任意の無限小変位$(\delta \pi_1,...,\delta \pi_n)$において外力が系にする仕事を$\delta W = F_1\delta \pi_1+\cdots+F_n\delta \pi_n$とすると，$F_r$が新しい座標系における「一般化力」となり，
$$
\sum_{k=1}^n b_{kr}\left\lbrace \frac{d}{dt}\left(\frac{\partial T}{\partial \dot{q}_k}\right)-\frac{\partial T}{\partial q_k}\right\rbrace = F_r
$$
を得る．

#### 運動エネルギーの書き換え

運動エネルギーも新しい速度の定義で書き直そう．
$$
T(\dot{q}_1,...,\dot{q}_n)=\bar{T}(\omega_1,...,\omega_n)
$$
としたとき
$$
\frac{\partial T}{\partial \dot{q}_k}=\sum_{s=1}^n a_{ks}\frac{\partial \bar{T}}{\partial \omega_s}
$$
となり，ラグランジュ方程式は
$$
\sum_{k} b_{kr}\left\lbrace \sum_{s} a_{ks}\frac{d}{dt}\left(\frac{\partial \bar{T}}{\partial \omega_s}\right)+ \sum_{s}\frac{\partial \bar{T}}{\partial \omega_s}\frac{d a_{ks}}{dt} -\frac{\partial T}{\partial q_k}\right\rbrace = F_r
$$
と書き直される．

#### 係数の整理

ここで，
$$
\dot{q}_k = b_{k1}\omega_1 + \cdots + b_{kn}\omega_n\\
= b_{k1}(a_{11}\dot{q}_1+\cdots+a_{1k}\dot{q}_k+\cdots+a_{1n}\dot{q}_n)\\
+b_{k2}(a_{21}\dot{q}_1+\cdots+a_{2k}\dot{q}_k+\cdots+a_{2n}\dot{q}_n)\\
\vdots\\
+b_{kn}(a_{n1}\dot{q}_1+\cdots+a_{nk}\dot{q}_k
+\cdots+a_{nn}\_dot{q}_n)\\
=\sum_s b_{ks}a_{s1}\dot{q}_1 + \cdots + \sum_s b_{ks}a_{sk}\dot{q}_k + \cdots + \sum_s b_{ks}a_{sn}\dot{q}_n
$$
であるから，
$$
\sum_s b_{ks}a_{sl}=\begin{cases}
1 & k=l\\
0 & k \neq l
\end{cases}
$$
となる．これをラグランジュ方程式に代入して整理すると，
