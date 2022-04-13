**# シンボリック計算によって運動方程式を求める

ある系に対してラグランジアンを求め，そこから運動方程式を求めることができる．ただし，この計算は常に手計算によって簡単に完了するものとは限らない．
ここでは，MATLABやMapleといった代数計算を可能とするソフトウェアを用いて，運動方程式を導出する方法をまとめる．

## 求める運動方程式

系に対してラグランジアン$L$が求められているとして，ラグランジュの運動方程式は
$$
    \frac{{\rm d}}{{\rm d}t}\left(\frac{\partial L}{\partial \dot{q}_i}\right) - \frac{\partial L}{\partial q_i} = Q_i  \tag{1}
$$
で与えられる．ここで，$q_i$は一般化座標の$i$番目の成分である．
運動方程式はまた，
$$
M(q)\ddot{q}+h(q,\dot{q})+g(q)=Q    \tag{2}
$$
と表すこともできる．$M(q)$は慣性行列，$h(q,\dot{q})$は遠心力とコリオリ力の和，$g(q)$はポテンシャルから受ける力である．
今回は，(1)式から(2)式を導出する過程を，MATLABシンボリック計算で実行する方法を紹介する．他の言語に応用することも容易いだろう．

## 準備

### 時間微分

ラグランジュの運動方程式を導出する上で，まず直面する壁は，シンボリック計算でどのようにして時間微分を行うか，というところにある．
あらかじめ一般化座標を時間の関数として定義し，微分関数`diff`を用いて時間微分を行う方法もあるが，ここではもっと簡便な方法を説明する．

ある関数$f(x_1, x_2, \cdots, x_n)$の時間微分を考える．このとき，連鎖律より
$$
    \frac{{\rm d}f}{{\rm d}t} = \frac{\partial f}{\partial x_1}\frac{{\rm d}x_1}{{\rm d}t} + \frac{\partial f}{\partial x_2}\frac{{\rm d}x_2}{{\rm d}t} + \cdots + \frac{\partial f}{\partial x_n}\frac{{\rm d}x_n}{{\rm d}t}\\
    = \sum_{k=1}^n \frac{\partial f}{\partial x_k}\dot{x}_k
$$
と表すことができる．

これをMATLABで計算する方法を考えよう．
まず，一般化座標$q$と一般化速度$\dot{q}$を独立変数として定義する．

```matlab
syms x1 y1 x2 y2
syms dx1 dy1 dx2 dy2
q = [x1; y1; x2; y2];
dq = [dx1; dy1; dx2; dy2];
```

`q`は一般化座標，`dq`は全微分のような表記になっているが，一般化座標の時間微分としていることに注意されたい．ある関数$f(x_1, x_2, y_1, y_2)$を時間微分するという演算は，
```matlab
dfdt = diff(f,x1)*dx1 + diff(f,y1)*dy1 + diff(f,x2)*dx2 + diff(f,y2)*dy2
```
と書ける．


**一般化座標と一般化速度を独立変数として扱う**ことは，解析力学的な観点から見ても妥当だろう．これらは微分・積分の関係にあり，一見独立ではないように思えるが，例えばある粒子を考えたとき，その位置と速度は独立に設定することができる．（運動があらかじめわかっているのでなければ，ある時点での位置を決めたからといって，その速度が一意に定まるというのはおかしな話であるから）

### ヤコビ行列を用いる

時間微分は，ヤコビ行列を用いるともっと簡単に書ける．まず，ヤコビ行列とは，ベクトル$q \in \mathbb{R}^n$とベクトル関数$f(q) \in \mathbb{R}^m$について
$$
\frac{\partial f}{\partial q} = \begin{bmatrix}
  \dfrac{\partial f}{\partial q_1} \ \dfrac{\partial f}{\partial q_2} \ \cdots \ \dfrac{\partial f}{\partial q_n}   
\end{bmatrix}\in \mathbb{R}^{m\times n}
$$
と定義される行列のことである．
これを用いると，$f(q)$の時間微分は，
$$
    \frac{{\rm d}f}{{\rm d}t} = 
    \begin{bmatrix}
        \dfrac{\partial f_1}{\partial q_1}\dfrac{{\rm d}q_1}{{\rm d}t} + \dfrac{\partial f_1}{\partial q_2}\dfrac{{\rm d}q_2}{{\rm d}t} + \cdots + \dfrac{\partial f_1}{\partial q_n}\dfrac{{\rm d}q_n}{{\rm d}t}\\
        \dfrac{\partial f_2}{\partial q_1}\dfrac{{\rm d}q_1}{{\rm d}t} + \dfrac{\partial f_2}{\partial q_2}\dfrac{{\rm d}q_2}{{\rm d}t} + \cdots + \dfrac{\partial f_2}{\partial q_n}\dfrac{{\rm d}q_n}{{\rm d}t}\\
        \vdots\\
        \dfrac{\partial f_m}{\partial q_1}\dfrac{{\rm d}q_1}{{\rm d}t} + \dfrac{\partial f_m}{\partial q_2}\dfrac{{\rm d}q_2}{{\rm d}t} + \cdots + \dfrac{\partial f_m}{\partial q_n}\dfrac{{\rm d}q_n}{{\rm d}t}
    \end{bmatrix}
    = \frac{\partial f}{\partial q}\dot{q}
$$
と表すことができる．
これをMATLABプログラムにすると，

```matlab
dfdt = jacobian(f,q)*q;
```

となる．`diff`を使ったときと比較して，かなり簡単にかけることに気づくだろう．

(註)ここで筆者がよくやるミスとして，`q`を縦ベクトルにするのを忘れてしまうことがある．

## 運動方程式の導出

ラグランジュの運動方程式をMATLABで計算する．時間微分に関する上記の関係から，
$$
\frac{{\rm d}}{{\rm d}t}\frac{\partial L}{\partial \dot{q}} = \frac{\partial}{\partial \dot{q}}\left( \frac{\partial L}{\partial \dot{q}}\right)\ddot{q} + \frac{\partial}{\partial q}\left( \frac{\partial L}{\partial \dot{q}}\right)\dot{q}
$$
であるため，(1)と(2)の係数を比較して
$$
M(q)=\frac{\partial}{\partial \dot{q}}\left( \frac{\partial L}{\partial \dot{q}}\right)\\
h(q, \dot{q}) + g(q) = \frac{\partial}{\partial q}\left( \frac{\partial L}{\partial \dot{q}}\right)\dot{q} - \frac{\partial L}{\partial q}
$$
だとわかる．
遠心力・コリオリ力は分けてもよいが，それをするメリットはない（後述参照）．

以上をまとめると，運動方程式は
$$
\left[\frac{\partial}{\partial \dot{q}}\left( \frac{\partial L}{\partial \dot{q}}\right)\right]\ddot{q} + \frac{\partial}{\partial q}\left( \frac{\partial L}{\partial \dot{q}}\right)\dot{q} - \frac{\partial L}{\partial q} = Q
$$
となる．

上記の計算をMATLABで行う．ラグランジアン`L`が計算できているものとして，

```matlab
M = jacobian(jacobian(L,dq),dq);
CoriGrav = jacobian(jacobian(L,dq),q)*dq - jacobian(L,q);
```

によってそれぞれの項が求められる．

## 1階の微分方程式に変換する

MATLABで微分方程式を数値積分するためには，`ode45`関数を用いる．ただし，これは1階の微分方程式しか解くことができない．そのため，上記で得られた運動方程式を下記の方法で1階の連立微分方程式に変換する．
$$
x=\begin{bmatrix}
    q\\
    \dot{q}
\end{bmatrix}
$$
という変数を用意すると，(1)を変形した
$$
\ddot{q} = M(q)^{-1}(-h(q,\dot{q})-g(q)+Q)
$$
から
$$
\dot{x} = \begin{bmatrix}
    \dot{q}\\
    \ddot{q}
\end{bmatrix}=
\begin{bmatrix}
    \dot{q}\\
    M(q)^{-1}(-h(q,\dot{q})-g(q)+Q)
\end{bmatrix}
$$
を得る．
`ode45`関数は，ベクトルの微分方程式，すなわち連立１次微分方程式は解くことができるので，この状態の方程式を渡してやればよい．すなわち，微分方程式を表すMATLAB関数は

```matlab
dx = [dq;　M\(-CoriGrav + Q)];
```

となる．2階微分を表す`ddq`は運動方程式を書き表す上で必要ない（拘束条件がない場合の話）．

## まとめ

シンボリック計算で運動方程式を導出する方法を紹介した．この方法は，シミュレータを作成するときに特に役立つだろう．MATLABでは，シンボリック計算を行った結果をMATLAB関数として出力する`matlabfunction`という関数がある．これを用いることで，シミュレータを作成するのが非常に簡単になる．**