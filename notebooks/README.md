# サンプルコード使用方法

## 環境構築方法

本書のサンプルコードを動作させるために必要な環境構築方法を、OSごとに記載します。

- [Windows（非プロキシ環境）]()
- [Windows（プロキシ環境）]()
- [Mac]()
- [Linux（Ubuntu等のDebian系）]()

### Windows

以下の環境を想定して環境構築します。

- OSのバージョン：Windows10またはWindows11
- Pythonのバージョン：3.10以降
- パッケージ管理ツール：conda（conda-forgeリポジトリ）
- プロキシ：なし

なお、パッケージ管理ツールにcondaを使用する理由として、Windows環境では[PyMCのインストールにcondaが推奨されており]()、pipやuvを使用する場合は自分でC++コンパイラ等をインストールする必要が生じるため、2025年10月時点ではインストールが簡単なcondaの利用を推奨します。

#### Gitのインストール

[Git]()は、ソースコードの変更履歴を記録・追跡するための分散型バージョン管理システムです。
ここではサポートサイト（Githubリポジトリ）からコードをダウンロード（Clone）するために使用します。

WindowsでGitをインストールする）には（[公式手順](https://git-scm.com/book/ja/v2/%E4%BD%BF%E3%81%84%E5%A7%8B%E3%82%81%E3%82%8B-Git%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB)に準拠）、[こちらの公式サイト](https://git-scm.com/install/windows)の`Click here to download`をクリックして、インストーラのexeファイルをダウンロードしてダブルクリックで実行します。

インストーラを実行するとインストール用のウィンドウが開くので、デフォルト設定のまま`Next`を押し続けると、インストールが始まります。

インストールが完了したら、エクスプローラの任意のフォルダを右クリックして、`Git Bash Here`と表示されていれば成功です（クリックするとGitのコマンドライン操作用のコンソールが開きます）。

#### Pythonのインストール

**uvを使用する（pipを使用しない）場合はこの作業は不要です**

WindowsにPythonをインストールするには、[公式のダウンロードページ](https://www.python.org/downloads/windows/)からダウンロードしたいバージョンのPythonを探し、`Download Windows installer (64-bit)`をクリックしてexeファイルをダウンロードします。

exeファイルを開いたら表示される`Install Now`を押し、指示に従って進めばインストールできます。

以下コマンドで、`-V:3.12 * C:\Users\ユーザー名\AppData\Local\Programs\Python\Python312\python.exe`のように表示されたらインストール成功です。

```
py -0p
```

インストールに失敗したら、

#### uvのインストール

**uvを使用しない（pipをパッケージ管理に使用する）場合はこの作業は不要です**

[uv](https://docs.astral.sh/uv/)は、Pythonのパッケージ管理ツールのひとつです。Pythonデフォルトのパッケージ管理システムであるpipや、デフォルトの仮想環境管理ツールであるvenvと近い操作感を維持したまま、高速動作やプラットフォームへの依存性を下げる工夫を実現しています。

Windowsにuvをインストールするには、PowerShellを開いて以下のコマンドを実行します（[公式インストール手順](https://docs.astral.sh/uv/getting-started/installation/#standalone-installer)に準拠）。

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

インストールが完了したら、PowerShellを一度閉じてから開きなおして、以下コマンドで`success`と出ればインストール成功です。

```powershell
uv self update
```

#### VSCodeのインストール

VSCodeは高機能なエディタで、Python等の

WindowsにVSCodeをインストールするには、[公式のダウンロードページ](https://code.visualstudio.com/download)から`Windows`をクリックしてexeファイルをダウンロードします。

ダウンロードしたexeファイルをダブルクリックで実行するとインストーラが開くので、指示に従いインストールします。
（途中「エクスプローラのファイルコンテキストメニューに[Codeで開く]アクションを追加する」「エクスプローラのディレクトリコンテキストメニューに[Codeで開く]アクションを追加する」をチェックすると、右クリックでフォルダやファイルを開けて便利です）

インストールが完了したらPCの再起動後にVSCodeを開き、左側の`Extensions`タブを開いて以下のアドオンをインストールします。

- Python
- Jupyter
- Rainbow CSV（必須ではありませんが、CSVファイルが見やすくなります）

####　本GitHubリポジトリのクローン

本GitHubリポジトリ（サンプルコードを含めた一連のコードやドキュメントが格納されたフォルダ）をダウンロード（クローン）したいフォルダをエクスプローラで開き、右クリックで出てくる`Git Bash Here`を選択します。
コンソールが開くので、以下コマンドを打ちます

```bash
git clone https://github.com/ghmagazine/python_anomaly_detection_book.git
```

`python_anomaly_detection_book`というフォルダができており、内部にサンプルコード等が格納されていればクローン成功です。

#### VSCodeでリポジトリを開く

VSCodeを起動し、左上のメニューの`File`→`Open Folder`をクリックし、先ほどクローンしたフォルダを選択して開きます。
フォルダを開いてターミナルが表示されていなければ、左上のメニューの`Terminal`→`New Terminal`をクリックします。

#### 必要ライブラリのインストール

Pythonの仮想環境を作成し、NumPyやPyMC等の必要ライブラリをインストールしていきます。pipを使う場合とuvを使う場合に分けて解説します。

##### pipによるインストール

**uvを使用する（pipを使用しない）場合はこの作業は不要です**

まずはライブラリをインストールするための仮想環境（venv）を作成します。
先ほどVSCodeでリポジトリを開いてから起動したターミナルから、以下コマンドで`.venv`という名前の仮想環境を作成します。

```shell
py -m venv .venv
```

以下コマンドで仮想環境をアクティベートします。

```shell
.venv/Scripts/activate.ps1
```

※「このシステムではスクリプトの実行が無効になっているため、‥を読み込むことができません」というようなエラーが出た場合、以下コマンドでスクリプトの実行を有効化します

```shell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
```

以下コマンドで、`requirements.txt`に記載されたライブラリ（NumPy、scikit-learn等）を一括インストールします。

```shell
py -m pip install -r requirements.txt
```

##### uvによるインストール

**uvを使用しない（pipをパッケージ管理に使用する）場合はこの作業は不要です**

以下コマンドで、`pyproject.toml`に記載されたライブラリ（NumPy、scikit-learn等）を一括インストールします。

```shell
uv sync
```

#### 動作確認

クローンしたリポジトリ内の任意のJupyterファイル（例：`notebooks/ch2_3&4_EDA.ipynb`）を開き、最初のコードセルの左側にある`▷`ボタンを押してコードを実行します。
最初の1回のみPythonの実行環境の選択が求められるので、`Python Envifonments`→`.venv`（先ほど作成した仮想環境）と選択します。

エラーなしで実行できれば成功です。

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
