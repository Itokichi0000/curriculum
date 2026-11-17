# 用語集（訳語の統一表）

[日本語版トップ](README.md)

日本語版で使う訳語をここで統一します。新しい週を訳すときは、まずこの表を確認し、足りない用語を追加してください。

方針：

- 文体は「です・ます」体にします。
- コマンド、RPC名、JSONのフィールド名（`vin`、`scriptPubKey` など）、エラーメッセージは英語のまま残します。
- Decoding Bitcoin（bitcoindevs.xyz）のレッスン名は、リンク先が英語なので英語のまま残します。
- 日本のビットコインコミュニティでカタカナ表記が定着している用語は、カタカナを使います。

## 基本

| 英語 | 日本語 | メモ |
|---|---|---|
| transaction | トランザクション | |
| input / output | インプット / アウトプット | |
| UTXO (unspent transaction output) | UTXO（未使用トランザクションアウトプット） | 2回目以降は「UTXO」 |
| UTXO set | UTXOセット | |
| coin | コイン | UTXO 1つを指す場合もそのまま「コイン」 |
| change / change output | おつり / おつりのアウトプット | |
| fee / fee rate | 手数料 / 手数料率 | 単位 sat/vB はそのまま |
| balance | 残高 | |
| account model | アカウントモデル | 残高を持つ「口座」は「口座」と訳す |
| wallet | ウォレット | |
| descriptor wallet | ディスクリプターウォレット | |
| address | アドレス | |
| private key / public key | 秘密鍵 / 公開鍵 | |
| signature | 署名 | |
| full node | フルノード | |
| peer | ピア | |
| block / block header | ブロック / ブロックヘッダー | |
| block height | ブロック高 | |
| genesis block | ジェネシスブロック | |
| blockchain / chain | ブロックチェーン / チェーン | |

## マイニングと合意

| 英語 | 日本語 | メモ |
|---|---|---|
| proof of work | プルーフ・オブ・ワーク | |
| miner / mining | マイナー / マイニング | |
| hashrate | ハッシュレート | |
| target / difficulty | ターゲット / 難易度 | |
| nonce | ナンス | |
| coinbase transaction | コインベーストランザクション | |
| coinbase maturity | コインベースの成熟（coinbase maturity） | 2回目以降は「コインベースの成熟」 |
| block subsidy / block reward | ブロック補助金 / ブロック報酬 | 報酬＝補助金＋手数料 |
| halving | 半減期 | |
| consensus rules | コンセンサスルール | |
| policy | ポリシー | ノードごとのリレー方針 |
| soft fork | ソフトフォーク | |
| reorg (chain reorganisation) | リオーグ（チェーンの再編成） | 2回目以降は「リオーグ」 |
| confirmation | 承認 | 「1承認」「6承認」 |
| double spend | 二重支払い | |
| accumulated work | 累積ワーク | |

## トランザクションの中身

| 英語 | 日本語 | メモ |
|---|---|---|
| version | バージョン | |
| locktime | ロックタイム | |
| sequence | シーケンス | |
| outpoint | アウトポイント | `txid:vout` |
| locking script (scriptPubKey) | ロックスクリプト（scriptPubKey） | |
| unlocking data (scriptSig / witness) | アンロックデータ（scriptSig / witness） | |
| witness | witness | カタカナにせず英語のまま |
| marker / flag | マーカー / フラグ | |
| raw transaction | 生トランザクション | |
| txid / wtxid | txid / wtxid | |
| malleability | マリアビリティ（展性） | |
| dust | ダスト | |
| coin selection | コインセレクション | |
| relative timelock | 相対タイムロック | |
| weight / virtual size (vsize) | ウェイト / 仮想サイズ（vsize） | |

## メンプールとリレー

| 英語 | 日本語 | メモ |
|---|---|---|
| mempool | メンプール | |
| relay | リレー | |
| broadcast | ブロードキャスト | |
| eviction | 追い出し | |
| replacement (RBF) | 置き換え（RBF） | |
| parent / child (transaction) | 親 / 子（トランザクション） | |
| ancestor / descendant | 祖先 / 子孫 | |
| block template | ブロックテンプレート | |

## ハッシュ

| 英語 | 日本語 | メモ |
|---|---|---|
| hash function | ハッシュ関数 | |
| double SHA-256 (hash256) | ダブルSHA-256（hash256） | |
| preimage resistance | 原像計算困難性（一方向性） | |
| collision resistance | 衝突耐性 | |
| avalanche effect | 雪崩効果 | |
| Merkle tree / Merkle root | マークルツリー / マークルルート | |

## コホートの運営

| 英語 | 日本語 | メモ |
|---|---|---|
| cohort | コホート | |
| session | セッション | 週1回90分の集まり |
| syllabus | シラバス | |
| opening question | オープニングの問い | |
| discussion question | ディスカッション問題 | |
| question owner | 問題の担当者 | |
| core exercises | 基本演習 | |
| hands-on lab | ハンズオンラボ | |
| stretch tasks | 発展課題 | |
| model answer | 解答例 | |
| Facilitator | ファシリテーター | |
| Summariser | サマライザー（まとめ役） | |
| Devil's advocate | デビルズ・アドボケイト（あえて反論する役） | |
| Exercise driver | エクササイズ・ドライバー（演習の実演役） | |
| common mix-ups | よくある勘違い | |
| takeaways | 学んだポイント | |
