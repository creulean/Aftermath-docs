# 架构

**架构和用法**

Afterburner Vault 本质上是一个农场保险库，根据质押金额发放奖励。该产品有两个版本：Strict 和 Relaxed，下面解释了它们之间的区别。

功能封装在 afterburner\_vaults 包中，并分散在两个子包中：**保险库** 和 **质押仓位**。
