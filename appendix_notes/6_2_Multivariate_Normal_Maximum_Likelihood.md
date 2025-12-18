# 6章付録2 多次元正規分布の最尤推定

多次元正規分布は平均ベクトル$\boldsymbol{\mu}$と分散共分散行列$\boldsymbol{\Sigma}$をパラメータとして持ちます。これらのパラメータの最尤推定値が、

<p align="center"><img src="https://latex.codecogs.com/svg.image?
\hat{\boldsymbol{\mu}}
=
\frac{1}{N} \sum_{i=1}^N \boldsymbol{x}^{(i)}
=
\left(\begin{array}{c}
\hat{\mu}_1 \\
\vdots \\
\hat{\mu}_M
\end{array}\right)
\tag{6.40}
" /></p>

<p align="center"><img src="https://latex.codecogs.com/svg.image?
\begin{aligned}
\hat{\boldsymbol{\Sigma}}
&=
\frac{1}{N} \sum_{i=1}^N (\boldsymbol{x}^{(i)}-\hat{\boldsymbol{\mu}}) (\boldsymbol{x}^{(i)}-\hat{\boldsymbol{\mu}})^T \\
&=
\left(\begin{array}{cccc}
\hat{\sigma}_1^2 & \hat{\sigma}_{12}^2 & \ldots & \hat{\sigma}_{1M}^2 \\
\hat{\sigma}_{12}^2 & \hat{\sigma}_2^2 & \ldots & \hat{\sigma}_{2M}^2 \\
\vdots & \vdots & \ddots & \vdots \\
\hat{\sigma}_{1M}^2 & \hat{\sigma}_{2M}^2 & \ldots & \hat{\sigma}_M^2
\end{array}\right)
\end{aligned}
\tag{6.41}
" /></p>

となることを示していきます。。なお使用している行列の微分公式については、[[Bishop 2012]](https://www.amazon.co.jp/dp/4621061224)の付録等を参照ください。

多次元正規分布の対数尤度は、書籍中の対数尤度の式 (4.20)と、多次元正規分布の確率密度関数の式 (6.35)から、以下のように表されます。

<p align="center"><img src="https://latex.codecogs.com/svg.image?
\begin{aligned}
\log L(\boldsymbol{X} \mid \boldsymbol{\mu}, \boldsymbol{\Sigma})
&=
\log \prod_{i=1}^N \mathcal{N}(\boldsymbol{x}^{(i)} \mid \boldsymbol{\mu}, \boldsymbol{\Sigma}) \\
&=
\sum_{i=1}^N \log \mathcal{N}(\boldsymbol{x}^{(i)} \mid \boldsymbol{\mu}, \boldsymbol{\Sigma}) \\
&=
\sum_{i=1}^N \log \frac{1}{(2\pi)^\frac{M}{2}}\frac{1}{|\boldsymbol{\Sigma}|^\frac{1}{2}} \exp \Bigl(-\frac{1}{2}(\boldsymbol{x}^{(i)}-\boldsymbol{\mu})^T \boldsymbol{\Sigma}^{-1} (\boldsymbol{x}^{(i)}-\boldsymbol{\mu}) \Bigr) \\
&=
-\frac{NM}{2}\log(2\pi)-\frac{N}{2}\log|\boldsymbol{\Sigma}| -
\frac{1}{2}\sum_{i=1}^N (\boldsymbol{x}^{(i)}-\boldsymbol{\mu})^T \boldsymbol{\Sigma}^{-1} (\boldsymbol{x}^{(i)}-\boldsymbol{\mu})
\end{aligned}
\tag{6.201}
" /></p>

1次元正規分布の場合と同様に、この対数尤度$\log L(\boldsymbol{X} \mid \boldsymbol{\mu}, \boldsymbol{\Sigma})$を$\boldsymbol{\mu}$および$\boldsymbol{\Sigma}$に関してそれぞれ微分して0とおき、$\boldsymbol{\mu}$と$\boldsymbol{\Sigma}$の極大値を計算することで、最尤推定値$\hat{\boldsymbol{\mu}}$、$\hat{\boldsymbol{\Sigma}}$を求めます。

### 平均ベクトル$\boldsymbol{\mu}$の最尤推定値

　対数尤度$\log L(\boldsymbol{X} \mid \boldsymbol{\mu}, \boldsymbol{\Sigma})$を$\boldsymbol{\mu}$に関して微分して0とおきます。

<p align="center"><img src="https://latex.codecogs.com/svg.image?
\begin{aligned}
0&=
\frac{\partial}{\partial \boldsymbol{\mu}} \log L(\boldsymbol{X} \mid \boldsymbol{\mu}, \boldsymbol{\Sigma}) \\
&=
\frac{\partial}{\partial \boldsymbol{\mu}} \sum_{i=1}^N \log \mathcal{N}(\boldsymbol{x}^{(i)} \mid \boldsymbol{\mu}, \boldsymbol{\Sigma}) \\
&=
\sum_{i=1}^N \frac{\partial}{\partial \boldsymbol{\mu}} \log \mathcal{N}(\boldsymbol{x}^{(i)} \mid \boldsymbol{\mu}, \boldsymbol{\Sigma})
\end{aligned}
\tag{6.202}
" /></p>

　ここで、総和の中の正規分布の対数に対する微分$\frac{\partial}{\partial \boldsymbol{\mu}} \log \mathcal{N}(\boldsymbol{x} \mid \boldsymbol{\mu}, \boldsymbol{\Sigma})$について考えると、

<p align="center"><img src="https://latex.codecogs.com/svg.image?
\begin{aligned}
\frac{\partial}{\partial \boldsymbol{\mu}} \log \mathcal{N}(\boldsymbol{x} \mid \boldsymbol{\mu}, \boldsymbol{\Sigma})
&=
\frac{\partial}{\partial \boldsymbol{\mu}} \log \frac{1}{(2\pi)^\frac{M}{2}}\frac{1}{|\boldsymbol{\Sigma}|^\frac{1}{2}} \exp \Bigl(-\frac{1}{2}(\boldsymbol{x}-\boldsymbol{\mu})^T \boldsymbol{\Sigma}^{-1} (\boldsymbol{x}-\boldsymbol{\mu}) \Bigr) \\
&=
\frac{\partial}{\partial \boldsymbol{\mu}} \Bigl(-\frac{M}{2}\log(2\pi)-\frac{1}{2}\log|\boldsymbol{\Sigma}| -
\frac{1}{2} (\boldsymbol{x}-\boldsymbol{\mu})^T \boldsymbol{\Sigma}^{-1} (\boldsymbol{x}-\boldsymbol{\mu})\Bigr) \\
&=
-\frac{1}{2}\frac{\partial}{\partial \boldsymbol{\mu}} (\boldsymbol{x}-\boldsymbol{\mu})^T \boldsymbol{\Sigma}^{-1} (\boldsymbol{x}-\boldsymbol{\mu})
\end{aligned}
\tag{6.203}
" /></p>

　$\boldsymbol{\mu}'=\boldsymbol{x}-\boldsymbol{\mu}$とおき、合成関数の微分公式を適用すると、

<p align="center"><img src="https://latex.codecogs.com/svg.image?
=
-\frac{1}{2}\frac{\partial \boldsymbol{\mu}'}{\partial \boldsymbol{\mu}} \frac{\partial}{\partial \boldsymbol{\mu}'} {\boldsymbol{\mu}'}^T \boldsymbol{\Sigma}^{-1} {\boldsymbol{\mu}'}
\tag{6.204}
" /></p>

　対称行列$\boldsymbol{A}$に対する二次形式の微分の公式$\frac{\partial}{\partial \boldsymbol{x}} \boldsymbol{x}^T\boldsymbol{A}\boldsymbol{x}=2\boldsymbol{A}\boldsymbol{x}$と、$\frac{\partial \boldsymbol{\mu}'}{\partial \boldsymbol{\mu}}=-1$を適用して、

<p align="center"><img src="https://latex.codecogs.com/svg.image?
\begin{aligned}
&=
-\frac{1}{2}(-1) \cdot 2 \boldsymbol{\Sigma}^{-1} {\boldsymbol{\mu}'} \\
&=
\boldsymbol{\Sigma}^{-1} (\boldsymbol{x}-\boldsymbol{\mu})
\end{aligned}
\tag{6.205}
" /></p>

これを式 (6.202)の$\frac{\partial}{\partial \boldsymbol{\mu}} \mathcal{N}(\boldsymbol{x}^{(i)} \mid \boldsymbol{\mu}, \boldsymbol{\Sigma})$に代入すると

<p align="center"><img src="https://latex.codecogs.com/svg.image?
\begin{aligned}
\sum_{i=1}^N \boldsymbol{\Sigma}^{-1} (\boldsymbol{x}^{(i)}-\boldsymbol{\mu})
&=
0 \\
\sum_{i=1}^N (\boldsymbol{x}^{(i)}-\boldsymbol{\mu})
&=
0 \\
\sum_{i=1}^N \boldsymbol{x}^{(i)}
&=
N \boldsymbol{\mu} \\
\boldsymbol{\mu}
&=
\frac{1}{N} \sum_{i=1}^N \boldsymbol{x}^{(i)}
\end{aligned}
\tag{6.206}
" /></p>

よって$\boldsymbol{\mu}$の最尤推定量$\hat{\boldsymbol{\mu}}$は、

<p align="center"><img src="https://latex.codecogs.com/svg.image?
\hat{\boldsymbol{\mu}}=\frac{1}{N} \sum_{i=1}^N \boldsymbol{x}^{(i)}
\tag{6.207}
" /></p>

と表されます。

### 分散共分散行列$\boldsymbol{\Sigma}$の最尤推定値

　対数尤度$\log L(\boldsymbol{X} \mid \boldsymbol{\mu}, \boldsymbol{\Sigma})$を$\boldsymbol{\Sigma}$に関して微分して0とおきます。

<p align="center"><img src="https://latex.codecogs.com/svg.image?
\begin{aligned}
0&=
\frac{\partial}{\partial \boldsymbol{\Sigma}} \log L(\boldsymbol{X} \mid \boldsymbol{\mu}, \boldsymbol{\Sigma}) \\
&=
\frac{\partial}{\partial \boldsymbol{\Sigma}} \sum_{i=1}^N \log \mathcal{N}(\boldsymbol{x}^{(i)} \mid \boldsymbol{\mu}, \boldsymbol{\Sigma}) \\
&=
\sum_{i=1}^N \frac{\partial}{\partial \boldsymbol{\Sigma}} \log \mathcal{N}(\boldsymbol{x}^{(i)} \mid \boldsymbol{\mu}, \boldsymbol{\Sigma})
\end{aligned}
\tag{6.208}
" /></p>

　ここで、総和の中の正規分布の対数に対する微分$\frac{\partial}{\partial \boldsymbol{\Sigma}} \log \mathcal{N}(\boldsymbol{x} \mid \boldsymbol{\mu}, \boldsymbol{\Sigma})$について考えると、

<p align="center"><img src="https://latex.codecogs.com/svg.image?
\begin{aligned}
\frac{\partial}{\partial \boldsymbol{\Sigma}} \log \mathcal{N}(\boldsymbol{x} \mid \boldsymbol{\mu}, \boldsymbol{\Sigma})
&=
\frac{\partial}{\partial \boldsymbol{\Sigma}} \log \frac{1}{(2\pi)^\frac{M}{2}}\frac{1}{|\boldsymbol{\Sigma}|^\frac{1}{2}} \exp \Bigl(-\frac{1}{2}(\boldsymbol{x}-\boldsymbol{\mu})^T \boldsymbol{\Sigma}^{-1} (\boldsymbol{x}-\boldsymbol{\mu}) \Bigr) \\
&=
\frac{\partial}{\partial \boldsymbol{\Sigma}} \Bigl(-\frac{M}{2}\log(2\pi)-\frac{1}{2}\log|\boldsymbol{\Sigma}| \\
& \quad -
\frac{1}{2} (\boldsymbol{x}-\boldsymbol{\mu})^T \boldsymbol{\Sigma}^{-1} (\boldsymbol{x}-\boldsymbol{\mu})\Bigr) \\
&=
-\frac{1}{2} \frac{\partial}{\partial \boldsymbol{\Sigma}}\log|\boldsymbol{\Sigma}| -\frac{1}{2} \frac{\partial}{\partial \boldsymbol{\Sigma}} (\boldsymbol{x}-\boldsymbol{\mu})^T \boldsymbol{\Sigma}^{-1} (\boldsymbol{x}-\boldsymbol{\mu})
\end{aligned}
\tag{6.209}
" /></p>

　式(6.209)の第1項に関して、行列式の微分の公式$\frac{\partial}{\partial \boldsymbol{A}}\log|\boldsymbol{A}|=(\boldsymbol{A}^{-1})^T$を適用すると、

<p align="center"><img src="https://latex.codecogs.com/svg.image?
-\frac{1}{2} \frac{\partial}{\partial \boldsymbol{\Sigma}}\log|\boldsymbol{\Sigma}|
=
-\frac{1}{2} (\boldsymbol{\Sigma}^{-1})^T
\tag{6.210}
" /></p>

　$\boldsymbol{\Sigma}$は対称行列であることから逆行列$\boldsymbol{\Sigma}^{-1}$も対称行列となり、対称行列の転置は元の行列と等しいことから、

<p align="center"><img src="https://latex.codecogs.com/svg.image?
=
-\frac{1}{2} \boldsymbol{\Sigma}^{-1}
\tag{6.211}
" /></p>

　式(6.209)の第2項に関して、二次形式と行列のトレースの関係$\boldsymbol{x}^T \boldsymbol{A} \boldsymbol{x}=\operatorname{Tr}(\boldsymbol{A}\boldsymbol{x}\boldsymbol{x}^T)$より、

<p align="center"><img src="https://latex.codecogs.com/svg.image?
-\frac{1}{2} \frac{\partial}{\partial \boldsymbol{\Sigma}} (\boldsymbol{x}-\boldsymbol{\mu})^T \boldsymbol{\Sigma}^{-1} (\boldsymbol{x}-\boldsymbol{\mu})
=
-\frac{1}{2} \frac{\partial}{\partial \boldsymbol{\Sigma}} \operatorname{Tr}\Bigl(\boldsymbol{\Sigma}^{-1} (\boldsymbol{x}-\boldsymbol{\mu}) (\boldsymbol{x}-\boldsymbol{\mu})^T\Bigr)
\tag{6.212}
" /></p>

　$\boldsymbol{S}=(\boldsymbol{x}-\boldsymbol{\mu}) (\boldsymbol{x}-\boldsymbol{\mu})^T$とおくと、

<p align="center"><img src="https://latex.codecogs.com/svg.image?
=
-\frac{1}{2} \frac{\partial}{\partial \boldsymbol{\Sigma}} \operatorname{Tr}\Bigl(\boldsymbol{\Sigma}^{-1} \boldsymbol{S}\Bigr)
\tag{6.213}
" /></p>

　詳細は[Bishop 2012]の演習公式回答[^prml_solution]を参照頂きたいですが、これは以下のように変形できます。

<p align="center"><img src="https://latex.codecogs.com/svg.image?
\begin{aligned}
&=
\frac{1}{2} \boldsymbol{\Sigma}^{-1} \boldsymbol{S} \boldsymbol{\Sigma}^{-1} \\
&=
\frac{1}{2} \boldsymbol{\Sigma}^{-1} (\boldsymbol{x}-\boldsymbol{\mu}) (\boldsymbol{x}-\boldsymbol{\mu})^T \boldsymbol{\Sigma}^{-1}
\end{aligned}
\tag{6.214}
" /></p>

式 (6.211)と式(6.214)を式(6.209)に代入すると、

<p align="center"><img src="https://latex.codecogs.com/svg.image?
\frac{\partial}{\partial \boldsymbol{\Sigma}} \log \mathcal{N}(\boldsymbol{x} \mid \boldsymbol{\mu}, \boldsymbol{\Sigma})
=
-\frac{1}{2} \boldsymbol{\Sigma}^{-1}
+\frac{1}{2} \boldsymbol{\Sigma}^{-1} (\boldsymbol{x}-\boldsymbol{\mu}) (\boldsymbol{x}-\boldsymbol{\mu})^T \boldsymbol{\Sigma}^{-1}
\tag{6.215}
" /></p>

これを式 (2.208)の$\frac{\partial}{\partial \boldsymbol{\Sigma}} \mathcal{N}(\boldsymbol{x}^{(i)} \mid \boldsymbol{\mu}, \boldsymbol{\Sigma})$に代入すると

<p align="center"><img src="https://latex.codecogs.com/svg.image?
\begin{aligned}
0
&=
\sum_{i=1}^N \Bigl( -\frac{1}{2} \boldsymbol{\Sigma}^{-1}
+\frac{1}{2} \boldsymbol{\Sigma}^{-1} (\boldsymbol{x}^{(i)}-\boldsymbol{\mu}) (\boldsymbol{x}^{(i)}-\boldsymbol{\mu})^T \boldsymbol{\Sigma}^{-1} \Bigr) \\
\frac{1}{2} \sum_{i=1}^N \boldsymbol{\Sigma}^{-1}
&=
\frac{1}{2} \boldsymbol{\Sigma}^{-1} \Bigl(\sum_{i=1}^N (\boldsymbol{x}^{(i)}-\boldsymbol{\mu}) (\boldsymbol{x}^{(i)}-\boldsymbol{\mu})^T\Bigr) \boldsymbol{\Sigma}^{-1} \\
N \boldsymbol{\Sigma}^{-1}
&=
\boldsymbol{\Sigma}^{-1} \Bigl(\sum_{i=1}^N (\boldsymbol{x}^{(i)}-\boldsymbol{\mu}) (\boldsymbol{x}^{(i)}-\boldsymbol{\mu})^T\Bigr) \boldsymbol{\Sigma}^{-1} \\
\boldsymbol{\Sigma}^{-1}
&=
\frac{1}{N} \boldsymbol{\Sigma}^{-1} \Bigl(\sum_{i=1}^N (\boldsymbol{x}^{(i)}-\boldsymbol{\mu}) (\boldsymbol{x}^{(i)}-\boldsymbol{\mu})^T\Bigr) \boldsymbol{\Sigma}^{-1}
\end{aligned}
\tag{6.216}
" /></p>

　両辺に両側から$\boldsymbol{\Sigma}$を掛けると

<p align="center"><img src="https://latex.codecogs.com/svg.image?
\begin{aligned}
\boldsymbol{\Sigma}\boldsymbol{\Sigma}^{-1}\boldsymbol{\Sigma}
&=
\frac{1}{N} \boldsymbol{\Sigma}\boldsymbol{\Sigma}^{-1} \Bigl(\sum_{i=1}^N (\boldsymbol{x}^{(i)}-\boldsymbol{\mu}) (\boldsymbol{x}^{(i)}-\boldsymbol{\mu})^T\Bigr) \boldsymbol{\Sigma}^{-1}\boldsymbol{\Sigma} \\
\boldsymbol{\Sigma}
&=\frac{1}{N} \sum_{i=1}^N (\boldsymbol{x}^{(i)}-\boldsymbol{\mu}) (\boldsymbol{x}^{(i)}-\boldsymbol{\mu})^T
\end{aligned}
\tag{6.217}
" /></p>

先ほど求めた$\hat{\boldsymbol{\mu}}$を$\boldsymbol{\mu}$に代入すると、

<p align="center"><img src="https://latex.codecogs.com/svg.image?
\frac{1}{N} \sum_{i=1}^N (\boldsymbol{x}^{(i)}-\hat{\boldsymbol{\mu}}) (\boldsymbol{x}^{(i)}-\hat{\boldsymbol{\mu}})^T
\tag{6.218}
" /></p>

よって$\boldsymbol{\Sigma}$の最尤推定量$\hat{\boldsymbol{\Sigma}}$は、

<p align="center"><img src="https://latex.codecogs.com/svg.image?
\hat{\boldsymbol{\Sigma}}
=
\frac{1}{N} \sum_{i=1}^N (\boldsymbol{x}^{(i)}-\hat{\boldsymbol{\mu}}) (\boldsymbol{x}^{(i)}-\hat{\boldsymbol{\mu}})^T
\tag{6.219}
" /></p>

と表されます。

[^prml_solution]:https://www.microsoft.com/en-us/research/wp-content/uploads/2016/05/prml-web-sol-2009-09-08.pdf
