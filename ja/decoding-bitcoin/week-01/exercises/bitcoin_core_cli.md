# Decoding Bitcoin - Week 1 演習：Bitcoin Core CLI

> Code Orange Dev School | [codeorange.dev](https://codeorange.dev)

このラボでは、自分のマシンでプライベートなビットコインネットワーク（regtest）を動かし、はじめての `bitcoin-cli` コマンドをひととおり試します。Week 1 に宿題はないので、Week 2 に向けたセットアップだと考えてください。解答例は [`../solutions/README.md`](../solutions/README.md) にあります。

## 必要なもの

- Bitcoin Core v29 以降（`bitcoind` と `bitcoin-cli`）
- Linux、macOS、または Windows のターミナル（Windows では WSL2 が使いやすいです）
- 約 1 GB のディスク空き容量（regtest のデータはごく小さいですが、ソースからビルドする場合はもっと必要です）

Bitcoin Core を入手する方法は 2 つあります。どちらかを選んでください。

### 方法 A（かんたん）：リリース版のバイナリをインストールする

1. [bitcoincore.org/en/download](https://bitcoincore.org/en/download/) を開き、自分の環境に合った最新リリースをダウンロードします（一般的な PC の Linux なら `bitcoin-<version>-x86_64-linux-gnu.tar.gz`）。
2. 同じページから `SHA256SUMS` と `SHA256SUMS.asc` をダウンロードし、ファイルを検証します。署名の検証方法もダウンロードページに説明があります。必ずやりましょう。「Don't trust, verify（信頼するな、検証せよ）」はここから始まります。

```bash
# ファイルをダウンロードしたフォルダで実行
sha256sum --ignore-missing --check SHA256SUMS

# 展開してインストール（<version> はダウンロードしたバージョンに置き換える）
tar -xzf bitcoin-<version>-x86_64-linux-gnu.tar.gz
sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-<version>/bin/*

# 動作確認
bitcoind -version
bitcoin-cli -version
```

macOS では、自分のチップに合った `.tar.gz`（Apple シリコンは `arm64-apple-darwin`）をダウンロードし、`bin/` の中のファイルを `PATH` の通ったフォルダにコピーします。

### 方法 B：ソースからビルドする（CMake）

v29 から、Bitcoin Core は CMake でビルドします。以前の `./autogen.sh`、`./configure`、`make` という手順はもう使えません。以下は Ubuntu/Debian 向けの手順です。ほかの環境では、Bitcoin Core リポジトリの [`doc/build-unix.md`](https://github.com/bitcoin/bitcoin/blob/master/doc/build-unix.md) や、ほかの `doc/build-*.md` を見てください。

```bash
# ビルドに必要なパッケージをインストール（Ubuntu/Debian）
sudo apt-get update
sudo apt-get install build-essential cmake pkgconf python3 \
  libevent-dev libboost-dev libsqlite3-dev libcapnp-dev capnproto

# ソースを取得し、最新リリースのタグをチェックアウト
git clone https://github.com/bitcoin/bitcoin.git
cd bitcoin
git tag -l 'v*' --sort=-v:refname | grep -v rc | head -5   # 新しいリリースから順に表示
git checkout v32.1        # 一覧のいちばん新しいタグに置き換える

# 設定してビルド（初回は時間がかかります）
cmake -B build
cmake --build build -j"$(nproc)"

# バイナリは build/bin/ にできる
ls build/bin/
./build/bin/bitcoind -version
```

補足：

- `libsqlite3-dev` はウォレットに必要です。これがないと CMake はウォレットなしで Bitcoin Core をビルドしますが、このラボではウォレットを使います。
- GUI（`bitcoin-qt`）はデフォルトではビルドされません。このコホートでは必要ありません。
- `libcapnp-dev` と `capnproto`（Cap'n Proto）は v30 以降で必要です。v30 からは multiprocess/IPC ビルドがデフォルトで有効になっているためです。これがないと、`cmake -B build` は Cap'n Proto が見つからないというエラーで止まります。インストールできない場合は、代わりに `cmake -B build -DENABLE_IPC=OFF` で設定してください。
- `libevent-dev` が必要なのは v31 までです。v32 以降は省いてかまいません。
- 以下のコマンドをフルパスなしで使うには、フォルダを `PATH` に追加します：`export PATH="$PWD/build/bin:$PATH"`（`bitcoin` フォルダで実行するか、フルパスを `~/.bashrc` に書いておきます）。
- 任意：ユニットテストは `ctest --test-dir build -j"$(nproc)"` で実行できます。

### regtest ノードを起動する

```bash
bitcoind -regtest -daemon -txindex=1 -fallbackfee=0.0001
```

- `-regtest` は、プライベートなテスト用チェーンを動かします。ブロックは自分で作り、コインに価値はありません。
- `-txindex=1` を付けると、`getrawtransaction` がメンプールにあるものだけでなく、どのトランザクションでも見つけられるようになります。
- `-fallbackfee=0.0001` は、ウォレットが使う手数料率を指定します（0.0001 BTC/kvB = 10 sat/vB）。できたばかりの regtest チェーンには手数料の履歴がないため、これがないと `sendtoaddress` は "Fee estimation failed" で失敗します。

あとでノードを止めるには `bitcoin-cli -regtest stop` を実行します。空のチェーンからやり直すには、ノードを止めてから regtest フォルダを削除します（Linux では `~/.bitcoin/regtest`、macOS では `~/Library/Application Support/Bitcoin/regtest`）。

---

## 演習 1：regtest ネットワークを起動してブロックをマイニングする

regtest（regression test、回帰テスト）は、自分のマシン上で動くプライベートなブロックチェーンです。すべてを自分でコントロールでき、本物のネットワークと同期する必要はありません。

### タスク

**1.1** bitcoind を regtest モードで起動します（すでに動いている場合は飛ばします）：
```bash
bitcoind -regtest -daemon -txindex=1 -fallbackfee=0.0001
```

**1.2** ノードが動いていることを確認します：
```bash
bitcoin-cli -regtest getblockchaininfo
```

**質問**：ブロック高はいくつですか。チェーンの名前は何ですか。難易度はいくつですか。

**1.3** ウォレットを作ります：
```bash
bitcoin-cli -regtest createwallet "mywallet"
```

これでディスクリプターウォレット（デフォルト）ができます。あとでノードを再起動したときは、`bitcoin-cli -regtest loadwallet "mywallet"` で読み込み直してください。

**1.4** 101 ブロックをマイニングします（コインベースの報酬が使えるようになるには、100 ブロック分の成熟が必要です）：
```bash
bitcoin-cli -regtest -generate 101
```

**質問**：なぜ 1 ではなく 101 なのでしょうか。コインベースの成熟（coinbase maturity）のルールとは何で、なぜ存在するのでしょうか。

**1.5** 残高を確認します：
```bash
bitcoin-cli -regtest getbalance
```

**質問**：何 BTC 持っていますか。regtest の最初のうちのブロック報酬は、1 ブロックあたり 50 BTC です。なぜ残高は 5050 ではなく 50 なのでしょうか。

---

## 演習 2：トランザクションを作って調べる

**2.1** アドレスを 2 つ生成します：
```bash
bitcoin-cli -regtest getnewaddress "alice"
bitcoin-cli -regtest getnewaddress "bob"
```

"alice" と "bob" はただのラベルです。どちらのアドレスも同じウォレットのものです。

**質問**：これらはどの種類のアドレスですか。（ヒント：先頭を見てください。`bcrt1q` = P2WPKH、`bcrt1p` = P2TR）

**2.2** "bob" に 10 BTC を送ります：
```bash
bitcoin-cli -regtest sendtoaddress <bob_address> 10
```

返ってきた txid を控えておきます。

**2.3** マイニングする前に、トランザクションを調べます：
```bash
bitcoin-cli -regtest gettransaction <txid>
bitcoin-cli -regtest getrawtransaction <txid> true
```

**質問**：デコードされたトランザクションには、どんなフィールドがありますか。それぞれ挙げて、役割を説明してください：
- `txid`：
- `version`：
- `vin`（インプット）：
- `vout`（アウトプット）：
- `locktime`：

**質問**：このトランザクションにはアウトプットがいくつありますか。なぜ 1 つより多いのでしょうか。（ヒント：おつりのアウトプット）

**2.4** ブロックを 1 つマイニングして、トランザクションを承認させます：
```bash
bitcoin-cli -regtest -generate 1
```

**2.5** トランザクションが承認されたことを確認します：
```bash
bitcoin-cli -regtest gettransaction <txid>
```

**質問**：マイニングのあと、トランザクションの詳細で何が変わりましたか。

---

## 演習 3：生トランザクションをデコードする

**3.1** トランザクションの生の 16 進数データを取得します：
```bash
bitcoin-cli -regtest getrawtransaction <txid>
```

**3.2** デコードします：
```bash
bitcoin-cli -regtest decoderawtransaction <raw_hex>
```

**3.3** 手作業でのデコードに挑戦：

生の 16 進数データから、次のフィールドを自分の手で見つけてみましょう。この表を参考にしてください：

| フィールド | サイズ | 説明 |
|-------|------|-------------|
| バージョン | 4 バイト（リトルエンディアン） | トランザクションのバージョン（たいてい 01000000 か 02000000） |
| マーカー | 1 バイト | SegWit のマーカー：00 |
| フラグ | 1 バイト | SegWit のフラグ：01 |
| インプット数 | compact size | インプットの数 |
| インプット | 可変 | 前の txid（32 バイト、逆順）＋ vout インデックス（4 バイト）＋ scriptSig の長さ ＋ scriptSig ＋ シーケンス（4 バイト） |
| アウトプット数 | compact size | アウトプットの数 |
| アウトプット | 可変 | 金額（8 バイト、リトルエンディアン、satoshi 単位）＋ scriptPubKey の長さ ＋ scriptPubKey |
| witness | 可変 | 各インプットの witness データ |
| ロックタイム | 4 バイト | トランザクションのロックタイム |

**課題**：自分の生トランザクションの 16 進数データのうち、少なくとも最初の 20 バイトにラベルを付けてください。各バイトが何を意味するかを書き出します。（Week 3 で、すべてのフィールドを詳しく見ていきます。）

---

## 演習 4：ブロックを探索する

**4.1** 最新（best）のブロックハッシュを取得します：
```bash
bitcoin-cli -regtest getbestblockhash
```

**4.2** ブロックの全データを取得します：
```bash
bitcoin-cli -regtest getblock <blockhash> 2
```

（`2` を付けると、トランザクションの詳細まですべて表示されます。）

**4.3** このブロックについて、次の質問に答えてください：
- ブロックにはトランザクションがいくつ入っていますか。
- コインベーストランザクションとは何ですか。ふつうのトランザクションとどう違いますか。
- `previousblockhash` は何ですか。ブロック 0（ジェネシスブロック）ではどうなるでしょうか。
- `merkleroot` は何ですか。どうやって計算されますか。
- `nonce` と `bits` のフィールドは何ですか。マイニングとどう関係していますか。

**4.4** ジェネシスブロック（ブロック 0）を取得します：
```bash
bitcoin-cli -regtest getblockhash 0
bitcoin-cli -regtest getblock <genesis_hash>
```

**質問**：ジェネシスブロックの特別なところは何ですか。

---

## 演習 5：UTXO モデル

**5.1** 自分の未使用トランザクションアウトプット（UTXO）を一覧表示します：
```bash
bitcoin-cli -regtest listunspent
```

**5.2** 次の質問に答えてください：
- UTXO はいくつありますか。
- すべての UTXO の合計金額はいくらですか。
- なぜ 1 つの大きな残高ではなく、複数の UTXO を持っているのでしょうか。

**5.3** 複数の UTXO をまとめて使うトランザクションを送ります：
```bash
# どの UTXO 1 つよりも大きい金額を送る
bitcoin-cli -regtest sendtoaddress <address> 75
```

**質問**：このトランザクションにはインプットがいくつありますか。なぜでしょうか。

**5.4** マイニングしてから、もう一度 listunspent を確認します：
```bash
bitcoin-cli -regtest -generate 1
bitcoin-cli -regtest listunspent
```

**質問**：UTXO セットはどう変わりましたか。どの UTXO が消費されましたか。新しくできたのはどれですか。

---

## ディスカッション問題

短く明確な答え（それぞれ数段落）を書いて、月曜のセッションに持ってきてください。解答例は [`../solutions/README.md`](../solutions/README.md) の「ボーナス問題」にあります。

### 問題 1

**UTXO モデルを説明してください。アカウントベースのモデル（イーサリアムなど）とどう違いますか。トレードオフは何ですか。**

考えるポイント：
- それぞれのモデルは、残高をどう管理していますか。
- プライバシーへの影響は何ですか。
- UTXO には、並列処理の面でどんな利点がありますか。
- 欠点は何ですか（例：UTXO の管理、ダスト）。

### 問題 2

**ビットコインのトランザクションが作られてから承認されるまでの一生をたどってください。各段階で何が起きますか。**

次の内容を含めてください：
1. トランザクションの作成（UTXO の選択、インプット／アウトプットの組み立て）
2. トランザクションへの署名
3. ネットワークへのブロードキャスト
4. メンプールでの検証
5. マイニング（ブロックへの取り込み）
6. 承認（その後に続くブロック）

---

## 作業を共有する

質問、エラー、スクリーンショットは、コホートの Discord チャンネルに投稿してください。セットアップがうまくいかないときは、エラーメッセージをそのまま投稿します。たいてい、誰かが同じエラーを見たことがあります。Week 2 のラボはこのノードを前提に進むので、Week 2 のセッションまでにノードが動くようにしておきましょう。

---

*Code Orange Dev School | [codeorange.dev](https://codeorange.dev) | CC0 1.0 Universal*
