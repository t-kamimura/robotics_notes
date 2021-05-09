# MATLABのシンボリック計算

## はじめに

MATLABには，数値計算だけでなく文字式の処理も行うシンボリック計算機能がついている．
これはSymbolic Math Toolboxが必要になる．

## 文字式の定義

この文字はシンボリックですよと宣言する．

```matlab
syms a b c
syms x y
```

## 文字式の計算

MATLAB文法で書ける．

```matlab
z = a*x + b*y + c
```

新たに`z`という変数が定義されたが，これはシンボリック変数から定義されたので，これもまたシンボリック変数として扱われる（`syms z`が必要ではない）

## 線形代数の演算

行列計算も得意．
まず，適当な行列$A$とベクトル$b$を用意しておく．

$$
    A = \begin{bmatrix}
        a_{11}    & a_{12}  & a_{13}\\
        a_{21}    & a_{22}  & a_{23}\\
        a_{31}    & a_{32}  & a_{33}
    \end{bmatrix},\quad
    B = \begin{bmatrix}
        b_{11}    & b_{12}  & b_{13}\\
        b_{21}    & b_{22}  & b_{23}\\
        b_{31}    & b_{32}  & b_{33}
    \end{bmatrix}
$$
$$
    b = \begin{bmatrix}
        b_{1}\\
        b_{2}\\
        b_{3}
    \end{bmatrix},\quad
    c = \begin{bmatrix}
        c_{1}\\
        c_{2}\\
        c_{3}
    \end{bmatrix}
$$

要素をシンボリック変数として定義し，行列とベクトルを作る．書き方は通常のMATLAB構文と同じ．

```matlab
syms a11 a12 a13 a21 a22 a23 a31 a32 a33
syms b11 b12 b13 b21 b22 b23 b31 b32 b33
syms b1 b2 b3
syms c1 c2 c3
A = [a11, a12, a13; a21, a22, a23; a31, a32, a33];
B = [b11, b12, b13; b21, b22, b23; b31, b32, b33];
b = [b1; b2; b3];
c = [c1; c2; c3];
```


### 加減算

```matlab
b + c   % ベクトルの加算
b - c   % ベクトルの減算
A + B   % 行列の加算
A - B   % 行列の減算
```

### 乗算

```matlab
A * B       % 行列同士の乗算
A * b       % 行列とベクトルの乗算
b.' * A * c % 二次形式（.'で転置を表す）
dot(b,c)    % ベクトルの内積
cross(b,c)  % ベクトルの外積
```

転置は`a'`ではなく`a.'`で表されることに注意しよう．

### 逆行列

逆行列は`inv(A)`で求められる．

```matlab
inv(A)      % 単純に逆行列を求める
inv(A)*b    % 逆行列とベクトルの積(1)
A\b         % 逆行列とベクトルの積(2)
```

`inv(A)`を計算してからベクトル`b`にかけるよりも，`A\b`と書いたほうが計算が速いらしい．

## 方程式を解く

解ける方程式であれば，`solve(方程式，変数)`関数が根をシンボリックに返してくれる．

```matlab
eq = a * x^2 + b * x + c;
solve(eq, x)
```

## 関数として保存

`matlabfunction`を使うことで，シンボリック計算の結果をMATLAB関数として保存できる．これでシンボリック計算と数値計算の橋渡しができる．

```matlab
matlabFunction(return_value,'file','filename','vars',{arg1, arg2, arg3});
```