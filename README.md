# Toy Shell

SSH 接続できない環境でコマンド操作や作業を行うのに便利な PHP 製の Web Shell  
共有サーバー等でシェルが実行できない環境用に作成

## 機能

- Phar を使用した単一ファイルの設置で動作可能な Web Shell  
  ビルド済みの Phar ファイルを公開ディレクトリ内に設置するだけですぐに Web Shell が使用可能。
- ファイルのダウンロード機能  
  `ll`コマンドを使用してファイルのダウンロードリンクを表示します。
- 簡易的なコマンド入力補正機能
- 簡易的なパスワード認証機能
- IP アドレスを使用したホワイトリスト方式のアクセス制御機能  
  リスト以外のアクセスに対しては HTTP ステータスコードの 404 をレスポンスします。
- シンタックスハイライト機能  
  [highlight.js](https://github.com/highlightjs/highlight.js)を使用して自動判定でカラフルな出力結果を得られます。

## スクリーンショット

## 使い方

### 設置方法

1. ビルドされた単一ファイルを設置して使用する場合  
   build/ToyShell.phar.php をサーバー上の公開ディレクトリ内に設置してアクセス。

1. 複数のファイルを設置して使用する場合  
   src/ 移行を公開ディレクトリ内に設置して shell.php にアクセス。

### 予約コマンド

当プログラムが個別に認識するコマンドについて

- `clear`  
  セッション変数のクリアを行います。  
  実際のシェルでは`clear`コマンドのプロセスは発行されていません。
- `cd`  
  当プログラムの都合上、カレントディレクトリの記録をセッション変数内に格納するため、  
  `cd`コマンドで指定されたパスをリアルパスに変換したうえで記録します。  
  実際のシェルでは`cd`コマンドのプロセスは発行されていません。
- `ll`  
  `ls -la`のエイリアスとして機能します。  
  ファイル名にリンクが付与されダウンロードすることが可能になります。

### 設定

src/config/config.inc.php の設定項目について

- `simple_auth`
  - `valid` 簡易認証機能の ON/OFF
  - `user` ユーザ名
  - `password` パスワード
- `IP_restriction`
  - `valid` アクセス制限機能の ON/OFF
  - `IPs` 許可されている IP アドレスのリストを配列で格納
- `command_list`
  - 入力補完に使用 `'コマンド詳細' => '値にコマンド'`

### ビルド

単一ファイルの実行には Phar を使用しています。

Phar については以下の URL を参照  
**PHP: Phar - Manual**  
[https://www.php.net/manual/ja/book.phar.php](https://www.php.net/manual/ja/book.phar.php)

Phar ビルド環境の整備については以下を参照  
**Box Project**  
[https://box-project.github.io/box2/](https://box-project.github.io/box2/)

box.json があるディレクトリで以下のコマンドを実行

```shell
$ box build
```

## TODO

- ファイルのアップロード機能
- 標準エラー出力（stderr）の表示

## 更新

- 2020/05/05 1.0.4
  - シンタックスハイライト機能を追加
  - クラスの構造を変更
  - ファイルダウンロードURLをパーセントエンコードするように修正
- 2020/05/04 1.0.3
  - `ll`コマンドでファイル名にリンクの表示、ファイルのダウンロード機能を追加
  - コマンドの入力補完機能を追加
  - HTML や CSS を修正
- 2020/05/01 1.0.2
  - `cd`コマンドの動作を修正
- 2020/04/28 1.0.1
  - IP アドレスによるアクセス制御機能を追加
  - アクセス制御の有効化、無効化機能を追加
- 2020/04/ 1.0.0
  - 公開
