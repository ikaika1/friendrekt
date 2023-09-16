
# <img src="https://github.com/evmcheb/friendrekt/assets/50129617/e3ba3f2d-62fd-4c6c-a9db-df95f93b9794" width="48"> friend.tech mempool sniper bot <img src="https://github.com/evmcheb/friendrekt/assets/50129617/e3ba3f2d-62fd-4c6c-a9db-df95f93b9794" width="48">

mempool sniper bot for new friend.tech joiners. 
the story goes: 
- op-stack is supposed to be blind mempool. but base node default config had txpool+ws rpcs open (see the [patch notes](https://github.com/ethereum-optimism/op-geth/pull/118))
- friend.tech uses blast-api rpc
- blast-api used base node default config for their backend nodes

## important parts

1. friendrekt-rs
    - rust bot for finding new joiners, caching follow count and sniping
2. friendrekt-contracts
    - solidity contract for sniping w/ fail-safes
3. twt-follower-api
    - python http api for retrieving follower count

## algo
```
/*
    スナイパーの概要です：
    tokio のスレッドは2つある。

    1.すべてのブロックを聞く。
        すべてのETH転送またはブリッジリレーについて：
            friend.techで関係するアドレスを逆検索する。
            フォロワーの数を見つける
            アドレスがキャッシュされていない場合
                アドレスをキャッシュする。

    2. blast-api eth_newPendingTransactions をリッスンする。
        複数の(4?)バックエンドノードがあるので、数回サブスクライブする。
            (どのストリームを取得するかは、ほとんどrngである。）
            (このボットを複数の地理的に分散したサーバーで動作させる。）
            最初のシェア購入（サインアップ）の場合：
                アドレスがキャッシュされている場合
                    フォロー数>20kの場合: スナイプTXを送信
                そうでなければ
                    フォロー数のライブ検索を行う
                    フォロー数>20kの場合：スナイプTXを送る
*/
```

## devs
- [cheb](https://twitter.com/evmcheb)
- [rage](https://twitter.com/rage_pit)
