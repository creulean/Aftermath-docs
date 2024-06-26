---
cover: ../.gitbook/assets/截屏2024-03-19 22.43.07 (1).png
coverY: 0
---

# 恒定函数做市商

与SUI上所有其他AMM不同，后续提供了每个池最多可容纳8种资产的恒定函数做市商。这为什么重要？对于像Sui这样新兴生态系统来说，大部分流动性将通过桥接方式到达。

不幸的是，从不同链和/或不同桥接器到达的资产并非可互换。这意味着如果你从Arbitrum桥接一枚ETH代币，你无法在一个由相同代币组成但是从Solana桥接而来的池中交易它。或者通过另一个桥梁到达。

我们对这个问题的解决方案是将所有类似代币放在一起进行汇集，使用稳定交换不变量将它们的价值锚定在大致相同，并允许各种代币之间进行轻松低滑点交易。

<figure><img src="../.gitbook/assets/spaces_meKfXaQnIP3bbI1AdlVX_uploads_0U3CeTidN8RBkXNiWgdD_Screenshot 2024-02-22 at 9.webp" alt=""><figcaption><p>Aftermath Wormhole的多资产池</p></figcaption></figure>

我们的CFMM还支持不相关资产，用于ETH、BTC、SUI、USDC等池，或者用户想要的任何其他组合，以相对权重。除了促进池中多个币种之间的高效交换外，这些不相关池还允许创建不同类型的篮子。例如，您可以创建一个蓝筹指数或者模因币指数，每个单独币种代表总池的任意百分比即可长达它们总和为100。

创建池是完全无需权限的，为社区提供了完全创作自由来部署他们最感兴趣的池。
