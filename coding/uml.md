# 開発メモ：Plant UML技術

**★当リポジトリの利用にあたっては、必ず本readmeを確認してください★**  
  

このドキュメントは、UMLの書き方 の標準テンプレートです。  
  
シーケンス図、クラス図に対応してます。  
Plank UMLの記述にご利用ください。  
  





## 目次

* [readme.md](../readme.md)
  * [リポジトリの利用規約](../readme.md#リポジトリの利用規約--repository-terms-of-use)
  * [参考 (Material)](#参考--material)

* [VS CodeとPlank UMLのセットアップ](#vs-codeとplank-umlのセットアップ)

* [VS Codeのおすすめ拡張](#vs-codeのおすすめ拡張)

* 【シーケンス図】
  * [基本書式](#シーケンス--基本書式)
  * [分類子の宣言](#シーケンス--分類子の宣言)
  * [シーケンス線の書式](#シーケンス--シーケンス線の書式)
  * [応答メッセージを矢印の下に表示する](#応答メッセージを矢印の下に表示する)
  * [自動番号振り](#自動番号振り)
  * [条件分岐](#条件分岐)
  * [テキストボックス](#テキストボックス)

* [クラス図](#クラス図)
  





## VS CodeとPlank UMLのセットアップ

Plant UMLは、Javaで動作しますが、GUIベースで使うにはVS Codeをベースに利用します。  
VS CodeからPlank UMLのJavaを起動します。  
  
セットアップは以下のようにおこないます。  

* 1.VS Codeをダウンロード、インストールします。  
  VS Codeは誰でもmicrosoftから無料で利用できます。  
  
  [VS Code](https://azure.microsoft.com/ja-jp/products/visual-studio-code)  
  

* 2.左のバー「Extention」、左上の窓で「Japanese Language Pack」で日本語パッケージを検索します。  
  Japanese Language Pack for VS Codeの「Install」をクリックします。  
  インストールが完了したら、左下の「Restart」でVS Codeが再起動され、日本語化されます。  
  
  コマンドパレットからも言語の変更ができます。  
  「表示」-「コマンドパレット」で「> display」を入力。  
  「標示言語を構成する」で「日本語」を選択する。  
  

* 3.左のバー「Extention」、左上の窓で「Plant UML」を検索します。  
  「Install」をクリックします。  

* 4.Java Deveropment Kitがインストールされているか確認します。  
  Java 8か16でも動作します。  
  
確認するには、コマンドプロンプト（スタートメニューの右クリック-> コマンドプロンプト）で以下を実行します。  

```text
> java -version

java version "16.0.1" 2021-04-20
Java(TM) SE Runtime Environment (build 16.0.1+9-24)
Java HotSpot(TM) 64-Bit Server VM (build 16.0.1+9-24, mixed mode, sharing)
※バージョンが表示されていれば OKです

```

> **Java Devがインストールされていなかった場合...**  
> Java Deveropment Kitがインストールされていなければセットアップします。  
> Java Deveropment Kitは誰でもOracleから無料で利用できます。  
>
> [[Java Deveropment Kit]](https://www.oracle.com/jp/java/technologies/downloads/)  
>
> Windowsの場合、「Windows」の「x64 Installer」とかでいけると思います。  
  

* 5.記述したコードをPlant UMLで表示するには、「Alt」+「D」でプレビュー表示できます。  
  
* 6.ワークスペースの設定もしておくといいです。  
  左下の「設定」-「設定」の「ワークスペース」で、検索窓を指定。  
  
  File.encoding：utf-8　デフォルトのエンコード形式を設定する。  
  
  editor.mouseWheelZoom：ON　「Ctrl」+マウスホイールで文字の大きさが変更できる。  
  
  editor.renderWhitespace：all　半角スペースを可視化できる。  
  
  Editor: Font Family：MS Gothic  等幅フォントを設定できる。  





## VS Codeのおすすめ拡張

* **CSS Peek**  
  CSSのピーク表示  
  

* **Zenkaku**  
  全角スペースの可視化  
  

* **Live Server**  
  簡単にローカルサーバを立ち上げ、webの挙動を確認できる。  
  右下の「Go Live」より。  
  

* **Whitespace+**  
  半角スペースの可視化ができる。  
  キーバインドが必要。  
  「ファイル」-「設定」-「ショートカット」で、「extension.toggleWhitespacePlus」  
  
  コマンドパレットで「Whitespace+ Config」を実行する。  


```text
autostart：ON　起動時自動実行  

"dark": {
         "backgroundColor": "rgba(0, 0, 128, 0.3)",
         "borderColor": "rgba(0, 0, 192, 0.4)"
       }

※カラーパターン
  r..赤, g..緑, b..青, a..透明度

```
  

* **vscode-color-picker**  
  カラーピッカーを表示する。  
  が、言語を有効にする必要がある。  
  
「ユーザ」-「拡張機能」-「vscode-color-picker」でsetting.jsonで編集。  
  
```text
{
    "editor.renderWhitespace": "all",
    "vscode-color-picker.languages": [

        "python",
        "javascript",
        "typescript",
        "css",
        "html",
        "markdown"

    ]
}

コード一覧
https://code.visualstudio.com/docs/languages/identifiers  

```
  

* **markdownlint**  
  markdownの書式チェックをし統一性をもたせる。  
  setting.jsonから任意の警告を消すこともできる。  
  「設定」で「markdownlint」を検索し、setting.jsonを編集。  
  
```text
    "editor.useTabStops": false,
    "markdownlint.config": {
        
        "MD012": false,
        "MD033": false
    }

```





## シーケンス / 基本書式

* 基本ドキュメント
* ヘッダー+フッター
* 類分子+グループ化
* タイトルの付加
* 基本線
* 分割線
* ページ区切り
  

```text
@startuml practice1

'################################
' ヘッダ・フッター
'################################
header Page Header
footer Page %page% of %lastpage%


'################################
' 類分子
'################################
participant "Participant 1" as Foo1
participant "Participant 2" as Foo2

box Group100
    participant "Participant 3" as Foo3
    participant "Participant 4" as Foo4
end box

'################################
' タイトル
'################################
title Example Title


'################################
' シーケンス本文
'################################

'### 要求 -> 応答
Foo1 -> Foo2 : Request 1
Foo1 <- Foo2 : Ack(OK) 1

'### 分割線
== 分割線 ==
Foo1 -> Foo2 : Request 1-A
Foo1 <- Foo2 : Ack(OK) 1-A

Foo2 -> Foo3 : Request 1-B
Foo2 <- Foo3 : Ack(OK) 1-B

Foo3 -> Foo4 : Request 1-C
Foo3 <- Foo4 : Ack(OK) 1-C

'### 要求 -> 応答(2ページ目)
newpage
Foo1 -> Foo2 : Request 2
Foo1 <- Foo2 : Ack(OK) 2

'### 要求 -> 応答(3ページ目) +タイトル付き
newpage A title for the\nlast page
Foo1 -> Foo2 : Request 3
Foo1 <- Foo2 : Ack(OK) 3

@enduml
```
  





## シーケンス / 分類子の宣言

* 分類子
* 分類子+カラー
* 分類子+改行や複数行
  

```text
@startuml practice2

'################################
' 類分子
'################################
participant Participant as Foo
actor       Actor       as Foo1
boundary    Boundary    as Foo2
control     Control     as Foo3
entity      Entity      as Foo4
database    Database    as Foo5
collections Collections as Foo6
queue       Queue       as Foo7

'### +カラー
participant "Participant 2" as L #c00000

'### +改行 \nを入れる
participant "Participant\ntext 1" as F0011

'### +複数行
participant Participant [
    =Title
    ----
    ""SubTitle""
]



'################################
' シーケンス本文
'################################
Foo -> Foo1 : To actor 
Foo -> Foo2 : To boundary
Foo -> Foo3 : To control
Foo -> Foo4 : To entity
Foo -> Foo5 : To database
Foo -> Foo6 : To collections
Foo -> Foo7: To queue

@enduml
```





## シーケンス / シーケンス線の書式

* 自分自身へのメッセージ
* 要求・応答
* 基本線・点線・断線
* 線と線の間隔開け
* 線の色付け
* 縦ラインの色付け・解除

```text
@startuml practice3

'################################
' 類分子
'################################
participant "Participant 1" as Foo1
participant "Participant 2" as Foo2
participant "Participant 3" as Foo3


'################################
' シーケンス本文
'################################

== シーケンス本文 ==
'### 自分自身へのメッセージ(右)
Foo1 -> Foo1 : 自分自身への\nメッセージ(右)

'### 自分自身へのメッセージ(左)
Foo1 <- Foo1 : 自分自身への\nメッセージ(左)

'### 要求 -> 応答
Foo1 -> Foo2 : Request
Foo1 <- Foo2 : Ack(OK)


'################################
' シーケンス線の書式
'################################

== シーケンス線の書式 ==
Foo1 -> Foo2 : 基本線
Foo1 --> Foo2 : 点線
Foo1 ->x Foo2 : シーケンス断？

note over Foo1 #00ffff
    <font color=#0000ff><b>★★間隔★★
end note
|||
Foo1 ->o Foo2 : 〇
Foo1 <-> Foo2 : 両方向

note over Foo1 #00ffff
    <font color=#0000ff><b>★★間隔 100pix★★
end note
||100||
Foo1 -[#ff0000]> Foo2 : 赤い線（カラー）
Foo1 -[#0000ff]-> Foo2 : 青い点線（カラー）

Foo1 -> Foo2 : <font color =#ff0000><b>赤い文字+太字

' == あんま使わない書式かも？ ==
' Foo1 ->> Foo2
' Foo1 -\ Foo2
' Foo1 \\- Foo2
' Foo1 //-- Foo2
' Foo1 o\\-- Foo2
' Foo1 <->o Foo2


== 活性・破棄 ==
Foo1 -> Foo2 : Request 1
activate Foo2 #0000ff

Foo1 <- Foo2 : Ack 1(OK)
deactivate Foo2

note right #ffff00
    <font color=#ff0000>終了
end note


Foo1 -> Foo3 : Request 2
activate Foo3

Foo1 <- Foo3 : <font color="ff0000>Ack 2(NG)
destroy Foo3

note right #ff0000
    <font color=#ffffff>破棄
end note

@enduml
```





## 応答メッセージを矢印の下に表示する

```text
@startuml practice4

'################################
' 応答メッセージを矢印の下に表示する
'################################
skinparam responseMessageBelowArrow true

'################################
' 類分子
'################################
participant "Participant 1" as Foo1
participant "Participant 2" as Foo2


'################################
' シーケンス本文
'################################

== シーケンス本文 ==

'### 要求 -> 応答
Foo1 -> Foo2 : Request
Foo1 <- Foo2 : Ack(OK)

@enduml
```
  





## 自動番号振り

* 自動番号振り
* 自動番号振り・開始番号指定
* 自動番号振り・桁指定
* 自動番号振り・ヘッダ文字+フォント書式
* 自動番号の参照
  

```text
@startuml practice5

'################################
' 類分子
'################################
participant "Participant 1" as Foo1
participant "Participant 2" as Foo2


'################################
' シーケンス本文
'################################

== 自動番号振り(1) ==
autonumber
Foo1 -> Foo2 : Request
Foo1 <- Foo2 : Ack(OK)


== 自動番号振り(2) ==
autonumber 1.1
Foo1 -> Foo2 : Request
Foo1 <- Foo2 : Ack(OK)


== 自動番号振り(桁書式付き) ==
autonumber "000"
Foo1 -> Foo2 : Request
Foo1 <- Foo2 : Ack(OK)


== 自動番号振り(ヘッダ文字+フォント書式) ==
autonumber "<b>number [000]"
Foo1 -> Foo2 : Request
Foo1 <- Foo2 : Ack(OK)


== 自動番号振り(自動番号の参照) ==
autonumber "[000]"
Foo1 -> Foo2 : Request "%autonumber%"
Foo1 <- Foo2 : Ack(OK) "%autonumber%"

@enduml
```





## 条件分岐

* 単一if分岐（opt）
* 複数if分岐（alt）
* 他シーケンス参照
* 処理終了（return）
* 繰り返し（loop）
* loop中のbreak
* 例外（critical）
* 遅延（タイマ）
* 並列処理
* オブジェクト生成
* イン・アウト（call文）
  

```text
@startuml practice6

'################################
' 類分子
'################################
participant "Participant 1" as Foo1
participant "Participant 2" as Foo2
participant "Participant 3" as Foo3


'################################
' シーケンス本文
'################################

== opt（単一if分岐） ==
opt Branch case 1
    ''' 分岐1
    Foo1 -> Foo2 : Request 1
end


== alt / else（複数if分岐） / ref参照 / return ==
alt Branch case 2-1
    Foo1 -> Foo2 : Request 2-1

else Branch case 2-2
    Foo1 -> Foo2 : Request 2-2

' Groupラベル（用途がよくわからん）
' else Branch case 2-3 + Label
'     ''' Groupラベル
'     group Label 2-3
'         Foo1 -> Foo2 : Request 2-3
'     end

else Branch case 2-4
    return return (処理終わり)

else
    ''' 分岐2-5
    Foo1 -> Foo2 : Request 2-5

    ''' 他シーケンス参照
    ref over Foo1 : <font color=#0000ff><b>Sequence 111\n<font color=#0000ff><b>(他シーケンス参照)

end


== loop（while / forループ / 条件break） / critical（例外処理） ==
loop Counter num 100
    Foo1 -> Foo2 : Request 3-1

    break Counter num > 80
        Foo1 -> Foo2 : Request 3-2（break時に実行）
        note right
            breakで実行される処理
            空欄でもいける
        end note
    end

    critical
        note over Foo2 #ff0000
            <font color=#ffffff>critical時に実行される処理
        end note
        Foo1 <[#ff0000]- Foo2 : <font color=#ff0000>Critical Message 4-4
    end

end


== 遅延処理（タイマ）==

Foo1 -> Foo2 : Request 4-1
Foo1 <- Foo2 : Ack(OK) 4-1
... about 10 second ...
Foo1 -> Foo2 : Request 4-2
Foo1 <- Foo2 : Ack(OK) 4-2

' Plank ULMだと上手く動かない？
'... about 10 second ...
' {start} Foo1 -> Foo2 : Request 4-3
' Foo2 -> Foo3 : Indication 4-3
' {end} Foo1 <- Foo2 : Ack(OK) 4-3
' {start} <-> {end} : some time


== par（並列処理）==
par
    note over Foo1, Foo2
        Request 5-1, 5-2, 5-3は
        並列で実行される
    end note

    Foo1 -> Foo2 : Request 5-1
    Foo1 -> Foo2 : Request 5-2
    Foo1 -> Foo2 : Request 5-3

end



== オブジェクト生成 ==
create Control String
Foo1 -> String
return bye



== イン・アウト（callとか？） ==
[-> Foo2 : Remote Server Request 1

Foo1 <-] : Local Server Request 2

@enduml
```
  






## テキストボックス

* テキスト（左）
* テキスト相対位置指定
* テキスト（右）+テキストカラー
* 六角形のテキスト
* 全てのラインに跨るテキスト
* 別ラインのテキストを同一位置に並べる
* ラインを跨るテキスト（ライン指定）

```text
@startuml practice7

'################################
' 類分子
'################################
participant "Participant 1" as Foo1
participant "Participant 2" as Foo2
participant "Participant 2" as Foo3


'################################
' シーケンス本文
'################################

alt Branch case 7-1
    Foo1 -> Foo2 : Request 7-1

else Branch case 7-2
    Foo1 -> Foo2 : Request 7-2
    note left
            テキスト(左)
            改行もいける
    end note

    note right of Foo3
        相対位置指定
    end note

else Branch case 7-3
    Foo1 -> Foo2 : Request 7-3
    note right #ffffff
            <font color=#ff0000><b>テキスト(右)
    end note

else Branch case 7-4

    hnote over Foo1
        六角形のテキスト
    end note

    note across
        全てのラインに跨る
    end note

    ''' Foo1とFoo2を同一レベルに並べる
    note over Foo1
        Foo1 Note
        Foo1, Foo2を並べる
    end note

    / note over Foo2
        Foo2 Note
    end note


else
    note over Foo1, Foo2 #ff0000
            <font color=#ffffff><b>跨るテキスト
    end note

    Foo1 -> Foo2 : Request 7-X

end

@enduml
```





## クラス図

* 可視状態
* オブジェクト宣言
* オブジェクトの関係性
  

```text
@startuml practice8

'################################
' Hide members
'################################
' hide members

'################################
' Hiding independent classes
'################################
' remove @unlinked


'################################
' 可視状態
'################################
' + : public
' - : private
' # : protected
' ~ : package private

'################################
' Objects
'################################

class ClassA

class ClassB {
''' コンストラクタ
    ClassB();
''' デストラクタ
    ~ClassB();
''' クラス関数
    +BOOL classFunc1(char aaa);
    -BOOL classFunc2(char bbb);
''' クラス変数
    +CHAR classChar3;
    -INT classInt4;
    -BOOL flag5;
}

class ClassC {
    ClassC();
    ~ClassC();
    +BOOL classFunc13(int ccc);
    -BOOL classFunc14(int ddd);
    +CHAR classChar15;
}


'################################
' 関係性
'################################
' <|-- : Extension      継承（馴染みのある継承）
' <|.. : Realization    実装（馴染みのある実装）
' o--  : Aggregation    集約（子が親から独立して存在できる関係）
'                       =人は家がなくても存在できる
' *--  : Composition    構成（子が親から独立して存在できない関係を表す。一般に強い集約と表現される。）
'                       =頭は人がいないと存在できない

ClassA <|-- ClassB
ClassA *-- ClassC
ClassA o-- ClassD


'### <|-- : Extension
' abstract class AbstractClassA {
' }
' class ClassA {
' }
' AbstractClassA <|-- ClassA

'### <|.. : Realization
' Interface InterfaceA {
' }
' class ClassA {
' }
' InterfaceA <|.. ClassA

'### o--  : Aggregation
' Class House {
' }
' class Persion {
' }
' House o-- Persion

'### *--  : Composition
' Class Persion {
' }
' class Head {
' }
' Persion *-- Head

@enduml
```
  





## 参考 / Material

【※敬称略 / Titles omitted】  

* [Plant UML シーケンス図](https://plantuml.com/ja/sequence-diagram)  
  

* [UML org(公式)](https://www.uml.org/)  
  





***
***
[[トップへ戻る]](../readme.md)  
  
::Admin= Korei (@korei-xlix)  
::github= [https://github.com/korei-xlix/](https://github.com/korei-xlix/)  
::Web= [https://website.koreis-labo.com/](https://website.koreis-labo.com/)  
::X= [https://x.com/korei_xlix](https://x.com/korei_xlix)  
***
