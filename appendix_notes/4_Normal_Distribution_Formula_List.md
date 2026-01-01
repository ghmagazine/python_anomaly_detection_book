# 4章付録：ホテリング理論の異常度が従う確率分布の求め方

書籍4.4節(176ページ)および4.5節(188ページ)において、サンプルサイズ $N$ が小さい場合（最尤推定の誤差を考慮する場合）、以下の関係が成り立つことを紹介しました。

1. 異常度 $a(x)=(\frac{x-\hat{\mu}}{\hat{\sigma}})^2$ を $\frac{N-1}{N+1}$ 倍した統計量 $\frac{N-1}{N+1}a(x)$ は、自由度 $(1,N-1)$ のF分布に従う**→異常度が従う分布の導出に使用**

2. 正規分布に従う変数 $x$ を標準化して $\sqrt{\frac{N-1}{N+1}}$ 倍した統計量 $t(x)=\sqrt{\frac{N-1}{N+1}}\frac{x-\hat{\mu}}{\hat{\sigma}}$ は、**→元の変数** $x$ **にしきい値を設ける場合のしきい値計算に使用**

これらの関係が成り立つことを示していきます。

### 正規分布の標本統計量に関する公式

上記の関係を求めるには、正規分布の標本統計量に関する公式をいくつか組み合わせる必要があります。よってまずは、これらの公式について紹介します。

各公式導出の詳細は本書では割愛しますが、関心のある読者は[井手 2015]などを参照し、正規分布の確率密度関数の式

```math
\begin{aligned}
p(x)=\frac{1}{\sqrt{2 \pi \sigma^2}} \exp{\Bigl( -\frac{(x-\mu)^2}{2\sigma^2} \Bigr)}
\end{aligned}
```

から計算してみると、理解が深まるでしょう。

#### 正規分布の和の公式

　独立な確率変数 $X$ と $Y$ がそれぞれ、正規分布 $\mathcal{N}(x \mid \mu_1,\sigma_1^2)$ と $\mathcal{N}(y|\mu_2,\sigma_2^2)$ に従う場合、その線形和 $aX+bY$ は以下に示す正規分布に従います。

```math
\begin{aligned}
aX+bY \sim \mathcal{N}(a\mu_1+b\mu_2,a^2\sigma_1^2+b^2\sigma_2^2)
\end{aligned}
\tag{4.101}
```

本公式を応用すると、正規分布 $\mathcal{N}(x \mid \mu,\sigma^2)$ から独立に $N$ 個サンプリングした標本の平均（すなわち標本平均 $\hat{\mu}$ ）は、以下に示す正規分布に従います

```math
\begin{aligned}
\hat{\mu} \sim \mathcal{N}(\mu,\frac{\sigma^2}{N})
\end{aligned}
\tag{4.102}
```

また、正規分布 $\mathcal{N}(x \mid \mu,\sigma^2)$ に従う確率変数 $X$ と定数 $b$ との線形和 $aX+b$ は、以下の正規分布に従います

```math
\begin{aligned}
aX+b \sim \mathcal{N}(a\mu+b,a^2\sigma^2)
\end{aligned}
\tag{4.103}
```

#### 正規分布の二乗和の公式

独立な確率変数 $X_1,X_2,\cdots,X_k$ がそれぞれ標準正規分布 $\mathcal{N}(0,1)$ に従う場合、その二乗和 $X_1^2+X_2^2+\cdots+X_k^2$ は、以下に示す自由度 $k$ のカイ二乗分布に従います。

```math
\begin{aligned}
X_1^2+X_2^2+\cdots+X_k^2 \sim \chi^2(k)
\end{aligned}
\tag{4.104}
```

　本公式を応用すると、正規分布 $\mathcal{N}(x \mid \mu,\sigma^2)$ から独立に $N$ 個サンプリングした標本の分散（すなわち標本分散 $\hat{\sigma}^2$ ）と母分散 ${\sigma}^2$ との比に、サンプルサイズ $N$ を掛けた指標 $N\hat{\sigma}^2/\sigma^2$ は、以下に示す自由度 $N-1$ のカイ二乗分布に従います。

```math
\begin{aligned}
N\frac{\hat{\sigma}^2}{\sigma^2} \sim \chi^2(N-1)
\end{aligned}
\tag{4.105}
```

#### カイ二乗分布の比の公式

　独立な確率変数 $X$ と $Y$ がそれぞれ、カイ二乗分布 $\chi^2(k_1)$ と $\chi^2(k_2)$ に従う場合、その比をそれぞれの自由度で調整したフィッシャーの分散比 $\frac{X/k_1}{Y/k_2}$ は、以下に示す自由度 $(k_1,k_2)$ のF分布に従います。

```math
\begin{aligned}
\frac{X/k_1}{Y/k_2} \sim \mathcal{F}(k_1,k_2)
\end{aligned}
\tag{4.106}
```

#### 正規分布とカイ二乗分布の比の公式

　独立な確率変数 $X$ と $Y$ がそれぞれ、標準正規分布 $\mathcal{N}(0,1)$ とカイ二乗分布 $\chi^2(k)$ に従う場合、前者を後者の平方根で割ってカイ二乗分布の自由度で調整した $t$統計量 $t=\frac{X}{\sqrt{Y/k}}$ は、以下に示す自由度 $k$ のスチューデントのt分布に従います。

```math
\begin{aligned}
\frac{X}{\sqrt{Y/k}} \sim \mathcal{S}(k)
\end{aligned}
\tag{4.107}
```

### 1. 異常度が従う分布の導出

ここからは、ここまで紹介した公式を用いて異常度 $a(x)=(\frac{x-\hat{\mu}}{\hat{\sigma}})^2$ が従う確率分布を導出します。

　異常度の式を見ると、標本平均 $\hat{\mu}$ 標本分散 $\hat{\sigma}^2$ を含むため、式（4.102）と式（4.105）を組み合わせて、異常度の確率分布をモデリングできそうに見えます。しかし、標本平均、標本分散ともに、求めた確率分布には未知量である母分散 $\sigma^2$ が含まれているため、以下のステップに分けて式変形を行い、未知量を削除した異常度の確率分布を求めていきます。

1. 分子 $(x-\hat{\mu})^2$ の確率分布
2. 分母 $\hat{\sigma}^2$ の確率分布
3. 分母と分母の比（ $=$異常度）の確率分布

##### 1. 分子の確率分布

　分子 $(x-\hat{\mu})^2$ の確率分布を求めるためには、まず平方根である $x-\hat{\mu}$ の確率分布に着目します。

　$x$ は正規分布 $\mathcal{N}(\mu,\sigma^2)$ に従い、標本平均 $\hat{\mu}$ は式 (4.102)より正規分布 $\mathcal{N}(\mu,\frac{\sigma^2}{N})$ に従います。

　$x-\hat{\mu}$ は両者の引き算となるので、式 (4.101)を適用すると、平均 $\mu-\mu=0$ 、分散 $\sigma^2+\frac{\sigma^2}{N}=\frac{N+1}{N}\sigma^2$ の正規分布に従い、以下のように表せます

```math
\begin{aligned}
x-\hat{\mu} \sim \mathcal{N}(0,\frac{N+1}{N}\sigma^2)
\end{aligned}
\tag{4.108}
```

　この分布を標準化すると、以下のように標準正規分布に従います。
　
```math
\begin{aligned}
\sqrt{\frac{N}{(N+1)\sigma^2}}(x-\hat{\mu}) \sim \mathcal{N}(0,1)
\end{aligned}
\tag{4.109}
```

　これを二乗して式 (4.103)を適用すると、以下のように自由度1のカイ二乗分布に従います。

```math
\begin{aligned}
\frac{N}{(N+1)\sigma^2}(x-\hat{\mu})^2 \sim \chi^2(1)
\end{aligned}
\tag{4.110}
```

　よって、分子を $\frac{N}{(N+1)\sigma^2}$ 倍した統計量は、自由度 $1$ のカイ二乗分布に従うことが分かります。ここではまだ未知量 $\sigma^2$ が残っていますが、これは後で消去できるので先に進みます。

##### 2. 分母の確率分布

　式 (4.105)より、分母 $\hat{\sigma}^2$ を $\frac{N}{\sigma^2}$ 倍した統計量 $\frac{N\hat{\sigma}^2}{\sigma^2}$ は、自由度 $N-1$ のカイ二乗分布に従います。ここではまだ未知量 $\sigma^2$ が残っていますが、これは後で消去できるので先に進みます。

##### 3. 異常度の確率分布

　式 (4.110)の左辺を分子、式 (4.105)の左辺を分母にとり、 $N-1$ を掛けた統計量を定義し、以下のように式変形します。

```math
\begin{aligned}
(N-1) \frac{\frac{N}{(N+1)\sigma^2}(x-\hat{\mu})^2}{\frac{N\hat{\sigma}^2}{\sigma^2}}
&=\frac{N-1}{N+1} \Bigl(\frac{x-\hat{\mu}}{\hat{\sigma}}\Bigr)^2 \\
&=\frac{N-1}{N+1} a(x)
\end{aligned}
\tag{4.111}
```

　このとき、ステップ1の結果から、分子は自由度 $1$ のカイ二乗分布 $\chi^2(1)$ に従い、ステップ2の結果から、分母は自由度 $N-1$ のカイ二乗分布 $\chi^2(N-1)$ に従います。よって式 (4.106)を適用すると、式 (4.111)で示す統計量は自由度 $(1,N-1)$ のF分布に従います。これを式で表すと

```math
\begin{aligned}
\frac{N-1}{N+1} a(x) \sim \mathcal{F}(1,N-1)
\end{aligned}
\tag{4.112}
```

となり、異常度の確率分布を未知量を含まないF分布で表せることが分かりました。

### 2. 元の変数 $x$ を標準化して $\sqrt{\frac{N-1}{N+1}}$ 倍した統計量 $t(x)$ が従う分布の導出

正規分布に従う変数 $x$ を標準化して $\sqrt{\frac{N-1}{N+1}}$ 倍した統計量

```math
\begin{aligned}
t(x) = \sqrt{\frac{N-1}{N+1}}\frac{x-\hat{\mu}}{\hat{\sigma}}
\end{aligned}
\tag{4.113}
```

を考えます。この式を変形すると

```math
\begin{aligned}
t(x) = \frac{(x-\hat{\mu})\sqrt{\frac{N}{(N+1)\sigma^2}}}{\sqrt{\frac{N\hat{\sigma}^2}{\sigma^2}\frac{1}{N-1}}}
\end{aligned}
\tag{4.114}
```

となります。

この式において、分子は式 (4.109)より標準正規分布 $\mathcal{N}(x \mid 0,1)$ に従い、分母の $\frac{N\hat{\sigma}^2}{\sigma^2}$ の部分は式 (4.105)より自由度 $N-1$ のカイ二乗分布 $\chi^2(N-1)$ に従います。これに式 (4.107)の関係を適用すると、式 (4.114)の $t(x)$ は自由度 $N-1$ のスチューデントのt分布に従います。これを式で表すと

```math
\begin{aligned}
t(x) \sim \mathcal{S}(N-1)
\end{aligned}
\tag{4.115}
```

　となり、統計量 $t(x)$ の確率分布を未知量を含まないスチューデントのt分布で表せることが分かりました。
