# Week 1 演習

[Week 1 の概要](../README.md) · [解答例](../solutions/README.md) · [シラバス](../../README.md)

Week 1 はイントロの週なので、最初のセッションまでにやっておくべきことはありません。できれば、セッションのあとに基本演習の 3 つに取り組んでください。ハンズオンラボでは、Week 2 以降で使う regtest ノードをセットアップします。Week 2 までに動く状態にしておきましょう。

## 基本演習

### 1. Discord で自己紹介する

コホートの Discord チャンネルに、短い自己紹介を投稿します。

手順：

1. 3〜5 文で書きます。経歴（使っている言語、取り組んでいること）、参加した理由、ビットコインで作ってみたいものを 1 つ。
2. ほかの人の自己紹介を 3 つ以上読み、そのうち 1 つに返信します。

書き留めること：自分とは違う経歴を持つ人を 1 人選んでその名前と、コホートの期間中にその人に聞いてみたいことを 1 つ。

### 2. Hash Functions ツールで遊ぶ

Decoding Bitcoin の [Hash Functions ツール](https://bitcoindevs.xyz/decoding/hash-functions)を開きます。

手順：

1. 自分の名前を SHA-256 でハッシュし、出力をコピーします。
2. 名前を 1 文字だけ変えて（または大文字を小文字に変えて）、もう一度ハッシュします。
3. 2 つの出力を上下に並べ、同じ位置にある同じ 16 進数の文字がいくつあるか数えます。
4. 空文字列（入力なし）をハッシュします。出力は空になりますか。
5. とても長い文章（段落をまるごと貼り付けます）をハッシュします。出力の長さはどうなりますか。

書き留めること：

- 小さな変更 1 つで、64 文字の 16 進数のうち何文字が変わりましたか。
- 短い入力、空の入力、長い入力で、出力の長さはそれぞれいくつですか。
- 当てずっぽうで試す以外に、出力から自分の名前に戻る方法を思いつきますか。

### 3. mempool.space で本物のトランザクションを見る

[mempool.space](https://mempool.space) を開き、最近のブロックをクリックして、その中からアウトプットが 2 つ以上あるトランザクションをどれかクリックします。

手順：

1. インプットとアウトプットの数、それぞれの金額を書き留めます。
2. mempool.space に表示されている手数料と手数料率（sat/vB）を書き留めます。
3. インプットの合計とアウトプットの合計を出し、引き算をします。手数料と一致しますか。
4. どのアウトプットがおつり（送り主に戻るお金）らしいかを判断します。

書き留めること：おつりだと推測したアウトプットと、その理由。よく使われる手がかりは次のとおりです。切りのよい金額はたいてい支払いです。おつりは、インプットと同じ種類のアドレスに送られることがよくあります。おつりは「余り」の半端な金額であることが多いです。

## ハンズオンラボ（bitcoin-cli、regtest）

Bitcoin Core のインストール方法（リリース版バイナリ、または CMake でのビルド）を含むラボの全体は、[`bitcoin_core_cli.md`](bitcoin_core_cli.md) にあります。その中の演習 1、2、5 は最低限やってください。以下はセットアップを手早く確認するための短縮版です。

### ステップ 1：インストールを確認する

```bash
bitcoind -version
bitcoin-cli -version
```

**質問：** どのバージョンが入っていますか。このコホートでは v29 以降が必要です。

### ステップ 2：regtest ノードを起動する

```bash
bitcoind -regtest -daemon -txindex=1 -fallbackfee=0.0001
bitcoin-cli -regtest getblockchaininfo
```

**質問：** `chain`、`blocks`、`difficulty` はそれぞれ何ですか。このチェーンでは、なぜノートパソコンで 1 秒もかからずにブロックをマイニングできるのでしょうか。

### ステップ 3：ウォレットを作ってマイニングする

```bash
bitcoin-cli -regtest createwallet "mywallet"
bitcoin-cli -regtest -generate 101
bitcoin-cli -regtest getbalance
bitcoin-cli -regtest getbalances
```

**質問：** 101 ブロックをマイニングしたのに、`getbalance` は 50 BTC と表示します。残りはどこにありますか。`getbalances` の `immature` を見てください。

### ステップ 4：コマンドラインでハッシュする

ビットコインは SHA-256 を多用し、2 回続けてかけることもよくあります（「ダブルSHA-256」または hash256）。自分で試してみましょう。

```bash
echo -n "satoshi" | sha256sum
echo -n "satoshj" | sha256sum
python3 -c "import hashlib; d=hashlib.sha256(b'satoshi').digest(); print(hashlib.sha256(d).hexdigest())"
```

**質問：** 最初の 2 つの出力に、何か関係があるように見えますか。`echo` になぜ `-n` が必要なのでしょうか。（`-n` なしで試して比べてみてください。）

### ステップ 5：ブロックヘッダーを見る

```bash
bitcoin-cli -regtest getblockheader "$(bitcoin-cli -regtest getbestblockhash)"
```

**質問：** ヘッダーのフィールドのうち、ほかのデータ（別のブロック、トランザクション）を指しているのはどれですか。ブロック同士をつないでいるのは、どのハッシュ関数ですか。

## 発展課題

- [`bitcoin_core_cli.md`](bitcoin_core_cli.md) の演習 3 と 4（生トランザクションのデコード、ブロックの探索）をやってみましょう。
- 入力をほんの少しだけ変えて、出力 256 ビットのうち何ビットが反転するかを数えます。下の例は最後の文字を `i` から `j` に変えていて、入力で変わるのは 2 ビットだけです。小さな変更を 10 通り試してください。毎回、半分（128）に近い数になるはずです。これを雪崩効果と呼びます。

  ```bash
  python3 -c "
  import hashlib
  a = hashlib.sha256(b'satoshi').digest()
  b = hashlib.sha256(b'satoshj').digest()
  print(sum(bin(x ^ y).count('1') for x, y in zip(a, b)), 'of 256 bits differ')
  "
  ```
- [ビットコインのホワイトペーパー](https://bitcoin.org/bitcoin.pdf)のセクション 1 と 2 を読みます。「電子コイン」の定義は、mempool.space で見たものとどう対応していますか。
- 任意の [Interactive Developer Roadmap](https://bitcoindevs.xyz/decoding/interactive-roadmap) を試し、Week 10 までに理解したいトピックを 1 つ選びましょう。
