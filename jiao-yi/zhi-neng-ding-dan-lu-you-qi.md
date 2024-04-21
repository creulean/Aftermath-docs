---
description: 在一个地方找到Sui在任何DEX上的最佳交换价格
cover: ../.gitbook/assets/截屏2024-03-19 22.29.36 (1).png
coverY: 0
---

# 智能订单路由器

我们的智能订单路由器（SOR）是一个DEX聚合器，它不仅连接到Aftermath上的所有流动性池，还连接到Sui上任何提供API并具有足够流动性的其他DEX。这意味着当您选择要交易的资产时，我们的路由器将搜索Sui上的每个DEX，为您找到最佳交易，即使它不来自我们自己的流动性池之一。

目前，Aftermath的智能订单路由器已与Aftermath、DeepBook、Cetus、Turbos、FlowX、Kriya、Suiswap和BlueMove上的流动性池集成。随着Sui DeFi生态系统增长以及新来源的流动性在线化，它们也将被整合到我们的路由器中，以确保您只需去一个地方就可以确保获得所有交换最佳价格。

<figure><img src="../.gitbook/assets/spaces_meKfXaQnIP3bbI1AdlVX_uploads_xmlLTXA1XPmhgJ7vsPLf_Screenshot 2024-02-21 at 11.webp" alt=""><figcaption><p>Aftermath 智能订单路由整合的流动性来源</p></figcaption></figure>

除了仅在 Sui 上搜索每个流动性 DEX 外，智能订单路由器还能够将单个交易拆分为多个子路径。这意味着一部分交易可以通过一个或多个池在一个 DEX 上进行路由，而其他多个子路径可以完成剩余的交易。当执行大宗交易时，这特别有用，因为当交易可以跨越多个DEX上的多个池进行拆分时，所产生的滑点会被极大地减少。我们在设计聚合器时充分利用了Sui的本机功能，因此无论路线的整体复杂性或总换手数如何，在任何情况下用户都只需要签署一笔交易。

将一笔交易拆分成多条子路径是通过使用可编程事务块（PTB）实现的。借助 PTB，可以将相关联的多笔交易批量打包到一个原子执行事务中。使用热土豆模式强制执行整条路线范围内有效性检查以确保不超出滑点容忍度。这也通过阻止对沿途涉及到的硬币进行错误使用来提高安全性, 因为某些子路径涉及用户指定输入和输出硬币之外的硬币. 通过在合同级别强制执行这些安全措施, 可以实现无需许可即可组合, 从而使其他人能够构建在SOR之上。

<figure><img src="../.gitbook/assets/spaces_meKfXaQnIP3bbI1AdlVX_uploads_7nSHyBIZhXijPzJBnCut_Screenshot 2024-02-21 at 11.webp" alt=""><figcaption><p>智能订单路由器交换分成多个子路径</p></figcaption></figure>

通过考虑无需许可的可组合性来设计我们的路由器，我们已经为其他 Sui 构建者简化了将 SOR 集成到他们的 dApps 中。当前的 SOR 集成包括 Aftermath 的[动态气体](../kai-shi-shi-yong/dong-tai-qi-ti.md)功能，在 [Nightly wallet](https://twitter.com/Nightly\_app)中进行钱包内交换，在 [Scallop](https://twitter.com/Scallop\_io) 工具 UI 中进行交换，以及通过 [Suiba](https://twitter.com/SuibaOnSUI) 电报机器人进行交易，更多集成即将宣布！
