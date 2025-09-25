学習ログ / Study Log
■ 日付（JST）/ Date

2025/09/25

■ 学習テーマ / Topic

TryHackMe — Putting It All Together（Web全体の流れの統合理解）

■ 目的 / Goal (JP→EN one-liner)

JP: Web通信の全体像をつかみ、主要コンポーネントの役割を自分の言葉で説明できるようにする。

EN: Learn how the individual components of the web work together to deliver your favorite websites, and be able to explain each role clearly.

■ 今日やったこと（一次メモ・JP中心）

クライアント→サーバの一連の流れを概観：DNS解決 → TCP(3WHS) → TLS(SNI/証明書検証) → HTTP要求/応答。

経路上の装置と役割：CDN（配信/キャッシュ）、リバースプロキシ、WAF（L7防御）、ネットワーク/ホストFW。

アプリ側：仮想ホスト（Hostヘッダ/SNI）、静的/動的コンテンツ、バックエンド（DB/キャッシュ）連携。

自覚：各段階のつながりと**配置（どこにあるか）**が曖昧。

■ 参照した資料・リンク

TryHackMe: Putting It All Together（学習ルーム）

コマンド例：dig, nslookup, traceroute/tracert, curl -I, openssl s_client -connect host:443 -servername host

■ 自分の理解で怪しい所（要修正ポイント）

誤記：「IP adress」→ IP address。

順序の固定観念：DNS→FW→ポートの“固定順序”ではない。FW/WAF/CDN/Proxyは複層に存在し得る。

Virtual Hosts：HTTPはHostヘッダで、TLSはSNIでドメイン識別。

CDN vs WAF：CDN=配信最適化/キャッシュ、WAF=L7で攻撃検知/遮断。

静的/動的：生成方法とキャッシュ適性が主な違い（動的はキャッシュ戦略が重要）。

■ 正しい説明（ショートメモ）

標準フロー：URL入力 → DNS解決 → TCP 3WHS →（HTTPSなら）TLS → HTTP要求 →（CDN/WAF/Reverse Proxy通過）→ アプリ → 応答 → キャッシュ。

ポート：80(HTTP)/443(HTTPS)など。OSが該当ポートで待機中のプロセス（nginx等）へ渡す。

WAF：L7でHTTPペイロードを解析（SQLi/XSS対策）。L3/4中心のFWとは別役割。

CDN：エッジから配布し遅延/負荷を低減。静的資産に強いが動的も一部対応可。

■ 英語の簡単要約（2–3文）

I reviewed the end-to-end web flow: DNS resolution, TCP/TLS handshakes, and HTTP over ports like 80/443. I clarified roles of CDN (delivery/caching) and WAF (L7 protection), and how virtual hosts use the Host header and TLS SNI. I still need hands-on practice to connect these steps confidently.

■ 成果物（コード/図/ノート）

簡易フロー図とコマンド実行計画のノートを作成（次回は実行結果を貼付）。

