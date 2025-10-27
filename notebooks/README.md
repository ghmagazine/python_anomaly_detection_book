# 環境構築方法

本書のサンプルコードを動作させるために必要な環境構築方法を、OSごとに記載します。

- [Windows（非プロキシ環境）]()
- [Windows（プロキシ環境）]()
- [Mac]()
- [Linux（Ubuntu等のDebian系）]()

## Windows

以下の環境

- OSのバージョン：Windows10またはWindows11
- Pythonのバージョン：3.10以降
- パッケージ管理ツール：pipまたは[uv]()
- プロキシ：なし

### Gitのインストール

[Git]()は、ソースコードの変更履歴を記録・追跡するための分散型バージョン管理システムです。
ここではサポートサイト（Githubリポジトリ）からコードをダウンロード（Clone）するために使用します。

WindowsでGitをインストールする）には（[公式手順](https://git-scm.com/book/ja/v2/%E4%BD%BF%E3%81%84%E5%A7%8B%E3%82%81%E3%82%8B-Git%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB)に準拠）、[こちらの公式サイト](https://git-scm.com/install/windows)の`Click here to download`をクリックして、インストーラのexeファイルをダウンロードしてダブルクリックで実行します。

インストーラを実行するとインストール用のウィンドウが開くので、デフォルト設定のまま`Next`を押し続けると、インストールが始まります。

インストールが完了したら、

### uvのインストール

[uv](https://docs.astral.sh/uv/)は、Pythonのパッケージ管理ツールのひとつです。Pythonデフォルトのパッケージ管理システムであるpipや、デフォルトの仮想環境管理ツールであるvenvと近い操作感を維持したまま、高速動作やプラットフォームへの依存性を下げる工夫を実現しています。

Windowsでuvをインストールするには、Powershellを開いて以下のコマンドを実行します（[公式インストール手順](https://docs.astral.sh/uv/getting-started/installation/#standalone-installer)に準拠）。

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

### VSCodeのインストール

###

## Windows（プロキシ環境）

## Mac

- OSのバージョン：MacOS 15 (Sequoia)以降
- Pythonのバージョン：3.10以降
- パッケージ管理ツール：Conda（Miniforge）

### Miniforgeのインストール

Miniforgeは、condaによるパッケージ管理環境を、無償で使用できるconda-forgeリポジトリで利用するように簡単に環境構築できるツールです。

pipではなくcondaを利用する背景として、2025年現在Macの多くで用いられているMシリーズCPUは、WindowsやLinuxで多く用いられているx86-64アーキテクチャのCPUとは仕様が異なるため、pip（やそれをベースとしたuv等）でのライブラリインストールがうまくいかないケースが頻発していました。よってMシリーズ対応のライブラリをより簡単にインストールできるcondaをここでは利用します（pipによるMシリーズでのインストール環境は近年改善してきているため、そのうちこちらのページでもcondaの代わりにpipやuvを使う方法に移行します）。

[こちらのMiniforgeのGitHub](https://github.com/conda-forge/miniforge#download)から、Mシリーズ用のインストーラ (Miniforge3-MacOSX-arm64と書いたリンク)をダウンロード

ターミナルから以下のコマンドでダウンロードフォルダに移動し

```bash
cd ~/Downloads
```

以下のコマンドでダウンロードしたMiniforge3-MacOSX-arm64.shを実行

```bash
bash Miniforge3-MacOSX-arm64.sh
```

### Conda仮想環境作成

以下コマンドでPython3.10の仮想環境を作成

```bash
conda create --name py310 python=3.10
```

以下コマンドで作成した仮想環境をアクティベート

```bash
conda activate py310
```

### Condaで必要パッケージインストール

以下コマンドで必要パッケージをインストール

```bash
conda install numpy pandas jupyter seaborn scipy scikit-learn statsmodels
```

### PyMCのインストール

依存パッケージであるgraphvizをインストールします

```bash
conda install python-graphviz
```

[こちらに記載](https://discourse.pymc.io/t/performance-issue-with-pymc-training-with-macbook-m1-chip/12658/8)のように、M1 Macでは特定のバージョンのPyMCがうまく動かないようなので、以下のようにバージョン指定でインストールします。

```bash
conda install pymc==5.7
```

### PyTorchのインストール

MPSを有効にするため、[こちら](https://towardsdatascience.com/gpu-acceleration-comes-to-pytorch-on-m1-macs-195c399efcc1)を参考に以下コマンドでPyTorchと関連パッケージ（TorchVision、TorchAudio）インストールします。

```bash
pip3 install -U --pre torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/nightly/cpu
```

### Anomalibのインストール

[こちら](https://github.com/openvinotoolkit/anomalib/tree/main?tab=readme-ov-file#-installation)を参考に、以下コマンドでanomalibをインストールします

```bash
pip install anomalib
```

依存パッケージを以下コマンドでインストールします

```bash
anomalib install -v
```
