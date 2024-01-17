# vagrant-files
Vagrantの書き方例

## このレポジトリー
Windowsしか持たない人でもLinuxやDockerを動かすために、
Vagrantを使った方法をここに書いておく。


## 事前準備
- Virturalboxのインストール
  - Web検索してインストールしてください。
- Vagrantのインストール
  - Web検索してインストールしてください。


## Vagrant plugin（オプショナル）
プロクシ環境下で設定をする場合、vagrant-proxyconfプラグインがあると便利です。
Vagrantをインストール後、DOSからCUIでインストールします。
プラグインをインストールする前に、DOSのプロクシ環境設定が必要です。

```
> set http_proxy=http://userid:PWD@proxy.local:8080
> set https_proxy=http://userid:PWD@proxy.local:8080
```
この環境変数を設定した上でプロクシプラグインをインストールします。
```
> vagrant plugin install vagrant-proxyconf
```

# VagrantによるVMの起動
- 下記の内容を「Vagrantfile」というファイル名でテキストで作成します。
- Proxyの「userid」「PWD」などは、ご自身の使用している値へ変更してください。プロクシ環境下でない場合は、当該行は消すかコメントアウト（先頭に#）してください。
```
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-22.04"
  config.vm.box_version = "202309.08.0"
  #config.proxy.http     = "http://userid:PWD@proxy.local:8080"
  #config.proxy.https    = "http://userid:PWD@proxy.local:8080"
  #config.proxy.no_proxy = "localhost,127.0.0.1"
  
  config.vm.provider "virtualbox" do |v|
    #v.gui = true
    v.gui = false
  end
  config.vm.define "myvm" do |mymachine|
    mymachine.vm.hostname = "myhostname"
    mymachine.vm.synced_folder "hostshare1/", "/guestshare", create: true
    mymachine.vm.network "forwarded_port", guest: 10082, host: 10082
    mymachine.vm.provision "docker"
  end
end
```

WindowsでDOS (cmd)を立ち上げます。
立ち上げ方はWindowsのバージョンによって若干異なりますが、スタートメニューのアイコンを押して「cmd」とタイプしてEnterキーを押すか、スタートメニューの中からマウスで「コマンドプロンプト」を探してクリックします。
「Vagrantfile」を保存したフォルダーに移動（cd）し、下記コマンドでVMを起動します。
```
> vagrant up
```
タイムアウトを繰り返す場合は、VirtualBoxの画面を表示して、当該VMの起動画面を表示すると進む場合があります。

VMが起動したら下記コマンドでssh接続でVM内部に入ります。
```
> vagrant ssh
```

VM内部に入ったら、下記コマンドにより、プログラムをインストール可能です。
```
$ sudo apt update
$ sudo apt install postgresql-all
```


## 共有ディレクトリ

ホストOS（おそらくWindows）とゲストOS（おそらくLinux）は別の環境ですが、共有フォルダを介してデータをやり取りできます。
デフォルトでは、ホストOSの「Vagrantfile」があるフォルダと、ゲストOSの「/vagrant」が共有されます。

上記の例の「Vagrantfile」ではホストマシンの「hostshare1/」とVMの「/guestshare」が共有されます。


## （オプショナル）dockerのhello-world

Dockerの設定がうまくいっているかどうかは下記を実行しエラー無く終わることを確認します。
```
$ docker run hello-world
```



 