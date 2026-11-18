# Decoding Bitcoin - 10 週間の開発者向けスタディコホート

> **The Bitcoin Dev Project による [Decoding Bitcoin](https://bitcoindevs.xyz/decoding) を、グループで読み進めるスタディコホートです。トランザクションの一生から始めて、最後は自分で Taproot アウトプットを作り、それを使うところまで進みます。**

[![License: CC0-1.0](https://img.shields.io/badge/License-CC0_1.0-orange.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

> **日本語版について：** このページで日本語になっているのは、冒頭から「スケジュール」まで、Week 1 の節、そして末尾の運営ガイドです。Week 2〜10 の節は、[英語版シラバス](../../decoding-bitcoin/README.md#week-by-week-syllabus)を見てください。翻訳の状況は[日本語版トップ](../README.md)にまとめています。

---

## 概要

Decoding Bitcoin は、開発者向けの 10 週間のスタディコホートです。参加者は、[The Bitcoin Dev Project](https://bitcoindevs.xyz/) が作った [Decoding Bitcoin](https://bitcoindevs.xyz/decoding) の無料のレッスン、ツール、コーディング演習に取り組み、週に 1 回集まって学んだことを話し合います。

レッスン本体は Decoding Bitcoin にあり、ここではコピーせずにリンクしています。このフォルダは、そのレッスンのまわりに置く学習ガイドです。各週について、ディスカッション問題、ハンズオン演習、解答例、ファシリテーター用のスライドとノートがあります。これらはすべて Code Orange が作ったもので、CC0 で公開されています。フォークして、自分のコホートを開くことができます。

## 前提条件

- 少なくとも 1 つの言語で、コードを読み書きできること（演習には Python か JavaScript ができれば十分です）
- ビットコインが内部でどう動いているかへの好奇心。ビットコイン開発の経験は必要ありません
- 任意（ハンズオンラボ用）：regtest で動く [Bitcoin Core](https://bitcoincore.org/en/download/)（Week 1 で手順を説明します）と Python 3.8 以降

## 形式

| 項目 | 内容 |
|-----------|---------|
| **期間** | 10 週間 |
| **時間の目安** | 週 3〜5 時間（レッスン、演習、セッション） |
| **毎週のセッション** | 90 分のグループセッションを 1 回。ソクラテス式セミナーで進めます |
| **人数** | 10〜25 人 |
| **毎週やること** | Decoding Bitcoin のレッスン、自分が担当するディスカッション問題 1 つ、演習 3 つ |
| **最終プロジェクト** | Taproot（P2TR）アウトプットを作って使う（Week 10） |

### 1 週間の流れ

1. **セッションの前：** その週の Decoding Bitcoin のレッスンを読み、演習に取り組み、自分に割り当てられたディスカッション問題を準備します。
2. **セッション中：** オープニングの問いのあと、全員が自分の問題を説明し、ほかの人が反論します。1 人が画面を共有して、演習を 1 つ実演します。
3. **セッションのあと：** サマライザーが、学んだポイントと残った疑問を、コホートの Discord チャンネルに投稿します。

Week 1 はイントロの週です。参加者は来るだけでよく、宿題は Week 2 から始まります。

### セミナーの役割

役割は、毎週グループの中で持ち回りにします。

| 役割 | 仕事 |
|---|---|
| **ファシリテーター** | 時間を管理し、オープニングの問いを投げかけ、発言の少ない人にも声をかけます。講義はせず、導きます。 |
| **サマライザー**（まとめ役） | 学んだポイントと残った疑問をメモし、1 日以内に Discord に投稿します。 |
| **デビルズ・アドボケイト**（あえて反論する役） | 反対側のいちばん強い主張を代弁し、「なぜ別のやり方にしないのか」と問いかけます。 |
| **エクササイズ・ドライバー**（演習の実演役） | 画面を共有し、ハンズオン演習の 1 つをグループと一緒に進めます。 |

---

## スケジュール

日付は Code Orange の 2026〜27 年のコホートのものです（毎週月曜 19:00、UTC+8。日本時間では 20:00）。自分のコホートに合わせて変更してください。

| 週 | 日付 | テーマ | Decoding Bitcoin のレッスン |
|---|---|---|---|
| [1](./week-01/) | 11月16日 | [オリエンテーションと基礎](#week-1オリエンテーションと基礎) | Welcome!、Bitcoin History、UTXO vs Account Models |
| [2](./week-02/) | 11月23日 | [トランザクションの一生（英語）](../../decoding-bitcoin/README.md#week-2-how-a-transaction-lives) | Transactions roadmap、Transaction Lifecycle、Transaction Structure（1 回目の読み：主な部分） |
| [3（英語）](../../decoding-bitcoin/week-03/) | 11月30日 | [トランザクションの中身を、1 バイトずつ（英語）](../../decoding-bitcoin/README.md#week-3-inside-a-transaction-byte-by-byte) | Technical Foundation、Transaction Structure（2 回目の読み：すべてのフィールド） |
| [4（英語）](../../decoding-bitcoin/week-04/) | 12月7日 | [トランザクションを組み立てて手数料を払う（英語）](../../decoding-bitcoin/README.md#week-4-building-a-transaction-and-paying-the-fee) | Creating a Transaction、Fee Calculation |
| [5（英語）](../../decoding-bitcoin/week-05/) | 12月14日 | [署名とトランザクションの演習（英語）](../../decoding-bitcoin/README.md#week-5-signing-and-the-transaction-exercises) | Signing Transactions、Exercises (GitHub Classroom) |
| [6（英語）](../../decoding-bitcoin/week-06/) | 12月21日 | [スクリプトの基本（英語）](../../decoding-bitcoin/README.md#week-6-script-basics) | Scripts overview、P2PK: Pay To Public Key、P2PKH: Pay To Public Key Hash |
| [7（英語）](../../decoding-bitcoin/week-07/) | 12月28日 | [P2SH とマルチシグ（英語）](../../decoding-bitcoin/README.md#week-7-p2sh-and-multisig) | P2SH: Pay To Script Hash (BIP 16)、P2MS: Pay To Multisig |
| [8（英語）](../../decoding-bitcoin/week-08/) | 1月4日 | [プロジェクト：自分のビットコインスタックを作る（英語）](../../decoding-bitcoin/README.md#week-8-project-build-your-own-bitcoin-stack) | Project: Build your own bitcoin Stack |
| [9（英語）](../../decoding-bitcoin/week-09/) | 1月11日 | [Taproot：鍵と Schnorr（英語）](../../decoding-bitcoin/README.md#week-9-taproot-keys-and-schnorr) | Introduction to Taproot、Pay to Taproot、Schnorr & BIP340、Key-path Taproot |
| [10（英語）](../../decoding-bitcoin/week-10/) | 1月18日 | [Taproot スクリプトと修了（英語）](../../decoding-bitcoin/README.md#week-10-taproot-scripts-and-graduation) | Script-path Taproot、Taproot Signatures、Capstone: Build & Spend a P2TR |

Week 10 を終えたら、修了生は [After the cohort（英語）](../../decoding-bitcoin/after-the-cohort.md)に進みます。Bitcoin Core のアーキテクチャ、プルリクエストのレビュー、はじめてのオープンソースへの貢献を扱います。

## 各週のフォルダの中身

```
week-NN/
├── README.md        # その週の概要：レッスン、オープニングの問い、ディスカッション問題、演習
├── exercises/       # ハンズオン演習と regtest での bitcoin-cli ラボ（Week 3・4 は Python ラボも）
├── solutions/       # すべての問題と演習の解答例（まずは自分で解いてみてください）
├── slides/          # 90 分のセッション用のファシリテータースライド（Marp 形式の Markdown）
└── notes/           # 重要な考え方、よくある勘違い、セッションの進行表、用語集、参考資料
```

### スライドの表示方法

各週の `slides/slides.md` は [Marp](https://marp.app/) のスライドです。ふつうの Markdown なので GitHub でもそのまま読めて、本物のスライドにも変換できます。

- **VS Code：** 拡張機能 "Marp for VS Code" をインストールし、`slides.md` を開いて、プレビューのアイコンをクリックします。
- **コマンドライン：** `npx @marp-team/marp-cli@latest week-02/slides/slides.md --pdf`（`--html` や `--pptx` も使えます）。日本語版は `ja/decoding-bitcoin/` で実行してください。

スピーカーノートは、各スライドの下に `<!-- コメント -->` の形で書いてあり、Marp の発表者ビューに表示されます。

### Python ラボ

Week 3 と 4 には、本物のメインネットのトランザクションで採点する小さな Python ラボがあります。英語版のフォルダ（`decoding-bitcoin/`）で、Python 3.8 以降だけで実行できます（インストールは不要です）。

```bash
python3 week-03/check.py              # parse a real transaction, compute its txid and wtxid
python3 week-04/check.py              # weight, vsize, fee and fee rate
python3 week-03/check.py --solution   # see the reference solution pass
```

1 行目は本物のトランザクションを解析して txid と wtxid を計算し、2 行目はウェイト、vsize、手数料、手数料率を計算します。3 行目では、参考解答がテストに通るところを見られます。

---

## 週ごとのシラバス

### Week 1：オリエンテーションと基礎

**オープニングの問い：** ビットコインを友だちに 2 文で説明するとしたら、何と言いますか。そして、何を省きますか。

イントロの週です。コホートのメンバーと顔を合わせ、ダッシュボードの使い方を覚え、Decoding Bitcoin に慣れます。下のレッスンは、やさしい導入になっています。ウェルカムページ、ビットコインの歴史、そしてビットコインが「誰が何を持っているか」をどう記録しているか（口座の残高ではなく、UTXO と呼ばれるコインで記録します）です。よければセッションのあとに読んでください。**イントロの週なので、セッションの前の宿題はありません。**

**レッスン：**

- [Welcome!](https://bitcoindevs.xyz/decoding/welcome)
- [Bitcoin History](https://bitcoindevs.xyz/decoding/bitcoin-history)
- [UTXO vs Account Models](https://bitcoindevs.xyz/decoding/utxo)

**ディスカッション問題：**

1. それまでのデジタルキャッシュの試み（DigiCash、b-money、Bit Gold）には解けず、ビットコインが解いた問題は何ですか。
2. Bitcoin History のレッスンから出来事を 1 つ選び、それが今のビットコインの仕組みにとってなぜ重要だったのかを説明してください。
3. ハッシュ関数とは何ですか。ビットコインが頼りにしている性質を 3 つ挙げ、それぞれがどこで使われているかを答えてください。
4. UTXO モデルを自分の言葉で説明してください。なぜ口座の残高はどこにも保存されていないのでしょうか。
5. アカウントモデルと比べたときの UTXO の長所と短所を、1 つずつ挙げてください。
6. なぜ「Don't trust, verify（信頼するな、検証せよ）」と言われるのでしょうか。自分で検証できるものは何で、ふだん信頼に任せているものは何ですか。

**週のフォルダ：** [`week-01/`](./week-01/) · [演習](./week-01/exercises/README.md) · [スライド](./week-01/slides/slides.md) · [ノート](./week-01/notes/README.md) · [解答例](./week-01/solutions/README.md)

---

### Week 2〜10

まだ翻訳していません。[英語版シラバスの Week 2 以降](../../decoding-bitcoin/README.md#week-2-how-a-transaction-lives)を見てください。Week 2 のフォルダは日本語版があります：[`week-02/`](./week-02/)。

---

## コホートのあとに

修了生には、次のことをおすすめしています。

1. **Bitcoin Core をもっと深く知る** - [After the cohort（英語）](../../decoding-bitcoin/after-the-cohort.md)に取り組みます。コードベース、テストフレームワーク、本物のプルリクエストのレビューを扱います
2. **はじめての貢献をする** - ドキュメント、テスト、レビュー、小さな修正、どれも立派な貢献です
3. **レビュークラブに参加する** - [Bitcoin Core PR Review Club](https://bitcoincore.reviews/) が毎週開かれています
4. **学び続ける** - このリポジトリの [Privacy Track（英語）](../../privacy-track/) と [Bitcoin Dojo（英語）](../../bitcoin-dojo/)
5. **フェローシップや助成金に応募する** - Chaincode Labs、Summer of Bitcoin、Btrust、Vinteum、Brink など、ビットコイン開発者向けの助成プログラム
6. **次のコホートのメンターになる** - これからの Decoding Bitcoin コホートでファシリテーターを務めます

---

## ファシリテーターガイド

### コホートの前に

- [ ] 開始日と毎週のセッションの時間を決め、上のスケジュールの表を更新する
- [ ] 参加申し込みを受け付け、週ごとにスレッドを分けた Discord チャンネルを用意する
- [ ] Week 1 の[ノート](./week-01/notes/README.md)と[スライド](./week-01/slides/slides.md)を読む
- [ ] 共同ホストを 1〜2 人集める（以前の修了生が理想的です）

### 毎週

- [ ] 参加者 1 人ひとりにディスカッション問題を 1 つ割り当て、セミナーの役割を交代する
- [ ] 前回のセッションのあとに、その週のレッスンと演習を投稿する
- [ ] その週の `notes/`（進行表とよくある勘違い）にざっと目を通し、`slides/` を使って進行する
- [ ] 参加できない人のために、セッションを録画する
- [ ] サマライザーの投稿を確認し、Discord で残った疑問に答える
- [ ] 2 週間発言のない人に、声をかける

### コホートのあとに

- [ ] フィードバックを集める（匿名のアンケート）
- [ ] 最終プロジェクトをみんなで称え、（本人の許可を得て）共有する
- [ ] その後 3〜6 か月、修了生のはじめての貢献を追いかける
- [ ] フィードバックをもとにこのカリキュラムを更新し、プルリクエストを出す

---

## クレジット

このコホートで使うレッスン、ツール、コーディング演習は、[The Bitcoin Dev Project](https://bitcoindevs.xyz/) による [Decoding Bitcoin](https://bitcoindevs.xyz/decoding) です。このコホートを開くときは、彼らを応援し、クレジットを表記してください。この学習ガイド（問題、演習、解答例、スライド、ノート）は Code Orange が作ったものです。

## ライセンス

この学習ガイドは [CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/) のもとでパブリックドメインに提供されています。フォークも、翻訳も、教えるのに使うのも自由で、許可はいりません。Decoding Bitcoin のレッスンそのものは作者のものであり、このライセンスの対象ではありません。
