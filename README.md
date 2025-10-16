# 学習ログ / Learning Log

## ■ 日付（JST）/ Date
2025/10/16

## ■ 学習テーマ / Topic
- TryHackMe – Windows Fundamentals（System Configuration / Tools）
- 基礎数学（関数の定義・対応の確認 / Khan Academy）
- Python 基本文法（リスト内包表記・型変換）

## ■ 目的 / Goal (JP→EN one-liner)
JP: Windowsの管理ツールの実行コマンドを正しく特定し、数学とPython基礎の穴を埋める。  
EN: Identify correct Windows admin tool commands and patch gaps in basic math and Python.

## ■ 今日やったこと（一次メモ・JP中心）
- TryHackMe の設問対応  
  - **System Configuration → Tools → Internet Protocol Configuration** の “Selected command” を確認  
    - 回答：`C:\Windows\System32\cmd.exe /k %windir%\system32\ipconfig.exe`  
  - **Registry Editor のコマンド名**（フルパスではなく実行ファイル名）：`regedit.exe`
- Khan Academy：**「科目→趣味」は関数か？** の判定問題  
  - 入力（科目）ごとに出力（趣味）が一意 → **関数である** と判断
- Python 演習：**スペース区切り入力→float リスト** への変換  
  - 正しい内包表記を再確認（下の「成果物」にサンプル）

## ■ 参照した資料・リンク
- TryHackMe（Windows Fundamentals / System Configuration）  
- Microsoft Docs  
  - `ipconfig`（Internet Protocol Configuration）  
  - `cmd.exe /k` スイッチの意味  
  - Registry Editor（`regedit.exe`）

## ■ 自分の理解で怪しい所（要修正ポイント）
1) **「フルコマンド」と「実行ファイル名だけ」の区別が曖昧**  
   - ✖️ いつもフルパスだと思ってしまう  
   - ✅ **設問文を精読**：「full command」なら `cmd.exe /k ...` を含む形式／「the name of the .exe」なら **`regedit.exe`** のように拡張子までの**名前のみ**。

2) **`cmd.exe /k` の挙動**  
   - ✖️ `/k` と `/c` の違いが曖昧  
   - ✅ `/k` は **コマンド実行後もウィンドウを開いたまま**、`/c` は **実行後に閉じる**。msconfig の Tools は表示保持のために `/k` をよく使う。

3) **環境変数 `%windir%` の解釈**  
   - ✖️ 文字列の一部だと思いがち  
   - ✅ `%windir%` は Windows ディレクトリ（例：`C:\Windows`）を指す**環境変数**。  
     例：`%windir%\system32\ipconfig.exe` → 実体は `C:\Windows\System32\ipconfig.exe`

4) **関数の定義（数学）**  
   - ✖️ 「同じ入力が複数回出てくる＝関数でない」と混同  
   - ✅ **関数の要件は「同じ入力に複数の異なる出力がないこと」**。  
     - 同じ「科目→同じ趣味」の重複行は **OK**。  
     - 「科目A → 趣味X」と「科目A → 趣味Y」が同時に存在したら **関数でない**。

5) **Python の変数の使い回し**  
   - ✖️ ループ変数名で元の変数を**上書き**（例：`for a in li:` など）  
   - ✅ 入力リスト `a` と出力リスト `li` を**別名で明確に**し、**内包表記**で一気に変換する。

## ■ 英語の簡単要約（Draft）
Today I confirmed the exact command shown in System Configuration → Tools for Internet Protocol Configuration and the executable name for Registry Editor. I also reviewed the definition of a function (each input maps to exactly one output) and practiced Python list comprehensions for converting string inputs to floats.

## ■ 成果物（コード/図/ノート）
### 1) Windows Tools（覚え書き）
- Internet Protocol Configuration（msconfig → Tools → Selected command）  
