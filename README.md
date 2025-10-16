# まるごと学べる 異常検知の実践知

書籍『[まるごと学べる 異常検知の実践知](https://gihyo.jp/book/2025/978-4-297-15226-0)』(技術評論社発行)のサポートページです。書籍中のソースコードや、書面に掲載されていない補足解説をまとめています。

## サポートページの構成

本サポートページは、以下のコンテンツを含んでいます。

|項目|概要|
|---|---|
|[**異常検知アルゴリズム チートシート**]()|書籍に記載した手法から適切なものを選ぶためのフローチャート|
|[**ソースコード**]()|書籍中のソースコード（Jupyter）|
|[**付録解説**]()|書面に掲載されていない、各種理論やアルゴリズムに関する補足解説|
|[**正誤表**]()|書籍の正誤表|

## 異常検知アルゴリズム チートシート

異常検知アルゴリズムを選択するためのフローチャートです（画像、時系列データが対象の手法は含まず）。

```mermaid
%%{init: {"themeVariables": { "fontSize": "20px", "fontFamily": "Meiryo UI" }}}%%

flowchart LR;
    %% ---------- common node styles ----------
    classDef title fill:#ffffff,stroke:#333,stroke-width:0px,color:#111,font-weight:bold,font-size:24px;
    classDef block fill:#fff,stroke:#2f7e,stroke-width:2px,rx:8px,ry:8px;
    classDef action fill:#ffffff,stroke:#2f7e,stroke-width:2px,rx:10,ry:10;
    classDef decision fill:#fff6d6,stroke:#f0ad00,stroke-width:2px,rx:4,ry:4;
    classDef tryNext fill:#fff,stroke:#f39c12,stroke-dasharray:3 3,rx:8,ry:8,color:#f39c12;
    classDef light fill:#fff;

    %% ---------- 教師あり学習 ----------
    subgraph CLASSIF["<b style='font-size:28px;'>教師あり学習</b>"]
        direction LR
        class CLASSIF title
        sklearn[Scikitlearnの<br/>チートシート参照]
        class sklearn block
    end
    style CLASSIF fill:#fff6b8,stroke:#fff6b8,stroke-width:6px,rx:24,ry:24

    %% ---------- 計数データ向け ----------
    subgraph COUNT["<b style='font-size:28px;'>計数データ向け手法</b>"]
        direction LR
        class COUNT title
        d_binom
        d_binom_overdisp
        d_pois_overdisp
        c_binom[二項分布の最尤推定]
        c_beta_binom[二項ベータ分布モデル]
        c_pois[ポアソン分布の最尤推定]
        c_neg_binom[負の二項分布モデル]
        class c_binom,c_beta_binom,c_pois,c_pois_regr,c_pois_regr_random,c_neg_binom block
    end
    style COUNT fill:#ffd9df,stroke:#ffd9df,stroke-width:6px,rx:24,ry:24

    %% ---------- 統計モデリング ----------
    subgraph STATMODEL["<b style='font-size:28px;'>統計モデリング</b>"]
        direction LR
        class STATMODEL title
        d_regr_binom
        d_regr_binom_overdisp
        d_regr_pois_overdisp
        d_regr_linear
        d_regr_norm
        d_regr_simple
        d_regr_ridge
        s_binom_logistic[二項ロジスティック回帰]
        s_binom_logistic_random[個体差によるランダム効果を含む二項ロジスティック回帰]
        s_pois_regr[ポアソン回帰]
        s_pois_regr_random[個体差によるランダム効果を含むポアソン回帰]
        s_simple_regr[1変数線形回帰モデル]
        s_multi_regr[多変数線形回帰モデル]
        s_ridge_regr[リッジ回帰モデル]
        s_other_glm[その他のGLM]
        s_gauss_proc[ガウス過程回帰]
        class s_binom_logistic,s_binom_logistic_random,s_pois_regr,s_pois_regr_random,s_simple_regr,s_multi_regr,s_ridge_regr,s_other_glm,s_gauss_proc block
    end
    style STATMODEL fill:#e9d7ff,stroke:#e9d7ff,stroke-width:6px,rx:24,ry:24

    subgraph NONNORM["<b style='font-size:28px;'>非正規分布</br>ベースの手法</b>"]
        direction LR
        class NONNORM title
        d_non_ocsvm
        non_knn[k-NN]
        non_ocsvm[OC-SVM]
        non_gmm[GMM]
        non_other[1次元非正規分布]
        class non_knn,non_ocsvm,non_gmm,non_other block
    end
    style NONNORM fill:#d8e8ff,stroke:#d8e8ff,stroke-width:6px,rx:24,ry:24

    subgraph NORM["<b style='font-size:28px;'>正規分布</br>ベースの手法</b>"]
        direction LR
        class NORM title
        d_norm_mt
        norm_mt[マハラノビス・タグチ法]
        norm_hotelling[ホテリング理論]
        class norm_mt,norm_hotelling block
    end
    style NORM fill:#bce4ba,stroke:#bce4ba,stroke-width:6px,rx:24,ry:24

    START((START))
    d_supervised{異常データ>50 and<br/>未知異常の判別不要？}
    d_count{検知対象が回数で<br/>表される計数データ？}
    d_count_regr{検知対象の変数に<br/>影響を与える<br/>他の変数が存在？}
    d_regr{検知対象の変数に<br/>影響を与える<br/>他の変数が存在？}
    d_nonparam{データの分布形状が複雑 and 30次元以下？}
    d_multimodal{データに多峰性<br/>がみられる？}
    d_simple{一変数？}
    d_norm{検知対象のデータが<br/>正規分布に従う？}

    d_binom{検知対象が試行数n<br/>あたりの発生数x？}
    d_binom_overdisp{過分散を考慮する？}
    d_pois_overdisp{過分散を考慮する？}

    d_regr_binom{検知対象が試行数n<br/>あたりの発生数x？}
    d_regr_binom_overdisp{過分散を考慮する？}
    d_regr_pois_overdisp{過分散を考慮する？}
    d_regr_linear{説明変数と応答変数<br/>の関係が線形？}
    d_regr_norm{残差が正規分布<br/>に従う？}
    d_regr_simple{1変数？}
    d_regr_ridge{データ数≫変数の数<br/>and 多重共線性低}

    d_non_ocsvm{データ数≫変数の数}

    d_norm_mt{変数ごとの寄与度<br/>を求めたい？}

    class START action
    class d_supervised,d_count,d_count_regr,d_norm,d_regr,d_nonparam,d_multimodal,d_simple,d_binom,d_binom_overdisp,d_pois_overdisp,d_regr_binom,d_regr_binom_overdisp,d_regr_pois_overdisp,d_regr_linear,d_regr_norm,d_regr_simple,d_regr_ridge,d_non_ocsvm,d_norm_mt decision

    %% ---------- CLASSIF branch ----------
    START --> d_supervised
    d_supervised -- YES --> CLASSIF
    d_supervised -- NO --> d_count

    CLASSIF --> sklearn

    %% ---------- COUNT branch ----------
    d_count -- NO --> d_regr
    d_count -- YES --> d_count_regr
    d_count_regr -- YES --> d_regr_binom
    d_count_regr -- NO --> d_binom

    d_binom -- NO --> d_pois_overdisp
    d_binom -- YES --> d_binom_overdisp
    d_binom_overdisp -- NO --> c_binom
    d_binom_overdisp -- YES --> c_beta_binom
    d_pois_overdisp -- NO --> c_pois
    d_pois_overdisp -- YES --> c_neg_binom

    %% ---------- STATMODEL branch ----------
    d_regr -- NO --> d_nonparam
    d_regr -- YES --> d_regr_linear

    d_regr_binom -- NO --> d_regr_pois_overdisp
    d_regr_binom -- YES --> d_regr_binom_overdisp
    d_regr_binom_overdisp -- NO --> s_binom_logistic
    d_regr_binom_overdisp -- YES --> s_binom_logistic_random
    d_regr_pois_overdisp -- NO --> s_pois_regr
    d_regr_pois_overdisp -- YES --> s_pois_regr_random

    d_regr_linear -- NO --> s_gauss_proc
    d_regr_linear -- YES --> d_regr_norm
    d_regr_norm -- NO --> s_other_glm
    d_regr_norm -- YES --> d_regr_simple
    d_regr_simple -- NO --> d_regr_ridge
    d_regr_simple -- YES --> s_simple_regr
    d_regr_ridge -- NO --> s_ridge_regr
    d_regr_ridge -- YES --> s_multi_regr

    %% ---------- NONNORM branch ----------
    d_nonparam -- NO --> d_multimodal
    d_nonparam -- YES --> d_non_ocsvm
    d_multimodal -- NO --> d_simple
    d_multimodal -- YES --> non_gmm
    d_simple -- NO --> d_norm_mt
    d_simple -- YES --> d_norm
    d_norm -- NO --> non_other
    d_norm -- YES --> norm_hotelling

    d_non_ocsvm -- NO --> non_ocsvm
    d_non_ocsvm -- YES --> non_knn

    %% ---------- NORM branch ----------
    d_norm_mt -- YES --> norm_mt
    d_norm_mt -- NO --> norm_hotelling
```

※ 本チートシートをブラッシュアップしていきたいので、改善提案があればIssuesに書き込んで頂けるとありがたいです

## ソースコード

[環境構築方法]()

本文中で解説したソースコード

|章|手法名|書籍中のページ|
|---|---|---|
|2|[**データの可視化とEDA**]()||
|2|[**教師なし学習向けトイデータ生成**]()||
|3|[**SVM**]()||
|3|[**ロジスティック回帰**]()||
|4|[**1変数のホテリング理論**]()||
|4|[**1次元非正規分布**]()||
|5|[**二項分布の最尤推定**]()||
|5|[**ポアソン分布の最尤推定**]()||
|6|[**多変数のホテリング理論とマハラノビス・タグチ法**]()||
|6|[**混合正規分布モデル（GMM）**]()||
|6|[**k-NN**]()||
|7|[**統計モデリング向けトイデータ生成**]()||
|7|[**1変数線形回帰モデル**]()||
|7|[**多変数線形回帰モデル**]()||
|7|[**リッジ回帰モデル**]()||
|7|[**ガンマ回帰（非正規GLM）モデル**]()||
|8|[**ベイズ線形回帰モデル**]()||
|8|[**二項ロジスティック回帰モデル**]()||
|8|[**ランダム効果を含む二項ロジスティック回帰モデル**]()||
|9|[**各種前処理**]()||
|9|[**評価指標の算出**]()||
|9|[**交差検証**]()||

付録（本文中で解説していないコード）

|関連する章|手法名|書籍中のページ|
|---|---|---|
|5|[**二項ベータ分布モデル（過分散付き二項分布）**]()||
|5|[**負の二項分布モデル（過分散付きポアソン分布）**]()||
|6|[**OC-SVM**]()||
|7|[**ガウス過程回帰**]()||
|8|[**ポアソン回帰モデル**]()||
|8|[**グループ差を含むGLMM**]()||

## 付録解説

|書籍中のページ|中分類||
|---|---|---|
||||
||||
||||

## 正誤表
