## ■ 日付（JST）/ Date
2025-10-15

---

## ■ 学習テーマ / Topic
TryHackMe Pre-Security / Windows 基本操作と隠し共有の理解

---

## ■ 目的 / Goal (JP→EN one-liner)
JP: Windows における管理用共有やコマンドの存在を理解する  
EN: Understand the existence of administrative shares and basic Windows commands

---

## ■ 今日やったこと（一次メモ・JP中心）
- TryHackMe の課題で以下を調査・回答  
  - Sysinternals が作ったサービス名（PsShutdown）  
  - Windows ライセンス登録者（Windows User）  
  - Windows Troubleshooting コマンド（`control.exe /name Microsoft.Troubleshooting`）  
  - Control Panel を開くコマンド（`control.exe`）  
  - 隠し共有フォルダの名前（`C$`）  
- Tools タブ（msconfig）の使い方を確認  
- Mac からは直接試せないが、TryHackMe 上のターゲットや smbclient 経由で共有列挙できる方法を学習  
- Windows の「$」付き共有（C$, ADMIN$, IPC$ など）は管理者用の隠し共有であることを理解

---

## ■ 参照した資料・リンク
- TryHackMe Pre-Security room (Windows 基本)  
- [Microsoft Docs - Administrative Shares](https://learn.microsoft.com/en-us/troubleshoot/windows-server/networking/administrative-shares-in-windows)  
- [smbclient man page](https://www.samba.org/samba/docs/current/man-html/smbclient.1.html)

---

## ■ 自分の理解で怪しい所（要修正ポイント）
- 「Sysinternals のサービス名」を最初「サービス一覧」で探そうとしたが、実際は Tools タブにあるユーティリティ名 → **正しくは PsShutdown**  
- 「Control Panel」項目が Tools に見当たらなかった → **環境によって表示が異なる。正解は control.exe**  
- 隠し共有は物理フォルダではなく管理共有 → **「$」が末尾につくと隠し共有**というルールを押さえる必要がある  

---

## ■ 英語の簡単要約（あれば下書き）
Today I practiced Windows basics on TryHackMe.  
I learned about administrative shares (C$, ADMIN$) and basic commands like `control.exe`.  
Some answers required background knowledge, but now I understand how hidden shares and Tools commands work.

---

## ■ 成果物（コード/図/ノート）
- コマンド例:
  ```powershell
  net share
  net view \\<targetIP>
  smbclient -L //<targetIP> -N
