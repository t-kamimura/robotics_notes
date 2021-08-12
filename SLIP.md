# SLIPモデルの支配方程式

**走行**を表すためのシンプルなモデルの一つとして，バネと質点からなる**SLIP (Spring-Loaded Inverted Pendulum) モデル**  が存在する．これはヒト・カンガルー・ウマ・ゴキブリなど様々な動物の走行運動を近似するモデルとして広く用いられている．質点は身体を，質量のない線形な直動バネは脚を表している．


<div align="center">
    <img src="fig/SLIPmodel.png" alt="SLIPmodel" width = "450">
</div>


本稿では，このモデルの支配方程式を考える．
モデルは質点$m$と，質量を持たない脚からなる．脚は線形の直動バネ$k$とダンパ$c$からなるとする（$c=0$とする研究も多い）．脚の自然長は$l_0$とする．
脚の付根には駆動用のモーターが取り付けられており（ダンパ項を持たない場合ではモーターも無いことが多く，完全に受動的なモデルとなる），接地期において脚を動かすための駆動トルク$-\tau$を発生する．

このモデルは脚が地面に接地している**支持脚期 (Stance phase)** と，脚が地面から離れている**遊脚期 (Flight phase)** において運動方程式が切り替わる**ハイブリッドシステム**である．
遊脚期には，脚が鉛直方向に対してなす角は$\gamma^{\rm td}$を常に保つものとする．脚に質量はないので，この制御にトルクは必要ない．
脚先が高さ$0$となり地面に接したとき，遊脚期から支持脚期に切り替わる．このとき脚先は地表面に固定され，このあとは摩擦のないピンジョイントとして振る舞う．
支持脚期において，脚の長さを$l$，脚が鉛直方向に対してなす角を$\gamma$とする．
床反力がゼロになったとき，脚先の拘束は解除され，支持脚期から遊脚期に切り替わる．

質点の水平方向位置と鉛直方向位置をそれぞれ$x$と$y$で表す．

## 遊脚期の運動方程式

遊脚期 (Flight phase) には，質点には重力以外なんの力も働かない．バネで表された脚が質量を持たないからである．
このとき，運動方程式は以下のように表される．
$$
    m\ddot{x} = 0\\
    m\ddot{y} = -mg
$$
すなわち，遊脚期においてモデルは放物運動を行う．

## 支持脚期の運動方程式

ラグランジュの運動方程式から求める．まず，系のラグランジアン$L$は
$$
L = \frac{m}{2}(\dot{x}^2 + \dot{y}^2) - mgy - \frac{k}{2}(l-l_0)
$$
となる．ここで，
<!-- $$
    x = l \sin \gamma\\
    y = l \cos \gamma
$$
を用いて，状態変数を$l$と$\gamma$で置き換えてやると計算の見通しが良い．
ラグランジアンは
$$
    L = \frac{m}{2}(\dot{l}^2+l^2\dot{\gamma}^2) - mgl\cos\gamma - \frac{k}{2}(l-l_0)
$$
と書き直せることから，運動方程式は
$$
\frac{d}{dt}\left(\frac{\partial L}{\partial \dot{l}}\right) - \frac{\partial L}{\partial l} = m\ddot{l} -ml\dot{\gamma}^2 + mg\cos\gamma + k (l - l_0) = -c\dot{l}
$$

$$
\frac{d}{dt}\left(\frac{\partial L}{\partial \dot{\gamma}}\right) - \frac{\partial L}{\partial \gamma} = ml^2\ddot{\gamma} + 2ml\dot{l}\dot{\gamma} + mgl\sin\gamma = -\tau
$$
となる． -->
$$
l=\sqrt{x'^2 + y^2},
\gamma = \arctan\left(\frac{x'}{y}\right),\\
\dot{l} = \frac{x'\dot{x}+y\dot{y}}{\sqrt{x'^2+y^2}},
\dot{\gamma} = \frac{-x'\dot{y}+y\dot{x}}{x'^2+y^2}
$$
を用いて変数を$x$と$y$だけに書き換える．ここで$x'=x-x_0$は脚先が固定されている位置$x_0$から見た質点の水平方向位置である．
ラグランジュの運動方程式から，
$$
\frac{d}{dt}\left(\frac{\partial L}{\partial \dot{x}}\right) - \frac{\partial L}{\partial x} = m\ddot{x} + k\left(\sqrt{x'^2+y^2}-l_0\right)\frac{x'}{\sqrt{x'^2+y^2}}=F_x,\\
\frac{d}{dt}\left(\frac{\partial L}{\partial \dot{y}}\right) - \frac{\partial L}{\partial y} = m\ddot{y} + mg + k\left(\sqrt{x'^2+y^2}-l_0\right)\frac{y}{\sqrt{x'^2+y^2}}=F_y\\
$$
となる．ここで，ダンパとモーターから生成される力$F_x, F_y$については仮想仕事$\delta W=0$から求める．すなわち，$r=[x \ y]^\top$，$q=[l \ \gamma]^\top$，$F=[F_x\ F_y]^\top$，$Q=[-c\dot{l}\ \tau]^\top$とすると，
$$
\delta W = F^\top\delta r=Q^\top \delta q=0
$$
から
$$
F =\left( \frac{\partial r}{\partial q} \right)^\top Q =
\begin{bmatrix}
    \dfrac{x'}{\sqrt{x'^2+y^2}} & \dfrac{y}{x'^2+y^2}\\
    \dfrac{y}{\sqrt{x'^2+y^2}} & -\dfrac{x}{x'^2+y^2}
\end{bmatrix}
\begin{bmatrix}
    -c\dfrac{x'\dot{x}+y\dot{y}}{\sqrt{x'^2+y^2}}\\
    -\tau
\end{bmatrix}
=\begin{bmatrix}
-c\dfrac{x'\dot{x}+y\dot{y}}{{x'^2+y^2}}x' + \dfrac{y} {x'^2+y^2}\tau\\
-c\dfrac{x'\dot{x}+y\dot{y}}{{x'^2+y^2}}y - \dfrac{x} {x'^2+y^2}\tau
\end{bmatrix}
$$
を得る．まとめると，
$$
m\ddot{x} = -k\left(\sqrt{x'^2+y^2}-l_0\right)\frac{x'}{\sqrt{x'^2+y^2}}-c\dfrac{x'\dot{x}+y\dot{y}}{{x'^2+y^2}}x' + \dfrac{y} {x'^2+y^2}\tau,\\
m\ddot{y} = -mg - k\left(\sqrt{x'^2+y^2}-l_0\right)\frac{y}{\sqrt{x'^2+y^2}}-c\dfrac{x'\dot{x}+y\dot{y}}{{x'^2+y^2}}y - \dfrac{x'} {x'^2+y^2}\tau
$$
となる．

$c=0$，$\tau=0$の場合，質点に働く力は重力とバネの力だけであり，
$$
m\ddot{x} = -k\left(\sqrt{x'^2+y^2}-l_0\right)\frac{x'}{\sqrt{x'^2+y^2}},\\
m\ddot{y} = -mg - k\left(\sqrt{x'^2+y^2}-l_0\right)\frac{y}{\sqrt{x'^2+y^2}}$$
となる．
## フェーズの切り替え条件

### 接地条件

遊脚期において脚先高さがゼロになったとき，接地する．この条件を
$$
r_{\rm td}(r) = y - l_0\cos\gamma^{\rm td} = 0
$$
と表す．

### 離地条件

垂直床反力がゼロになったとき，離地する．この条件は，支持脚期における$y$の運動方程式から，

$$
 r_{\rm lo}(r,\dot{r})=- k\left(\sqrt{x'^2+y^2}-l_0\right)\frac{y}{\sqrt{x'^2+y^2}}-c\dfrac{x'\dot{x}+y\dot{y}}{{x'^2+y^2}}y - \dfrac{x} {x'^2+y^2}\tau=0
$$

とする．
$c=0$，$\tau=0$のとき，この条件は単純に
$$
r_{\rm lo}(r) = \sqrt{x'^2+y^2}-l_0 = 0
$$
と書き直せる．ただし，$y=0$のときも$r_{\rm lo}(r)=0$を満たすが，この場合は転倒しているとみなし，離地条件には含めなかった．