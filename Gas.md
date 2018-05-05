# 什么是以太坊gas？

```
What is Gas?
Gas is a unit of measuring the computational work of running transactions or smart contracts in the Ethereum network. This system is similar to the use of kilowatts (kW) for measuring electricity in your house; the electricity you use isn’t measured in dollars and cents but instead through kWH or Kilowatts per hour.
什么是Gas？
Gas是测量以太坊网络中运行交易或智能合约的计算工作的单位。该系统类似于使用千瓦（kW）来测量房屋内的电力;您使用的电力不是以美元和美分计量，而是以每小时千瓦时或千瓦计。
```

Gas用来衡量执行某些动作需要多少“工作量”，这些“工作量”就是为了执行该动作支付给网络的费用额。通俗理解，Gas是给矿工的佣金，以ETH 支付，无论是交易、执行智能合约并启动 DApps，还是支付数据存储费用，都需要用到 Gas。

# 为什么引入gas系统？
- 激励

像任何工作对等系统一样，以太坊严重依赖矿工的哈希效率：更多的矿工，更多的哈希效率，更安全和快速的系统。为了吸引更多的矿工进入Ethereum，需要使Ethereum对矿工有利可图并尽可能诱人。

- 确保网络不会因为进行大量密集的工作而陷入僵局

由于Ethereum允许运行任意复杂的计算机代码，所以很短的代码实际上可以导致大量的计算工作才能完成。执行的每个操作（或合同执行）交易都要求支付其相应的费用，这样确保没有任何东西永远运行，而且人们会对他们运行的代码注意一点， 它使矿工和用户都能安全避免错误的代码！

# Gas Limit and Gas Price

```
Gas Limit
Gas limit refers to the maximum amount of gas you’re willing to spend on a particular transaction.
是指您愿意花费在特定交易上的最大气量。
```

```
Gas Price
Gas price refers to the amount of Ether you’re willing to pay for every unit of gas, and is usually measured in “Gwei”.
天然气价格是指你愿意为每个单位天然气支付的乙醚量，通常以“Gwei”来衡量。
```
如果您指定的gas太少，该怎么办？
您的交易最初将由矿工执行，但一旦gas用完，矿工将停止执行交易的工作。 区块链会将交易记录为“失败”，并且由于没有足够的gas来完全执行转帐，您的ETH仍将存在您的钱包中。 用于交易失败的gas将由矿工为他们的工作保留，并且您不会收回。
如果你指定的gas太少，这将会发生什么、交易会失败、失败原因是out of gas。

看一笔交易
https://etherscan.io/tx/0xddea7479a72bbb290b596ce34c6445f890bdf67ed02a9fa26b304de2e22f33a7
```
Gas Limit：用户为此次交易支付的最大gas量。本例子中，标准ETH转帐的默认金额为21,000gas
Gas Used by Txn：用于执行交易的实际gas量。 本例子中，由于这是标准转移，所用的气体也是21,000gas
Gas Price：用户准备为每个单位gas支付的ETH金额。 本例子中用户选择为每个gas单位支付5 Gwei。
Actual Tx Cost Fee：这是用户将为以Ether值进行的交易支付的实际费用金额。 本例子中是0.000105 Ether ($0.07)
Transaction (Tx) Fees=Gas Used by Txn * Gas Price
```










