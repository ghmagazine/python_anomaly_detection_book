# 7章付録2 多変数線形回帰モデルの最尤推定

多変数線形回帰モデル

```math
\begin{aligned}
&\mu=\boldsymbol{w}^T\boldsymbol{x}+w_0 \\
&p(y \mid \boldsymbol{x}, \boldsymbol{w}, w_0, \sigma^2) = \mathcal{N}(\mu,\sigma^2)
\end{aligned}
\tag{7.25}
```

は、$\boldsymbol{w},w_0,\sigma$をパラメータとして持ちます。これらのパラメータの最尤推定値が、

```math
\hat{\boldsymbol{w}} = \bigl(\tilde{\boldsymbol{X}}\tilde{\boldsymbol{X}}^T\bigr)^{-1}\tilde{\boldsymbol{X}}\tilde{\boldsymbol{y}}
\tag{7.28}
```

```math
\hat{w}_0 = \bar{y} - \hat{\boldsymbol{w}}^T\bar{\boldsymbol{x}}
\tag{7.29}
```

```math
\hat{\sigma}^2 = \frac{1}{N} \sum_{i=1}^N \bigl(y^{(i)}-\bar{y} - \hat{\boldsymbol{w}}^T(\boldsymbol{x}^{(i)}-\bar{\boldsymbol{x}})\bigr)^2
\tag{7.30}
```

となることを示していきます。
　なお、$\bar{\boldsymbol{x}}$、$\bar{y}$は$\boldsymbol{x}$の標本平均ベクトルと$y$の標本平均

```math
\bar{\boldsymbol{x}}=\frac{1}{N}\sum_{i=1}^N \boldsymbol{x}^{(i)}, \quad \bar{y}=\frac{1}{N}\sum_{i=1}^N y^{(i)}
\tag{7.37}
```

で、$\tilde{\boldsymbol{X}}$、$\tilde{\boldsymbol{y}}$は各データ$\boldsymbol{x}^{(i)}$、$y^{(i)}$を中心化して全データをまとめた行列、ベクトル

```math
\begin{aligned}
\tilde{\boldsymbol{X}}
&=
\bigl(\boldsymbol{x}^{(1)}-\bar{\boldsymbol{x}}, \cdots, \boldsymbol{x}^{(N)}-\bar{\boldsymbol{x}} \bigr) \\
&=
\begin{pmatrix} x_1^{(1)}-\bar{x}_1 & \cdots & x_1^{(N)}-\bar{x}_1 \\
\vdots & \ddots & \vdots \\
x_M^{(1)}-\bar{x}_M & \cdots & x_M^{(N)}-\bar{x}_M \end{pmatrix} \\
\tilde{\boldsymbol{y}}
&=
\bigl(y^{(1)}-\bar{y}, \cdots, y^{(N)}-\bar{y}\bigr)^T
\end{aligned}
\tag{7.31}
```

を表します。

### 対数尤度の式の整理

書籍中の対数尤度の式 (4.20)と、モデルの式 (7.25)をまとめると、多変数線形回帰モデルの対数尤度は以下のように表されます。

```math
\begin{aligned}
\log L(\boldsymbol{y} \mid \boldsymbol{X}, \boldsymbol{w}, w_0, \sigma^2)
&=
\log \prod_{i=1}^N p(y^{(i)} \mid x^{(i)}, \boldsymbol{w}, w_0, \sigma^2) \\
&=
\sum_{i=1}^N \log \mathcal{N}(y^{(i)} \mid \boldsymbol{w}^T\boldsymbol{x}^{(i)}+w_0,\sigma^2) \\
&=
\sum_{i=1}^N \log \Bigl( \frac{1}{\sqrt{2 \pi \sigma^2}} \exp{\Bigl( -\frac{(y^{(i)}-(\boldsymbol{w}^T\boldsymbol{x}^{(i)}+w_0))^2}{2\sigma^2} \Bigr)} \Bigr) \\
&=
-\frac{N}{2}\log(2 \pi) - \frac{N}{2}\log \sigma^2 - \frac{1}{2\sigma^2}\sum_{i=1}^N (y^{(i)}-(\boldsymbol{w}^T\boldsymbol{x}^{(i)}+w_0))^2 \\
&=
-\frac{N}{2}\log(2 \pi) - \frac{N}{2}\log \sigma^2 - \frac{1}{\sigma^2}E_D(\boldsymbol{X},\boldsymbol{y},\boldsymbol{w},w_0)
\end{aligned}
\tag{7.26}
```

ただし

```math
E_D(\boldsymbol{X},\boldsymbol{y},\boldsymbol{w},w_0)=\frac{1}{2}\sum_{i=1}^N \bigl(y^{(i)}-(\boldsymbol{w}^T\boldsymbol{x}^{(i)}+w_0)\bigr)^2
\tag{7.27}
```

この対数尤度$\log L(\boldsymbol{y} \mid \boldsymbol{X}, \boldsymbol{w}, w_0, \sigma^2)$を$\boldsymbol{w},w_0$および$\sigma^2$に関してそれぞれ微分して0とおき、$\boldsymbol{w},w_0,\sigma^2$の極大値を計算することで、最尤推定値$\hat{\boldsymbol{w}},\hat{w}_0,\hat{\sigma}^2$を求めます。

##### 線形予測子の係数$w_1$と切片$w_0$の最尤推定値

　式 (7.26)の対数尤度$\log L(\boldsymbol{y} \mid \boldsymbol{X},\boldsymbol{w}, w_0, \sigma^2)$を、$w_0$に関して微分して0とおきます。

```math
\begin{aligned}
0
&=
\frac{\partial}{\partial w_0} \log L(\boldsymbol{y} \mid \boldsymbol{X},\boldsymbol{w}, w_0, \sigma^2) \\
&=
\frac{\partial}{\partial w_0} \bigl(-\frac{1}{\sigma^2}E_D(\boldsymbol{X},\boldsymbol{y},\boldsymbol{w},w_0)\bigr) \\
&=
-\frac{1}{2\sigma^2} \sum_{i=1}^N \frac{\partial}{\partial w_0} \bigl(y^{(i)}-(\boldsymbol{w}^T\boldsymbol{x}^{(i)}+w_0)\bigr)^2 \\
&=
-\frac{1}{2\sigma^2} \sum_{i=1}^N -2\bigl(y^{(i)}-(\boldsymbol{w}^T\boldsymbol{x}^{(i)}+w_0)\bigr) \\
&=
-\frac{1}{\sigma^2} \Bigl( \boldsymbol{w}^T\sum_{i=1}^N \boldsymbol{x}^{(i)} - \sum_{i=1}^N y^{(i)} + Nw_0 \Bigr)
\end{aligned}
\tag{7.201}
```
　
　変形して

```math
\begin{aligned}
w_0
&=
\frac{1}{N}\sum_{i=1}^N y^{(i)} - \boldsymbol{w}^T\frac{1}{N}\sum_{i=1}^N \boldsymbol{x}^{(i)} \\
&=
\bar{y} - \boldsymbol{w}^T\bar{\boldsymbol{x}}
\end{aligned}
\tag{7.202}
```
　
　となります。
これを式 (7.27)に代入すると、

```math
\begin{aligned}
E_D(\boldsymbol{X},\boldsymbol{y},\boldsymbol{w},w_0)
&=
\frac{1}{2}\sum_{i=1}^N \bigl(y^{(i)}-(\boldsymbol{w}^T\boldsymbol{x}^{(i)}+\bar{y} - \boldsymbol{w}^T\bar{\boldsymbol{x}})\bigr)^2 \\
&=
\frac{1}{2}\sum_{i=1}^N \bigl((y^{(i)}-\bar{y}) - \boldsymbol{w}^T(\boldsymbol{x}^{(i)}-\bar{\boldsymbol{x}})\bigr)^2
\end{aligned}
\tag{7.203}
```

　ここで、以下のように$\boldsymbol{x}^{(i)}$、$y^{(i)}$を中心化して全データまとめて表記します。

```math
\begin{aligned}
\tilde{\boldsymbol{X}}
&=
\bigl(\boldsymbol{x}^{(1)}-\bar{\boldsymbol{x}}, \cdots, \boldsymbol{x}^{(N)}-\bar{\boldsymbol{x}} \bigr)
=
\begin{pmatrix} x_{1}^{(1)}-\bar{x}_1 & \cdots & x_{1}^{(N)}-\bar{x}_1 \\
\vdots & \ddots & \vdots \\
x_{M}^{(1)}-\bar{x}_M & \cdots & x_{M}^{(N)}-\bar{x}_M \end{pmatrix} \\
\tilde{\boldsymbol{y}}
&=
\bigl(y^{(1)}-\bar{y}, \cdots, y^{(N)}-\bar{y}\bigr)^T
\end{aligned}
\tag{7.204}
```
　
　このとき、

```math
\begin{aligned}
&\tilde{\boldsymbol{y}}^T - \boldsymbol{w}^T \tilde{\boldsymbol{X}} \\
&=
\bigl((y^{(1)}-\bar{y}) - \boldsymbol{w}^T(\boldsymbol{x}^{(1)}-\bar{\boldsymbol{x}}), \cdots, (y^{(N)}-\bar{y}) - \boldsymbol{w}^T(\boldsymbol{x}^{(N)}-\bar{\boldsymbol{x}}) \bigr)
\end{aligned}
\tag{7.205}
```
　
　より、式 (7.203)も考慮すると、

```math
\begin{aligned}
&\frac{1}{2}\bigl(\tilde{\boldsymbol{y}}^T - \boldsymbol{w}^T \tilde{\boldsymbol{X}}\bigr
) \bigl(\tilde{\boldsymbol{y}}^T - \boldsymbol{w}^T \tilde{\boldsymbol{X}}\bigr
)^T \\
&=
\frac{1}{2}\bigl((y^{(1)}-\bar{y}) - \boldsymbol{w}^T(\boldsymbol{x}^{(1)}-\bar{\boldsymbol{x}})\bigr)^2 + \cdots + \frac{1}{2}\bigl((y^{(N)}-\bar{y}) - \boldsymbol{w}^T(\boldsymbol{x}^{(N)}-\bar{\boldsymbol{x}})\bigr)^2 \\
&=
\frac{1}{2}\sum_{i=1}^N \bigl((y^{(i)}-\bar{y}) - \boldsymbol{w}^T(\boldsymbol{x}^{(i)}-\bar{\boldsymbol{x}})\bigr)^2 \\
&=
E_D(\boldsymbol{X},\boldsymbol{y},\boldsymbol{w},w_0)
\end{aligned}
\tag{7.206}
```
　
　となります。

　次に式 (7.26)の対数尤度$\log L(\boldsymbol{y} \mid \boldsymbol{X},\boldsymbol{w}, w_0, \sigma^2)$を、$\boldsymbol{w}$に関して微分して0とおきます。

```math
\begin{aligned}
0
&=
\frac{\partial}{\partial \boldsymbol{w}} \log L(\boldsymbol{y} \mid \boldsymbol{X},\boldsymbol{w}, w_0, \sigma^2) \\
&=
\frac{\partial}{\partial \boldsymbol{w}} \bigl(-\frac{1}{\sigma^2}E_D(\boldsymbol{X},\boldsymbol{y},\boldsymbol{w},w_0)\bigr)
\end{aligned}
\tag{7.207}
```

　式 (7.206)を代入して

```math
\begin{aligned}
&=
-\frac{1}{2\sigma^2} \frac{\partial}{\partial \boldsymbol{w}} \bigl(\tilde{\boldsymbol{y}}^T - \boldsymbol{w}^T \tilde{\boldsymbol{X}}\bigr
) \bigl(\tilde{\boldsymbol{y}}^T - \boldsymbol{w}^T \tilde{\boldsymbol{X}}\bigr
)^T \\
&=
-\frac{1}{2\sigma^2} \frac{\partial}{\partial \boldsymbol{w}} \bigl( \tilde{\boldsymbol{y}}^T\tilde{\boldsymbol{y}} - 2\boldsymbol{w}^T\tilde{\boldsymbol{X}}\tilde{\boldsymbol{y}} + \boldsymbol{w}^T\tilde{\boldsymbol{X}}\tilde{\boldsymbol{X}}^T\boldsymbol{w} \bigr)
\end{aligned}
\tag{7.208}
```
　
　$\tilde{\boldsymbol{X}}\tilde{\boldsymbol{X}}^T$は対称行列になるので、対称行列$\boldsymbol{A}$に対する二次形式の微分の公式$\frac{\partial}{\partial \boldsymbol{x}} \boldsymbol{x}^T\boldsymbol{A}\boldsymbol{x}=2\boldsymbol{A}\boldsymbol{x}$と、ベクトルの微分公式$\frac{\partial}{\partial \boldsymbol{a}}\boldsymbol{a}^T\boldsymbol{b}=\boldsymbol{b}$を適用して、

```math
\begin{aligned}
&=
-\frac{1}{2\sigma^2} \bigl(- 2\tilde{\boldsymbol{X}}\tilde{\boldsymbol{y}} + 2\tilde{\boldsymbol{X}}\tilde{\boldsymbol{X}}^T\boldsymbol{w} \bigr) \\
&=
\frac{1}{\sigma^2} \bigl(\tilde{\boldsymbol{X}}\tilde{\boldsymbol{y}} - \tilde{\boldsymbol{X}}\tilde{\boldsymbol{X}}^T\boldsymbol{w} \bigr)
\end{aligned}
\tag{7.209}
```
　
　変形して

```math
\begin{aligned}
\tilde{\boldsymbol{X}}\tilde{\boldsymbol{X}}^T\boldsymbol{w}
&=
\tilde{\boldsymbol{X}}\tilde{\boldsymbol{y}} \\
\boldsymbol{w}
&=
\bigl(\tilde{\boldsymbol{X}}\tilde{\boldsymbol{X}}^T\bigr)^{-1}\tilde{\boldsymbol{X}}\tilde{\boldsymbol{y}}
\end{aligned}
\tag{7.210}
```

　よって$\boldsymbol{w}$の最尤推定量$\hat{\boldsymbol{w}}$は、

```math
\hat{\boldsymbol{w}} = \bigl(\tilde{\boldsymbol{X}}\tilde{\boldsymbol{X}}^T\bigr)^{-1}\tilde{\boldsymbol{X}}\tilde{\boldsymbol{y}}
\tag{7.211}
```
　
　と表せます。
　これを式 (7.202)に代入すると、$w_0$の最尤推定量$\hat{w}_0$は、

```math
\hat{w}_0 = \bar{y} - \hat{\boldsymbol{w}}^T\bar{\boldsymbol{x}}
\tag{7.212}
```
　
　のように表せます。

##### 分散パラメータ$\sigma^2$の最尤推定値

　式 (7.26)の対数尤度$\log L(\boldsymbol{y} \mid \boldsymbol{X},\boldsymbol{w}, w_0, \sigma^2)$を、$w_0$に関して微分して0とおきます。

```math
\begin{aligned}
0
&=
\frac{\partial}{\partial \sigma^2} \log L(\boldsymbol{y} \mid \boldsymbol{X},\boldsymbol{w}, w_0, \sigma^2) \\
&=
\frac{\partial}{\partial \sigma^2} \bigl( -\frac{N}{2}\log \sigma^2 - \frac{1}{\sigma^2}E_D(\boldsymbol{X},\boldsymbol{y},\boldsymbol{w},w_0)\bigr) \\
&=
\frac{E_D(\boldsymbol{X},\boldsymbol{y},\boldsymbol{w},w_0)}{\sigma^4}-\frac{N}{2\sigma^2}
\end{aligned}
\tag{7.213}
```

ここで、式 (7.203)の$\boldsymbol{w}$を最尤推定値$\hat{\boldsymbol{w}}$に置き換えると、二乗和誤差関数$E_D(\boldsymbol{X},\boldsymbol{y},\boldsymbol{w},w_0)$の最尤推定値は

```math
E_D(\hat{\boldsymbol{w}})
=
\frac{1}{2}\sum_{i=1}^N \bigl(y^{(i)}-\bar{y} - \hat{\boldsymbol{w}}^T(\boldsymbol{x}^{(i)}-\bar{\boldsymbol{x}})\bigr)^2
\tag{7.214}
```

　これを式 (7.213)の$E_D(\boldsymbol{X},\boldsymbol{y},\boldsymbol{w},w_0)$に代入すると、

```math
=\frac{1}{2\sigma^4} \Bigl(\sum_{i=1}^N \bigl(y^{(i)}-\bar{y} - \hat{\boldsymbol{w}}^T(\boldsymbol{x}^{(i)}-\bar{\boldsymbol{x}})\bigr)^2 - \sigma^2N \Bigr)
\tag{7.215}
```

　$\sigma^2>0$も考慮して変形すると、

```math
\sigma^2
=
\frac{1}{N} \sum_{i=1}^N \bigl(y^{(i)}-\bar{y} - \hat{\boldsymbol{w}}^T(\boldsymbol{x}^{(i)}-\bar{\boldsymbol{x}})\bigr)^2
\tag{7.217}
```

　よって$\sigma^2$の最尤推定量$\hat{\sigma}^2$は、

```math
\hat{\sigma}^2 = \frac{1}{N} \sum_{i=1}^N \bigl(y^{(i)}-\bar{y} - \hat{\boldsymbol{w}}^T(\boldsymbol{x}^{(i)}-\bar{\boldsymbol{x}})\bigr)^2
\tag{7.218}
```
　
　と表せます。
