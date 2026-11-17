# Code Orange Dev School カリキュラム 日本語版

[Code Orange Dev School のカリキュラム](https://github.com/code-orange-dev/curriculum)を日本語に翻訳したものです。原文は CC0 1.0（パブリックドメイン）で公開されており、この日本語版も同じく CC0 1.0 です。自由にフォーク、改変、利用できます。

フォルダ構成は原文と同じです。`ja/decoding-bitcoin/week-01/` は、原文の `decoding-bitcoin/week-01/` に対応します。

## 翻訳の状況

| プログラム | 対象 | 状況 |
|---|---|---|
| Decoding Bitcoin | [Week 1：オリエンテーションと基礎](decoding-bitcoin/week-01/README.md) | 翻訳済み |
| Decoding Bitcoin | [Week 2：トランザクションの一生](decoding-bitcoin/week-02/README.md) | 翻訳済み |
| Decoding Bitcoin | シラバス（[英語](../decoding-bitcoin/README.md)）、Week 3〜10 | 未着手 |
| その他のプログラム | Bitcoin Dojo、rawBit、Sovereign Bitcoiner、Privacy Track、Nostr ワークショップなど | 未着手 |

まだ訳していないページへのリンクは、原文（英語）に飛ぶようにしてあります。

## 翻訳元

- 翻訳元のコミット：[`7f660c3`](https://github.com/code-orange-dev/curriculum/commit/7f660c3cdfe4d5b657c3d232222afe5194044d37)（2026-11-17、本家 `main`）
- 原文が更新されたら、`git diff 7f660c3..upstream/main -- decoding-bitcoin/week-01 decoding-bitcoin/week-02` で差分を確認し、日本語版に反映してから、上のコミットを書き換えてください。

## 原文との違い

Week 1・2 のラボを Bitcoin Core v32.1（regtest）で最初から最後まで動かして確認しました。その中で見つけた次の修正を、日本語版では先に反映しています。同じ内容を本家にもプルリクエストとして提案しています（ブランチ `fix/decoding-bitcoin-weeks-1-2`）。

| 場所 | 修正の内容 |
|---|---|
| Week 1 `bitcoin_core_cli.md`（ソースからビルド） | v30 以降は Cap'n Proto がないと `cmake -B build` が止まるため、`libcapnp-dev capnproto` をインストール手順に追加。`libevent-dev` が必要なのは v31 までと追記。最新リリースのタグを探すコマンドをバージョン順の表示に変更 |
| Week 1 `exercises/README.md`（発展課題） | 「1ビット変える」と書かれていたが、例の `i`→`j` は入力の 2 ビットが変わるため、説明を修正 |
| Week 2 `notes/README.md` | `-rpcwallet` を付け忘れたときのエラー文を、v29 以降の実際の文言に修正 |
| Week 2 `solutions/README.md`（ステップ8） | おつりを忘れたトランザクションは 141 vB ではなく 110 vB のため、チェックをすり抜ける手数料の上限を約 0.011 BTC に修正 |
| Week 2 `exercises/README.md`（ステップ1） | 解答例は空のチェーンを前提にしているため、Week 1 のチェーンが残っている場合は作り直すよう明記 |

このほか、日本語版だけの調整として、訳語は[用語集](GLOSSARY.md)で統一しています。

## 翻訳に参加するには

1. [用語集](GLOSSARY.md)を読み、訳語をそろえます。
2. 原文と同じパスに日本語のファイルを置きます（例：`ja/decoding-bitcoin/week-03/README.md`）。
3. コマンド、フィールド名、エラーメッセージは英語のまま残します。
4. 原文の誤りに気づいたら、日本語版だけを直さず、本家にも英語でプルリクエストを出します。
