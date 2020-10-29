### darwinia-ethereum-relay

### 使用方式
blake2b需要使用go-ethereum客户端，javascript vm 执行会得到错误的结果。

* 安装[go-ethereum](https://geth.ethereum.org/docs/install-and-build/installing-geth)


* 创建初始用户
```
➜  mkdir dataDir
➜  geth --datadir=./dataDir --password ./passwd.txt account new > account1.txt
➜  geth --datadir=./dataDir --password ./passwd.txt account new > account2.txt
```

* 将生成的账号覆盖geth-genesis.json相应部分
```
"alloc":{
  "0x7118446aEB6d51F05C61741b3044C0ae4C5e7596": { "balance": "0x20000000000000" },
  "0xE99F3cBb6B550B36313722BA319e56ec251857cd": { "balance": "0x20000000000000" }
}
```

* 用指定配置初始化节点
```
➜  geth --datadir ./dataDir init ./geth-genesis.json
```

* 启动ethereum节点
```
➜  geth --port 4321 --networkid 1234 --datadir=./dataDir --rpc --rpcport 8543 --rpcaddr 127.0.0.1 --rpcapi "eth,net,web3,personal,miner" --gasprice 0 --etherbase 0x7118446aEB6d51F05C61741b3044C0ae4C5e7596 --allow-insecure-unlock --mine --minerthreads=1
```
* 解锁指定账户
```
➜  geth attach http://localhost:8543
> personal.unlockAccount("0x7118446aeb6d51f05c61741b3044c0ae4c5e7596","hello")
true
> personal.unlockAccount("0xe99f3cbb6b550b36313722ba319e56ec251857cd","hello")
true
```

* 安装[truffle](https://www.trufflesuite.com/docs/truffle/getting-started/installation)

* 部署合约

```
➜ truffle migrate
```

* 运行测试 
```
➜ yarn test-mmrlib
```


### 计划
- [x] Merkle Mountain Range
- [ ] Merkle Patricia Tree
- [ ] Darwinia Relay Game - [https://github.com/darwinia-network/relayer-game]


