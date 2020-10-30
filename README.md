# 加入海带区块链测试网络

::: tip 提示
请查看[testnet repo](https://github.com/haidai-network/testnet)获取最新的公共测试网信息，包含了所使用的 Haidai 的正确版本和genesis文件。
:::

- 当前测试网网络id

```
haidai-testnet2
```

--- 

### 使用编译好的二进制文件[推荐方式]

**下载文件**

```
前往 https://github.com/haidai-network/haidai-testnet/releases 下载最新测试网版本
```

**不同操作系统对应对应文件**

| Filename  | Description                                     |
| --------- | ----------------------------------------------- |
| haidaicli_darwin_amd64    | OSX(苹果操作系统客户端)客户端，如果为Mac系统则使用此二进制可执行文件 |
| haidaied_darwin_amd64    | OSX(苹果操作系统客户端)链服务端，如果为Mac系统则使用此二进制可执行文件 |
| haidaicli_linux_amd64   | Linux客户端，如果为Linux系统则使用此二进制可执行文件 |
| haidaied_linux_amd64    | Linux链服务端，如果为Linux系统则使用此二进制可执行文件 |
| haidaicli_windows_amd64.exe    | windows客户端，如果为Windows系统则使用此二进制可执行文件 |
| haidaied_windows_amd64.exe    | windows链服务端，如果为Windows系统则使用此二进制可执行文件 |


**解压文件**

| Filename  | Description                                     |
| --------- | ----------------------------------------------- |
| genesis.json   | 测试网络创世文件 |
| config.toml    | 链服务端配置文件，里面包含p2p种子节点信息 |
| haidaixxx   | 海带链客户端，二进制可执行文件 |

::: tip 提示
配置二进制文件执行权限
:::

```
chmod +x  haidai*

```

::: warning 注意
条件检查
:::

> 如果曾经运行过海带链测试网络则必须执行此步骤，如果从未运行过海带链程序则跳过此步骤

清除旧的测试网络数据，这里以Mac操作系统为例，如果为其他操作系统则使用对应的二进制可执行文件，命令步骤一样

```
// 删除创始文件，创始交易信息
rm -f ~/.haidaied/config/genesis.json ~/.haidaied/config/gentx/*

// 删除链数据
./haidaied_darwin_amd64 unsafe-reset-all

```

**haidaicli 客户端配置**

配置haidaicli，这里以Mac操作系统为例，如果为其他操作系统则使用对应的二进制可执行文件，命令步骤一样

```
./haidaicli_darwin_amd64 config output json

./haidaicli_darwin_amd64 config indent true

./haidaicli_darwin_amd64 config trust-node true

// 配置公共测试网络ID，当前为 haidai-testnet2
./haidaicli_darwin_amd64 config chain-id haidai-testnet2

./haidaicli_darwin_amd64 config keyring-backend test

```

**haidaied 链服务端配置**

配置haidaied，这里以Mac操作系统为例，如果为其他操作系统则使用对应的二进制可执行文件，命令步骤一样

```
// 配置测试网络
./haidaied_darwin_amd64 init haidai --chain-id haidai-testnet2

// 复制创始文件
cp genesis.json ~/.haidaied/config

// 复制配置文件
cp config.toml ~/.haidaied/config

// 检查创始文件正确性
./haidaied_darwin_amd64 validate-genesis

// 启动链服务
./haidaied_darwin_amd64 start

```

链服务启动后会尝试连接种子节点同步区块：

```
I[2020-10-12|17:40:03.047] starting ABCI with Tendermint                module=main 
I[2020-10-12|17:40:08.559] Executed block                               module=state height=3342 validTxs=0 invalidTxs=0
I[2020-10-12|17:40:08.574] Committed state                              module=state height=3342 txs=0 appHash=494AEEF2DF059B649A58D406DC293C7C49F3D5F1C7307805C3B619A768A79A8C
```

**🚀 haidai network 探索**

参考 <https://github.com/haidai-network/haidai/blob/master/docs/haidaicli.md> 文档进行操作，探索区块链世界！


---

### 源码编译运行[开发人员]

**升级软件**

升级软件：

```bash
cd $GOPATH/src/github.com/haidai-network/haidai
git fetch --all && git checkout master
```

- 国内使用 `goproxy.cn` 代理，参考：https://goproxy.cn/
- 也可以直接在 `Releases` 页面下载已经编译好的二进制文件，跳过此步骤
- 根据平台编译源码，默认为OSX (darwin）操作系统

**编译**

::: tip 提示
 根据操作系统情况编译，默认为mac系统，如果为其他系统，则添加系统名称，如：
 make build-linux，make build-windows
*注意*：如果在这一步出现问题，请检查是否安装了最新稳定版本的Go。
:::

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

- 进入 `build` 文件夹，运行 haidaicli_darwin_amd64 配置链客户端参数，这里以 OSX 平台为例：

```
./haidaicli_darwin_amd64 config output json
./haidaicli_darwin_amd64 config indent true
./haidaicli_darwin_amd64 config trust-node true
./haidaicli_darwin_amd64 config chain-id haidai-testnet2 // 当前测试网络
./haidaicli_darwin_amd64 config keyring-backend test

```

- 运行 haidaied 配置链节点参数，这里以 OSX 平台为例：

```
./haidaied_darwin_amd64 init test99 --chain-id haidai-testnet2 // 当前测试网络

cp genesis.json ~/.haidaied/config
cp config.toml ~/.haidaied/config

./haidaied_darwin_amd64 validate-genesis
```

- 启动链节点，会尝试连接种子节点同步区块

```
./haidaied_darwin_amd64 start
```

- 启动成功如下：

```
I[2020-10-12|17:40:03.047] starting ABCI with Tendermint                module=main 
I[2020-10-12|17:40:08.559] Executed block                               module=state height=3342 validTxs=0 invalidTxs=0
I[2020-10-12|17:40:08.574] Committed state                              module=state height=3342 txs=0 appHash=494AEEF2DF059B649A58D406DC293C7C49F3D5F1C7307805C3B619A768A79A8C
```

**🚀haidai network 探索**

参考 <https://github.com/haidai-network/haidai/blob/master/docs/haidaicli.md> 文档进行操作，探索区块链世界！