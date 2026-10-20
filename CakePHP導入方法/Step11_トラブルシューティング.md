## 11. トラブルシューティング

CakePHPの開発環境構築中によく発生するエラーと、その原因・対処方法をまとめる。

### 11-1. Apacheが起動しない

#### 症状

XAMPP Control PanelでApacheの「Start」をクリックしても起動しない、または起動後すぐに停止する。

#### 主な原因

Apacheが使用するポート番号（通常は80番・443番）が、ほかのアプリケーションによって使用されている可能性がある。

#### 対処方法

**手順1：XAMPPのログを確認する**

XAMPP Control PanelでApacheの「Logs」をクリックし、エラー内容を確認する。

**手順2：ポートの使用状況を確認する**

コマンドプロンプトで以下を実行する。

```cmd
netstat -ano | findstr :80
```

必要に応じて443番ポートも確認する。

```cmd
netstat -ano | findstr :443
```

**手順3：使用中のプロセスを確認する**

表示されたPIDを使用して、プロセスを調べる。

```cmd
tasklist /FI "PID eq 1234"
```

※ `1234` は実際に表示されたPIDに置き換える。

競合しているアプリケーションを確認し、必要に応じて設定を変更する。

※ 用途が分からないプロセスを強制終了しないこと。

### 11-2. MySQL（MariaDB）が起動しない

#### 症状

XAMPP Control PanelでMySQLの「Start」をクリックしても起動しない。

#### 主な原因

- 3306番ポートが別のMySQLなどに使用されている。
- MariaDBの設定ファイルに問題がある。
- データファイルに問題が発生している。

#### 対処方法

**手順1：MySQLのログを確認する**

XAMPP Control PanelからMySQLのログを開き、エラー内容を確認する。

**手順2：ポートの使用状況を確認する**

```cmd
netstat -ano | findstr :3306
```

別のプロセスが3306番ポートを使用している場合は、そのアプリケーションを確認する。

**注意：** 原因が分からない状態で `C:\xampp\mysql\data` を削除しないこと。データベース内の情報が失われる可能性がある。

### 11-3. PHPコマンドが認識されない

#### 症状

PowerShellやコマンドプロンプトで以下を実行する。

```powershell
php -v
```

次のようなエラーが表示される。

```text
php : 用語 'php' は、コマンドレット、関数、
スクリプト ファイル、または操作可能なプログラムの
名前として認識されません。
```

#### 原因

PHPの実行ファイルが存在していても、環境変数Pathが正しく設定されていない、または変更がターミナルに反映されていない可能性がある。

#### 対処方法

**手順1：PHPを直接実行する**

```powershell
& "C:\xampp\php\php.exe" -v
```

バージョン情報が表示されれば、PHP自体は動作している。

**手順2：環境変数Pathを確認する**

Windowsの「環境変数」から、ユーザー環境変数の `Path` を確認する。

次のパスが存在するか確認する。

```text
C:\xampp\php
```

存在しない場合は追加する。

**手順3：VS Codeを再起動する**

Pathを追加・変更した場合は、VS Codeをすべて終了してから再起動する。

**手順4：再確認する**

```powershell
php -v
where.exe php
```

正常にバージョンと実行ファイルのパスが表示されれば解決となる。

### 11-4. ComposerでZIP拡張機能のエラーが発生する

#### 症状

CakePHPのインストール時に、次のエラーが表示される。

```text
The zip extension and unzip/7z commands
are both missing, skipping.
```

#### 原因

ComposerがZIPファイルを展開するためのPHP拡張機能や外部コマンドを使用できない状態になっている。

#### 対処方法

**手順1：php.iniを開く**

以下のファイルを開く。

```text
C:\xampp\php\php.ini
```

**手順2：ZIP拡張機能を有効にする**

以下を検索する。

```ini
;extension=zip
```

先頭の `;` を削除する。

```ini
extension=zip
```

**手順3：設定を保存する**

`Ctrl + S` で保存する。

**手順4：有効になったか確認する**

新しいターミナルで以下を実行する。

```powershell
php -m
```

一覧に `zip` が表示されれば成功となる。

**手順5：インストールを再実行する**

```cmd
cd /d C:\xampp\htdocs
composer create-project --prefer-dist cakephp/app:"5.4.0" cakephp-app
```

作成が成功したら、ステップ6の「手順7：CakePHP本体を5.4.3に固定する」を実行する。

※ 失敗時に作成された `cakephp-app` フォルダーが残っている場合は、内容を確認する。削除する場合は、今回の失敗で作成された不要なフォルダーであることを確認する。

### 11-5. CakePHPの初期画面が表示されない

#### 症状

ブラウザで以下のURLにアクセスしても、CakePHPの初期画面が表示されない。

`http://localhost:8765/`

#### 主な原因

- 開発サーバーが起動していない。
- 開発サーバーがエラーで停止している。
- 別のアプリケーションが8765番ポートを使用している。

#### 対処方法

**手順1：プロジェクトフォルダーへ移動する**

```powershell
cd C:\xampp\htdocs\cakephp-app
```

**手順2：開発サーバーを起動する**

```powershell
php bin\cake.php server
```

**手順3：ブラウザで再確認する**

以下のURLにアクセスする。

`http://localhost:8765/`

起動時にエラーが表示された場合は、そのメッセージを確認する。

### 11-6. データベースに接続できない

#### 症状

CakePHPの初期画面に、データベース接続が失敗したことを示すメッセージが表示される。

#### 主な原因

- MySQL（MariaDB）が起動していない。
- データベースが作成されていない。
- ユーザー名やパスワードが間違っている。
- 接続先やポート番号が間違っている。

#### 対処方法

**手順1：XAMPPでMySQLを起動する**

XAMPP Control Panelを開き、MySQLが起動していることを確認する。

**手順2：データベースの存在を確認する**

phpMyAdminで `cakephp_db` が存在することを確認する。

**手順3：接続設定を確認する**

以下のファイルを開く。

```text
C:\xampp\htdocs\cakephp-app\config\app_local.php
```

`Datasources` → `default` の設定を確認する。

```php
'host' => 'localhost',
'port' => 3306,
'username' => 'root',
'password' => '',
'database' => 'cakephp_db',
```

※ パスワードが空欄なのは、XAMPPのrootユーザーにパスワードを設定していない場合の例。

**手順4：CakePHPの初期画面で再確認する**

以下のURLにアクセスする。

`http://localhost:8765/`

「Database」に次のメッセージが表示されれば成功となる。

```text
CakePHP is able to connect to the database.
```
