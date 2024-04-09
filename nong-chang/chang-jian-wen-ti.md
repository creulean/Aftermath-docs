# 常见问题

## **如何计算奖励？**

每个抵押头寸仓位赚取的年化利率是未领取奖励存入保险库当前时期的数量、抵押头寸相对于存入保险库的LP代币总量的大小，以及通过锁定一定时间获得的任何奖励倍增器所决定。

用于确定每个农业库的排放率的计算如下：

```
const emissionRateUsd =
            Coin.balanceWithDecimals(rewardCoin.emissionRate, decimals) * price;

        dayjs.extend(duration);
        const oneYearMs = dayjs.duration(1, "year").asMilliseconds();
        const rewardsUsdOneYear =
            emissionRateUsd * (oneYearMs / rewardCoin.emissionSchedulesMs);

        const apy = rewardsUsdOneYear / tvlUsd;
```

每个用户仓位所获奖励的计算方法是：用金库的总排放量除以每个仓位与投入金库的 LP 代币总数相比的相对大小。请注意，任何应用了锁定乘数的仓位都会按比例增加累积奖励。

每个仓位的一般年利率（APR）计算如下：

```
dayjs.extend(duration);
const oneYearMs = dayjs.duration(1, "year").asMilliseconds();
const timeSinceLastHarvestMs =
  dayjs().valueOf() - this.trueLastHarvestRewardsTimestamp;

const rewardsUsdOneYear =
  timeSinceLastHarvestMs > 0
    ? rewardsUsd * (oneYearMs / timeSinceLastHarvestMs)
    : 0;

const apr = stakeUsd > 0 ? rewardsUsdOneYear / stakeUsd : 0;
return apr < 0 ? 0 : apr;
```

在任何给定的时间点，我们的前端都会准确显示该时刻应计的奖励。但是，在奖励兑现之前，应将其视为应计奖励的估计值。这意味着您申请奖励的次数越多，您申请的奖励就越准确，也就越符合我们前端显示的奖励。

我们的保险库利用了Sui固有的所有权语义。当您将资产（例如我们的afSUI/SUI LP）抵押到我们的某个保险库中时，您创建了一个包装了您所抵押币种的头寸。作为这个头寸的所有者，只有您才能调用与之交互的交易。总而言之，保险库绝对不会处理您抵押资金，因为它根本无法访问这些资金。

我们的保险库无法与您的抵押头寸进行交互 - 因为它们归您所有，只有您拥有 - 包括向您的头寸分发奖励。因此，在您签署交易以与您的头寸进行交互之后，才会在链上更新您头寸的奖励。我们已经设置了这一点，以便任何操作都将更新您头寸累积的奖励，并不仅限于领取奖励行为。

## **为什么我不能锁定？**

我们的保险库设计为不允许用户将其位置锁定到当前时期结束之后，因为奖励每个时期都会完全分配。如果您无法锁定您的位置，这意味着当前时期即将结束。目前，这种情况每两周的星期日发生一次。当新的时代开始、运行时间以及将分配的激励金额确定后，Aftermath总是在推特上宣布。如果无法锁定，请查看我们的推特动态以获取公告，并在发布后再次尝试。

## **我可以自动复利奖励或自动重新锁定吗？**

在Sui上这些是可能的，但我们选择反对这样做的主要原因是：我们希望您作为用户能够保持对您位置的控制。就目前而言，您拥有自己的锁定的仓位，并且由于Sui上的所有权语义，只有您可以签署涉及此对象的交易。这意味着我们无法添加赌注（自动补仓）或更改锁定期限（自动锁定），因为我们无法直接与您的赌注头寸进行交互。

这些功能是可以创建的，但会删除 Sui 本身所具有的所有权属性。如果用户对这些功能有需求，这绝对值得考虑，但我们希望确保用户了解，如果他们选择这些功能，他们将放弃的所有权。

顺便提一句，您所押注的 LP 硬币将保存在您所押注的头寸中，因此除非您先签字，否则Aftermath或其他合约不可能与之互动。这是一个神奇的功能，也是 Sui 的众多优点之一！

## **农业排放会持续多久？**

目前，排放量以两周为一个周期，一个周期结束，下一个周期从周日开始。

## **我如何知道 Afterburner 保险库何时新增奖励？**

Aftermath 总是在 [twitter](https://twitter.com/AftermathFi) 上公布新纪元的开始时间、持续时间和奖励金额。

## **如何质押/取消质押/领取奖励？**

有关如何执行每个操作的说明，请参阅文档中的 "[质押到农场](jiao-cheng/jiang-zi-chan-di-ya-dao-nong-chang.md)"、"[索赔奖励](jiao-cheng/suo-pei-jiang-li.md)"和 "[解除质押](jiao-cheng/jie-chu-zhi-ya.md)"部分。

## **如何跟踪我的所有农场头寸？**

查看您的投资组合：参阅文档中的 "农场 "部分，了解如何通过[投资组合](../aftermath-dao-hang/cha-kan-nin-de-tou-zi-zu-he.md)监控所有农场头寸。

