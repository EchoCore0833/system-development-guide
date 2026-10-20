## 12. 付録・参考情報

CakePHPの開発環境構築後も参照できるように、公式サイト、コマンド、主要フォルダー、URL、注意事項をまとめる。

### 12-1. 公式サイト・参考資料

環境構築中に不明な点が発生した場合は、各ソフトウェアの公式サイトやドキュメントを確認する。

| ソフトウェア | 公式サイト・資料 |
|---|---|
| CakePHP | https://cakephp.org/ |
| CakePHP 5.x | https://book.cakephp.org/5/ja/ |
| PHP | https://www.php.net/ |
| PHPマニュアル | https://www.php.net/manual/ja/ |
| XAMPP | https://www.apachefriends.org/jp/index.html |
| Composer | https://getcomposer.org/ |
| VS Code | https://code.visualstudio.com/ |
| MariaDB | https://mariadb.org/ |

※ CakePHPはバージョンによって仕様が異なる場合があるため、使用しているバージョンに対応したドキュメントを確認する。

### 12-2. よく使用するコマンド一覧

#### PHP・Composer

| コマンド | 用途 |
|---|---|
| `php -v` | PHPのバージョン確認 |
| `php -m` | PHP拡張機能の確認 |
| `where.exe php` | PHP実行ファイルの場所を確認（PowerShell） |
| `composer --version` | Composerのバージョン確認 |
| `composer diagnose` | Composerの設定診断 |
| `composer install` | 依存パッケージのインストール |
| `composer update` | 依存パッケージの更新 |

※ `composer update` は依存パッケージのバージョンが変更される場合があるため、必要性を確認して実行する。

#### CakePHP

CakePHPのコマンドは、プロジェクトフォルダーで実行する。

```powershell
cd C:\xampp\htdocs\cakephp-app
```

| コマンド | 用途 |
|---|---|
| `php bin\cake.php --help` | CakePHPのコマンド一覧を確認 |
| `php bin\cake.php server` | 開発サーバーの起動 |
| `php bin\cake.php routes` | ルーティングの確認 |
| `php bin\cake.php cache clear_all` | キャッシュの削除 |
| `php bin\cake.php migrations status` | マイグレーションの状態確認（プラグイン導入時） |

開発サーバーを停止する場合は `Ctrl + C` を押す。

### 12-3. CakePHPの主要フォルダーとファイル

CakePHPのプロジェクトには、用途ごとに複数のフォルダーが用意されている。

| フォルダー | 用途 |
|---|---|
| `bin/` | CakePHPのコマンド |
| `config/` | アプリケーションの設定 |
| `logs/` | ログファイル |
| `src/` | アプリケーションの処理 |
| `templates/` | 画面表示用テンプレート |
| `tests/` | テストコード |
| `tmp/` | 一時ファイル |
| `vendor/` | Composer管理のライブラリ |
| `webroot/` | 公開用の静的ファイル |

特に重要なファイルは以下のとおり。

| ファイル | 用途 |
|---|---|
| `config/app.php` | 共通設定 |
| `config/app_local.php` | 開発環境ごとの設定 |
| `config/routes.php` | URLと処理の対応付け |
| `composer.json` | PHPの依存パッケージなどの定義 |
| `templates/Pages/home.php` | 初期画面のテンプレート |
| `webroot/index.php` | Webリクエストの入口 |

※ `vendor/` 内のファイルは、基本的に直接編集しない。

### 12-4. ローカル環境のURL一覧

今回のマニュアルで使用したURLをまとめる。

| 用途 | URL |
|---|---|
| XAMPP | `http://localhost/` |
| phpMyAdmin | `http://localhost/phpmyadmin/` |
| CakePHP | `http://localhost:8765/` |

`localhost` は、現在操作している自分のパソコンを指す。

CakePHPの `8765` は開発サーバーが使用するポート番号で、標準設定ではこの番号が使用される。

### 12-5. 開発環境を使用する際の注意点

#### データベースのパスワード

XAMPPの初期状態では、MariaDBの `root` ユーザーにパスワードが設定されていない場合がある。

この設定は学習用のローカル環境に限定し、外部に公開する環境では適切なユーザーとパスワードを設定する。

#### 設定ファイルの管理

`config/app_local.php` にはデータベースの接続情報などが含まれる。

GitHubなどに登録する場合は、パスワードなどの機密情報を公開しないように注意する。

#### 開発サーバーの利用

`php bin\cake.php server` で起動する開発サーバーは、開発・動作確認用のものである。

本番環境での公開には、適切に設定されたWebサーバーを使用する。

#### バージョンの違い

PHP・Composer・CakePHPなどは継続的に更新される。

本マニュアルと異なるバージョンを使用する場合、画面や操作方法、必要な設定が異なる可能性がある。