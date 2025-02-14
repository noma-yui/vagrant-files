# Latex書くのにWindowsに入れたくない

VMにTexlive全部入れたらええやん。

## 実行手順

Vagrantfileを適当なディレクトリに置き、```vagrant up``` をする。
環境にもよるが、インストールには30分から1時間ぐらいかかる。

## 確認手順

このフォルダにある`test01.tex`を使ってコンパイルのテストを実施する。
```bash
vagrant@my1:~$ lualatex -shell-escape test01.tex
```

## 少し便利なこと

デフォルトで、ホストOSのVagrantfileがあるフォルダーと、ゲストOSの`/vagrant`は共有フォルダーとなる。
一方で、自分のノートを作成するときに、そのフォルダーまでファイルをコピーするのは管理の手間がかかるであろう。例えば、そのフォルダをgitで管理しているなどをしていると、とても厄介な状況になる。
そこで、Vagrantfileに下記のように書くと、ノートのあるフォルダーを共有フォルダーとしてしまうことができる。
もちろん書いたらVMの再起動は必要である。

```
mymachine.vm.synced_folder "C:/Path/To/Your/Research/Note", "/home/vagrant/syncfolder", create: true
```
