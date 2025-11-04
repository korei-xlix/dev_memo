# 開発メモ：Linux / CentOS 技術メモ

**★当リポジトリの利用にあたっては、必ず本readmeを確認してください★**  
  

このドキュメントは、Linux関係の技術メモです。  
  





## 目次 / Table of contents

* [readme.md](../readme.md)
  * [リポジトリの利用規約](../readme.md#リポジトリの利用規約--repository-terms-of-use)

* システム管理系
  * [環境](#環境)
  * [よく見るファイルのパス](#よく見るファイルのパス)
  * [システム管理](#システム管理系)
    * [yumコマンド](#yumコマンド)
    * [システム確認](#システム確認)

* [ユーザ管理系](#ユーザ管理系)
  * [ユーザ確認](#ユーザ確認)
  * [ユーザ操作](#ユーザ操作作成パスワード変更削除)
  * [グループ操作](#グループ操作)

* [ネットワーク管理系](#ネットワーク管理系)

* [サービス管理系](#サービス管理系)

* [フォルダ管理系](#フォルダ管理系)
  * [ディスク容量確認](#ディスク容量確認)
  * [ファイル検索](#ファイル検索)
  * [フォルダ操作](#フォルダ操作)
  * [フォルダ権限](#フォルダ権限)

* アプリ
  * [viエディタ](#viエディタ)
  * [PHP系](#php系)

* その他情報
  * [nkf network kanji](#nkf-network-kanji)
  





## 環境

[目次へ戻る](#目次--table-of-contents)  
  

起動時に読み込ませる環境変数の編集します。  
  
```text

${HOME}    ユーザのホームディレクトリ

${PATH}    システムアプリのパス


$ vi ~/.bash_profile

CFLAGS=-fPIC
CPPFLAGS=/usr/include
LDFLAGS=/usr/lib64
LD_LIBRARY_PATH=/usr/lib:/usr/lib64
PKG_CONFIG_PATH=/usr/lib64/pkgconfig

:wq  ←保存・終了コマンド

```
  


コマンドから環境変数をエクスポートする。  
  
```text
エクスポート
$ export HENSU="Oniku Tabetai"

$ echo ${HENSU}
Oniku Tabetai

```
  


### よく見るファイルのパス
  
```text
エラーログ関係
$ ls /var

メールのエラーログ
$ ls /var/spool/mail

ユーザパスワード情報
$ ls /etc/passwd

ユーザグループ情報
$ ls /etc/group

ユーザ情報
$ ls /etc/shadow

ユーザホーム
$ ls /home[ユーザ名]

```
  





## システム管理系

[目次へ戻る](#目次--table-of-contents)  
  

### yumコマンド
  
```text
yumパッケージの確認
$ yum list [パッケージ名]
例  インストール済みパッケージ
$ yum list installed

yumパッケージのインストール
$ yum install [パッケージ名]

```
  


### システム確認
  
```text
OSバージョン確認
$ cat /etc/os-release

CPUの情報。コアごとに情報を出す。
$ cat /proc/cpuinfo

3秒ごとにOSで利用しているプロセスの数や状態、またOS全体のシステムリソース状況
$ top
  %CPU..CPU使用率
  %MEM..メモリ利用率
    左から7番目の「S」と書かれた列..プロセスの状態
      R->Running(実行状態もしくは実行可能状態)
      S->Sleeping(スリープ状態。ネットワークを介したデータ送受信の際もこのステータス)
      D->Uninterruptible sleep(IO待ち)
    ※プロセス状態がDの状態が続いてるプロセスがあれば
      IO待ちによってパフォーマンス遅延が発生している可能性がある

メモリやCPU使用率
$ vmstat
  cpu項の「id」列ではアイドル(空いている)割合をパーセントで表示
  「wa」列ではストレージのIO完了待ちを示す。

現在利用しているプロセス・ストッドごとのCPUやメモリ使用率が分かる。
$ ps

プロセスのみ
$ ps a

メモリに特化して詳細を表示
$ free
  Mem行のfree列の値は 何の用途にも使っていない物理メモリ量

メモリの詳細がわかる。
$ cat /proc/meminfo

実装されている物理メモリの詳細。
$ dmidecode --type memory
$ dmidecode --type memory | grep Size

```
  





## ユーザ管理系

[目次へ戻る](#目次--table-of-contents)  
  
### ユーザ確認

```text
ユーザID、所属グループの確認
$ id [ユーザ名]

ユーザ一覧
$ cat /etc/passwd

名前だけ表示
$ cat /etc/passwd|sed -e 's/:.*//g'

```
  


### ユーザ操作（作成/パスワード変更/削除）
  
```text
ユーザ作成
$ useradd [ユーザ名]

オプションつきユーザ作成
# useradd -d /users/user1 -g 551 -m -u 114514
    -d [dir] ログインディレクトリを設定
    -g [gid] グループIDを設定
    -m ホームディレクトリを作成
    -u [uid] ユーザーIDを設定

パスワードの設定
$ passwd [ユーザ名]

ホームディレクトリの変更
$ usermod -d /home/new-home [ユーザ名]

ユーザ削除
$ userdel [ユーザ名]
    -r ホームディレクトリも同時に削除
```
  


### グループ操作
  
```text
グループ一覧
$ cat /etc/group

グループの作成
$ groupadd [グループ名]
    -g [数値] グループID指定

グループの削除
$ groupdel [グループ名]

```
  





## ネットワーク管理系

[目次へ戻る](#目次--table-of-contents)  
  

```text
使用ポート
$ ss -nat

```
  





## サービス管理系

[目次へ戻る](#目次--table-of-contents)  
  

```text
サービス起動
$ systemctl start vsftpd

サービスの状態を見る
$ systemctl status vsftpd

サービス停止
$ systemctl stop vsftpd

サービス再起動
$ systemctl restart vsftpd

定義されているサービス全てを見る
$ systemctl list-unit-files --type=service

```
  





## フォルダ管理系

[目次へ戻る](#目次--table-of-contents)  
  

### ディスク容量確認
  
```text
フォルダ以下の容量
$ du -h -d 1 live/public/system/

ディスク容量
$ df

```
  


### ファイル検索
  
```text
rootフォルダ以下からライブラリ検索
$ find / -name libcrypto.so.3

/usr以下から証明書検索
$ find /usr -name ca-bundle.crt

ホームディレクトリ以下から証明書検索
$ find ~/ -name *.crt

```
  


### フォルダ操作
  
```text
ディレクトリ配下の詳細ファイル構成
$ ls -la

現在のパス
$ pwd

ディレクトリの作成
$ mkdir -p [名前]

ディレクトリの削除（確認型）
$ rmdir [名前]

ファイルの削除（確認型）
$ rm [名前]

ディレクトリの強制削除
$ rm -rf [名前]

tar形式のアーカイブ解凍
$ tar zxvf [名前]

```
  


### フォルダ権限
  
```text
基礎：パーミッションの読み方
  -rw-r--r--
  *uuugggooo

  *..ファイル種別
      - ファイル
      d ディレクトリ
      l シンボリックリンク（ショートカットリンクな感じ）
  u..ファイル所有者に対する権限
  g..ファイル所有グループに対する権限
  o..その他に対する権限（everyone？）

  権限ビット（16進数表示）
  rwx   7(111)   読み書き実行 ALL
  r--   4(100)   読みだけ
  -w-   2(010)   書きだけ
  --x   1(001)   実行だけ（だけはありえない）

フォルダの権限変更
$ chmod [パーミッション] [フォルダ名]
    -R フォルダ以下を再帰的に変更する

所有者の変更
$ chown [ユーザ名] [フォルダ名]

```
  





## viエディタ

[目次へ戻る](#目次--table-of-contents)  
  

```text
viエディタで編集開始
$ vi [ファイル名]
    ファイル名のファイルが存在しない場合、保存時にカレントにファイルを作成する
```


### viエディタのコマンド
  
```text
i テキスト入力モード
  ESCで終了

Ctrl+F  1ページ後ろ
Ctrl+B  1ページ前

1G ファイルの先頭行へ
G  ファイルの最終行へ

yy カーソル行をコピー
p  コピー行をカーソル行に挿入

x  カーソルの1文字削除
dd カーソル行を削除

/[文字]  文字を検索
?[文字]  文字を逆検索

:q!  終了（保存なし）
:qw 保存して終了

```
  





## PHP系

[目次へ戻る](#目次--table-of-contents)  
  

```text
PHP情報の参照
$ php -i

```
  





## nkf network kanji

[目次へ戻る](#目次--table-of-contents)  
  

nkf network kanjiはBase64のエンコードをおこなう変換モジュールです。  
  
  **参考**  
    [nkf network kanji（Homepage）](https://ja.osdn.net/projects/nkf/releases/)  
  
```text
make
make install

$ env
環境

$ locale
文字エンコーディング

```
  





***
***
[[トップへ戻る]](../readme.md)  
  
::Admin= Korei (@korei-xlix)  
::github= [https://github.com/korei-xlix/](https://github.com/korei-xlix/)  
::Web= [https://website.koreis-labo.com/](https://website.koreis-labo.com/)  
::X= [https://x.com/korei_xlix](https://x.com/korei_xlix)  
***
