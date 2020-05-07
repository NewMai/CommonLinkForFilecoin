
# 一、常用链接：


## 0.0. CoinSummer 整理的常用命令和链接

https://github.com/CoinSummer/filecoin

## 0.1. 同步数据每日备份

来源于 **CoinSummer**：

https://filecoin.coinsummer.io/datastore.html


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

## 9. testnet/3 使用文档：

在Github项目中的Testnet/3分支下：

    https://github.com/filecoin-project/lotus/blob/testnet/3/documentation/en/join-testnet.md

搭建Testnet/3的本地测试网：

    https://github.com/filecoin-project/lotus/blob/testnet/3/documentation/en/local-dev-net.md

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
    最新版发布地址(最快更新 Proof 参数的地方【官方】): https://proofs.filecoin.io/

### A. 使用方法一：

直接导出环境变量，然后再运行 miner init 的时候，或者启动 miner 的时候都会自动从这个 JDCloud 中下载：
```Shell
export IPFS_GATEWAY=https://proof-parameters.s3.cn-south-1.jdcloud-oss.com/ipfs/
```

### B. 使用方法二：

下载 https://filecoin-proofs.coinsummer.io/v25.txt 中的url地址，保存这些 URL 地址到一个文件中（比如，保存到 url.txt 文件中），然后使用 wget 工具下载，命令如下：
```Shell
wget -c -t 0 -i url.txt
```

**【注意】** v25 版本的参数命名方式比较特别，在 Windows 上下载的时候会出现问题，因为 Windows 上不支持这种命名方式，如果在 Windows 上下载证明参数，然后再拷贝到 Linux 中，则需要自己手动重命名每个文件名。

[参考](https://filecoinproject.slack.com/archives/CPFTWMY7N/p1587615402405300)

## 14  rust 和 rustup 的安装环境配置（Cargo）：

当你不正确的安装 rust 环境，此时 lotus 编译的时候会找不到你的 cargo，你会看到如下的错误：

```Shell
Error: cargo is not installed.
```

此时，你就需要卸载以前的安装版本（如果安装有的话），比如，使用sudo方式安装的版本等：

```Shell
# 尝试执行以下命令
sudo /usr/local/lib/rustlib/uninstall.sh
sudo apt remove cargo
```

然后使用官方推荐的方式安装 Cargo （注意不要使用 sudo 安装）：

```Shell
# 方法一：
curl https://sh.rustup.rs -sSf | sh

# 方法二：
wget https://sh.rustup.rs -O ./cargo_install_script.sh     # 下载安装脚本
chmod +x ./cargo_install_script.sh                         # 添加可执行权限
./cargo_install_script.sh                                  # 安装，不要用 sudo
```

**参考链接：**

[【官方文档】](https://www.rust-lang.org/tools/install)

[【社区文档】](https://learnku.com/docs/rust-lang/2018/ch01-01-installation/4494)

[【免翻墙版】](https://www.cnblogs.com/honyer/p/11877145.html)

## 15. Lotus 可执行文件备份

地址： https://github.com/NewMai/lotus_bin

下载：
```Shell
git clone https://github.com/NewMai/lotus_bin.git
```
## 16. 使用 GPU 算 Precommit2

https://github.com/filecoin-project/neptune

[【相关链接】](https://filecoinproject.slack.com/archives/CEGB67XJ8/p1587776730458900)











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

## 10. 手动修改扇区状态

```Shell
lotus-storage-miner sectors update-state --really-do-it <SectorID> <NewSectorStatus>
# 例如：手动修改扇区 1 的状态到 Unsealed 状态
./lotus-storage-miner sectors update-state --really-do-it 1 Unsealed
```
## 11. 查看扇区的历史状态

```Shell
# 列举所有扇区信息：
lotus-storage-miner sectors list
# 查看某个扇区的历史状态
lotus-storage-miner sectors status --log <SectorID>
```

## 12. 未完

```Shell
lotus sync status
```


【**注**】以上内容仅为个人整理，如有侵权或不当的地方，请及时指出，我会及时修改！

