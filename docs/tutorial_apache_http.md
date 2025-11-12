# Apache HTTP Server チュートリアル

このドキュメントでは、Ubuntu 上に Apache HTTP Server をインストールし、80番ポートで Web サーバーを公開する方法について説明します。

## Apache HTTP Server とは

Apache HTTP Server（通常「Apache」と呼ばれる）は、世界で最も広く使用されているオープンソースの Web サーバーソフトウェアです。静的コンテンツの配信から動的な Web アプリケーションのホスティングまで、幅広い用途で使用されています。

---

## 前提条件

- Ubuntu Server または Ubuntu Desktop がインストールされていること
- sudo 権限を持つユーザーアカウント
- インターネット接続

---

## Apache のインストール

### 1. パッケージリストの更新

まず、システムのパッケージリストを最新の状態に更新します。

```bash
$ sudo apt update
```

### 2. Apache のインストール

Apache をインストールします。Ubuntu では Apache のパッケージ名は `apache2` です。

```bash
$ sudo apt install apache2 -y
```

**注意:** CentOS/RHEL では `httpd` という名前ですが、Ubuntu では `apache2` という名前になります。

### 3. インストールの確認

Apache が正常にインストールされたことを確認します。

```bash
# Apache のバージョンを確認
$ apache2 -v

# 出力例:
# Server version: Apache/2.4.52 (Ubuntu)
```

---

## Apache の起動と管理

Ubuntu では systemd を使用して Apache を管理します。

### Apache の起動

```bash
$ sudo systemctl start apache2
```

### Apache の停止

```bash
$ sudo systemctl stop apache2
```

### Apache の再起動

```bash
$ sudo systemctl restart apache2
```

### Apache の設定リロード

設定ファイルを変更した後、サービスを停止せずに設定を再読み込みできます。

```bash
$ sudo systemctl reload apache2
```

### Apache のステータス確認

```bash
$ sudo systemctl status apache2
```

**出力例:**

```
● apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2024-01-01 10:00:00 UTC; 5min ago
       Docs: https://httpd.apache.org/docs/2.4/
   Main PID: 1234 (apache2)
      Tasks: 55 (limit: 4915)
     Memory: 5.2M
     CGroup: /system.slice/apache2.service
             ├─1234 /usr/sbin/apache2 -k start
             ├─1235 /usr/sbin/apache2 -k start
             └─1236 /usr/sbin/apache2 -k start
```

### システム起動時に自動起動を有効化

```bash
$ sudo systemctl enable apache2
```

### 自動起動を無効化

```bash
$ sudo systemctl disable apache2
```

---

## Apache の動作確認

### 1. ローカルでの確認

curl コマンドを使用して、ローカルから Apache が応答するか確認します。

```bash
$ curl http://localhost
```

または、ブラウザで以下の URL にアクセスします：

- `http://localhost`
- `http://127.0.0.1`
- `http://サーバーのIPアドレス`

### 2. Apache のデフォルトページ

正常に動作している場合、「Apache2 Ubuntu Default Page」が表示されます。

### 3. リスニングポートの確認

Apache が 80番ポートでリスニングしていることを確認します。

```bash
$ sudo ss -tuln | grep :80
```

**出力例:**

```
tcp   LISTEN 0      511          0.0.0.0:80        0.0.0.0:*
tcp   LISTEN 0      511             [::]:80           [::]:*
```

または netstat を使用：

```bash
$ sudo netstat -tuln | grep :80
```

---

## ファイアウォールの設定

Ubuntu で UFW（Uncomplicated Firewall）を使用している場合、80番ポートを開放する必要があります。

### UFW の状態確認

```bash
$ sudo ufw status
```

### Apache トラフィックを許可

Apache 用のプリセットプロファイルが用意されています。

```bash
# HTTP (80番ポート) のみ許可
$ sudo ufw allow 'Apache'

# または、HTTP と HTTPS (80番と443番ポート) を許可
$ sudo ufw allow 'Apache Full'

# HTTPS (443番ポート) のみ許可
$ sudo ufw allow 'Apache Secure'
```

### 利用可能なプロファイルの確認

```bash
$ sudo ufw app list | grep Apache
```

**出力例:**

```
  Apache
  Apache Full
  Apache Secure
```

### ポート番号を直接指定する方法

```bash
# 80番ポートを開放
$ sudo ufw allow 80/tcp

# 443番ポートも開放（HTTPS用）
$ sudo ufw allow 443/tcp
```

---

## Apache の重要なファイルとディレクトリ

### 設定ファイル

| パス | 説明 |
|------|------|
| `/etc/apache2/` | Apache の設定ディレクトリ |
| `/etc/apache2/apache2.conf` | メイン設定ファイル |
| `/etc/apache2/ports.conf` | リスニングポートの設定 |
| `/etc/apache2/sites-available/` | 利用可能なサイト設定 |
| `/etc/apache2/sites-enabled/` | 有効化されたサイト設定 |
| `/etc/apache2/mods-available/` | 利用可能なモジュール |
| `/etc/apache2/mods-enabled/` | 有効化されたモジュール |
| `/etc/apache2/conf-available/` | 追加の設定ファイル |
| `/etc/apache2/conf-enabled/` | 有効化された追加設定 |

### ドキュメントルート

| パス | 説明 |
|------|------|
| `/var/www/html/` | デフォルトのドキュメントルート |
| `/var/www/html/index.html` | デフォルトのトップページ |

### ログファイル

| パス | 説明 |
|------|------|
| `/var/log/apache2/` | Apache のログディレクトリ |
| `/var/log/apache2/access.log` | アクセスログ |
| `/var/log/apache2/error.log` | エラーログ |

---

## 簡単な Web ページの作成

### 1. デフォルトページの編集

```bash
# バックアップを作成
$ sudo cp /var/www/html/index.html /var/www/html/index.html.bak

# vim で編集
$ sudo vim /var/www/html/index.html
```

**vim の基本操作:**

- `i` - 挿入モードに入る
- `Esc` - ノーマルモードに戻る
- `:w` - 保存
- `:q` - 終了
- `:wq` - 保存して終了
- `:q!` - 保存せずに終了

**例: シンプルな HTML ページ**

```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>私の Web サイト</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 50px auto;
            padding: 20px;
            text-align: center;
        }
        h1 {
            color: #333;
        }
        p {
            color: #666;
            line-height: 1.6;
        }
    </style>
</head>
<body>
    <h1>Apache HTTP Server へようこそ！</h1>
    <p>このページは Ubuntu 上で動作する Apache HTTP Server で公開されています。</p>
    <p>現在の時刻: <span id="time"></span></p>
    <script>
        document.getElementById('time').textContent = new Date().toLocaleString('ja-JP');
    </script>
</body>
</html>
```

### 2. ファイルの権限確認

```bash
$ ls -l /var/www/html/index.html
```

通常は以下のような権限になっています：

```
-rw-r--r-- 1 root root 1234 Jan 01 10:00 /var/www/html/index.html
```

### 3. ブラウザで確認

ブラウザで `http://localhost` または `http://tailscaleのIPアドレス` にアクセスして、新しいページが表示されることを確認します。

---

## ポート設定の変更

### デフォルトポート（80番）の確認

```bash
$ cat /etc/apache2/ports.conf
```

**デフォルトの内容:**

```apache
Listen 80

<IfModule ssl_module>
    Listen 443
</IfModule>

<IfModule mod_gnutls.c>
    Listen 443
</IfModule>
```

### ポート番号を変更する場合

例えば、8080番ポートで公開したい場合：

```bash
$ sudo vim /etc/apache2/ports.conf
```

以下のように変更：

```apache
Listen 8080
```

サイト設定ファイルも変更：

```bash
$ sudo vim /etc/apache2/sites-available/000-default.conf
```

```apache
<VirtualHost *:8080>
    # ... 他の設定 ...
</VirtualHost>
```

設定を反映：

```bash
$ sudo systemctl reload apache2
```

**注意:** ポートを変更した場合、ファイアウォールの設定も変更する必要があります。

```bash
$ sudo ufw allow 8080/tcp
```

---

## 仮想ホストの設定

複数のドメインやサブドメインをホストする場合、仮想ホストを使用します。

### 1. ディレクトリ構造の作成

例: `example.com` というドメインの設定

```bash
# ドキュメントルートを作成
$ sudo mkdir -p /var/www/example.com/html

# 所有者を変更（www-data は Apache のデフォルトユーザー）
$ sudo chown -R $USER:$USER /var/www/example.com/html

# 権限を設定
$ sudo chmod -R 755 /var/www/example.com
```

### 2. サンプル HTML ファイルの作成

```bash
$ vim /var/www/example.com/html/index.html
```

```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <title>Example.com</title>
</head>
<body>
    <h1>Example.com へようこそ！</h1>
    <p>これは仮想ホストのテストページです。</p>
</body>
</html>
```

### 3. 仮想ホスト設定ファイルの作成

```bash
$ sudo vim /etc/apache2/sites-available/example.com.conf
```

```apache
<VirtualHost *:80>
    ServerAdmin webmaster@example.com
    ServerName example.com
    ServerAlias www.example.com
    DocumentRoot /var/www/example.com/html

    ErrorLog ${APACHE_LOG_DIR}/example.com-error.log
    CustomLog ${APACHE_LOG_DIR}/example.com-access.log combined

    <Directory /var/www/example.com/html>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

### 4. 仮想ホストを有効化

```bash
# サイトを有効化
$ sudo a2ensite example.com.conf

# Apache の設定をテスト
$ sudo apache2ctl configtest

# 出力が "Syntax OK" であることを確認

# Apache をリロード
$ sudo systemctl reload apache2
```

### 5. デフォルトサイトを無効化（オプション）

```bash
$ sudo a2dissite 000-default.conf
$ sudo systemctl reload apache2
```

### 6. ローカルでのテスト

実際のドメインを持っていない場合、`/etc/hosts` ファイルを編集してテストできます。

```bash
$ sudo vim /etc/hosts
```

以下の行を追加：

```
127.0.0.1 example.com www.example.com
```

ブラウザで `http://example.com` にアクセスして確認します。


**例2: URL のリダイレクト**

```apache
# HTTP から HTTPS へリダイレクト
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

**例3: Basic 認証**

```apache
AuthType Basic
AuthName "Restricted Area"
AuthUserFile /etc/apache2/.htpasswd
Require valid-user
```

---

## ログの確認

### アクセスログの確認

```bash
# リアルタイムでログを監視
$ sudo tail -f /var/log/apache2/access.log

# 最新の50行を表示
$ sudo tail -n 50 /var/log/apache2/access.log

# 特定のIPアドレスのアクセスを検索
$ sudo grep "192.168.1.100" /var/log/apache2/access.log
```

### エラーログの確認

```bash
# リアルタイムでログを監視
$ sudo tail -f /var/log/apache2/error.log

# 最新のエラーを表示
$ sudo tail -n 20 /var/log/apache2/error.log
```

### vim でログファイルを開く

```bash
# アクセスログを vim で開く
$ sudo vim /var/log/apache2/access.log

# エラーログを vim で開く
$ sudo vim /var/log/apache2/error.log
```

**vim でのログ確認に便利なコマンド:**

- `G` - ファイルの最後に移動
- `gg` - ファイルの先頭に移動
- `/検索語` - 前方検索
- `?検索語` - 後方検索
- `n` - 次の検索結果へ
- `N` - 前の検索結果へ

### ログのローテーション

Ubuntu では `logrotate` が自動的にログをローテーションします。設定は以下にあります：

```bash
$ cat /etc/logrotate.d/apache2
```

---

## トラブルシューティング

### Apache が起動しない場合

**1. 設定ファイルの文法チェック**

```bash
$ sudo apache2ctl configtest
```

**2. 詳細なエラーメッセージを確認**

```bash
$ sudo systemctl status apache2
$ sudo journalctl -xe
$ sudo tail -n 50 /var/log/apache2/error.log
```

**3. ポートの競合を確認**

```bash
# 80番ポートを使用しているプロセスを確認
$ sudo ss -tuln | grep :80
$ sudo lsof -i :80
```

他のプロセスが 80番ポートを使用している場合は、そのプロセスを停止するか、Apache のポートを変更します。

### ページが表示されない場合

**1. Apache が動作しているか確認**

```bash
$ sudo systemctl status apache2
```

**2. ファイアウォールを確認**

```bash
$ sudo ufw status
```

**3. SELinux を確認（Ubuntu ではデフォルトで無効）**

```bash
$ getenforce
```

**4. ファイルの権限を確認**

```bash
$ ls -l /var/www/html/
```

### 403 Forbidden エラー

**原因:**
- ファイルやディレクトリの権限が不適切
- Apache の設定で `Require all denied` になっている
- ディレクトリインデックスが無効で index.html がない

**対処法:**

```bash
# 権限を確認
$ ls -l /var/www/html/

# 権限を修正
$ sudo chmod 755 /var/www/html/
$ sudo chmod 644 /var/www/html/index.html

# 設定を確認
$ sudo vim /etc/apache2/sites-available/000-default.conf
```

### 設定を変更しても反映されない

```bash
# 設定のリロード
$ sudo systemctl reload apache2

# それでもダメな場合は再起動
$ sudo systemctl restart apache2

# ブラウザのキャッシュをクリア
# または、シークレットモードで確認
```

---

## よく使うコマンドまとめ

```bash
# Apache の起動・停止・再起動
$ sudo systemctl start apache2
$ sudo systemctl stop apache2
$ sudo systemctl restart apache2
$ sudo systemctl reload apache2

# ステータス確認
$ sudo systemctl status apache2

# 設定ファイルの文法チェック
$ sudo apache2ctl configtest

# サイトの有効化・無効化
$ sudo a2ensite サイト名
$ sudo a2dissite サイト名

# モジュールの有効化・無効化
$ sudo a2enmod モジュール名
$ sudo a2dismod モジュール名

# ログの確認
$ sudo tail -f /var/log/apache2/access.log
$ sudo tail -f /var/log/apache2/error.log

# ポートの確認
$ sudo ss -tuln | grep :80
$ sudo netstat -tuln | grep :80

# 設定ファイルの編集
$ sudo vim /etc/apache2/apache2.conf
$ sudo vim /etc/apache2/sites-available/000-default.conf
```

---

## 次のステップ

Apache の基本的なセットアップができたら、以下の内容を学習する:(どっかで書く)

---

## まとめ

このチュートリアルでは、Ubuntu 上で Apache HTTP Server をインストールし、80番ポートで Web サーバーを公開する方法について学びました。

**主要なポイント:**

- Ubuntu では Apache のパッケージ名は `apache2`
- `systemctl` コマンドでサービスを管理
- ドキュメントルートは `/var/www/html/`
- 設定ファイルは `/etc/apache2/` 配下
- ファイアウォールで 80番ポートを開放
- 仮想ホストで複数サイトをホスト可能
- ログファイルでアクセスとエラーを監視
- vim を使って設定ファイルを編集

Apache は非常に強力で柔軟な Web サーバーです。基本的な設定をマスターしたら、さらに高度な機能を探索してみてください！
