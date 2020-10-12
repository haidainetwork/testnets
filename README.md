
# 海带链部署文档

### 当前网络为测试网络

- 链id

```
haidai-testnet2
```

### 编译源码

- 国内使用goproxy.cn代理，参考：https://goproxy.cn/
- 根据平台编译源码，默认为OSX (darwin）操作系统

编译 OSX

```
make build
```

编译 Linux

```
make build-linux
```

编译 Windows

```
make build-windows
```

### 部署

- 复制编译好的二进制可执行文件到 `deploy` 文件夹

```
cp build/* deploy
```

- 进入 `deploy` 文件夹，运行 haidaicli 配置链客户端参数，这里以 OSX 平台为例：

```
./haidaicli config output json
./haidaicli config indent true
./haidaicli config trust-node true
./haidaicli config chain-id haidai-testnet2 // 当前测试网络
./haidaicli config keyring-backend test

```

- 运行 haidaied 配置链节点参数，这里以 OSX 平台为例：

```
./haidaied init test99 --chain-id haidai-testnet2 // 当前测试网络

cp genesis.json ~/.haidaied/config
cp config.toml ~/.haidaied/config

./haidaied validate-genesis
```

- 启动链节点，会尝试连接种子节点同步区块

```
./haidaied start
```

- 启动成功如下：

```
I[2020-10-12|17:40:03.047] starting ABCI with Tendermint                module=main 
I[2020-10-12|17:40:08.559] Executed block                               module=state height=3342 validTxs=0 invalidTxs=0
I[2020-10-12|17:40:08.574] Committed state                              module=state height=3342 txs=0 appHash=494AEEF2DF059B649A58D406DC293C7C49F3D5F1C7307805C3B619A768A79A8C
```

- 其他操作文档请参考 `docs` 文件夹





