# 学習ログ / Learning Log

## ■ 日付（JST） / Date

2025/10/02

## ■ 学習テーマ / Topic

Linux（TryHackMe: Linux Fundamentals – Part 3）

## ■ 目的 / Goal (JP→EN one-liner)

* JP: 端末上での運用タスク（編集・配信・プロセス管理・自動化・ログ確認）を“手順化”して再現できるようにする
* EN: Turn common Linux ops tasks (edit, serve, process control, automation, log review) into repeatable routines.

---

## ■ 今日やったこと（一次メモ→整理済）

* 端末テキストエディタ：`nano` / `vi`（保存・終了・検索などの最小操作）
* ユーティリティ：`curl`/`wget` での取得、`python -m http.server` での簡易配信
* プロセス基礎：`ps`/`top`/`htop`、`kill`/`pkill`、`nice`/`renice`
* 自動化：ユーザーcrontab（`crontab -e`）とシステムcrontab（`/etc/crontab`、`/etc/cron.*`）
* パッケージ管理：`apt update`/`upgrade`/`install`/`remove`
* ログの確認：`/var/log/`、Apache の `access.log` / `error.log`（`/var/log/apache2`）

---

## ■ 理解が不十分だった点と正しい説明（要修正ポイント）

1. **`/etc/crontab` の読み方が曖昧**

   * 誤：ユーザー crontab と同じ5列だと思っていた
   * 正：**`/etc/crontab` は「分 時 日 月 曜日 ユーザー コマンド」の6列**。ユーザー名列が入る点が違い。
   * 特殊語：`@reboot`（起動時1回）, `@hourly`/`@daily`/`@weekly`/`@monthly` などは **列を使わない**“ショートカット”。

2. **「When will the crontab run?」の答え方**

   * 誤：時刻文字列だけをいろいろ試して混乱
   * 正：対象行を特定→**5列（または`@…`）だけ読む**。今回のユーザーcrontabは

     ```
     @reboot /var/opt/processes.sh
     ```

     なので回答は **「on reboot（@reboot）」** が本質。

3. **パス操作の基本**

   * 誤：`/var.log$ ls` のように **パスをコマンドとして実行**していた
   * 正：**コマンド + 引数**の形にする。例：`cd /var/log/apache2` → `ls -l` → `tail -n 50 access.log`

4. **Apacheログの場所**

   * 正：Debian/Ubuntu 系は **`/var/log/apache2`**、RHEL/CentOS 系は `/var/log/httpd`。今回の環境は前者。

5. **ログの見方の最小セット**

   * 直近を見る：`tail -n 50 /var/log/apache2/access.log` / `error.log`
   * 古い圧縮ログ：`zcat access.log.1.gz | head`
   * 連続監視：`tail -f access.log`

---

## ■ “実務で使う最小手順”メモ（コピペOK）

### A. テキスト編集（nano と vi）

```bash
# nano
nano file.txt             # 保存: Ctrl+O → Enter / 終了: Ctrl+X / 検索: Ctrl+W
# vi
vi file.txt               # 挿入: i / 保存終了: Esc → :wq / 破棄終了: Esc → :q!
```

### B. ダウンロード & 簡易Web配信

```bash
wget https://example.com/file         # または curl -O https://example.com/file
python3 -m http.server 8000           # カレントを http://<host>:8000 で配信
```

### C. プロセス & 優先度

```bash
ps aux | grep <name>
top                                  # qで終了
kill <PID>                           # 強制は kill -9 <PID>（最終手段）
renice 10 -p <PID>                   # nice値を +10 に
```

### D. cron（ユーザー / システム）

```bash
crontab -l                           # ユーザーのジョブ一覧
crontab -e                           # 追加・編集（例：*/2 * * * * date >> ~/cron.log）
cat /etc/crontab                     # システムのスケジュール（6列 + ユーザー）
ls /etc/cron.{hourly,daily,weekly,monthly}
```

### E. パッケージ管理（Debian/Ubuntu）

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install <pkg>
sudo apt remove <pkg>
```

### F. ログ（Apache 例）

```bash
cd /var/log/apache2
ls -l
tail -n 50 access.log
tail -n 50 error.log
zcat access.log.1.gz | head
```

---

## ■ 英語の簡単要約（2–3文）

Today I practiced core Linux ops tasks: editing files in the terminal, fetching and serving content with a Python HTTP server, inspecting and controlling processes, scheduling with cron, managing packages via apt, and reviewing logs, especially Apache logs in `/var/log/apache2`.
I clarified how to read `/etc/crontab` (6 fields with a username) vs user crontab (5 fields) and the meaning of `@reboot`.

---

## ■ 成果物（抜粋）

* `@reboot /var/opt/processes.sh` の解釈：**on reboot**
* Apache ログの場所確認：`/var/log/apache2/{access.log,error.log}`
* 検証スニペット（2分おきログ）

  ```bash
  (crontab -l 2>/dev/null; echo '*/2 * * * * date "+%F %T" >> ~/cron_test.log') | crontab -
  ```

---

## ■ 所要時間 / Time spent

3時間

---

## ■ 次にやりたいこと（具体アクション）

1. **cron 検証を5分で完了**：上記の2分おきジョブを入れて`tail -f ~/cron_test.log`で動作確認→`crontab -r`で削除
2. **ログ横断の手札づくり**：`grep -i 'error\|warn' /var/log/apache2/error.log | tail -n 20` など“定型”を自分用に3本作る
3. **入力ミス撲滅**：Tab補完の徹底（`cd /var/lo<Tab>`）と、**コマンド+引数**の形に慣れる
4. **Part 3 の復習チェック**（5問ミニクイズ）

   * `@reboot` はいつ実行？
   * `/etc/crontab` と `crontab -e` の列数の違いは？
   * Apache ログの標準パスは？
   * 直近50行を見るコマンドは？
   * 強制終了の前に試すべきシグナルは？（答：`TERM` → それでもダメなら `KILL`）

---

## ■ メンタルメモ（短く）

* 今日は“形式（@rebootや6列）を掴む日”。**型を得た＝次は速い**。
* 次回は「1問=最長20分」の**タイムボックス**と、上の“手札”で回転を上げる。
