---
description: 适用于 Sui 的 Aftermath Finance 官方脚本类型SDK
---

# 入门

## 安装

{% code overflow="wrap" %}
```javascript
npm i aftermath-ts-sdk
```
{% endcode %}

## 使用方法

创建一个 Aftermath 实例，以便于调用我们的服务器，或创建一个 Aftermath API 实例，以便更精细地控制事务构建。

## Aftermath SDK

### 1.创建 Aftermath provider

{% code fullWidth="false" %}
```javascript
const afSdk = new Aftermath("MAINNET"); // "MAINNET" | "TESTNET" | "DEVNET"
await afSdk.init(); // initialize provider
```
{% endcode %}

### 2.创建 protocol provider

```javascript
const router = afSdk.Router(); 
const pools = afSdk.Pools(); 
const staking = afSdk.Staking(); 
const farms = afSdk.Farms();
```

## Aftermath API <a href="#aftermath-api" id="aftermath-api"></a>

### 1.创建 Aftermath API provider

```javascript
const fullnodeEndpoint = "https://fullnode.mainnet.sui.io";
const addresses = {...};

const afApi = new AftermathApi(
    new SuiClient({
        transport: new SuiHTTPTransport({
            url: fullnodeEndpoint,
        }),
    }),
    addresses,
    new IndexerCaller("MAINNET"), // "MAINNET" | "TESTNET" | "DEVNET"
);
```

### 2.创建 new protocol provider

```javascript
const poolsApi = afApi.Pools(); 
const stakinApi = afApi.Staking(); 
const farmsApi = afApi.Farms();
```
