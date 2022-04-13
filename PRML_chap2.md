# PRMLノート 第2章 確率分布 <!-- omit in toc -->

- [1. 二値変数](#1-二値変数)
  - [1.1. ベータ分布](#11-ベータ分布)
- [2. 多値変数](#2-多値変数)
  - [2.1. ディリクレ分布](#21-ディリクレ分布)
- [3. ガウス分布](#3-ガウス分布)
  - [3.1. 分割されたガウス分布](#31-分割されたガウス分布)
  - [3.2. ガウス分布の最尤推定](#32-ガウス分布の最尤推定)
  - [3.3. 逐次推定](#33-逐次推定)
  - [ガウス分布に対するベイズ推論](#ガウス分布に対するベイズ推論)

## 1. 二値変数

コインの表・裏のように2つの値を取る確率変数$x$について，$x=1$となる確率を$\mu$とすると，$x$の確率分布は
$$
\mathrm{Bern}(x|\mu) = \mu^x(1-\mu)^{(1-x)}
$$
となる．これを**ベルヌーイ分布**という．この分布の平均と分散は
$$
\mathbb{E}[x]=\mu\\
\mathrm{var}[x] = \mu(1-\mu)
$$
である．

$N$個のデータ$\{x_n\}$からパラメータ$\mu$を推定する．最尤推定から
$$
\mu_\mathrm{ML} = \frac{1}{N}\sum_{n=1}^N x_n
$$
を得る．これは**サンプル平均**．

$N$回の試行のうち$x=1$となる回数$m$の分布を考える．
$$
    \mathrm{Bin}(m|N,\mu) = \begin{pmatrix}N\\m\end{pmatrix}\mu^n(1-\mu)^{N-m}
$$
これを**二項分布**という．この分布の平均と分散は
$$
\mathbb{E}[m]=N\mu\\
\mathrm{var}[m] = N\mu(1-\mu)
$$
である．

### 1.1. ベータ分布

ベイズ的にベルヌーイ分布を扱う．このとき，事前分布と事後分布が同じ関数形式になるよう（**共役性**）にしたい．

次の**ベータ分布**を事前分布とする．
$$
\mathrm{Beta}(\mu|a,b)=\frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)}\mu^{a-1}(1-\mu)^{b-1}
$$
ここで$\Gamma(\cdot)$は**ガンマ関数**．$a$と$b$は**超パラメータ**．
ベータ分布は正規化されており，平均と分散は
$$
\mathbb{E}[x]=\frac{a}{a+b}\\
\mathrm{var}[x] = \frac{ab}{(a+b)^2(a+b+1)}
$$
である．

$\mu$の事後分布を求める．
$$
p(\mu|m,l,a,b) \propto \mathrm{Bin}(m|N,\mu)\mathrm{Beta}(\mu|a,b)
=\mu^{m+a-1}(1-\mu)^{l+b-1}
$$
$N$は全試行回数．$m$はそのうち$x=1$となった回数．$l=N-m$は$x=0$の回数．$a$と$b$は予め分かっていた$x=1$と$x=0$の回数（**有効観測数**）．

## 2. 多値変数

様々な値を取る離散変数は，二値変数を並べたものとして扱う．すなわち，要素の一つが1で残り全部が0であるような$K$次元ベクトル$\mathbf{x}$．
$\mathbf{x}$の分布は
$$
p(\mathbf{x}|\mathbf{\mu}) = \prod_{k=1}^K \mu_k^{x_k}
$$
で与えられる．

$N$個のデータから最尤推定で$\mu_\mathrm{ML}$を求めると，
$$
\mu_k^\mathrm{ML}=\frac{m_k}{N}
$$
すなわち$N$個のうち$x_k=1$となっているものの割合．

$\mu$と$N$が与えられた中で，$m_1,\ldots, m_K$の同時確率は
$$
\mathrm{Mult}(m_1,\ldots,m_K|\mu,N) = \begin{pmatrix}N\\m_1m_2\cdots m_K\end{pmatrix}\prod_{k=1}^K \mu_k^{m_k}
$$
であり，これを**多項分布**という．

### 2.1. ディリクレ分布

多項分布の共役分布を考える．
$$
\mathrm{Dir}(\boldsymbol{\mu}|\boldsymbol{\alpha}) = \frac{\Gamma(\alpha_0)}{\Gamma(\alpha_1)\cdots\Gamma(\alpha_K)}\prod_{k=1}^K\mu_k^{\alpha_k - 1}
$$
これを**ディリクレ分布**という．

## 3. ガウス分布

$D$次元ベクトル$\mathbf{x}$のガウス分布
$$
\mathcal{N}(\mathbf{x}|\boldsymbol{\mu},\boldsymbol{\Sigma}) = \frac{1}{(2\pi)^{D/2}}\frac{1}{|\boldsymbol{\Sigma}|^{1/2}}\exp\left\{\frac{1}{2}(\mathbf{x}-\boldsymbol{\mu})^\top\boldsymbol{\Sigma}^{-1}(\mathbf{x}-\boldsymbol{\mu})\right\}
$$
平均と分散は
$$
\mathbb{E}(\mathbf{x}) = \boldsymbol{\mu}\\
\mathrm{cov}(\mathbf{x}) = \boldsymbol{\Sigma}
$$
二次形式のところだけ取り出して考えることが多い．これを**マハラノビス距離**という．
$$
\Delta^2 = (\mathbf{x}-\boldsymbol{\mu})^\top\boldsymbol{\Sigma}^{-1}(\mathbf{x}-\boldsymbol{\mu})
$$

### 3.1. 分割されたガウス分布

$\mathbf{x}$を$\mathbf{x}_a$と$\mathbf{x}_b$に分割する．
$$
\mathbf{x} = \begin{pmatrix}
    x_a\\x_b
\end{pmatrix},
\boldsymbol{\mu} = \begin{pmatrix}
    \mu_a\\\mu_b
\end{pmatrix},
\boldsymbol{\Sigma}= \begin{pmatrix}
    \boldsymbol{\Sigma}_{aa} & \boldsymbol{\Sigma}_{ab}\\ \boldsymbol{\Sigma}_{ba} & \boldsymbol{\Sigma}_{bb}
\end{pmatrix}
$$
**精度行列**$\boldsymbol{\Lambda}=\boldsymbol{\Sigma}^{-1}$として，
$$
\boldsymbol{\Lambda}= \begin{pmatrix}
    \boldsymbol{\Lambda}_{aa} & \boldsymbol{\Lambda}_{ab}\\ \boldsymbol{\Lambda}_{ba} & \boldsymbol{\Lambda}_{bb}
\end{pmatrix}
$$
とおくと，二次形式の部分を**平方完成**することにより条件付き分布
$$
  p(\mathbf{x}_a|\mathbf{x}_b) = \mathcal{N}(\mathbf{x}|\boldsymbol{\mu}_{a|b},\boldsymbol{\Lambda}_{aa}^{-1})\\
  \boldsymbol{\mu}_{a|b}=\boldsymbol{\mu}_{a} - \boldsymbol{\Lambda}_{aa}^{-1}\boldsymbol{\Lambda}_{ab}(\mathbf{x}_b - \boldsymbol{\mu}_b)
$$
を得る．
また周辺確率は
$$
  p(\mathbf{x}_a) = \mathcal{N}(\mathbf{x}_a|\boldsymbol{\mu}_a, \boldsymbol{\Sigma}_{aa})
$$
となる．

### 3.2. ガウス分布の最尤推定

多変量ガウス分布から得られrたデータ集合$\mathbf{X} = (\mathbf{x}_1,\ldots,\mathbf{x}_N)^\top$がある時，最尤推定により
$$
  \boldsymbol{\mu}_{\mathrm{ML}}=\frac{1}{N}\sum_{n=1}^N \mathbf{x}_n\\
  \boldsymbol{\Sigma}_{\mathrm{ML}}=\frac{1}{N}\sum_{n=1}^N (\mathbf{x}_n - \boldsymbol{\mu}_{\mathrm{ML}})(\mathbf{x}_n - \boldsymbol{\mu}_{\mathrm{ML}})^\top
$$
このとき
$$
  \mathbb{E}[\boldsymbol{\mu}_{\mathrm{ML}}] = \boldsymbol{\mu}\\
  \mathbb{E}[\boldsymbol{\Sigma}_{\mathrm{ML}}] = \frac{N-1}{N}\boldsymbol{\Sigma}
$$
であり，$N$が小さいと共分散行列を過小評価してしまう．そこで，
$$
\tilde{\boldsymbol{\Sigma}}_{\mathrm{ML}}=\frac{1}{N-1}\sum_{n=1}^N (\mathbf{x}_n - \boldsymbol{\mu}_{\mathrm{ML}})(\mathbf{x}_n - \boldsymbol{\mu}_{\mathrm{ML}})^\top
$$
とすると，$\tilde{\boldsymbol{\Sigma}}_{\mathrm{ML}}$の期待値は真の共分散行列と一致する．

### 3.3. 逐次推定

$N$回の観測に基づく推定量を$\boldsymbol{\mu}^{(N)}$と表す．
$$
  \boldsymbol{\mu}^{(N)} = \boldsymbol{\mu}^{(N-1)} + \frac{1}{N}(\mathbf{x}_N - \boldsymbol{\mu}^{(N-1)})
$$

### ガウス分布に対するベイズ推論

パラメータ上の事前分布を導入する．

１変数のガウス分布で，分散$\sigma$は既知とする．
与えられたデータ$\boldsymbol{\mathsf{x}}=\{x_1,\ldots,x_N\}$から平均$\mu$を求める．尤度関数は
$$
p(\boldsymbol{\mathsf{x}}|\mu)=\prod_{n=1}^N p(x_n|\mu)=\frac{1}{(2\pi\sigma^2)^{N/2}}\exp\left\{-\frac{1}{2\sigma^2}\sum_{n=1}^N (x_n-\mu)^2\right\}
$$
尤度関数の共役事前分布としてガウス分布を選ぶ．
$$
p(\mu) = \mathcal{N}(\mu|\mu_0,\sigma_0^2)
$$
このとき事後分布は
$$
p(\mu|\boldsymbol{\mathsf{x}})=\mathcal{N}(\mu|\mu_N, \sigma_N^2)\\
\mu_N = \frac{\sigma^2}{N\sigma_0^2+\sigma^2}\mu_0 + \frac{N\sigma_0^2}{N\sigma_0^2+\sigma^2}\mu_\mathrm{ML}\\
\frac{1}{\sigma_N^2}=\frac{1}{\sigma_0^2}+\frac{N}{\sigma^2}
$$
ただし$\mu_\mathrm{ML}$はサンプル平均で，$\mu$の最尤推定解．
$N\rightarrow \infty$の極限で，事後分布の平均は最尤推定解となり，分散$\sigma_N^2$はゼロに近づく．

逆に平均が既知で，分散を推定する問題を考える．
尤度関数は
$$
p(\boldsymbol{\mathsf{x}}|\lambda)=\prod_{n=1}^N\mathcal{N}(x_n|\lambda)\propto \lambda^{N/2}\exp\left\{\frac{\lambda}{2}\sum_{n=1}^{N}(x_n-\mu)^2\right\}
$$
共役事前分布としてガンマ分布を取る．
$$
\mathrm{Gam}(\lambda|a,b)=\frac{1}{\Gamma(a)}b^a\lambda^{a-1}\exp(-b\lambda)
$$
事後分布は
$$
p(\lambda|\boldsymbol{\mathsf{x}})\propto \lambda^{a_0-1}\lambda^{N/2}\exp\left\{-b_0\lambda-\frac{\lambda}{2}\sum_{n=1}^{N}(x_n-\mu)^2\right\}
$$
ハイパーパラメータは，その分散が$2b_0/(2a_0)$であるような，$2a_0$個の有効な観測値があることを示す．


平均も分散も未知のとき，共役事前分布は**正規-ガンマ分布**
$$
p(\mu,\lambda)=\mathcal{N}(\mu|\mu_0,(\beta\lambda)^{-1})\mathrm{Gam}(\lambda|a,b)
$$

$D$次元多変量ガウス分布$\mathcal{N}(\mathbf{x}|\boldsymbol{\mu},\boldsymbol{\Lambda}^{-1})$を考える．

平均が未知で分散が既知なら共役事前分布はガウス分布である．

平均が既知で分散が未知なら，共役事前分布はウィシャート分布
$$
\mathcal{W}(\boldsymbol{\Lambda}|\mathbf{W},\nu)=B|\Lambda|^{(\nu-D-1)/2}\exp\left(-\frac{1}{2}\mathrm{Tr}(\mathbf{W}^{-1}\boldsymbol{\Lambda})\right)
$$

