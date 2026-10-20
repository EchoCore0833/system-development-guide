## 10. 開発環境の最終動作確認

これまでに構築したXAMPP・PHP・Composer・CakePHP・MariaDB・VS Codeが正常に動作しているかを確認する。

### 10-1. XAMPPの動作確認

#### 手順1：XAMPP Control Panelを開く

以下のファイルを実行する。

```text
C:\xampp\xampp-control.exe
```

#### 手順2：ApacheとMySQLを起動する

ApacheとMySQLの「Start」をクリックする。

両方の行が緑色になり、「Start」が「Stop」に変われば起動成功となる。

#### 手順3：ブラウザで確認する

以下のURLにアクセスする。

| 確認対象 | URL |
|---|---|
| XAMPP | `http://localhost/` |
| phpMyAdmin | `http://localhost/phpmyadmin/` |

それぞれの画面が表示されれば成功となる。

### 10-2. PHPとComposerの動作確認

#### 手順1：PHPのバージョンを確認する

VS Codeのターミナルを開き、以下を実行する。

```powershell
php -v
```

PHPのバージョン情報が表示されれば成功となる。

#### 手順2：PHPの実行場所を確認する

以下のコマンドを実行する。

```powershell
where.exe php
```

実行結果に以下のパスが表示されることを確認する。

```text
C:\xampp\php\php.exe
```

表示されない場合は、環境変数PathとVS Codeの再起動を確認する。

#### 手順3：Composerのバージョンを確認する

以下のコマンドを実行する。

```powershell
composer --version
```

Composerのバージョン情報が表示されれば成功となる。

#### 手順4：PHP拡張機能を確認する

以下のコマンドを実行する。

```powershell
php -m
```

表示される一覧から、以下の拡張機能を確認する。

| 拡張機能 | 主な役割 |
|---|---|
| `mbstring` | 日本語などの文字列処理 |
| `intl` | 日付・数値などの国際化処理 |
| `openssl` | 暗号化通信 |
| `pdo_mysql` | MySQL・MariaDBへの接続 |
| `zip` | ComposerでのZIPファイル展開 |

必要な拡張機能が読み込まれていない場合は、`C:\xampp\php\php.ini` の設定を確認する。

### 10-3. CakePHPの動作確認

#### 手順1：プロジェクトフォルダーへ移動する

VS Codeのターミナルで以下を実行する。

```powershell
cd C:\xampp\htdocs\cakephp-app
```

#### 手順2：CakePHPのコマンドを確認する

以下を実行する。

```powershell
php bin\cake.php --help
```

CakePHPで使用できるコマンドの一覧やヘルプが表示されれば成功となる。

続いて、本体のバージョンと実行環境の要件を確認する。

```cmd
composer show cakephp/cakephp
composer check-platform-reqs
```

`versions` に `5.4.3` が表示され、PHPと拡張機能の要件チェックが成功することを確認する。

#### 手順3：開発サーバーを起動する

以下を実行する。

```powershell
php bin\cake.php server
```

※ すでに別のターミナルで開発サーバーが起動している場合は、先に停止する。

#### 手順4：ブラウザで確認する

以下のURLにアクセスする。

`http://localhost:8765/`

CakePHPの初期画面が表示されれば成功となる。

### 10-4. データベース接続の確認

#### 手順1：CakePHPの初期画面を確認する

CakePHPの初期画面にある「Database」の項目を確認する。

次のメッセージが表示されていれば、データベースへの接続に成功している。

```text
CakePHP is able to connect to the database.
```

#### 手順2：DebugKitの接続状態を確認する

「DebugKit」の項目に、以下のメッセージが表示されていることを確認する。

```text
DebugKit can connect to the database.
```

※ データベース接続に失敗した場合は、XAMPPのMySQLが起動しているか、`config/app_local.php` の接続情報が正しいかを確認する。

### 10-5. 最終確認と開発サーバーの停止

#### 手順1：プロジェクトフォルダーを確認する

VS Codeのエクスプローラーで、以下のフォルダーが存在することを確認する。

- `src/`
- `templates/`
- `config/`
- `webroot/`
- `vendor/`

#### 手順2：開発サーバーを停止する

開発サーバーを起動しているターミナルで `Ctrl + C` を押す。

コマンド入力待ちの状態に戻れば停止完了となる。
