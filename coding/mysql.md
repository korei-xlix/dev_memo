# 開発メモ：MySQLメモ

**★当リポジトリの利用にあたっては、必ず本readmeを確認してください★**  
  

このドキュメントは、MySQLのメモを示したものです。  
  





## 目次 / Table of contents

* [readme.md](/readme.md)
  * [リポジトリの利用規約](/readme.md#リポジトリの利用規約--repository-terms-of-use)

* [よく使うコマンド](#よく使うコマンド)

* [MySQLあれこれ](#mysqlあれこれ)

* [MySQLコマンド](#mysqlコマンド)

* [DB操作](#db操作)

* [ユーザ操作](#ユーザ操作)
  * [ユーザ一覧](#ユーザ一覧表示)
  * [ユーザ作成/パスワード付与](#ユーザ作成パスワード付与)
  * [ユーザ権限](#ユーザ権限)
  * [ユーザ削除](#ユーザ削除)

* [テーブル操作](#テーブル操作)
  * [テーブル一覧](#データ一覧表示select)
  * [テーブル作成](#テーブル削除)
  * [インデックス作成](#インデックス削除)
  * [テーブル削除](#テーブル削除)
  * [インデックス削除](#インデックス削除)
  * [カラム表示](#テーブルのカラム列を表示する)
  * [カラム追加](#テーブルにカラム列を追加する)
  * [カラム削除](#テーブルのカラム列を削除する)

* [データ操作](#データ操作)
  * [データ一覧（Select）](#データ一覧表示select)
  * [データ挿入（Insert）](#データ挿入insert)
  * [データ更新（Update）](#条件に合うデータ更新update)
  * [データ削除（Delete）](#条件に合うデータ削除delete)
  





## よく使うコマンド

### MySQLサービスの起動・終了・確認

```text
サービス起動
$ systemctl start mysqld

サービス停止
$ systemctl stop mysqld

サービス再起動
$ systemctl restart mysqld

サービス状態確認
$ systemctl status mysqld

MySQLのバージョン確認
$ mysql --version

DBに接続する
$ mysql -h [ホスト名] -u [ユーザ名] -p [データベース名]

rootで接続する場合
$ mysql -u root -p

```
  


### ファイルの場所

```text
MySQLシステムファイル
# ls /var/lib/mysql/

MySQLコンフィグファイル
# vi /etc/my.cnf

ログファイル
# ls /var/log/musql.log

MySQLサービスコンフィグ
# vi /usr/lib/systemd/system/mysqld.service

```
  





## MySQLコマンド

```text
終了
mysql> \q

状態確認
mysql> \s

ヘルプ
mysql> \h

エディタ起動？
mysql> \e

```
  





## ユーザ操作

全てスーパバイザ（root）での操作です。  
  

### ユーザ一覧表示

```text
ユーザの確認
mysql> select user, host, plugin from mysql.user;

```
  


### ユーザ作成、パスワード付与

```text
ユーザ作成だけ
mysql> create user '[ユーザ名]'@'[ホスト名]';
user1の作成
mysql> create user 'user1'@'localhost';

パスワードの設定（v8.0以降）
mysql> ulter user '[ユーザ名]'@'[ホスト名]' identified by '[パスワード]';
user1へのパスワード設定
mysql> ulter user 'user1'@'localhost' identified by 'password1';

ユーザ作成＆パスワード設定
mysql> create user '[ユーザ名]'@'[ホスト名]' identified by '[パスワード];
user1の作成＆パスワード設定
mysql> create user 'user1'@'localhost' identified by 'password1';

```
  


### ユーザ権限

```text
ユーザの権限確認
mysql> show grants for '[ユーザ名]'@'[ホスト名]';

ユーザの権限付与
mysql> grant [権限] on [レベル] to '[ユーザ名]'@'[ホスト名]' identified by '[パスワード]';
  [権限]...select、update、insert、delete、の組み合わせやall
  [レベル]...4段階ある
    グローバルレベル    ： *.*
    データベースレベル  ： [データベース名].*
    テーブルレベル      ： [データベース名].[テーブル名]
    カラムレベル        ： (カラム1, カラム2, カラム3...) on [データベース名].[テーブル名]

例：user1にdb1に対してselectとupdateの権限を与える
mysql> grant select, update on db1.* to 'user1'@'localhost';

ユーザの権限削除
mysql> revoke [権限] on [レベル] from '[ユーザ名]'@'[ホスト名]';
例：user1からupdateの権限を削除する
mysql> revoke update on db1.* to 'user1'@'localhost';

```
  


### ユーザ削除

```text
ユーザ削除
mysql> drop user [ユーザ名];

```
  





## DB操作

全てスーパバイザ（root）での操作です。  
  
```text
DB一覧
mysql> show databases;

DB作成
mysql> create database [DB名];

DB削除
mysql> drop database [DB名];

使うデータベースを選択する
mysql> use [DB名];
  なおMySQLには選択解除コマンドがなさそうです。

```
  





## テーブル操作

全てスーパバイザ（root）での操作です。  
  
### テーブル一覧表示

```text
テーブル一覧
mysql> show tables from [DB名];

```
  


### テーブル作成

```text
mysql> create table [DB名].[テーブル名] ([カラム1名前] [カラム1型], [カラム2名前] [カラム2型]... );
例：table1の作成
mysql> create table db1.table1 (column1 tinyint, column2 text);

```
  


### インデックス作成

```text
mysql> create index [インデックス名] on [DB名].[テーブル名] ([対象カラム名]);
例：table1のcolumn1でインデックス作成
mysql> create index index_id on table db1.table1 (column1);
  インデックスを作成しておくと、処理が速くなるらしいよ？

```
  


### テーブル削除

```text
mysql> drop table [DB名].[テーブル名];

```
  


### インデックス削除

```text
mysql> drop index [インデックス名] on [DB名].[テーブル名];
例：table1のインデックス削除
mysql> drop index index_id on table db1.table1;

```
  


### テーブルのカラム（列）を表示する

```text
mysql> show columns from [DB名].[テーブル名];

```
  


### テーブルにカラム（列）を追加する

```text
mysql> alter table [DB名].[テーブル名] add [カラム名] [カラムの型] [制約];
  [カラムの型]
    TINYINT型   ： tinyint(1)   ： 1バイト整数（-128～128）
    INT型       ： int(100)     ： 4バイト整数。
    BIGINT型    ： bigint(100)  ： 8バイト整数。範囲はINTより多い。
      後ろにunsignedを付けると、負の数なし整数で扱われます。
    
    DECIMAL型   ： decimal(5,2) ： 固定小数点。例は5桁の整数、2桁の小数で桁は固定される。
    FLOAT型     ： float        ： 4バイト浮動小数点
    DOUBLE型    ： double       ： 8バイト浮動小数点
      float、doubleにdecimalのような精度、スケールを付けられるが非推奨となってます。
    
    CHAR型      ： char(10)     ： 4バイト文字列（0～255文字）
    VARCHAR型   ： varchar(10)  ： 文字列（0～65535文字）
    TEXT型      ： 文字列。
    ENUM型      ： enum(a,b,c)  ： 1～2バイト特定の文字から一つ。
    SET型       ： set(a,b,c,d) ： 1～8バイト特定の文字から複数。
    BOOL型      ： bool         ： 真偽。true か false
    
    DATE型      ： date         ： 3バイト日付。YYYY-MM-DD
    TIME型      ： time         ： 3バイト時間。hh:mm:dd.ss
    DATETIME型  ： timedate     ： 8バイト日時。YYYY-MM-DD hh:mm:dd.ss

  [制約]
    Default     ： default 設定値 ： insert時、nullの場合に初期値を設定します。
    Not Null    ： not null       ： insert時、nullの場合に警告を出します。

```
  


### テーブルのカラム（列）を削除する

```text
mysql> alter table [DB名].[テーブル名] drop column [カラム名];

```
  





## データ操作

### データ一覧表示（Select）

```text
列全てを表示
mysql> select * from [DB名].[テーブル名];

条件に合う列全てを表示
mysql> select * from [DB名].[テーブル名] where [条件];
例 colum1が1以上のデータを全て表示
mysql> select * from db1.table1 where colum1>=1;

カラムを絞る(colum1,colum2のみ)
mysql> select colum1, colum2 from [DB名].[テーブル名];

```
  


### データ挿入（Insert）

```text
mysql> insert into [DB名].[テーブル名] (colum1, colum2...) values (value1, value2...);

```
  


### 条件に合うデータ更新（Update）

```text
全データの更新
mysql> update [DB名].[テーブル名] set [colum1の更新, colum2の更新...];
例 colum1=1, colum2=20
mysql> update db1.table1 set colum1=1, colum2=20;

条件に合うデータのみ更新
mysql> update [DB名].[テーブル名] set [更新データ] where [条件];
例 colum1が1以上のデータのみcolum2を更新
mysql> update db1.table1 set colum2=20 where colum1>=1;

```
  


### 条件に合うデータ削除（Delete）

```text
mysql> delete [DB名].[テーブル名] where [条件];
例 colum2が以上のデータのみ削除
mysql> delete db1.table1 where colum2>=1;

```
  





## MySQLあれこれ

### mysql_native_passwordについて

v8.4からmysql_native_passwordは非推奨となり、新方式であるcaching_sha2_passwordが推奨されています。  
古いスクリプトだとcaching_sha2_passwordに対応できず、ユーザ認証がエラーになる場合があるそうです。  
その場合、使用するユーザの認証方式をmysql_native_passwordに変更する必要があります。  
  





***
***
[[トップへ戻る]](/readme.md)  
  
::Admin= Korei (@korei-xlix)  
::github= [https://github.com/korei-xlix/](https://github.com/korei-xlix/)  
::Web= [https://website.koreis-labo.com/](https://website.koreis-labo.com/)  
::X= [https://x.com/korei_xlix](https://x.com/korei_xlix)  
***
