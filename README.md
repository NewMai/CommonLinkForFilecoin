
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




【**注**】以上内容仅为个人整理，如有侵权或不当的地方，请及时指出，我会及时修改！