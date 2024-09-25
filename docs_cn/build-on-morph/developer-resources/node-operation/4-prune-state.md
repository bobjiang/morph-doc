---
title: 修剪状态
lang: zh-CN
---

当存储大小达到较高容量时，全节点的性能将会下降。我们建议全节点通过修剪存储来始终保持轻存储。

### How to Prune

1.停止节点，包括共识客户端（morphnode）和执行客户端（geth）
2. 跑步```nohup geth snapshot prune-zk-state --datadir "$GETH_DB_DIR" > prune.log &```。需要5~7小时才能完成。
3. 完成后启动节点。

The hardware is important, **make sure the SSD meets: solid-state drive(SSD), 8k IOPS, 500 MB/S throughput, read latency < 1ms.**

:::note
要修剪 Geth 节点，建议至少有 200 GB 的可用磁盘空间。这意味着修剪不能用于保存已完全填满的硬盘驱动器。一个好的经验法则是在节点填满约 80% 的可用磁盘空间之前进行修剪。
:::



