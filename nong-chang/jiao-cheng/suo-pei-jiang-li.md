# 索赔奖励

一旦您将资金存入Afterburner Vault，您就可以监控您的仓位状态并执行各种操作。如果您已经在多个农场中抵押了资金，您可以导航到“投资组合”选项卡，选择“农场”选项卡，并轻松查看所有的农场仓位并转到它们各自的页面。有关更多信息，请参阅文档中的“[查看投资组合：农场](../../aftermath-dao-hang/cha-kan-nin-de-tou-zi-zu-he.md)”部分。

<figure><img src="../../.gitbook/assets/spaces_meKfXaQnIP3bbI1AdlVX_uploads_89wNspydTalA4IkgIuiA_Screenshot 2024-02-22 at 10.webp" alt=""><figcaption></figcaption></figure>

一旦您导航到Afterburner Vault页面，您将看到可以执行的几个操作。这些操作包括**添加质押、解除质押、延长锁定和领取奖励**。

<figure><img src="../../.gitbook/assets/spaces_meKfXaQnIP3bbI1AdlVX_uploads_zTPTefMAks9oP5rfuntQ_Screenshot 2024-02-22 at 10.webp" alt=""><figcaption></figcaption></figure>

**添加质押**允许您增加已承诺给农场的LP代币数量。如果选择此选项，您将能够在执行操作之前查看这将对您的位置造成的更改。可以查看指标，如新锁定剩余、新APY锁定提升和总APY以及质押金额。

<figure><img src="../../.gitbook/assets/spaces_meKfXaQnIP3bbI1AdlVX_uploads_yXqKaZSMF792GvRglxdf_Screenshot 2024-02-22 at 10.webp" alt=""><figcaption></figcaption></figure>

通过**延长锁定**，您可以通过将之前抵押的LP代币锁定更长时间来赚取额外奖励。如果选择此选项，您将能够在执行交易之前查看质押位置的变化，包括查看新的APY和新的剩余锁定时间。

<figure><img src="../../.gitbook/assets/spaces_meKfXaQnIP3bbI1AdlVX_uploads_x5Qonuoe1SPETW44aGSp_Screenshot 2024-02-22 at 10.webp" alt=""><figcaption></figcaption></figure>

**索赔奖励** 可以让您领取所有已存入钱包的奖励。然后，您就可以随心所欲地使用它们了。

<figure><img src="../../.gitbook/assets/spaces_meKfXaQnIP3bbI1AdlVX_uploads_kKb81siav3QLARpOnd2f_Screenshot 2024-02-22 at 10.webp" alt=""><figcaption></figcaption></figure>

在任何给定时间点，我们的前端显示了截至该时刻累积的准确奖励。然而，在奖励实现之前，应将其视为累积奖励的估计值。这意味着您索取奖励越频繁，您索取到的奖励就会更准确地与我们前端显示的内容相匹配。

我们的保险库利用了Sui固有的所有权语义。当您将资产（例如我们afSUI/SUI LP）质押到我们其中一个保险库中时，您创建了一个包装了您所抵押代币的仓位。由于保险库无法与您所拥有且仅属于您自己的抵押仓位进行交互 - 包括向您的仓位分发奖励，因此只有在签署一笔交易以与您的仓位进行交互后才会更新你仓位上面额外获得收益。 我们已经设置好这样做，以便任何操作都可以更新你仓位上面额外获得收益，并不仅限于索赔奖励行为。

作为这个仓位的所有者，您是唯一可以调用与之交互的交易的人。所有这些都是为了说明保险库绝对不会使用您质押的资金，因为它根本无法访问这些资金。

就是这样！如果您有任何问题，请随时在[Discord](https://discord.gg/tDDw5zYP)上联系Aftermath团队，我们将乐意帮助您。
