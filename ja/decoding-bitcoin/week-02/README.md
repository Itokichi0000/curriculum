# Week 02：トランザクションの一生

[← Week 1](../week-01/) · [シラバス](../README.md) · [Week 3（英語）→](../../../decoding-bitcoin/week-03/)

> [Decoding Bitcoin シラバス（英語）](../../../decoding-bitcoin/README.md#week-2-how-a-transaction-lives)の一部です。レッスン本体は The Bitcoin Dev Project の [Decoding Bitcoin](https://bitcoindevs.xyz/decoding)（英語）にあります。このフォルダは、Code Orange がその週のために用意した学習ガイドです。

**オープニングの問い：** ビットコインの支払いが本当に確定するのはいつで、それを決めるのは誰でしょうか。

1 つの支払いを、それを組み立てるウォレットから、メンプールを通って、ブロックに入るまで追いかけます。そのあと、トランザクションが何でできているのかをはじめて見ます。バージョン、インプット、アウトプット、ロックタイムです。来週はバイト単位まで掘り下げるので、バイトレベルの細かい点はまだ気にしなくてかまいません。

## レッスン（Decoding Bitcoin）

- [Transactions roadmap](https://bitcoindevs.xyz/decoding/roadmap)
- [Transaction Lifecycle](https://bitcoindevs.xyz/decoding/transaction-lifecycle)
- [Transaction Structure（1 回目の読み：主な部分）](https://bitcoindevs.xyz/decoding/transaction-structure)

**ツールと追加教材：**

- [ツール：Reorg Calculator](https://bitcoindevs.xyz/decoding/reorg-calculator)
- [ツール：Transaction Decoder](https://bitcoindevs.xyz/decoding/transaction-decoder)

## ディスカッション問題

参加者は 1 人 1 問を担当し、説明できるように準備してきます。解答例は [`solutions/`](solutions/README.md) にありますが、まずは自分で考えてみてください。

1. 支払いの一生をたどってください。誰が組み立て、誰がリレーし、誰が検証し、いつ承認されますか。
2. メンプールとは何ですか。なぜ全員が共有する 1 つのメンプールは存在しないのでしょうか。
3. チェーンの再編成（リオーグ）とは何ですか。なぜ店は 2 承認以上を待つことがあるのでしょうか。
4. なぜおつりは、元のアウトプットを一部だけ使うのではなく、新しいアウトプットとして送り主に戻るのでしょうか。
5. トランザクションの主な部分を順番に挙げ、それぞれの役割を 1 行で述べてください。
6. インプットは具体的に何を指していますか。なぜそれだけで、お金の出どころを証明できるのでしょうか。

## 演習

1. 自分が作ったのではないトランザクションが、未承認から 1 承認になるまでを mempool.space で見守ります。どれくらい時間がかかりましたか。（[mempool.space](https://mempool.space)）
2. Reorg Calculator を使います。ハッシュレートの 10% を持つ攻撃者が、1 承認、3 承認、6 承認のあとに支払いを覆せる確率はどれくらいですか。（[Reorg Calculator](https://bitcoindevs.xyz/decoding/reorg-calculator)）
3. 生トランザクションを Transaction Decoder に貼り付け、バージョン、インプット、アウトプット、ロックタイムを見つけます。各インプットは何を指していますか。（[Transaction Decoder](https://bitcoindevs.xyz/decoding/transaction-decoder)）

regtest での bitcoin-cli ラボなど、さらに手を動かす課題は [`exercises/`](exercises/README.md) にあります。

## このフォルダの中身

| フォルダ | 内容 |
|---|---|
| [`exercises/`](exercises/README.md) | 今週のハンズオン演習 |
| [`solutions/`](solutions/README.md) | 問題と演習の解答例（まずは自分で解いてみてください） |
| [`slides/`](slides/slides.md) | セッション用のファシリテータースライド（[スライドの表示方法](../README.md#スライドの表示方法)） |
| [`notes/`](notes/README.md) | 重要な考え方、よくある勘違い、セッションの進行表、参考資料 |
