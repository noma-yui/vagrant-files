# Ubuntu + Jupyter。ただしアクセスはホストから

Ubuntuを JupyterLabをインストールして、ホストOSのブラウザーからアクセスする。

## 実行手順

Vagrantfileを適当なディレクトリに置き、```vagrant up``` をする。

## 確認手順

ホストOS（Windows）でブラウザーを開き、URLを入力するところに「localhost:8080」を入力する。
JupyterLabの画面が出てくればよい。
