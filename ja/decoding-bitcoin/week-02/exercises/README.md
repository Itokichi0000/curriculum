# Week 2 演習

[Week 2 の概要](../README.md) · [解答例](../solutions/README.md) · [シラバス（英語）](../../../../decoding-bitcoin/README.md)

月曜までに、基本演習の 3 つをやってください。考え方が本当に身につくのはハンズオンラボなので、少なくともステップ 1〜7 には挑戦しましょう。答えは書き留めておきます。グループの前で説明することになるからです。

## 基本演習

### 1. mempool.space でトランザクションが承認されるのを見守る

1. [mempool.space](https://mempool.space) を開きます。上部のバーの左側にあるブロックは、メンプールから組み立てた「予測」ブロックです。右側にあるのが、マイニング済みのブロックです。
2. いちばん手前の予測ブロックをクリックし、上のほうにあるトランザクションを 1 つ選びます（手数料率が高いので、すぐに承認されるはずです）。時刻をメモし、txid をコピーします。
3. トランザクションのページを開いたままにします。"Confirmed" と表示されて 1 承認になるまで待ちます。
4. 任意：もっと後ろにある予測ブロックの下のほうから、2 つ目のトランザクション（手数料率が低いもの）を選び、同じように追いかけます。

書き留めること：

- txid、手数料率（sat/vB）、最初に見た時刻、承認された時刻。
- どれくらい時間がかかったか。ブロック間隔の平均である 10 分と比べてどうだったか。
- 手数料の低いトランザクションを追いかけた場合：次のブロックで承認されましたか。されなかったなら、なぜでしょうか。

### 2. Reorg Calculator を使う

[Reorg Calculator](https://bitcoindevs.xyz/decoding/reorg-calculator) を開きます。

1. 攻撃者のハッシュレートの割合を 10% に設定します。
2. 1 承認、3 承認、6 承認のあとに、支払いの取り消しが成功する確率を読み取ります。
3. 30% と 45% でも繰り返します。

書き留めること：

- 小さな表：攻撃者のハッシュレート（10%、30%、45%）と承認数（1、3、6）。
- 10% のとき、承認が増えるとリスクはどれくらい速く下がりますか。45% のときはどうですか。
- コーヒー、ノートパソコン、車を引き渡す前に、それぞれ何承認ほしいですか。理由も添えてください。

### 3. Transaction Decoder でトランザクションを読む

[Transaction Decoder](https://bitcoindevs.xyz/decoding/transaction-decoder) を開きます。

1. 生トランザクションを用意します。ツールにある例を使うか、mempool.space で好きなトランザクションを開いて生の 16 進数データをコピーするか（mempool.space では、トランザクションの詳細の中にあります）、自分の regtest ノードのものを使います（`bitcoin-cli -regtest getrawtransaction <txid>`）。
2. デコーダーに貼り付けます。
3. 4 つの主な部分を見つけます：バージョン、インプット、アウトプット、ロックタイム。
4. 各インプットについて、それが指している txid とアウトプットのインデックス（vout）を見つけます。
5. その前のトランザクションの 1 つを mempool.space で調べ、使われているアウトプットを見つけます。

書き留めること：バージョン番号、インプットとアウトプットの数、ロックタイム。そして各インプットについて、"txid:vout" と、それが使うアウトプットの金額。

## ハンズオンラボ（bitcoin-cli、regtest）

Bitcoin Core v29 以降が必要です。まだインストールしていない場合は、[`week-01/exercises/bitcoin_core_cli.md`](../../week-01/exercises/bitcoin_core_cli.md) に従ってください。一部のステップでは、JSON からフィールドを取り出すために `jq` を使います。`sudo apt install jq`（Linux）または `brew install jq`（macOS）でインストールできます。

このラボでは、`$TXID` のようなシェル変数に値を入れておきます。新しいターミナルを開いた場合は、もう一度設定してください。

### ステップ 1：ウォレットを 2 つ持つ、新しい regtest ノードを起動する

古い regtest チェーンが残っている場合（たとえば Week 1 のラボのもの）は、ブロック高や金額が解答例と一致するよう、最初から作り直してください。`bitcoin-cli -regtest stop` を実行してから、regtest フォルダを削除します（Linux では `~/.bitcoin/regtest`、macOS では `~/Library/Application Support/Bitcoin/regtest`）。

```bash
bitcoind -regtest -daemon -txindex=1 -fallbackfee=0.0001
bitcoin-cli -regtest createwallet alice
bitcoin-cli -regtest createwallet bob
bitcoin-cli -regtest -rpcwallet=alice -generate 101
bitcoin-cli -regtest -rpcwallet=alice getbalance
```

ウォレットを 2 つ読み込んでいる場合、ウォレットのコマンドにはすべて `-rpcwallet=<name>` が必要です。

**質問：** アリスの残高は 50 BTC です。これはどのブロックの報酬ですか。ほかの 100 個の報酬は、なぜまだ使えないのでしょうか。

### ステップ 2：空のメンプールを見る

```bash
bitcoin-cli -regtest getmempoolinfo
bitcoin-cli -regtest getrawmempool
```

**質問：** `size` と `bytes` は何ですか。`mempoolminfee` とは何で、これより低い手数料しか払わないトランザクションはどうなりますか。

### ステップ 3：アリスがボブに支払い、メンプールを観察する

```bash
BOB_ADDR=$(bitcoin-cli -regtest -rpcwallet=bob getnewaddress)
TXID=$(bitcoin-cli -regtest -rpcwallet=alice sendtoaddress "$BOB_ADDR" 1)
echo "$TXID"

bitcoin-cli -regtest getmempoolinfo
bitcoin-cli -regtest getrawmempool
bitcoin-cli -regtest getmempoolentry "$TXID"
```

ヒント：2 つ目のターミナルで `watch -n 1 bitcoin-cli -regtest getmempoolinfo` を実行し、ラボが終わるまで開いたままにしておきましょう。

**質問：** `getmempoolentry` の `vsize`、`weight`、`time`、`height`、`fees.base` はそれぞれ何ですか。`fees.base` と `vsize` から、手数料率を sat/vB で計算してください。`-fallbackfee` で設定した 10 sat/vB に近いですか。

### ステップ 4：未承認の支払いをボブの側から見る

```bash
bitcoin-cli -regtest -rpcwallet=bob getbalances
bitcoin-cli -regtest -rpcwallet=bob listunspent 0
```

**質問：** ボブの 1 BTC は、なぜ `trusted` ではなく `untrusted_pending` と表示されるのでしょうか。ボブは今、商品を渡すべきでしょうか。

### ステップ 5：インプットをさかのぼる

```bash
bitcoin-cli -regtest getrawtransaction "$TXID" true
```

出力から `vin[0].txid` と `vin[0].vout` を見つけ、その前のトランザクションを見ます：

```bash
PREV=$(bitcoin-cli -regtest getrawtransaction "$TXID" true | jq -r '.vin[0].txid')
bitcoin-cli -regtest getrawtransaction "$PREV" true
```

**質問：** `$PREV` はどんな種類のトランザクションですか。アリスの支払いは、そのどのアウトプットを使っていて、その金額はいくらでしたか。アリスの支払いにはアウトプットがいくつあり、どれがおつりですか。

### ステップ 6：ブロックをマイニングして承認させる

```bash
bitcoin-cli -regtest -rpcwallet=alice -generate 1
bitcoin-cli -regtest getmempoolinfo
bitcoin-cli -regtest -rpcwallet=alice gettransaction "$TXID"
bitcoin-cli -regtest -rpcwallet=bob getbalances
```

**質問：** メンプールはどうなりましたか。`gettransaction` のどのフィールドが変わりましたか。ボブの残高は今いくらで、どの残高の区分に入っていますか。

### ステップ 7：トランザクションを手作業で組み立てる

ここからは、ウォレットがやってくれていたことを、1 ステップずつ自分でやります。まず、使うコインを選びます：

```bash
bitcoin-cli -regtest -rpcwallet=alice listunspent
```

`"amount": 50.00000000` の UTXO（成熟したコインベース報酬）を選び、その `txid` と `vout` をコピーします：

```bash
IN_TXID=<ここに txid を貼り付ける>
IN_VOUT=<ここに vout を貼り付ける>
BOB_ADDR2=$(bitcoin-cli -regtest -rpcwallet=bob getnewaddress)
CHANGE_ADDR=$(bitcoin-cli -regtest -rpcwallet=alice getrawchangeaddress)
```

ボブに 2 BTC を支払い、手数料として 0.0001 BTC を払い、残りをアリスに戻します：50 - 2 - 0.0001 = 47.9999 BTC。

```bash
INPUTS='[{"txid":"'$IN_TXID'","vout":'$IN_VOUT'}]'
OUTPUTS='{"'$BOB_ADDR2'":2,"'$CHANGE_ADDR'":47.9999}'
RAW=$(bitcoin-cli -regtest createrawtransaction "$INPUTS" "$OUTPUTS")
bitcoin-cli -regtest decoderawtransaction "$RAW"
```

**質問：** このトランザクションは、まだ署名されていません。ステップ 5 のトランザクションと比べて、`vin[0]` には何が欠けていますか。手数料はどこに書かれていますか。

次に、署名して、ブロードキャストせずにテストします：

```bash
SIGNED=$(bitcoin-cli -regtest -rpcwallet=alice signrawtransactionwithwallet "$RAW" | jq -r '.hex')
bitcoin-cli -regtest testmempoolaccept '["'$SIGNED'"]'
```

**質問：** `allowed` になっていますか。`testmempoolaccept` は、`vsize` と `fees` をいくつと報告していますか。それは sat/vB でいくらの手数料率ですか。

### ステップ 8：よくある失敗（これはブロードキャストしないでください）

おつりのアウトプットを忘れたら、どうなるでしょうか。

```bash
BAD_OUTPUTS='{"'$BOB_ADDR2'":2}'
BAD_RAW=$(bitcoin-cli -regtest createrawtransaction "$INPUTS" "$BAD_OUTPUTS")
BAD_SIGNED=$(bitcoin-cli -regtest -rpcwallet=alice signrawtransactionwithwallet "$BAD_RAW" | jq -r '.hex')
bitcoin-cli -regtest testmempoolaccept '["'$BAD_SIGNED'"]'
```

**質問：** なぜ拒否されるのでしょうか。もしノードがこれを受け入れたら、残りの 48 BTC は誰のものになりますか。ここでは何があなたを守ってくれていますか。そして、ミスがもっと小さかった場合も守ってくれるでしょうか。

### ステップ 9：正しいトランザクションをブロードキャストする

```bash
MANUAL_TXID=$(bitcoin-cli -regtest sendrawtransaction "$SIGNED")
echo "$MANUAL_TXID"
bitcoin-cli -regtest getmempoolentry "$MANUAL_TXID"
```

**質問：** `sendrawtransaction` は、なぜ `-rpcwallet` なしで実行できるのでしょうか。（ヒント：この時点で、何か秘密の情報は必要ですか。）

### ステップ 10：未承認の親を使う子

手作業で作ったトランザクションのおつりのアウトプットは、アウトプット 1 です（アウトプットは指定した順序のまま並びます）。これを、承認される前に使います：

```bash
CHILD_INPUTS='[{"txid":"'$MANUAL_TXID'","vout":1}]'
CHILD_OUTPUTS='{"'$BOB_ADDR2'":47.9998}'
CHILD_RAW=$(bitcoin-cli -regtest createrawtransaction "$CHILD_INPUTS" "$CHILD_OUTPUTS")
CHILD_SIGNED=$(bitcoin-cli -regtest -rpcwallet=alice signrawtransactionwithwallet "$CHILD_RAW" | jq -r '.hex')
CHILD_TXID=$(bitcoin-cli -regtest sendrawtransaction "$CHILD_SIGNED")

bitcoin-cli -regtest getrawmempool true
bitcoin-cli -regtest getmempoolentry "$CHILD_TXID"
bitcoin-cli -regtest getmempoolentry "$MANUAL_TXID"
```

**質問：** `depends`、`spentby`、`ancestorcount`、`descendantcount` を見てください。メンプールは、この 2 つのトランザクションがつながっていることをどうやって知るのでしょうか。親がいつまでもマイニングされなかったら、子はどうなりますか。

### ステップ 11：両方をまとめて承認させる

```bash
bitcoin-cli -regtest -rpcwallet=alice -generate 1
bitcoin-cli -regtest getblock "$(bitcoin-cli -regtest getbestblockhash)" 1 | jq '.tx'
bitcoin-cli -regtest -rpcwallet=bob getbalances
```

**質問：** 新しいブロックにはトランザクションがいくつ、どんな順序で入っていますか。ブロックの中で、子が親より前に来ることはありえますか。

## 発展課題

### A. リオーグをシミュレートする

`invalidateblock` は、あるブロックを無効として扱うよう自分のノードに指示します。これは、そのブロックを取り除くリオーグに似た状況になります。

```bash
BEST=$(bitcoin-cli -regtest getbestblockhash)
bitcoin-cli -regtest invalidateblock "$BEST"
bitcoin-cli -regtest getmempoolinfo
bitcoin-cli -regtest -rpcwallet=alice gettransaction "$CHILD_TXID"
bitcoin-cli -regtest reconsiderblock "$BEST"
bitcoin-cli -regtest getblockcount
```

**質問：** ブロックが取り除かれたとき、2 つのトランザクションはどこへ行きましたか。そのブロックのコインベーストランザクションはどうなりましたか。このことから、店は 1 承認について何を学べますか。

### B. 2 つのノード、2 つのメンプール

別のポートで 2 つ目の regtest ノードを起動し、1 つ目に接続します：

```bash
mkdir -p "$HOME/regtest-node2"
bitcoind -regtest -daemon -datadir="$HOME/regtest-node2" -bind=127.0.0.1:18555 -rpcport=18554
bitcoin-cli -regtest -datadir="$HOME/regtest-node2" -rpcport=18554 addnode 127.0.0.1:18444 onetry
bitcoin-cli -regtest -datadir="$HOME/regtest-node2" -rpcport=18554 getpeerinfo | jq '.[].addr'
bitcoin-cli -regtest -datadir="$HOME/regtest-node2" -rpcport=18554 getblockcount
```

ノード 1 でアリスから新しい支払いを送り、数秒後に両方のノードの `getrawmempool` を比べます。次にノード同士を切断し（ノード 2 で `disconnectnode 127.0.0.1:18444`）、もう 1 つ支払いを送って、もう一度比べます。

**質問：** 2 つのメンプールが同じになるのはどんなときで、違うのはどんなときですか。なぜグローバルなメンプールは 1 つにできないのでしょうか。

### C. メンプールの上限

`bitcoin-cli -regtest help getmempoolinfo` を実行し、`maxmempool` と `mempoolminfee` の説明を読みます。`bitcoind -help | grep -A2 maxmempool` も読んでください。

**質問：** メンプールがいっぱいになったとき、ノードは何をしますか。それによって、受け入れる最低手数料はどう変わりますか。
