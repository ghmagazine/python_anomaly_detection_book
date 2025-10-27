# サンプルコード使用方法

## 環境構築方法

本書のサンプルコードを動作させるために必要な環境構築方法を、OSごとに記載します。

- [Windows](https://github.com/ghmagazine/python_anomaly_detection_book/blob/main/notebooks/README.md#windows)
- [Mac](https://github.com/ghmagazine/python_anomaly_detection_book/blob/main/notebooks/README.md#mac)
- [Linux（Ubuntu等のDebian系）]()

### Windows

以下の条件を想定して環境構築します。

- OSのバージョン：Windows10またはWindows11
- Pythonのバージョン：3.10以降
- パッケージ管理システム：conda（Miniforge）

なお、パッケージ管理にcondaを使用する理由として、Windows環境では[PyMCのインストールにcondaが推奨されており](https://www.pymc.io/projects/docs/en/stable/installation.html)、pipやuvを使用する場合は自分でC++コンパイラ等をインストールしてビルドする必要が生じるため、2025年10月時点ではインストールが簡単なcondaの利用がおすすめです。

#### Gitのインストール

[Git](https://git-scm.com/)は、ソースコードの変更履歴を記録・追跡するための分散型バージョン管理システムです。
ここではサポートサイト（Githubリポジトリ）からコードをダウンロード（Clone）するために使用します。

WindowsでGitをインストールするには（[公式手順](https://git-scm.com/book/ja/v2/%E4%BD%BF%E3%81%84%E5%A7%8B%E3%82%81%E3%82%8B-Git%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB)に準拠）、[こちらの公式サイト](https://git-scm.com/install/windows)の`Click here to download`をクリックして、インストーラのexeファイルをダウンロードしてダブルクリックで実行します。

インストーラを実行するとインストール用のウィンドウが開くので、デフォルト設定のまま`Next`を押し続けると、インストールが始まります。

インストールが完了したら、エクスプローラの任意のフォルダを右クリックして、`Git Bash Here`と表示されていれば成功です（クリックするとGitのコマンドライン操作用のターミナルが開きます）。

初回起動時は`Git Bash Here`で開いたターミナルから、以下コマンドでユーザ名とメールアドレスを登録しておきます。

```bash
git config --global user.name "好きな名前"
git config --global user.email "好きなメールアドレス"
```

#### conda（Miniforge）のインストール

condaはPythonのパッケージ管理システムの一種です。Pythonのパッケージ管理システムは他にもpipやuv等が存在しますが、前述のようにPyMCのインストールを簡略化するため、ここではcondaを使用します。
Miniforgeは、condaによるパッケージ管理環境を、無償で使用できるconda-forgeリポジトリと紐付けて構築するツールです。

[こちらのMiniforgeのGitHub](https://github.com/conda-forge/miniforge?tab=readme-ov-file#windows)から、`the Windows installer`と書いたリンクをクリックすることで、Miniforgeインストーラexeファイルをダウンロードできます。

ダウンロードしたインストーラをダブルクリックして指示の通りにインストールを進めます。
インストールが完了したら、miniforgeがインストールされているフォルダの場所（`conda.exe`があるフォルダ）を確認します。デフォルトでは`C:\Users\ユーザー名\miniforge3\Scripts`または`C:\ProgramData\miniforge3\Scripts`フォルダにインストールされているはずです。

Windows画面下の検索窓に「環境変数」と打つと出てくる「環境変数を編集」画面に入り、「システム環境変数」→「Path」をダブルクリック→「新規」で出てくる欄に、先ほど確認したインストールフォルダ（デフォルトでは`C:\Users\ユーザー名\miniforge3\Scripts`または`C:\ProgramData\miniforge3\Scripts`）を入力し、「OK」を押してパスを通します。

PowerShellを開き、以下コマンドでシェルの初期設定をします

```shell
conda init
```

以下コマンドを実行して`base`環境が表示されれば、インストールとパス設定が成功しています。

```shell
conda env list
```

#### VSCodeのインストール

VSCodeは高機能なエディタで、Pythonのようなプログラミング言語を開発・デバッグするために用いられます。

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

`python_anomaly_detection_book`というフォルダができて、内部にサンプルコード等が格納されていればクローン成功です。

#### VSCodeでリポジトリを開く

VSCodeを起動し、左上のメニューの`File`→`Open Folder`をクリックし、先ほどクローンした`python_anomaly_detection_book`フォルダを選択して開きます。
フォルダを開いてターミナルが表示されていなければ、左上のメニューの`Terminal`→`New Terminal`をクリックします。

#### 仮想環境の作成とライブラリのインストール

Pythonの仮想環境を作成し、NumPyやPyMC等の必要ライブラリをインストールしていきます。

まず先ほど開いたVSCodeのターミナルから以下コマンドを打ち、`environment_windows.yml`の記載内容に基づきライブラリがインストールされた、`anomaly_detection`という名前のcondaの仮想環境を作成します。

```shell
conda env create -f environment_windows.yml
```

以下コマンドで、作成した仮想環境をアクティベートしてください（うまくいかない場合はターミナルを一度閉じて開き直してください）

```shell
conda activate anomaly_detection
```

ターミナルの左に`(anomaly_detection)`のように表示されればアクティベート成功です。

##### ※`environment_windows.yml`から作成した仮想環境がうまく動作しない場合

上記で作成された仮想環境でうまく動作しない場合、[PyMC公式のインストール手順に基づき](https://www.pymc.io/projects/docs/en/stable/installation.html)以下のように一から仮想環境を作成してください

```shell
conda create -n anomaly_detection "pymc>=5"
```

```shell
conda activate anomaly_detection
conda install jupyter
conda install seaborn
conda install scikit-learn
```

#### 動作確認

クローンしたリポジトリ内の任意のJupyterファイル（例：`notebooks/ch8_4_Bayesian_Linear_Regression.ipynb`）を開き、最初のコードセルの左側にある`▷`ボタンを押してコードを実行します。
最初の1回のみPythonの実行環境の選択が求められるので、`Python Envifonments`→`anomaly_detection`（先ほど作成した仮想環境）と選択します。

エラーなしで実行できれば成功です。

## Mac

以下の条件を想定して環境構築します。

- OSのバージョン：MacOS 15 (Sequoia)以降
- Pythonのバージョン：3.10以降
- パッケージ管理ツール：conda（Miniforge）

MacもWindowと同様、PyMCのインストールにcondaが推奨されていることや、2025年現在Macの多くで用いられているMシリーズCPUがconda＋conda-forge構成と相性が良いことから、Miniforgeを用いたパッケージ管理システムのインストールをおすすめします。

#### Gitのインストール

Macでは基本的にデフォルトでGitがインストールされているので、新たにインストールする必要はありません。

### conda（Miniforge）のインストール

[こちらのMiniforgeのGitHub](https://github.com/conda-forge/miniforge?tab=readme-ov-file#unix-like-platforms-macos-linux--wsl)の手順に基づきインストールを進めていきます。

ターミナルから以下コマンドでMiniforgeのインストール用スクリプトをダウンロードします。

```bash
curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
```

以下のコマンドでダウンロードしたMiniforge3-xxx-arm64.shを以下コマンドで実行すると、インストールが始まります。

```bash
bash Miniforge3-$(uname)-$(uname -m).sh
```

#### VSCodeのインストール

MacにVSCodeをインストールする場合、Homebrew（Mac向けパッケージ管理ツール）がインストールされているのであればこれを利用すると便利です。以下コマンドでインストールできます。

```zsh
brew install visual-studio-code --cask
```

Homebrewを使用しない場合、[公式のダウンロードページ](https://code.visualstudio.com/download)から`Mac`をクリックして`Visual Studio Code.app`と名前のついたアプリケーションファイルをダウンロードします。ダウンロードしたFinderでMacの「アプリケーション」フォルダにドラッグ＆ドロップすれば、VSCodeを使用できるようになります。

インストールが完了したらPCの再起動後にVSCodeを開き、左側の`Extensions`タブを開いて以下のアドオンをインストールします。

- Python
- Jupyter
- Rainbow CSV（必須ではありませんが、CSVファイルが見やすくなります）

####　本GitHubリポジトリのクローン

本GitHubリポジトリ（サンプルコードを含めた一連のコードやドキュメントが格納されたフォルダ）をダウンロード（クローン）したいフォルダにターミナルで移動し、

```bash
cd リポジトリをCloneしたいフォルダ
```

以下コマンドでクローンを実行します。

```bash
git clone https://github.com/ghmagazine/python_anomaly_detection_book.git
```

`python_anomaly_detection_book`というフォルダができて、内部にサンプルコード等が格納されていればクローン成功です。

#### VSCodeでリポジトリを開く

VSCodeを起動し、左上のメニューの`File`→`Open Folder`をクリックし、先ほどクローンした`python_anomaly_detection_book`フォルダを選択して開きます。
フォルダを開いてターミナルが表示されていなければ、左上のメニューの`Terminal`→`New Terminal`をクリックします。

#### 仮想環境の作成とライブラリのインストール

Pythonの仮想環境を作成し、NumPyやPyMC等の必要ライブラリをインストールしていきます。

まず先ほど開いたVSCodeのターミナルから以下コマンドを打ち、`environment_mac.yml`の記載内容に基づきライブラリがインストールされた、`anomaly_detection`という名前のcondaの仮想環境を作成します。

```shell
conda env create -f environment_mac.yml
```

以下コマンドで、作成した仮想環境をアクティベートしてください（うまくいかない場合はターミナルを一度閉じて開き直してください）

```shell
conda activate anomaly_detection
```

ターミナルの左に`(anomaly_detection)`のように表示されればアクティベート成功です。

##### ※`environment_mac.yml`から作成した仮想環境がうまく動作しない場合

上記で作成された仮想環境でうまく動作しない場合、[PyMC公式のインストール手順に基づき](https://www.pymc.io/projects/docs/en/stable/installation.html)以下のように一から仮想環境を作成してください

```shell
conda create -n anomaly_detection "pymc>=5"
```

```shell
conda activate anomaly_detection
conda install jupyter
conda install seaborn
conda install scikit-learn
```

#### 動作確認

クローンしたリポジトリ内の任意のJupyterファイル（例：`notebooks/ch8_4_Bayesian_Linear_Regression.ipynb`）を開き、最初のコードセルの左側にある`▷`ボタンを押してコードを実行します（初回実行時は時間がかかります）。
最初の1回のみPythonの実行環境の選択が求められるので、`Python Envifonments`→`anomaly_detection`（先ほど作成した仮想環境）と選択します。

エラーなしで実行できれば成功です。
