---
description: 稳定和不相关资产的可变权重 AMM 池，每个池最多 8 项资产。
---

# 池

```javascript
const pools = new Aftermath("TESTNET").Pools();
```

## 池子

```javascript
// single pool
const pool = await pools.getPool({
	objectId: "0x..",
});

// multiple pools
const somePools = await pools.getPools({
	objectIds: ["0x1..", "0x2.."],
});

// all pools
const allPools = await pools.getAllPools();
```

## 事件

### Deposit

```javascript
const eventData = await pool.getDepositEvents({
	// optional
	cursor: {
		txDigest: "0x..",
		eventSeq: "0x..",
	},
	limit: 10,
});

console.log(eventData);
/*
{
	events: [
		{
			poolId: "0x..",
			depositor: "0x.."
			types: ["0x1..", "0x2..", "0x3.."],
			deposits: [1_000n, 1_000_000n, 500n],
			lpMinted: 34_000_000n,
		},
		...
	],
	nextCursor: {...},
}
*/
```

### Withdraw

```javascript
const eventData = await pool.getWithdrawEvents({
	// optional
	cursor: {
		txDigest: "0x..",
		eventSeq: "0x..",
	},
	limit: 10,
});

console.log(eventData);
/*
{
	events: [
		{
			poolId: "0x..",
			withdrawer: "0x.."
			types: ["0x1..", "0x2..", "0x3.."],
			withdrawn: [1_000n, 1_000_000n, 500n],
			lpBurned: 34_000_000n,
		},
		...
	],
	nextCursor: {...},
}
*/
```

## 交易

### Deposit

```javascript
const tx = await pool.getDepositTransaction({
	walletAddress: "0x..",
	amountsIn: {
		"0x1..": 1_000_000_000n,
		"0x2..": 50_000_000n,
		"0x3..": 700_000n,
	},
	slippage: 0.01,	// 1% max slippage
	
	// optional
	referrer: "0x..",
});
```

### Withdraw

```javascript
const tx = await pool.getWithdrawTransaction({
	walletAddress: "0x..",
	// Amounts out approximation for coins wanting to withdraw
	amountsOutDirection: {
		"0x1..": 1_000_000_000n,
		"0x3..": 700_000n,
		"0x5..": 5_000_000n,
	},
	lpCoinAmount: 1_000_000_000n, // LP coin amount being sent
	slippage: 0.01,	// 1% max slippage
	
	// optional
	referrer: "0x..",
});
```

## 计算

### Spot Price <a href="#spot-price" id="spot-price"></a>

```javascript
const spotPrice = pool.getSpotPrice({
	coinInType: "0x1...",
	coinOutType: "0x2...",
	
	// optional
	withFees: true,
});

console.log(spotPrice); // in/out
// 1.22312342123412
```

### Trade Amount Out <a href="#trade-amount-out" id="trade-amount-out"></a>

```javascript
const amountOut = pool.getTradeAmountOut({
	coinInType: "0x1...",
	coinOutType: "0x2...",
	coinInAmount: 1_000_000n,
	
	// optional
	referral: true, // apply referral discount to calculation
});

console.log(amountOut);
// 1_200_000n
```

### Trade Amount In <a href="#trade-amount-in" id="trade-amount-in"></a>

```javascript
const amountIn = pool.getTradeAmountIn({
	coinInType: "0x1...",
	coinOutType: "0x2...",
	coinOutAmount: 1_200_000n,
	
	// optional
	referral: true, // apply referral discount to calculation
});

console.log(amountIn);
// 1_000_000n
```

### Deposit LP Amount Out <a href="#deposit-lp-amount-out" id="deposit-lp-amount-out"></a>

```javascript
const depositResult = pool.getDepositLpAmountOut({
	amountsIn: {
		"0x1..": 1_000_000_000n,
		"0x2..": 50_000_000n,
		"0x3..": 700_000n,
	},
	
	// optional
	referral: true, // apply referral discount to calculation
});

console.log(depositResult);
/*
{
	lpAmountOut: 6_500_000_000n, // 6.5 (9 decimals)
	lpRatio: 1.01342132, // LP ratio after deposit
}
*/
```

### Withdraw Amounts Out <a href="#withdraw-amounts-out" id="withdraw-amounts-out"></a>

```javascript
const amountsOut = pool.getWithdrawAmountsOut({
	lpRatio: 0.98988789, // LP ratio after withdraw
	// Amounts out approximation for coins wanting to withdraw
	amountsOutDirection: {
		"0x1..": 1_000_000_000n,
		"0x3..": 700_000n,
		"0x5..": 5_000_000n,
	},
	
	// optional
	referral: true, // apply referral discount to calculation
});

console.log(amountsOut);
/*
{
	"0x1..": 1_130_000_000n,
	"0x3..": 710_000n,
	"0x5..": 5_400_000n,
}
*/
```
