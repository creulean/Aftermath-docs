---
description: 在 Sui 上质押 SUI 并获得 afSUI，以赚取可靠的收益，并持有最分散的质押衍生品。
---

# 流动性质押

## afSUI SDK

```javascript
const staking = new Aftermath("TESTNET").Staking();
```

## 交易

### Staking Positions <a href="#staking-positions" id="staking-positions"></a>

```javascript
const stakingPositions = await staking.getStakingPositions({
    walletAddress: "0x..",
});
```

### Stake

```javascript
const tx = await staking.getStakeTransaction({
    walletAddress: "0x..",
    suiStakeAmount: 1_000_000_000n, // 1 Sui
    validatorAddress: "0x..",
});
```

### Unstake

```javascript
const tx = await staking.getUnstakeTransaction({
    walletAddress: "0x..",
    afSuiUnstakeAmount: 1_000_000_000n, // 1 AfSui
    isAtomic: true,
});
```

## 检查

### Staked SUI TVL <a href="#staked-sui-tvl" id="staked-sui-tvl"></a>

```javascript
const suiTvl = await staking.getSuiTvl();

console.log(suiTvl);
// 9_540_200_000n
```

### afSUI Exchange Rate

```javascript
// (1 SUI = x afSUI)
const afSuiExchangeRate = await staking.getAfSuiExchangeRate();
console.log(afSuiExchangeRate);
// 1.000149000231
```

## afSUI API <a href="#afsui-api" id="afsui-api"></a>

```javascript
const testnetStakingAddresses = {
    staking: {
        packages: {
            events:
"0x58e6bdd081ae6035141871a1c7cdf82895e944a8b7673f78d22e370a07cbf99b",
            lsd:
"0x58e6bdd081ae6035141871a1c7cdf82895e944a8b7673f78d22e370a07cbf99b",
            afsui:
"0x5783fa2298e7301a1c7f99ce45d4a207478fbf3003eca9482ae823d6f6c7cd60",
        },
        objects: {
            stakedSuiVault:
"0x690f36f9c5249b0c4c9b3efdf8a2864c750a8021037360e3b7bedc9ceafb277f",
            safe:
"0x091686a693e86929f91ef539d867fae334a33d124bc2c204dcb3b53dd9016501",
            treasury:
"0xf3d41534e43ecf36da8657b48350a09a3e50eeb2ce61f8ceb80e6d2f85828bc0",
            referralVault: 
"0x8d357115058f22976cd01c5415116d9aca806d1ded37eecd75d87978f404e927",
            validatorConfigsTable:
"0xc9b9c0f1115793a24e0551609e51daa5ffe2b11429d12b46fdf8a3b0bfc0e908",
         },
     },
 },
 
 const afApi = new AftermathApi(
     new SuiClient({
         transport: new SuiHTTPTransport({
             url: "https://testnet.mainnet.sui.io",
         }),
     }),
     testnetStakingAddresses,
     new IndexerCaller("TESTNET"),
 );
 
 const stakingApi = afApi.Staking();
```

## Transaction Command Examples <a href="#transaction-command-examples" id="transaction-command-examples"></a>

```javascript
const stakingApi = afApi.Staking();

const suiCoin = await afApi.Coin().fetchCoinWithAmountTx({
    walletAddress: "0x...",
    coinType: "0x02::sui::SUI",
    coinAmount: BigInt(1_423_837_387), // ~1.4 SUI
});

const afSuiCoin = stakingApi.stakeTx({
    tx,
    suiCoin,
    validatorAddress: "0x...",
});

stakingApi.atomicUnstakeTx({
    tx,
    afSuiCoin,
    withTransfer: true
});
```
