# PRMLノート 第2章 確率分布

- [PRMLノート 第2章 確率分布](#prmlノート-第2章-確率分布)
  - [二値変数](#二値変数)
    - [ベータ分布](#ベータ分布)
  - [多値変数](#多値変数)
    - [ディリクレ分布](#ディリクレ分布)
  - [ガウス分布](#ガウス分布)

## 二値変数

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

### ベータ分布

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

## 多値変数

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

### ディリクレ分布

多項分布の共役分布を考える．
$$
\mathrm{Dir}(\boldsymbol{\mu}|\boldsymbol{\alpha}) = \frac{\Gamma(\alpha_0)}{\Gamma(\alpha_1)\cdots\Gamma(\alpha_K)}\prod_{k=1}^K\mu_k^{\alpha_k - 1}
$$
これを**ディリクレ分布**という．

## ガウス分布

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