
# 一、常用链接：

## 1. lotus安装文档：
    https://docs.lotu.sh/en+install-lotus-ubuntu

## 2. GOPROXY（编译时使用）：
    export GOPROXY=https://goproxy.io
    或者
    export GOPROXY=https://goproxy.cn

## 3. 区块浏览器：
    https://stats.testnet.filecoin.io/      【按ESC可以选择看Testnet3的数据】
    https://filscout.io/en/                 【星际联盟团队开发，可切换Testnet2和Testnet3】
    https://filscan.io/#/
    http://testnet3.1475ipfs.com:10300/d/z6FtI92Zz/testnet3?orgId=1&refresh=25s   【1475团队开发， 仅Testnet3】

## 4. 区块同步数据备份（目前是Testnet2的同步数据）：
    https://lotus-archives.textile.io/

## 5. 官方博客：
    https://filecoin.io/blog/

## 6. Lotus Specification 说明文档：
    https://filecoin-project.github.io/specs/

## 7. Slack:
    https://filecoinproject.slack.com/

## 8. Lotus 代码下载:
    Lotus：         https://github.com/filecoin-project/lotus
    Go-filecoin：   https://github.com/filecoin-project/go-filecoin
    Rust-fil-proof: https://github.com/filecoin-project/rust-fil-proofs

## 9. testnet/3 最大化内存参数（仅针对32GB扇区）：
    export FIL_PROOFS_MAXIMIZE_CACHING=1

## 10. 水龙头地址：
    Testnet2(旧版): https://faucet.testnet.filecoin.io/
    Testnet3(新版): http://t01000.miner.interopnet.kittyhawk.wtf
    
## 11. Benchmark数据共享：
    Testnet2(V20): https://github.com/filecoin-project/lotus/issues/839
    Testnet3(V24): https://github.com/filecoin-project/lotus/issues/1475
    Testnet3(V25): https://filecoin-benchmarks.on.fleek.co/
    
## 12. 甘特图：
    https://app.instagantt.com/shared/s/1152992274307505/latest
    
## 13 Proof 证明文件下载：
    JDCloud(v20): https://s3.cn-south-1.jdcloud-oss.com/proof-parameters/filecoin-proof-parameters-v20.tar.gz
    JDCloud(v25): env IPFS_GATEWAY=https://proof-parameters.s3.cn-south-1.jdcloud-oss.com/ipfs/
    CoinSummer(中国专用/ v24和v25): https://filecoin-proofs.coinsummer.io/
    CoinSummer(v25 URL): https://filecoin-proofs.coinsummer.io/v25.txt
[参考](https://filecoinproject.slack.com/archives/CPFTWMY7N/p1587615402405300)


# 二、常用命令：

## 1. v25 版本代码的编译命令：

```Shell
env RUSTFLAGS="-C target-cpu=native -g" FFI_BUILD_FROM_SOURCE=1 make clean all
```
特别是针对 AMD 处理器，使用该命令自己编译出来的代码更适合自己的机器。

## 2. 启用内存最大化参数：

```Shell
export FIL_PROOFS_MAXIMIZE_CACHING=1
```
该参数仅针对测试网3的 32 GB 扇区有效。

## 3. 启用 Log 日志：

```Shell
export RUST_LOG=Debug
```
运行 miner 之前加入该参数可以在 miner 的日志中查看更详细的输出信息（底层 rust 代码的输出信息），Log 登记从低到高分别有： **`Trace`**、**`Debug`**、**`Info`**、**`Warn`**、**`Error`**，**`Trace`** 输出的信息最详细，**`Error`** 输出的信息最少，仅输入错误信息。

## 4. 手动设置链的高度（比如设置成 3800）：

```Shell
lotus chain sethead --epoch 3800
```

## 5. Testnet3 设置存储路径：

```Shell
# 设置密封扇区的存储路径，密封完成之后该路径下的数据会被自动清空，相当于临时目录
# 执行该命令可能需要一点时间等待
lotus-storage-miner storage attach --seal --init /path/to/fast_cache

# 设置数据存储路径，该路径用来存储最终密封好的数据
# 执行该命令可能需要一点时间等待
lotus-storage-miner storage attach --store --init /path/to/persistent_storage
```

以上两个命令都是在启动了 miner 之后才可以执行，是一种动态添加存储路径的方式，非常灵活。
当然还可以在命令中添加权重 `--weight=10`，默认权重是 10。

默认存储路径是： ~/.lotusstorage ，每个存储路径下都会有个 sectorstore.json 配置文件，
该文件可以配置该存储路径的用途，比如，是否可以用来存储密封过程中生成的临时文件（"CanSeal": true,），
是否可以用来存储密封好的数据（"CanStore": true），以及该路径的权重（"Weight": 10）和一唯一标识符：ID。

```Json
user@user:~/.lotusstorage$ cat sectorstore.json 
{
"ID": "508165ac-5103-45b4-9bb9-a95f5973776e",
"Weight": 10,
"CanSeal": true,
"CanStore": true
}
```

## 6. Testnet3 查看 Worker 信息

```Shell
lotus-storage-miner workers list
```

## 7. Testnet3 启动 worker：

```Shell
lotus-seal-worker run --address=192.168.1.201:2333 --precommit1=false --precommit2=true --commit=true
```
要给 worker 指定**本机地址**和一个**随机端口（四位数以上）**，`precommit1`、`precommit2` 和`commit` 是默认启动，如果想要禁用，可以设置为 `false`，例如：`--precommit1=false`。
最后，`commit` 参数是配置 `commit2` 的，而 `commit1` 是无法在 Worker 中启用的。


## 8. 查看本节点与连接其它节点

```Shell
# 查看本节点所监听的地址：
lotus net listen
# 连接其它节点的地址（命令中的地址为示例地址）：
lotus net connect /ip4/47.240.110.221/tcp/44845/p2p/12D3KooWRgxLL84TSkYSjhvhCy5ZNSuJZZzHWp2FXDY7ufqGBmUW
```
当启动 daemon 之后无法正常同步链上的数据，可以试试在启动 daemon 的时候禁用自动连接 peers （即：加上 `--bootstrap=false` 参数），然后手动连接到一个正常节点，例如：
```Shell
lotus daemon --bootstrap=false
lotus net connect /ip4/47.240.110.221/tcp/44845/p2p/12D3KooWRgxLL84TSkYSjhvhCy5ZNSuJZZzHWp2FXDY7ufqGBmUW
```
上述的节点是示例节点，当您在使用该命令的时候，您需要自己去找一个可以使用的节点。

## 9. 赎回已获得的奖励（Testnet3 才需要手动赎回）

```Shell
lotus-storage-miner rewards redeem
lotus-storage-miner rewards list
```
赎回之后，可能需要过一段时间才能看到自己钱包的余额增加。

## 10. 未完

```Shell
lotus sync status
```


【**注**】以上内容仅为个人整理，如有侵权或不当的地方，请及时指出，我会及时修改！

