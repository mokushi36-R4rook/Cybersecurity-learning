# 学習ログ / Learning Log

## ■ 日付（JST） / Date

2025/09/30

## ■ 学習テーマ / Topic

TryHackMe – Linux Foundation 3（`ps` / `wget` / `python3 -m http.server`）

## ■ 目的 / Goal (JP→EN one-liner)

* **JP:** Linux上でのプロセス確認・簡易Web配信・ファイル取得を一連の手順として再現できるようにする。
* **EN:** Be able to verify processes, serve files via a quick web server, and fetch them end-to-end on Linux.

---

## ■ 今日やったこと（一次メモ→整理）

### 1) `ps`（プロセス確認）

* 基本：`ps` は**今のシェルのプロセス**を表示。
* よく使うオプション

  * `ps aux`：すべてのユーザー・すべてのプロセスを BSD 形式で表示
  * `ps -ef`：System V 形式で親子関係（PPID）を含めて表示
  * `ps aux | grep <pattern>`：特定プロセスの絞り込み（例：`http.server`）
* 関連：`pgrep http.server`（PIDだけ）、`top`/`htop`（動的表示）

### 2) `wget`（ファイル取得）

* 基本：`wget <URL>` でHTTP/HTTPSから取得。
* 便利オプション

  * `-O <file>`：保存ファイル名を指定
  * `-q`：静かに実行、`-nv`：必要最低限のログ
  * `--content-disposition`：サーバの提示名で保存（対応していれば）
* トラブル対処

  * **Connection refused**：相手ホストの該当ポートに**プロセスがリッスンしていない**
  * **404**：URL/パスの誤り or 配信ディレクトリにファイルがない
  * **タイムアウト**：ネットワーク未接続/ファイアウォール

### 3) `python3 -m http.server`（簡易Webサーバ）

* 正式名は **`http.server`**（大文字ではなく小文字）。
* **配信ディレクトリ＝起動ディレクトリ**。別場所なら `--directory <dir>`。
* 外部アクセス可にする例：

  ```bash
  python3 -m http.server 8000 --bind 0.0.0.0 --directory /home/tryhackme
  ```
* 停止：起動端末で `Ctrl + C`。
* バックグラウンド化（端末を閉じても維持したい場合）：

  ```bash
  nohup python3 -m http.server 8000 --bind 0.0.0.0 --directory /home/tryhackme >/tmp/pyhttp.log 2>&1 &
  disown
  ```
* 状態確認：

  ```bash
  ss -ltnp | grep :8000     # 0.0.0.0:8000 LISTEN が理想
  ps aux | grep http.server # プロセス確認
  ```

---

## ■ 参照した資料・リンク

* Python docs（`http.server` モジュール）
* GNU Wget マニュアル
* `man ps`, `man wget`, `python3 -m http.server -h` のヘルプ出力

> ※ 実学では各コマンドの `--help` を習慣にするのが速いです。

---

## ■ 自分の理解で怪しい所（要修正ポイント → 正しい説明）

1. **「HTTPServer」モジュール名**

   * **誤**：`HTTPServer` を直接モジュールとして起動する
   * **正**：Python 3 では `http.server` を `-m` で実行する（内部で `HTTPServer` クラス等を使う実装）

2. **「サーバを起動した端末で他コマンドが打てる」**

   * **誤**：同じ端末で `curl/wget` も打てる前提
   * **正**：前景で起動中は端末が占有される。**別ターミナル**を開くか、**バックグラウンド化**する。

3. **`Connection refused` の原因**

   * **誤**：ファイルが無いから拒否
   * **正**：**該当ポートにリスナー不在**（プロセス停止/`--bind 127.0.0.1` で外部から不可/ポート違い/IP違い）。ファイル不在なら 404。

4. **配信ディレクトリの考え方**

   * **誤**：どこで起動してもホームが配信される
   * **正**：**カレントディレクトリ**が配信。指定したいなら `--directory` を使う。

---

## ■ 英語の簡単要約（Draft）

Today I practiced three essentials on Linux: checking processes with `ps`, serving files using `python3 -m http.server`, and downloading them via `wget`. I learned to bind the server to `0.0.0.0`, keep it running in the foreground or background, and verify it with `ss` and `ps`. I also troubleshot “Connection refused” by confirming the IP, port, and bind address.

---

## ■ 成果物（コマンド断片）

```bash
# プロセス確認
ps -ef | grep http.server

# 簡易Webサーバ（外部公開）
python3 -m http.server 8000 --bind 0.0.0.0 --directory /home/tryhackme

# リッスン確認
ss -ltnp | grep :8000

# AttackBox 等からの取得
wget http://<MACHINE_IP>:8000/.flag.txt
cat .flag.txt
```

---

## ■ 所要時間 / Time spent

60分

---

## ■ 次にやりたいこと（下書き）

* `nohup` / `&` / `disown` の挙動差を短文で説明できるようにする。
* `ss` と `netstat` の違い、`ss` でのポート状態読み取りを練習。
* `curl -I` と `wget` の使い分け（HTTPヘッダ確認 vs 保存）。
* `systemctl` での常駐管理（本番寄りの練習）や `tmux` による複数セッション運用。
* 失敗時ログの読み方（`/tmp/pyhttp.log` など）を1分で確認するルーチン化。

---

### メモ（今日の教訓）

* **「接続拒否＝リスナー不在」**を最優先で疑う。IP/ポート/bind をまず確認。
* 「起動端末は触らない→別ターミナルで検証」を身体で覚える。
