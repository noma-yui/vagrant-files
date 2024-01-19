# Ubuntu + PostgreSQL + C locale

UbuntuをC ロケールにして、PostgreSQLをインストールするもの。

## 実行手順

Vagrantfileを適当なディレクトリに置き、```vagrant up``` をする。

## 確認手順

```
>vagrant ssh
```

```bash
vagrant@my1c:~$ sudo su - postgres
postgres@my1c:~$ psql
psql (14.10 (Ubuntu 14.10-0ubuntu0.22.04.1))
Type "help" for help.

postgres=# SELECT 1 + 2;
 ?column?
----------
        3
(1 row)
```
