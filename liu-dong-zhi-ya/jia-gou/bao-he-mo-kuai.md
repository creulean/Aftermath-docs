# 包和模块

## AftermathLSD 包

<figure><img src="../../.gitbook/assets/spaces_meKfXaQnIP3bbI1AdlVX_uploads_2iybTRxy4apZVxlThgPP_Screenshot 2024-02-22 at 11.webp" alt=""><figcaption><p>AftermathLSD包 图样</p></figcaption></figure>

包的功能分布在多个模块之间。主要模块介绍如下：

## _staked\_sui\_vault模块_

该模块实际上是一个接口，允许与协议进行交互。它为协议用户提供了主要的进入点。可以使用以下功能：

1. 质押请求：用户向协议提供SUI币，并根据当前时代的SUI <-> AFSUI汇率立即收到相应数量的AFSUI。
2. 解除抵押请求：用户提供 AFSUI 并收到相应数量的 SUI。有两种可能性。常规解锁，用户在下一个纪元开始时收到他的 SUI。原子解锁，用户立即收到他的 SUI。还可以重新抵押 StakedSui 对象。
3. 时代更替处理：Sui质押框架工作流程与时代更替处理紧密耦合。在每两个时代之间，Sui框架执行几项活动。最重要的是奖励收集和权益激活。为了在协议中反映这一点，必须触发一个摇柄功能。由于Sui框架的限制，很可能需要多次触发该功能。在进行时代更替处理之前，协议被视为处于未定义状态并且不起作用。一旦触发摇柄功能，就会收到激励支付。为了使时代更替处理顺利进行，Aftermath运行了一个监控Sui链状态并及时启动时代处理的机器人。
4. 更新验证器费用：如果协议知道有一个验证器，该验证器将收到操作能力对象，允许更改特定验证器的验证器费用。 验证器费用从每个铸造的AFSUI中扣除，并直接发送到验证器地址。

<figure><img src="../../.gitbook/assets/spaces_meKfXaQnIP3bbI1AdlVX_uploads_hI3nhxih7ru4QAt0JEkP_Screenshot 2024-02-22 at 11.webp" alt=""><figcaption><p>AftermathLSD协议stake_sui_vault模块图解</p></figcaption></figure>

## 行动模块

该模块实现了协议的业务逻辑，这些逻辑在staked\_sui\_vault模块描述中已经讨论过。

## staked\_sui\_vault\_state模块

该模块提供了staked sui vault的实际实现。它被授权铸造和销毁AFSUI。它还负责协议配置。主要目的是保持所有StakedSui对象和SUI余额。为了组织StakedSuis，使用了一个存储实体。

## 存储模块

存储是一个抽象概念，它允许我们保存 StakedSui 对象并实现取消记录的逻辑。取消认注本身就是 LSD 协议的重要组成部分，因为从某种意义上说，它决定了协议的性能。为了实现这一点，存储库中有一个解押队列，该队列按验证器性能升序排序，因此不活动和性能低的验证器的赌注将首先被解押。为避免验证器瞬间耗尽，每次解押都会在多个验证器之间进行分配。

## 验证器模块

该模块实现了操作能力对象逻辑。该对象允许更改特定验证器的验证器费用值。

Aftermath LSD 协议使用多个附加软件包。

## 安全包

软件包提供了一个名为 Safe 的模块。该模块允许存储任何类型的对象，并向授权模块提供该对象的可变引用。只能授权一个模块。LSD 协议使用该实体来存储 AFSUI 库，并提供从已标记的 sui 金库状态模块的授权访问。

## 推荐保险库包

Aftermath LSD 协议用户可使用推荐系统。该模块提供了管理推荐人与被推荐人关系和收取版税的逻辑。

## 财政包

该协议正在收取几类费用。国库实体允许我们收取特定部分的费用，并在以后用于不同的目的。

## 实用程序包

Aftermath 高性能数学原语和函数集。

## LinkedSet包

LinkedSet 基于 Sui 框架的链接表实现。该实体用于实现未记录队列。

## SuiSytemUtils包

与 Sui 生态系统互动的方法集。
