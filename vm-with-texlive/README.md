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
