
# 学習ログ / Learning Log（JST）

■ 日付（JST）/ Date  
2025/09/18

---

■ 学習テーマ / Topic  
TryHackMe: Pre Security  
- Intro to LAN  
- OSI Model

---

■ 目的 / Goal (JP→EN one-liner)  
JP: LAN・OSI・ARP・DHCP・スイッチ/ルータ・TCP/UDPを用語レベルで正確に説明できるようにする。  
EN: Be able to accurately explain LAN/OSI/ARP/DHCP, switch/router, and TCP/UDP at the terminology level.

---

■ 今日やったこと（一次メモ・JP中心）  
- 用語ざっと確認：LAN, ARP, DHCP, switch, router, TCP, UDP  
- OSIモデル（下層→上層）：Physical, **Data Link**, Network, Transport, Session, Presentation, Application  
- 役割の対応：  
  - L2（Data Link）＝MAC・スイッチ・同一LAN内転送  
  - L3（Network）＝IP・ルーティング・ネットワーク間中継  
  - Transport＝TCP/UDP（ポート、信頼性/順序や軽量性）  

---

■ 参照した資料・リンク  
- TryHackMe: *Intro to LAN*  
- TryHackMe: *OSI Model*  
（※必要に応じて受講環境のURLを追記）

---

■ 自分の理解で怪しい所（要修正ポイント）  
- 「OSIの層が1つ思い出せない」  
  - **正**：抜けていたのは **Data Link（第2層）**。同一ネットワーク内でMACアドレスを用いたフレーム転送を担い、スイッチが主役。  
- 「ARP/DHCP/TCP/UDP/スイッチ/ルータを口頭で説明できる自信がない」  
  - **ARP**：同一LAN内で **IP→MAC** を解決する仕組み。ARP Requestはブロードキャスト、Replyはユニキャスト。ポート番号の概念はない（TCP/UDPではない）。  
  - **DHCP**：IP・DNS・デフォルトゲートウェイ等を自動配布（アプリ層）。**UDP 67/68** を使用。流れは **DORA**（Discover→Offer→Request→Acknowledge）。  
  - **Switch**：L2機器。MACテーブルで同一L2セグメントの転送を最適化。原則としてブロードキャストドメインは分割しない（VLANで論理分割は可能）。  
  - **Router**：L3機器。IP/ルーティングで**異なるネットワーク間**を中継し、ブロードキャストドメインを分割。NAT/ACL等の機能を持つことが多い。  
  - **TCP**：コネクション確立（3-way）、再送/順序/輻輳制御あり＝**信頼性重視**（例：HTTPS/SSH/SMTP）。  
  - **UDP**：コネクションレスで制御が少ない＝**軽量・低遅延**（例：DNS/VoIP/ゲーム）。「必ず速い」ではなくオーバーヘッドが低い分有利になりやすい、が状況依存。  
- 「LANの範囲感」  
  - **正**：家庭/オフィス等のローカル範囲。端末はスイッチで接続し、外部ネットワークへは**デフォルトゲートウェイ（ルータ）**経由で出る。

---

■ 英語の簡単要約（あれば下書き）  
Today I studied TryHackMe’s *Intro to LAN* and *OSI Model* rooms. I filled the missing OSI layer (Data Link), reviewed how ARP resolves IP→MAC on a LAN, how DHCP works via the DORA process over UDP 67/68, the L2 vs L3 roles of switches/routers, and the trade-offs between TCP (reliable) and UDP (lightweight).

---

■ 成果物（コード/図/ノート）  
**ARPフローのメモ**  

**OSI↔TCP/IP 早見表（自作ノート）**  
- OSI: Physical / **Data Link** / Network / Transport / Session / Presentation / Application  
- TCP/IP: Link / Internet / Transport / Application  
  - 主な対応：L2↔Link、L3↔Internet、TCP/UDP↔Transport、HTTP/DNS/DHCP↔Application

---

■ 所要時間 / Time spent  
２時間

---

■ 次にやりたいこと（下書き）  
- TryHackMe Pre Security を**毎回1ルーム**ずつ継続（例：*Packets & Frames* / *HTTP in detail*）。  
- **手を動かす検証**：  
  - `arp -a` で ARPテーブル観察（IPとMACの対応）。  
  - ルータのDHCP割当一覧を確認し、DORAをイメージ化。  
  - 可能なら Wireshark で `arp` / `bootp` フィルタを使ってトレース取得。  
- **用語30秒プレゼン**（JP/EN）：LAN/ARP/DHCP/Switch/Router/TCP/UDP を見ずに説明。  
- **暗唱**：OSI順（下→上）と各層キーワード（MAC/IP/TCP-UDP 等）を1枚メモで固定。
