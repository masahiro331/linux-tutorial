# Linux Command Tutorial

このドキュメントでは、基本的なLinuxコマンドについて説明します。

## 基本的なLinux コマンドについて知ろう

### プロセス管理

### ps コマンド

実行中のプロセスを表示するコマンドです。

**基本的な使い方:**

```bash
$ ps
```

**ユースケース:**

- システムのリソース使用状況を確認する
- 特定のアプリケーションが実行中か確認する
- プロセスIDを調べてkillコマンドで終了させる

**よく使うオプション:**

- `ps aux` - システム上のすべてのプロセスを詳細表示
- `ps -ef` - すべてのプロセスをフルフォーマットで表示
- `ps aux | grep process_name` - 特定のプロセスを検索

---

### ファイル操作

### cp コマンド

ファイルやディレクトリをコピーするコマンドです。

**基本的な使い方:**

```bash
$ cp source.txt dest.txt
```

**ユースケース:**

- ファイルのバックアップを作成する
- 設定ファイルをコピーして編集用のコピーを作る
- ディレクトリ全体を別の場所に複製する

**よく使うオプション:**

- `cp -r dir1/ dir2/` - ディレクトリを再帰的にコピー
- `cp -i source.txt dest.txt` - 上書き前に確認
- `cp -p source.txt dest.txt` - タイムスタンプや属性を保持
- `cp -a dir1/ dir2/` - アーカイブモード（すべての属性を保持）

---

### mv コマンド

ファイルやディレクトリを移動・名前変更するコマンドです。

**基本的な使い方:**

```bash
$ mv old.txt new.txt
```

**ユースケース:**

- ファイル名を変更する
- ファイルを別のディレクトリに移動する
- 複数のファイルを一度に移動する

**よく使うオプション:**

- `mv -i old.txt new.txt` - 上書き前に確認
- `mv -n old.txt new.txt` - 既存ファイルを上書きしない
- `mv file.txt dir/` - ファイルをディレクトリに移動

---

### rm コマンド

ファイルやディレクトリを削除するコマンドです。

**基本的な使い方:**

```bash
$ rm file.tx
```

**ユースケース:**

- 不要なファイルを削除する
- ディレクトリとその中身をすべて削除する
- 特定のパターンに一致するファイルを削除する

**よく使うオプション:**

- `rm -r dir/` - ディレクトリを再帰的に削除
- `rm -i file.txt` - 削除前に確認
- `rm -f file.txt` - 強制削除（確認なし）
- `rm -rf dir/` - ディレクトリを強制的に再帰削除（注意: 危険）

---

### mkdir コマンド

ディレクトリを作成するコマンドです。

**基本的な使い方:**

```bash
$ mkdir dirname
```

**ユースケース:**

- プロジェクトの新しいディレクトリ構造を作る
- ログやバックアップ用のディレクトリを作成する
- 階層的なディレクトリ構造を一度に作成する

**よく使うオプション:**

- `mkdir -p dir1/dir2/dir3` - 親ディレクトリも含めて作成
- `mkdir -m 755 dirname` - パーミッションを指定して作成

---

### rmdir コマンド

空のディレクトリを削除するコマンドです。

**基本的な使い方:**

```bash
$ rmdir dirname
```

**ユースケース:**

- 使わなくなった空のディレクトリを削除する
- ディレクトリが本当に空かどうかを確認する

**よく使うオプション:**

- `rmdir -p dir1/dir2/dir3` - 親ディレクトリも含めて削除（すべて空の場合）

**注意:** 空でないディレクトリを削除する場合は `rm -r` を使用します。

---

### cat コマンド

ファイルの内容を表示するコマンドです。

**基本的な使い方:**

```bash
$ cat file.tx
```

**ユースケース:**

- ファイルの内容を確認する
- 複数のファイルを連結する
- ファイルの内容をパイプで他のコマンドに渡す

**よく使うオプション:**

- `cat file1.txt file2.txt` - 複数ファイルを連結して表示
- `cat -n file.txt` - 行番号を付けて表示
- `cat file1.txt > file2.txt` - ファイルをコピー
- `cat file1.txt >> file2.txt` - ファイルの内容を追記

---

### データを閲覧

### tail コマンド

ファイルの末尾部分を表示するコマンドです。

**基本的な使い方:**

```bash
$ tail file.txt
```

**ユースケース:**

- ログファイルの最新の内容を確認する
- リアルタイムでログを監視する
- ファイルの最後の数行だけを見たい場合

**よく使うオプション:**

- `tail -n 20 file.txt` - 最後の20行を表示（デフォルトは10行）
- `tail -f log.txt` - ファイルの変更をリアルタイムで監視
- `tail -F log.txt` - 参照しているファイルが再生成された場合でも追従する

---

### head コマンド

ファイルの先頭部分を表示するコマンドです。

**基本的な使い方:**

```bash
$ head file.txt
```

**ユースケース:**

- ファイルの形式やヘッダーを確認する
- CSVファイルのカラム名を見る
- 大きなファイルの一部だけを確認する

**よく使うオプション:**

- `head -n 20 file.txt` - 先頭20行を表示（デフォルトは10行）
- `head -c 100 file.txt` - 先頭100バイトを表示
- `head -n -5 file.txt` - 最後の5行を除いてすべて表示

---

### find コマンド

ファイルやディレクトリを検索するコマンドです。

**基本的な使い方:**

```bash
$ find /path/to/search -name "filename"
```

**ユースケース:**

- 特定の名前のファイルを探す
- 一定期間変更されていないファイルを見つける
- 特定のサイズや権限を持つファイルを検索する

**よく使うオプション:**

- `find . -name "*.txt"` - カレントディレクトリから.txtファイルを検索
- `find . -type f` - ファイルのみ検索
- `find . -type d` - ディレクトリのみ検索
- `find . -mtime -7` - 過去7日以内に変更されたファイル
- `find . -size +100M` - 100MB以上のファイル

---

### grep コマンド

テキストからパターンに一致する行を検索するコマンドです。

**基本的な使い方:**

```bash
$ grep "検索したい文字列" file.txt
```

**ユースケース:**

- ログファイルからエラーメッセージを探す
- 特定の文字列を含むファイルを見つける
- コード内で関数や変数の使用箇所を探す

**よく使うオプション:**

- `grep -i "pattern" file.txt` - 大文字小文字を区別しない
- `grep -r "pattern" dir/` - ディレクトリを再帰的に検索
- `grep -n "pattern" file.txt` - 行番号を表示
- `grep -v "pattern" file.txt` - パターンに一致しない行を表示
- `grep -c "pattern" file.txt` - 一致した行数をカウント

---

### diff コマンド

2つのファイルの差分を表示するコマンドです。

**基本的な使い方:**

```bash
$ diff file1.txt file2.txt

```

**ユースケース:**

- ファイルの変更箇所を確認する
- 設定ファイルのバージョン間の違いを見る
- 2つのディレクトリの内容を比較する

**よく使うオプション:**

- `diff -u file1.txt file2.txt` - Unified形式で差分表示（git diffと同じ形式）
- `diff -y file1.txt file2.txt` - 横並びで差分表示
- `diff -r dir1/ dir2/` - ディレクトリを再帰的に比較
- `diff -q file1.txt file2.txt` - 差分の有無のみ表示

---

### パイプを使った組み合わせ

Linuxでは `|`（パイプ）を使って複数のコマンドを組み合わせ、強力なデータ処理を行うことができます。

### tail | grep の組み合わせ

ログファイルの最新部分から特定のパターンを検索します。

**例:**

```bash
$ tail -n 100 /var/log/syslog | grep "error"

```

**ユースケース:**

- 直近のログから特定のエラーメッセージを探す
- ログをリアルタイムで監視しながら特定のキーワードをフィルタリングする

**実用例:**

```bash
# 直近100行からERRORを含む行を抽出
$ tail -n 100 app.log | grep "ERROR"

# ログをリアルタイム監視してエラーのみ表示
$ tail -f app.log | grep "ERROR"

# 複数のパターンを検索
$ tail -n 200 app.log | grep -E "ERROR|WARN"

```

---

### cat | sort | uniq | wc の組み合わせ

ファイル内のユニークな行の数をカウントします。

**例:**

```bash
$ cat access.log | sort | uniq | wc -l

```

**ユースケース:**

- アクセスログからユニークなIPアドレスの数を数える
- 重複を除いた項目の数を集計する
- データの種類や頻度を分析する

**実用例:**

```bash
# ユニークな行の数をカウント
$ cat data.txt | sort | uniq | wc -l

# 各行の出現回数をカウント
$ cat data.txt | sort | uniq -c

# 最も頻繁に出現する10項目を表示
$ cat access.log | sort | uniq -c | sort -rn | head -n 10

# IPアドレスのユニークな数を数える（アクセスログの例）
$ cat access.log | awk '{print $1}' | sort | uniq | wc -l

```

**各コマンドの役割:**

- `cat` - ファイルの内容を読み込む
- `sort` - 行をソートする（uniqは連続した重複のみ削除するためソートが必要）
- `uniq` - 連続する重複行を削除
- `wc -l` - 行数をカウント

---

## 追加の便利なコマンド

### sort コマンド

テキストファイルの行を並び替えるコマンドです。

**基本的な使い方:**

```bash
$ sort file.txt

```

**よく使うオプション:**

- `sort -r file.txt` - 逆順（降順）でソート
- `sort -n file.txt` - 数値としてソート
- `sort -k 2 file.txt` - 2番目のフィールドでソート
- `sort -u file.txt` - ソート後に重複行を削除

---

### uniq コマンド

連続する重複行を削除または検出するコマンドです。

**基本的な使い方:**

```bash
$ sort file.txt | uniq

```

**よく使うオプション:**

- `uniq -c file.txt` - 重複回数をカウントして表示
- `uniq -d file.txt` - 重複している行のみ表示
- `uniq -u file.txt` - 重複していない行のみ表示

---

### jq コマンド

JSONデータを処理・整形するコマンドです。

**基本的な使い方:**

```bash
$ cat data.json | jq '.'

```

**ユースケース:**

- APIレスポンスのJSONを読みやすく整形する
- JSONから特定のフィールドを抽出する
- JSON配列をフィルタリングや変換する

**よく使うオプション:**

- `jq '.' file.json` - JSONを整形して表示
- `jq '.field' file.json` - 特定のフィールドを抽出
- `jq '.[] | .name' file.json` - 配列の各要素からnameフィールドを抽出
- `jq -r '.field' file.json` - Raw出力（引用符なし）

---

### file コマンド

ファイルの種類を判定するコマンドです。

**基本的な使い方:**

```bash
$ file filename

```

**ユースケース:**

- 拡張子がないファイルの種類を調べる
- バイナリかテキストかを判定する
- 圧縮ファイルの形式を確認する

**よく使うオプション:**

- `file *` - カレントディレクトリの全ファイルの種類を表示
- `file -b filename` - ファイル名を表示せず、種類のみ表示
- `file -i filename` - MIMEタイプで表示

---

## ネットワーク関連

### ping コマンド

ネットワーク接続を確認するコマンドです。

**基本的な使い方:**

```bash
$ ping example.com

```

**ユースケース:**

- ホストが到達可能か確認する
- ネットワークの遅延（レイテンシ）を測定する
- パケットロスを確認する
- ネットワーク接続のトラブルシューティング

**よく使うオプション:**

- `ping -c 4 example.com` - 4回だけpingを送信して終了
- `ping -i 2 example.com` - 2秒間隔でpingを送信
- `ping -s 1000 example.com` - パケットサイズを1000バイトに指定
- `ping -q example.com` - 統計情報のみ表示（静かなモード）

**実用例:**

```bash
# Googleに到達可能か確認
$ ping -c 4 google.com

# ローカルネットワークのゲートウェイを確認
$ ping -c 3 192.168.1.1

# IPv6アドレスにping
$ ping -6 ipv6.google.com

```

---

### curl コマンド

URLからデータを取得・送信するコマンドです。

**基本的な使い方:**

```bash
$ curl https://example.com

```

**ユースケース:**

- Webページの内容を取得する
- APIエンドポイントをテストする
- ファイルをダウンロードする
- HTTPリクエストをカスタマイズして送信する

**よく使うオプション:**

- `curl -O https://example.com/file.zip` - ファイルを元の名前で保存
- `curl -o output.html https://example.com` - 指定した名前で保存
- `curl -I https://example.com` - HTTPヘッダーのみ取得
- `curl -X POST https://api.example.com/data` - POSTリクエストを送信
- `curl -H "Content-Type: application/json" url` - カスタムヘッダーを追加
- `curl -d "key=value" https://api.example.com` - データを送信
- `curl -L https://example.com` - リダイレクトに従う
- `curl -v https://example.com` - 詳細な情報を表示

**実用例:**

```bash
# ファイルをダウンロード
$ curl -O https://example.com/file.zip

# APIからJSONデータを取得
$ curl https://api.github.com/users/octocat

# JSONデータをPOST送信
$ curl -X POST -H "Content-Type: application/json" \
  -d '{"name":"John","age":30}' \
  https://api.example.com/users

# Basic認証を使用
$ curl -u username:password https://example.com/api

# レスポンスヘッダーを確認
$ curl -I https://example.com

```

---

### wget コマンド

ファイルをダウンロードするコマンドです。

**基本的な使い方:**

```bash
$ wget https://example.com/file.zip

```

**ユースケース:**

- インターネットからファイルをダウンロードする
- Webサイト全体をミラーリングする
- ダウンロードを中断・再開する
- 大容量ファイルのダウンロード

**よく使うオプション:**

- `wget -O filename.zip url` - 指定した名前で保存
- `wget -c url` - 中断したダウンロードを再開
- `wget -b url` - バックグラウンドでダウンロード
- `wget -r https://example.com` - 再帰的にダウンロード（ミラーリング）
- `wget --limit-rate=1m url` - ダウンロード速度を制限（1MB/s）
- `wget -i urls.txt` - ファイルに記載されたURLを一括ダウンロード

**実用例:**

```bash
# ファイルをダウンロード
$ wget https://example.com/file.zip

# 中断したダウンロードを再開
$ wget -c https://example.com/large-file.iso

# 複数のURLを一括ダウンロード
$ cat urls.txt
https://example.com/file1.zip
https://example.com/file2.zip
$ wget -i urls.txt

```

**curl vs wget:**

- **curl**: より多機能でAPIテストに適している、デフォルトで標準出力
- **wget**: ファイルダウンロードに特化、再帰的ダウンロードが得意

---

### ifconfig コマンド

ネットワークインターフェースの設定を表示・変更するコマンドです。

**基本的な使い方:**

```bash
$ ifconfig

```

**ユースケース:**

- ネットワークインターフェースの情報を確認する
- IPアドレスを確認する
- MACアドレスを確認する
- ネットワークインターフェースを有効・無効にする

**よく使うオプション:**

- `ifconfig -a` - すべてのインターフェースを表示（無効なものも含む）
- `ifconfig eth0` - 特定のインターフェースのみ表示
- `ifconfig eth0 down` - インターフェースを無効化（要root権限）
- `ifconfig eth0 up` - インターフェースを有効化（要root権限）

**実用例:**

```bash
# すべてのネットワークインターフェースを表示
$ ifconfig

# 特定のインターフェースを表示
$ ifconfig eth0

# IPアドレスのみ抽出
$ ifconfig eth0 | grep "inet " | awk '{print $2}'

```

**注意:** 最近のLinuxディストリビューションでは `ip` コマンドの使用が推奨されています。

---

### ip コマンド

ネットワーク設定を管理する現代的なコマンドです（ifconfig の後継）。

**基本的な使い方:**

```bash
$ ip addr show

```

**ユースケース:**

- ネットワークインターフェースの情報を表示
- ルーティングテーブルを確認
- IPアドレスを設定・削除
- ネットワークインターフェースを管理

**よく使うオプション:**

- `ip addr show` または `ip a` - IPアドレスを表示
- `ip link show` または `ip l` - ネットワークインターフェースを表示
- `ip route show` または `ip r` - ルーティングテーブルを表示
- `ip -s link` - 統計情報を含めて表示
- `ip addr add 192.168.1.100/24 dev eth0` - IPアドレスを追加
- `ip link set eth0 up` - インターフェースを有効化

**実用例:**

```bash
# すべてのIPアドレスを表示
$ ip addr show

# 特定のインターフェースのみ表示
$ ip addr show eth0

# ルーティングテーブルを表示
$ ip route show

# デフォルトゲートウェイを確認
$ ip route | grep default

# ネットワーク統計を表示
$ ip -s link

```

**ifconfig vs ip:**

- **ifconfig**: 古いコマンド、非推奨だが広く知られている
- **ip**: 現代的で多機能、推奨されている

---

### dig コマンド

DNS（Domain Name System）の問い合わせを行うコマンドです。

**基本的な使い方:**

```bash
$ dig example.com

```

**ユースケース:**

- ドメイン名のIPアドレスを調べる
- DNSレコードを確認する
- DNS設定のトラブルシューティング
- 権威DNSサーバーを特定する

**よく使うオプション:**

- `dig example.com A` - Aレコード（IPv4アドレス）を取得
- `dig example.com AAAA` - AAAAレコード（IPv6アドレス）を取得
- `dig example.com MX` - MXレコード（メールサーバー）を取得
- `dig example.com NS` - NSレコード（ネームサーバー）を取得
- `dig example.com +short` - 簡潔な出力（IPアドレスのみ）
- `dig @8.8.8.8 example.com` - 特定のDNSサーバーに問い合わせ
- `dig -x 8.8.8.8` - 逆引き（IPアドレスからドメイン名）

**実用例:**

```bash
# ドメインのIPアドレスを取得
$ dig example.com +short

# GoogleのDNSサーバーを使って問い合わせ
$ dig @8.8.8.8 example.com

# MXレコードを確認（メールサーバー）
$ dig example.com MX +short

# 詳細な情報を表示
$ dig example.com ANY

# 逆引きでホスト名を確認
$ dig -x 93.184.216.34 +short

```

---

### nslookup コマンド

DNSの問い合わせを行うインタラクティブなコマンドです。

**基本的な使い方:**

```bash
$ nslookup example.com

```

**ユースケース:**

- ドメイン名のIPアドレスを調べる
- DNSサーバーの応答を確認する
- 逆引きでホスト名を確認する

**よく使うオプション:**

- `nslookup example.com` - ドメインのIPアドレスを取得
- `nslookup example.com 8.8.8.8` - 特定のDNSサーバーに問い合わせ
- `nslookup -type=mx example.com` - MXレコードを取得
- `nslookup -type=ns example.com` - NSレコードを取得

**実用例:**

```bash
# ドメインのIPアドレスを取得
$ nslookup google.com

# 特定のDNSサーバーを使用
$ nslookup google.com 8.8.8.8

# MXレコードを確認
$ nslookup -type=mx gmail.com

```

**dig vs nslookup:**

- **dig**: より詳細な情報、スクリプトに適している
- **nslookup**: シンプルで使いやすい、インタラクティブモードあり

---

### netstat コマンド

ネットワーク接続、ルーティングテーブル、インターフェース統計を表示するコマンドです。

**基本的な使い方:**

```bash
$ netstat

```

**ユースケース:**

- 開いているポートを確認する
- アクティブなネットワーク接続を表示する
- リスニング中のサービスを確認する
- ネットワーク統計を表示する

**よく使うオプション:**

- `netstat -tuln` - リスニング中のTCP/UDPポートを表示
  - `-t`: TCP
  - `-u`: UDP
  - `-l`: リスニング中
  - `-n`: 数値形式で表示（名前解決しない）
- `netstat -an` - すべてのネットワーク接続を表示
- `netstat -r` - ルーティングテーブルを表示
- `netstat -i` - ネットワークインターフェースの統計
- `netstat -p` - プロセス情報を表示（要root権限）

**実用例:**

```bash
# リスニング中のポートを確認
$ netstat -tuln

# 特定のポートを使用しているプロセスを確認
$ sudo netstat -tulnp | grep :80

# すべてのアクティブな接続を表示
$ netstat -an

# ルーティングテーブルを表示
$ netstat -r

```

**注意:** 最近のLinuxでは `ss` コマンドの使用が推奨されています。

---

### ss コマンド

ソケット統計を表示する現代的なコマンドです（netstat の後継）。

**基本的な使い方:**

```bash
$ ss

```

**ユースケース:**

- ネットワーク接続の状態を確認する
- リスニング中のポートを表示する
- 確立された接続を確認する
- ネットワークパフォーマンスのトラブルシューティング

**よく使うオプション:**

- `ss -tuln` - リスニング中のTCP/UDPポートを表示
- `ss -a` - すべてのソケットを表示
- `ss -p` - プロセス情報を表示
- `ss -s` - 統計サマリーを表示
- `ss -t state established` - 確立されたTCP接続のみ表示
- `ss dst 192.168.1.100` - 特定のIPアドレスへの接続を表示

**実用例:**

```bash
# リスニング中のポートを確認
$ ss -tuln

# 確立された接続を表示
$ ss -t state established

# 特定のポートを確認
$ ss -tuln | grep :443

# プロセス情報を含めて表示
$ sudo ss -tulnp

# 統計サマリー
$ ss -s

```

**netstat vs ss:**

- **netstat**: 古いコマンド、広く知られている
- **ss**: より高速で詳細、推奨されている

---

### traceroute コマンド

パケットが宛先に到達するまでの経路を追跡するコマンドです。

**基本的な使い方:**

```bash
$ traceroute example.com

```

**ユースケース:**

- ネットワーク経路を確認する
- ネットワーク遅延の原因を特定する
- パケットがどのルーターを経由するか確認する
- ネットワークの問題箇所を特定する

**よく使うオプション:**

- `traceroute -n example.com` - 名前解決をスキップ（IPアドレスのみ表示）
- `traceroute -m 15 example.com` - 最大ホップ数を15に制限
- `traceroute -q 1 example.com` - 各ホップへの問い合わせ回数を1回に
- `traceroute -I example.com` - ICMPを使用（デフォルトはUDP）

**実用例:**

```bash
# Googleへの経路を追跡
$ traceroute google.com

# 名前解決なしで高速実行
$ traceroute -n 8.8.8.8

# ICMPを使用
$ traceroute -I example.com

```

**注意:**

- ファイアウォールやルーターの設定により、一部のホップが表示されない場合があります（`* * *`）
- 実行には時間がかかることがあります

---

### hostname コマンド

システムのホスト名を表示・設定するコマンドです。

**基本的な使い方:**

```bash
$ hostname

```

**ユースケース:**

- 現在のホスト名を確認する
- FQDNを確認する
- IPアドレスを確認する

**よく使うオプション:**

- `hostname` - ホスト名を表示
- `hostname -f` - FQDN（完全修飾ドメイン名）を表示
- `hostname -I` - すべてのIPアドレスを表示
- `hostname -i` - ホスト名に関連付けられたIPアドレスを表示

**実用例:**

```bash
# ホスト名を確認
$ hostname

# FQDNを確認
$ hostname -f

# IPアドレスを確認
$ hostname -I

```

---

### ネットワークコマンドの組み合わせ

**Webサーバーの動作確認:**

```bash
# ポート80がリスニングしているか確認
$ ss -tuln | grep :80

# curlでHTTPレスポンスを確認
$ curl -I http://localhost

# ローカルのWebサーバーに接続できるか確認
$ ping -c 1 localhost && curl http://localhost

```

**DNSトラブルシューティング:**

```bash
# DNSが正しく解決されるか確認
$ dig example.com +short

# 異なるDNSサーバーで比較
$ dig @8.8.8.8 example.com +short
$ dig @1.1.1.1 example.com +short

# 逆引きも確認
$ dig -x <IPアドレス> +short

```

**ネットワーク接続の診断:**

```bash
# ホストに到達可能か確認
$ ping -c 4 example.com

# 経路を確認
$ traceroute example.com

# DNS解決を確認
$ nslookup example.com

# ポートが開いているか確認（80番ポート）
$ curl -I http://example.com

```
