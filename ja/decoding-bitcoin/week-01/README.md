# Week 01：オリエンテーションと基礎

[シラバス（英語）](../../../decoding-bitcoin/README.md) · [Week 2 →](../week-02/)

> [Decoding Bitcoin シラバス（英語）](../../../decoding-bitcoin/README.md#week-1-orientation-and-foundations)の一部です。レッスン本体は The Bitcoin Dev Project の [Decoding Bitcoin](https://bitcoindevs.xyz/decoding)（英語）にあります。このフォルダは、Code Orange がその週のために用意した学習ガイドです。

> **イントロの週です。** 最初のセッションには、何も準備せずに参加してください。お互いに自己紹介をして、コホートの進め方とダッシュボードの使い方を説明し、今週のトピックを一緒に見ていきます。宿題は Week 2 から始まります。11月23日（月）までに、レッスン、自分の担当問題、演習に取り組みます。

**オープニングの問い：** ビットコインを友だちに 2 文で説明するとしたら、何と言いますか。そして、何を省きますか。

イントロの週です。コホートのメンバーと顔を合わせ、ダッシュボードの使い方を覚え、Decoding Bitcoin に慣れます。下のレッスンは、やさしい導入になっています。ウェルカムページ、ビットコインの歴史、そしてビットコインが「誰が何を持っているか」をどう記録しているか（口座の残高ではなく、UTXO と呼ばれるコインで記録します）です。よければセッションのあとに読んでください。

## レッスン（Decoding Bitcoin）

- [Welcome!](https://bitcoindevs.xyz/decoding/welcome)
- [Bitcoin History](https://bitcoindevs.xyz/decoding/bitcoin-history)
- [UTXO vs Account Models](https://bitcoindevs.xyz/decoding/utxo)

**ツールと追加教材：**

- [ツール：Hash Functions](https://bitcoindevs.xyz/decoding/hash-functions)
- [任意：Interactive Developer Roadmap](https://bitcoindevs.xyz/decoding/interactive-roadmap)

## ディスカッション問題

参加者は 1 人 1 問を担当し、説明できるように準備してきます。解答例は [`solutions/`](solutions/README.md) にありますが、まずは自分で考えてみてください。

1. それまでのデジタルキャッシュの試み（DigiCash、b-money、Bit Gold）には解けず、ビットコインが解いた問題は何ですか。
2. Bitcoin History のレッスンから出来事を 1 つ選び、それが今のビットコインの仕組みにとってなぜ重要だったのかを説明してください。
3. ハッシュ関数とは何ですか。ビットコインが頼りにしている性質を 3 つ挙げ、それぞれがどこで使われているかを答えてください。
4. UTXO モデルを自分の言葉で説明してください。なぜ口座の残高はどこにも保存されていないのでしょうか。
5. アカウントモデルと比べたときの UTXO の長所と短所を、1 つずつ挙げてください。
6. なぜ「Don't trust, verify（信頼するな、検証せよ）」と言われるのでしょうか。自分で検証できるものは何で、ふだん信頼に任せているものは何ですか。

## 演習

1. コホートの Discord チャンネルで自己紹介をします。これまでの経歴、参加した理由、作ってみたいものを書いてください。（[Discord](https://discord.gg/xd6dmPF9bA)）
2. Hash Functions ツールを使います。自分の名前をハッシュし、次に 1 文字だけ変えてみます。出力はどれくらい変わりますか。（[Hash Functions ツール](https://bitcoindevs.xyz/decoding/hash-functions)）
3. mempool.space で最近のブロックを開き、トランザクションを 1 つ選んで、インプット、アウトプット、手数料をメモします。どのアウトプットがおつりだと思いますか。その理由は何ですか。（[mempool.space](https://mempool.space)）

regtest での bitcoin-cli ラボなど、さらに手を動かす課題は [`exercises/`](exercises/README.md) にあります。

## このフォルダの中身

| フォルダ | 内容 |
|---|---|
| [`exercises/`](exercises/README.md) | 今週のハンズオン演習 |
| [`solutions/`](solutions/README.md) | 問題と演習の解答例（まずは自分で解いてみてください） |
| [`slides/`](slides/slides.md) | セッション用のファシリテータースライド（[スライドの表示方法（英語）](../../../decoding-bitcoin/README.md#presenting-the-slides)） |
| [`notes/`](notes/README.md) | 重要な考え方、よくある勘違い、セッションの進行表、参考資料 |
