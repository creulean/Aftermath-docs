---
description: 该协议提供以下切入点：
---

# 进入点

## AFSUI 获取器

**public fun afsui\_to\_sui\_exchange\_rate()：**返回当前时代的AFSUI<->SUI汇率。

**public fun afsui\_to\_sui()：**给定 AFSUI 金额返回相应的 SUI 金额。

**public fun sui\_to\_afsui\_exchange\_rate()：**返回当前纪元的SUI<->AFSUI汇率。

**public fun sui\_to\_afsui()：**给定 SUI 金额返回相应的 AFSUI 金额。

**public fun total\_sui\_amount()：** 返回在协议中锁定的总 SUI 金额（所有本金 + 奖励）

## 总金额获取器

**public fun total\_rewards\_amount()：**返回已收集的奖励总金额。&#x20;

**public fun epoch\_was\_changed()：**启动纪元更改处理。可能需要连续调用多次。

## 质押

**public fun request\_stake()：**将 SUI 硬币委托给指定的验证器，并立即返回等量的 AFSUI。请注意，验证器必须处于激活状态。&#x20;

**entry fun request\_stake\_and\_keep()：**Keep 版本，直接将 AFSUI 转入交易发送方账户。&#x20;

**public fun request\_stake\_vec()：**获取 SUI 硬币向量，将其加入指定的验证器，并立即返回等值的 AFSUI。请注意，验证器必须处于激活状态。

entry fun request\_stake\_vec\_and\_keep()：直接将 AFSUI 转入交易发送方账户的 Keep 版本。&#x20;

**public fun request\_stake\_staked\_sui()：**对提供的 StakedSui 对象进行再入股，提取相应金额的 AFSUI 并返回。&#x20;

**public fun request\_stake\_staked\_sui\_and\_keep()：**保留版本，直接将 AFSUI 转入交易发送者账户。&#x20;

**public fun request\_stake\_staked\_sui\_vec()：**获取 StakedSui 对象的矢量，重新获取它们，铸入相应金额的 AFSUI 并返回。&#x20;

**public fun request\_stake\_staked\_sui\_vec\_and\_keep()：**直接将 AFSUI 转入交易发送者账户的 Keep 版本。

## 定期解除质押

**public fun request\_unstake()：**该方法获取 AFSUI 作为输入，注册请求，以便在下一个纪元开始时提取相应数量的 SUI。&#x20;

**public fun request\_unstake\_vec()：**该方法获取 AFSUI 硬币向量作为输入，将它们连接起来，并注册请求，以便在下一个纪元开始时铸造相应数量的 SUI 硬币。

## 原子质押解除

**public fun request\_unstake\_atomic()：**该方法获取 AFSUI 硬币作为输入，并立即返回相应数量的 SUI。&#x20;

**entry fun request\_unstake\_atomic\_and\_keep()：**keep 版本直接将 SUI 转入交易发送者账户。&#x20;

**public fun request\_unstake\_vec\_atomic()：**该方法以 AFSUI 硬币向量为输入，将它们合并为一个向量，并立即返回相应的 SUI 金额。&#x20;

**public fun request\_unstake\_vec\_atomic\_and\_keep()：**保留版本，直接将 SUI 转入交易发送方账户。

## 验证费

**public fun rotate\_operation\_cap()：**创建并注册新的操作能力对象。&#x20;

**public fun update\_validator\_fee()：**更改相应的验证器费用。
