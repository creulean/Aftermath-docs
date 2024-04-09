---
description: 智能订单路由器可为特定交易在多个交易池和协议中找到最佳交易路由。
---

# 路由器

```javascript
const router = new Aftermath("TESTNET").Router();
```

## 交易路由

### 1.创建交易路线

```javascript
const route = await router.getCompleteTradeRouteGivenAmountIn({
	coinInType: "0x...",
	coinOutType: "0x...",
	coinInAmount: 1_000_000_000n,
	
	// optional
	referrer: "0x...",
	externalFee: {
		recipient: "0x...",
		feePercentage: 0.01, // 1% fee from amount out
	},
});

console.log(route);
/*
{
	coinIn: {
		type: "0x1...",
		amount: 1_000_000n,
		tradeFee: 1_00_000_000_000_000_000n, // 0.1% (18 decimals)
	},
	coinOut: {
		type: "0x2...",
		amount: 1_100_000n,
		tradeFee: 0n, // 0% (18 decimals)
	},
	spotPrice: 0.90909090909, // in/out (ignoring fees)
	routes: [...],
	
	// optional
	referrer: "0x...",
	externalFee: {
		recipient: "0x...",
		feePercentage: 0.01, // 1% fee from amount out
	},
}
*/
```

### 2.获取交易

```javascript
const tx = await router.getTransactionForCompleteTradeRoute({
	walletAddress: "0x...",
	completeRoute: route,
	slippage: 0.01,	// 1% max slippage
});
```
