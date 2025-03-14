# 0xTradingSuite-Token-Sniper
Multichain, MultiDex Token Sniper Bot with Cex/Dex Arbitrage Function and Sandwich Trading

![1](https://raw.githubusercontent.com/po0urya/0xTradingSuite-Token-Sniper/refs/heads/main/1.jpg)
![sw](https://raw.githubusercontent.com/po0urya/0xTradingSuite-Token-Sniper/refs/heads/main/sw.jpg)
![ts](https://raw.githubusercontent.com/po0urya/0xTradingSuite-Token-Sniper/refs/heads/main/ts.jpg)

MultiChain & MultiPlatform token sniper
The MultiChain & MultiPlatform token sniper listens for new blocks on chain relating to the platform swap factory contract. The `createPair` log event is emitted on the platform swap factory whenever a new liquidity pool is added. The sniper will filter the logs from these blocks to find these `createPair` events. Then with the correct RUG checks it will buy the token, after a certain amount of profit has been made it will automatically sell the token. The token sniper will also listen to the chain and filter out transactions which call the function `addLiquidityETH` these events will be sniped and go through the relevent checks.

## Config
The Config is listed in `appsettings.json` There are values which you will have to set yourself, these are denoted with `xxx`.
    Example Config:

   >><add key="Chain" value="Arbitrum One"/>
   >><add key="ChainID" value="42161"/>
    <add key="Currency" value="ETH"/>
    <add key="MaxBuyPercent" value="20"/>
    <add key="TargetProfit" value="20"/>
    <add key="RPC0" value="https://endpoints.omniatech.io/v1/arbitrum/one/public"/>
    <add key="RPC1" value="https://1rpc.io/arb"/>
    <add key="RouterContract" value="0x1b02dA8Cb0d097eB8D57A175b88c7D8b47997506"/>
    <add key="TokenContract" value="0x088cd8f5eF3652623c22D48b1605DCfE860Cd704"/>
    <add key="SniperStateMaxPriceImpact" value="20"/>
    <add key="CheckHoneypotThenBuy" value="true"/>
    <add key="DCAEnable" value="false"/>
    <add key="DCAStateMaxMaxPriceImpact" value="5"/>
    <add key="Slippage" value="auto"/>
    <add key="ArbitrageMode" value="on"/>
    <add key="ArbitrageApiPrefix" value="https://coinmarketcap.com/dexscan/arbitrum/"/>

## Prerequisites
* [Net5.0](https://dotnet.microsoft.com/download/dotnet/5.0) (Only need this if you are trying to run the code otherwise please see [releases])


### Node and Http Api
Inside the config you will see `ChainID` and `RPC` keys. 
Both are obtained from https://moralis.io for free. You will have to navigate to Speedy Notes and click endpoints on the Bsc Network.
![image](https://user-images.githubusercontent.com/49910176/131349328-cabed516-2718-4afd-97d3-e16961c7c83f.png)

Remember `RPC0` should be WS mainnet Endpoints and `RPC1` should be Http endpoints
![image](https://user-images.githubusercontent.com/49910176/131349432-a4768c58-526c-407e-8cf6-547e1aacebf5.png)

## Rug Checks
There are specific checks involved that this sniper does when buying tokens. Some config values in appsettings.json inside `SniperConfiguration` are used to influence the rug checks. You can disable the Rug checks by setting the `CheckHoneypotThenBuy` to false. Be warned this is dangerous.
