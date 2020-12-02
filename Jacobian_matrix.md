# ベクトルにかかっている行列を求める

## 定理

あるベクトル$x \in {\rm R}^n$, $y \in {\rm R}^m$の間に
$$
    Ax = y
$$
という関係が成立している．
$x$と$y$は既知であり，$A\in {\rm R}^{m\times n}$が未知の場合を考えよう．

このとき，かかっている行列$A$はヤコビ行列を用いて

$$
A = \frac{\partial y}{\partial x}
=\begin{bmatrix}
\dfrac{\partial y_1}{\partial x_1} & \dfrac{\partial y_1}{\partial x_2} & \cdots & \dfrac{\partial y_1}{\partial x_n}\\
\dfrac{\partial y_2}{\partial x_1} & \dfrac{\partial y_2}{\partial x_2} & \cdots & \dfrac{\partial y_2}{\partial x_n}\\
\vdots & \vdots & \ddots & \vdots\\
\dfrac{\partial y_n}{\partial x_1} & \dfrac{\partial y_n}{\partial x_2} & \cdots & \dfrac{\partial y_n}{\partial x_n}\\
\end{bmatrix}
$$

で求められる．

## 証明

$x \in {\rm R}^n$に対して定義される関数$f(x) \in {\rm R}$の全微分は

$$
f'(x) = \dfrac{\partial f}{\partial x_1} dx_1+ \dfrac{\partial f}{\partial x_2} dx_2 + \cdots +\dfrac{\partial f}{\partial x_n} dx_n
$$

で与えられる．

$y=f(x)\in {\rm R}^m$でも同様に，全微分は

$$
dy_1 = f_1'(x) = \dfrac{\partial f_1}{\partial x_1} dx_1+ \dfrac{\partial f_1}{\partial x_2} dx_2 + \cdots +\dfrac{\partial f_1}{\partial x_n} dx_n\\
dy_2 =f_2'(x) = \dfrac{\partial f_2}{\partial x_1} dx_1+ \dfrac{\partial f_2}{\partial x_2} dx_2 + \cdots +\dfrac{\partial f_2}{\partial x_n} dx_n\\
\vdots\\
dy_m =f_m'(x) = \dfrac{\partial f_m}{\partial x_1} dx_1+ \dfrac{\partial f_m}{\partial x_2} dx_2 + \cdots +\dfrac{\partial f_m}{\partial x_n} dx_n
$$

で与えられる．

ここでヤコビ行列$J$を

$$
J = \frac{\partial f}{\partial x}
=\begin{bmatrix}
\dfrac{\partial f_1}{\partial x_1} & \dfrac{\partial f_1}{\partial x_2} & \cdots & \dfrac{\partial f_1}{\partial x_n}\\
\dfrac{\partial f_2}{\partial x_1} & \dfrac{\partial f_2}{\partial x_2} & \cdots & \dfrac{\partial f_2}{\partial x_n}\\
\vdots & \vdots & \ddots & \vdots\\
\dfrac{\partial f_m}{\partial x_1} & \dfrac{\partial f_m}{\partial x_2} & \cdots & \dfrac{\partial f_m}{\partial x_n}\\
\end{bmatrix}
$$

とおいたとき，上式は

$$
dy = f'(x) = Jdx
$$

と書ける．

一方，$y=Ax$が成立することから
$$
dy = Adx
$$
も成立する．
したがって，$A=J=\partial y/\partial x$となる．（証明終了）