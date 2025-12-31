# 7章付録1 1変数線形回帰モデルの最尤推定

1変数線形回帰モデル

```math
\begin{aligned}
&\mu=w_1x+w_0 \\
&p(y \mid x, w_1, w_0, \sigma^2) = \mathcal{N}(\mu,\sigma^2)
\end{aligned}
\tag{7.11}
```

は、$w_1,w_0,\sigma$をパラメータとして持ちます。これらのパラメータの最尤推定値が、

```math
\hat{w}_1 = \frac{\hat{\sigma}_{xy}^2}{\hat{\sigma}_x^2}
\tag{7.17}
```

```math
\hat{w}_0 = \bar{y} - \hat{w}_1\bar{x}
\tag{7.18}
```

```math
\hat{\sigma}^2 = \frac{1}{N} \sum_{i=1}^N \bigl(y^{(i)}-\bar{y} - \hat{w}_1(x^{(i)}-\bar{x})\bigr)^2
\tag{7.19}
```
　
となることを示していきます。
　なお、$\bar{x}$、$\bar{y}$は$x$、$y$の標本平均

```math
\bar{x}=\frac{1}{N}\sum_{i=1}^N x^{(i)}, \quad \bar{y}=\frac{1}{N}\sum_{i=1}^N y^{(i)}
\tag{7.20}
```

で、$\hat{\sigma}_x^2$は$x$の標本分散、$\hat{\sigma}_{xy}^2$は$x$と$y$の標本共分散

```math
\begin{aligned}
\hat{\sigma}_x^2
&=
\frac{1}{N}\sum_{i=1}^N (x^{(i)}-\bar{x})(y^{(i)}-\bar{y})\\
\hat{\sigma}_{xy}^2
&=
\frac{1}{N}\sum_{i=1}^N (x^{(i)}-\bar{x})^2
\end{aligned}
\tag{7.21}
```

を表します。

### 対数尤度の式の整理

書籍中の対数尤度の式 (4.20)と、モデルの式 (7.11)をまとめると、1変数線形回帰モデルの対数尤度は以下のように表されます。

```math
\begin{aligned}
\log L(\boldsymbol{y} \mid \boldsymbol{X}, w_1, w_0, \sigma^2)
&=
\log \prod_{i=1}^N p(y^{(i)} \mid x^{(i)}, w_1, w_0, \sigma^2) \\
&=
\sum_{i=1}^N \log \mathcal{N}(y^{(i)} \mid w_1x^{(i)}+w_0,\sigma^2) \\
&=
\sum_{i=1}^N \log \Bigl( \frac{1}{\sqrt{2 \pi \sigma^2}} \exp{\Bigl( -\frac{(y^{(i)}-(w_1x^{(i)}+w_0))^2}{2\sigma^2} \Bigr)} \Bigr) \\
&=
-\frac{N}{2}\log(2 \pi) - \frac{N}{2}\log \sigma^2 - \frac{1}{2\sigma^2}\sum_{i=1}^N (y^{(i)}-(w_1x^{(i)}+w_0))^2 \\
&=
-\frac{N}{2}\log(2 \pi) - \frac{N}{2}\log \sigma^2 - \frac{1}{\sigma^2}E_D(\boldsymbol{X},\boldsymbol{y},w_1,w_0)
\end{aligned}
\tag{7.14}
```

ただし

```math
E_D(\boldsymbol{X},\boldsymbol{y},w_1,w_0)=\frac{1}{2}\sum_{i=1}^N \bigl(y^{(i)}-(w_1x^{(i)}+w_0)\bigr)^2
\tag{7.15}
```

この対数尤度$\log L(\boldsymbol{y} \mid \boldsymbol{X}, w_1, w_0, \sigma^2)$を$w_1,w_0$および$\sigma^2$に関してそれぞれ微分して0とおき、$w_1,w_0,\sigma^2$の極大値を計算することで、最尤推定値$\hat{w}_1,\hat{w}_0,\hat{\sigma}^2$を求めます。

### 線形予測子の係数$w_1$と切片$w_0$の最尤推定値

　式 (7.14)の対数尤度$\log L(\boldsymbol{y} \mid \boldsymbol{X}, w_1, w_0, \sigma^2)$を、$w_0$に関して微分して0とおきます。

```math
\begin{aligned}
0
&=
\frac{\partial}{\partial w_0} \log L(\boldsymbol{y} \mid \boldsymbol{X}, w_1, w_0, \sigma^2) \\
&=
\frac{\partial}{\partial w_0} \bigl(-\frac{1}{\sigma^2}E_D(\boldsymbol{X},\boldsymbol{y},w_1,w_0)\bigr) \\
&=
-\frac{1}{2\sigma^2} \sum_{i=1}^N \frac{\partial}{\partial w_0} \bigl(y^{(i)}-(w_1x^{(i)}+w_0)\bigr)^2 \\
&=
-\frac{1}{2\sigma^2} \sum_{i=1}^N -2\bigl(y^{(i)}-(w_1x^{(i)}+w_0)\bigr) \\
&=
-\frac{1}{\sigma^2} \Bigl( w_1\sum_{i=1}^N x^{(i)} - \sum_{i=1}^N y^{(i)} + Nw_0 \Bigr)
\end{aligned}
\tag{7.101}
```
　
　変形して

```math
\begin{aligned}
w_0
&=
\frac{1}{N}\sum_{i=1}^N y^{(i)} - w_1\frac{1}{N}\sum_{i=1}^N x^{(i)} \\
&=
\bar{y} - w_1\bar{x}
\end{aligned}
\tag{7.102}
```

　式 (7.102)を式 (7.15)に代入すると、

```math
\begin{aligned}
E_D(\boldsymbol{X},\boldsymbol{y},w_1,w_0)
&=
\frac{1}{2}\sum_{i=1}^N \bigl(y^{(i)}-(w_1x^{(i)}+\bar{y} - w_1\bar{x})\bigr)^2 \\
&=
\frac{1}{2}\sum_{i=1}^N \bigl(y^{(i)}-\bar{y} - w_1(x^{(i)}-\bar{x})\bigr)^2 \\
&=
\frac{1}{2}\sum_{i=1}^N \bigl(\tilde{y}^{(i)} - w_1\tilde{x}^{(i)} \bigr)^2
\end{aligned}
\tag{7.104}
```

　ただし、$\tilde{x}^{(i)}$、$\tilde{y}^{(i)}$は$x^{(i)}$、$y^{(i)}$を中心化した

```math
\tilde{x}^{(i)}=x^{(i)}-\bar{x}, \quad \tilde{y}^{(i)}=y^{(i)}-\bar{y}
\tag{7.105}
```

　となります。
　次に式 (7.14)の対数尤度$\log L(\boldsymbol{y} \mid w_1, w_0, \sigma^2)$を、$w_1$に関して微分して0とおきます。

```math
\begin{aligned}
0
&=
\frac{\partial}{\partial w_1} \log L(\boldsymbol{y} \mid w_1, w_0, \sigma^2) \\
&=
\frac{\partial}{\partial w_1} \bigl(-\frac{1}{\sigma^2}E_D(\boldsymbol{X},\boldsymbol{y},w_1,w_0)\bigr)
\end{aligned}
\tag{7.106}
```
　
　式 (7.104)を代入して

```math
\begin{aligned}
&=
-\frac{1}{2\sigma^2} \sum_{i=1}^N \frac{\partial}{\partial w_1} (\tilde{y}^{(i)} - w_1\tilde{x}^{(i)})^2 \\
&=
-\frac{1}{2\sigma^2} \sum_{i=1}^N \bigl(-2\tilde{x}^{(i)} (\tilde{y}^{(i)} - w_1\tilde{x}^{(i)})\bigr) \\
&=
\frac{1}{\sigma^2} \Bigl(\sum_{i=1}^N \tilde{x}^{(i)} \tilde{y}^{(i)} - w_1\sum_{i=1}^N {\tilde{x}^{(i)}}^2 \Bigr)
\end{aligned}
\tag{7.107}
```

　変形して

```math
\begin{aligned}
w_1
&=
\frac{\sum_{i=1}^N \tilde{x}^{(i)} \tilde{y}^{(i)}}{\sum_{i=1}^N {\tilde{x}^{(i)}}^2} \\
&=
\frac{\sum_{i=1}^N (x^{(i)}-\bar{x})(y^{(i)}-\bar{y})}{\sum_{i=1}^N (x^{(i)}-\bar{x})^2} \\
&=
\frac{\hat{\sigma}_{xy}^2}{\hat{\sigma}_x^2}
\end{aligned}
\tag{7.108}
```

　よって$w_1$の最尤推定量$\hat{w}_1$は、

```math
\hat{w}_1 = \frac{\hat{\sigma}_{xy}^2}{\hat{\sigma}_x^2}
\tag{7.109}
```
　
　と表せます。
　この$\hat{w}_1$を式 (7.102)の$w_1$と置き換えると、$w_0$の最尤推定量$\hat{w}_0$は、

```math
\hat{w}_0 = \bar{y} - \hat{w}_1\bar{x}
\tag{7.110}
```
　
　のように表せます。

#### 分散パラメータ$\sigma^2$の最尤推定値

　式 (7.14)の対数尤度$\log L(\boldsymbol{y} \mid w_1, w_0, \sigma^2)$を、$w_0$に関して微分して0とおきます。

```math
\begin{aligned}
0
&=
\frac{\partial}{\partial \sigma^2} \log L(\boldsymbol{y} \mid w_1, w_0, \sigma^2) \\
&=
\frac{\partial}{\partial \sigma^2} \bigl( -\frac{N}{2}\log \sigma^2 - \frac{1}{\sigma^2}E_D(\boldsymbol{X},\boldsymbol{y},w_1,w_0)\bigr) \\
&=
\frac{E_D(\boldsymbol{X},\boldsymbol{y},w_1,w_0)}{\sigma^4}-\frac{N}{2\sigma^2}
\end{aligned}
\tag{7.111}
```

ここで、式 (7.104)の$w_1$を最尤推定値$\hat{w}_1$に置き換えると、二乗和誤差関数$E_D(\boldsymbol{X},\boldsymbol{y},w_1,w_0)$の最尤推定値は

```math
E_D(\hat{w}_1)=\frac{1}{2}\sum_{i=1}^N \bigl(y^{(i)}-\bar{y} - \hat{w}_1(x^{(i)}-\bar{x})\bigr)^2
\tag{7.112}
```
　
　これを式 (7.111)の$E_D(\boldsymbol{X},\boldsymbol{y},w_1,w_0)$に代入すると、

```math
=\frac{1}{2\sigma^4} \Bigl(\sum_{i=1}^N \bigl(y^{(i)}-\bar{y} - \hat{w}_1(x^{(i)}-\bar{x})\bigr)^2 - \sigma^2N \Bigr)
\tag{7.113}
```

　変形して

```math
\sigma^2
=
\frac{1}{N} \sum_{i=1}^N \bigl(y^{(i)}-\bar{y} - \hat{w}_1(x^{(i)}-\bar{x})\bigr)^2
\tag{7.114}
```

　よって$\sigma^2$の最尤推定量$\hat{\sigma}^2$は、

```math
\hat{\sigma}^2 = \frac{1}{N} \sum_{i=1}^N \bigl(y^{(i)}-\bar{y} - \hat{w}_1(x^{(i)}-\bar{x})\bigr)^2
\tag{7.115}
```
　
　と表せます。
