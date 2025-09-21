# 学習ログ / Learning Log

## ■ 日付（JST）/ Date  
2025/09/21  

## ■ 学習テーマ / Topic  
TryHackMe - DNS in detail  

## ■ 目的 / Goal (JP→EN one-liner)  
- JP: DNSの仕組みと主要なレコードについて理解する  
- EN: Understand the mechanism of DNS and its main record types  

---

## ■ 今日やったこと（一次メモ・JP中心）  
- DNS (Domain Name System) とは何かを学んだ  
- ドメインの構造（サブドメイン、gTLD、ccTLD）を整理した  
- DNSレコードの種類（A, AAAA, CNAME, MX, TXT）を確認した  
- DNSの問い合わせの流れ（Recursive, Authoritative, TTL）を学んだ  
- `dig` コマンドでAレコードやTXTレコードを調べる演習をした  

---

## ■ 参照した資料・リンク  
- [TryHackMe: DNS in detail](https://tryhackme.com/room/dnsindetail)  

---

## ■ 自分の理解で怪しい所（要修正ポイント）  
- 「TMX」レコードと書いたが、正しくは「TXT」レコード  
- Recursive DNSとAuthoritative DNSの役割の違いを正確に説明できなかった  
  - Recursive: ユーザーの代わりに問い合わせを繰り返すサーバー  
  - Authoritative: ドメインの正しい情報を保持するサーバー  
- TTLを単なる数値と理解していたが、正しくは「キャッシュが保持される時間」を意味し、ネットワーク効率に関わる  

---

## ■ 英語の簡単要約  
Today I studied DNS in detail on TryHackMe.  
I learned the structure of domains (gTLD, ccTLD), record types (A, AAAA, CNAME, MX, TXT), and the process of DNS resolution including recursive and authoritative servers.  
I also practiced using the `dig` command to retrieve records and observed the role of TTL in caching.  

---

## ■ 成果物（コード/図/ノート）  
- 簡易図解：  
bash
  dig TXT website.thm
