# 学習ログ / Learning Log

## 日付 / Date
2025/09/26 (JST)

## 学習テーマ / Topic
TryHackMe – Linux Fundamentals (Part 1)

## 目的 / Goal (JP→EN one-liner)
- JP: Linuxの基本操作とファイル操作の考え方を身につける  
- EN: Build foundational fluency with Linux shell and file operations.

---

## 今日やったこと（一次メモ）/ What I did (notes)
- 基本コマンド：`pwd`, `ls`, `cd`, `touch`, `mkdir`, `mv`, `cp`, `rm`, `cat`, `file`
- 出力と改行：`echo` の挙動、`echo -n` と `printf` の違い
- 標準入出力の基礎：`>`, `>>`, `2>`, `2>/dev/null` の使い分け
- 検索：`find . -maxdepth N -type f -name 'pattern'`、`-iname`、グロブと正規表現の違い
- ファイルの中身確認：`cat`, `less`, `head`, `tail`
- “human-readable” 表示フラグ：`-h`（例：`ls -lh`, `du -h`, `df -h`）

---

## 参照した資料・リンク / References
- TryHackMe: Linux Fundamentals Part 1  
  https://tryhackme.com/room/linuxfundamentalspart1

---

## 自分の理解で怪しい所（要修正ポイント）/ Unclear points & fixes

1) **`echo` が改行を付ける → 文字数ズレ**  
- 誤：`echo TryHackMe` は 末尾に改行が付くため厳密一致問題でズレることがある  
- 正：改行なしは `echo -n TryHackMe` または `printf "TryHackMe"`

2) **stderr リダイレクトの綴り**  
- 誤：`2>dev/null`（スラッシュなし）  
- 正：`2>/dev/null`（先頭 `/` 必須）  
  例：`find . -maxdepth 3 -type f -name 'myfile' 2>/dev/null`

3) **`cat` の対象は“ファイル”であって“ディレクトリ”ではない**  
- 誤：`cat myfolder`  
- 正：`cat myfolder/myfile`（ディレクトリ/ファイルの区別を意識）

4) **ユーザー/ホームの取り違え**  
- プロンプトが `root@...:~#` のとき、ホームは `/root`。  
  THMの想定ファイルが `/home/tryhackme` にあるなら、`cd /home/tryhackme` してから探索する。

5) **`find` の条件結合（`-o` を使うときの括弧）**  
- `-o`（OR）を使う際は、括弧でグルーピングして **`-maxdepth` の適用範囲**を明示すると混乱がない。  
  例：  
  ```bash
  # 両方の -name に同じ深さ制限を掛けたい:
  find . -maxdepth 3 -type f \( -name 'myfile' -o -name 'myfile*' \) 2>/dev/null
