# lustre 文件系统认知 

https://git.whamcloud.com/fs/lustre-release.git

https://wiki.lustre.org/LNet_Router_Config_Guide
https://zhuanlan.zhihu.com/p/632518511


http://lustrefs.cn/

[存储李希](https://blog.csdn.net/fsdev/category_1090804.html)

从文档和介质包来看， lustre server端 只支持rhel 操作系统，客户端支持rhel,sles, ubuntu 等三种OS. 



[深入理解Lustre文件系统-第5篇 LDLM：锁管理者](https://blog.csdn.net/fsdev/article/details/7317424)


[DeepSeek第五弹炸裂收官！开源全新并行文件系统，榨干SSD全部带宽](https://www.qbitai.com/2025/02/259869.html)  

该集群由180个存储节点组成，每个存储节点配备2×200Gbps InfiniBand网卡和16个14TiB NVMe SSD。

大约500+个客户端节点用于读压测，每个客户端节点配置1x200Gbps InfiniBand网卡。

在训练作业的背景流量下，最终聚合读吞吐达到约6.6TiB/s。

[AI Infra 如何打造？云轴科技ZStack在中国CID大会上主题演讲](https://www.zstack.io/recentnews/marketing_voice/2024/1021/2815.html)


[DeepSeek AI Infra(1) - 如何搭建一个比DGX成本少一半的万卡GPU集群](https://zhuanlan.zhihu.com/p/27236485501)

[从3FS盘点分布式文件存储系统](https://zhuanlan.zhihu.com/p/27730717632)


[DeepSeek的训练平台HAI Platform](https://github.com/HFAiLab/hai-platform)

[开源高性能文件系统 3FS，DeepSeek为何自研存储？](http://tech.china.com.cn/roll/20250301/407907.shtml), 为了提升大模型训练速度，需要对大规模数据集进行快速加载，且一般采用数百甚至上万张GPU构成计算集群进行高效的并行计算，需要高并发输入/输出(I/O)处理，而训练数据集呈现海量小文件的特点，文件量在几亿到几十亿量级，对应的带宽需求可能每秒要达到上TB，这就要求存储系统具备强大的数据管理能力，业界能达到该能力的仅寥寥几家。



[动态挂载OBS并行文件系统](https://support.huaweicloud.com/usermanual-standard-modelarts/devtool-modelarts_0007.html)， 华为， 在ModelArts运行态的Notebook容器中，采用动态挂载特性，将OBS对象存储模拟成本地文件系统。其本质是通过挂载工具，将对象协议转为POSIX文件协议。挂载后应用层可以在容器中正常操作OBS对象。
