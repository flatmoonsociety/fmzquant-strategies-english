
> Name

Dual-Moving-Average-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
The Double Moving Average Breakout Strategy is a very simple moving average trading strategy. It uses breakouts of fast and slow moving averages to generate trading signals. When the fast moving average breaks through the slow moving average from below, buy. When the fast moving average breaks through the slow moving average from above, sell.
## Strategy Principle
This strategy uses two sets of moving averages, including fast moving averages (mafast, mafastL) and slow moving averages (maslow, maslowL). The fast moving average parameter setting is smaller and can respond quickly to price changes; the slow moving average parameter setting is larger and has the effect of smoothing prices.
When short-term price trends converge to the long-term price trend, a crossover between the fast and slow moving averages occurs. Carry out buying or selling operations based on trading signals.
This strategy utilizes the Golden Cross and Death Cross trading signals of moving averages. When the short-term moving average breaks through the long-term moving average from bottom to top, it is a golden cross signal, which indicates a bullish trend; when the short-term moving average breaks through the long-term moving average from top to bottom, it is a dead cross signal, which indicates a bearish trend.
## Strategic advantage analysis
- Use dual moving average filtering to increase signal reliability. A single moving average can easily produce false signals, while double moving averages can effectively filter out market noise.
- Used together with fast and slow moving averages, it can effectively capture changes in trends. The fast line responds quickly and the slow line has good filtering effect.
- The strategic ideas are simple and clear, easy to understand and implement, and suitable for novices to learn.
- The moving average cycle parameters can be customized to adapt to different market environments.
## Strategy risk analysis
- Moving average strategies are prone to lag, especially in scenarios where trends change rapidly.
- The moving average parameters need to be optimized. Different period parameters have a great impact on the results.
- The double moving average strategy is only suitable for markets with obvious trends and is not suitable for consolidating markets.
- The frequency of transactions may be low, and there may be no transactions for a long time.
- Stop loss needs to be strictly controlled to avoid large floating losses.
## Strategy optimization direction
- Test and optimize the moving average cycle parameters to find the best parameter combination. Optimal parameters can be found through statistical methods.
- Added volume filtering to avoid generating false signals when volume is insufficient.
- Combined with other technical indicators, such as MACD, RSI, etc., to form a comprehensive trading system to improve signal accuracy.
- Add stop loss strategies, such as trailing stop loss, rollover stop loss, etc., to proactively control risks.
- Optimize position management, different markets adopt different position and fund management strategies.
## Summarize
The overall idea of ​​the double moving average breakthrough strategy is simple and clear. Using double moving average filtering can improve signal quality, and the combination of fast and slow moving averages can effectively capture trend changes. However, this strategy also has problems such as lag and false positives. It can be improved by optimizing parameters, adding filter conditions, stop loss strategies, etc. Generally speaking, the double moving average strategy is suitable for markets with obvious trends and can be used as an introductory strategy for novices to learn.
||


## Overview

The dual moving average breakout strategy is a very simple moving average trading strategy. It uses fast and slow moving average crossovers to generate trading signals. When the fast moving average crossover above the slow moving average from below, a buy signal is triggered. When the fast moving average crossover below the slow moving average from above, a sell signal is generated.

## Strategy Logic

This strategy employs two sets of moving averages, including fast moving average (mafast, mafastL) and slow moving average (maslow, maslowL). The fast moving average has smaller parameters and can respond quickly to price changes. The slow moving average has larger parameters and smoothes out prices.

When short-term price trends converge with long-term trends, crossovers between fast and slow moving averages happen. Trading signals are generated based on the crossovers. 

The strategy utilizes the golden cross and death cross trading signals of moving averages. When the short-term MA crosses above the long-term MA, a golden cross appears, indicating an uptrend. When the short-term MA crosses below the long-term MA, a death cross occurs, signaling a downtrend.

## Advantage Analysis 

- Using dual MAs filters out false signals effectively. Single MA can generate many fake signals while dual MAs filter out market noise.

- Fast and slow MAs complement each other well in capturing trend changes. Fast MA reacts quickly and slow MA filters well.

- The strategy logic is simple and easy to understand, suitable for beginners.

- Customizable MA period parameters adapt to different market environments.

## Risk Analysis

- MA strategies can lag, especially when trends change rapidly.

- MA parameters need to be optimized carefully as different periods lead to varied results.

- Dual MA strategies fit trending markets best, not suitable for range-bound markets.

- Trading frequency may be low, with long idle periods.

- Stop loss should be applied strictly to avoid huge floating loss.

## Optimization Directions

- Test and optimize MA period parameters to find the best combination, using statistical methods.

- Add volume filter to avoid wrong signals when volume is low.

- Incorporate other technical indicators like MACD, RSI to build a robust system with higher accuracy.

- Employ stop loss techniques like trailing stop loss, position transfer stop loss to control risks actively. 

- Optimize position sizing and money management for different market environments.

## Conclusion

The dual moving average breakout strategy has simple and clear logic. Dual MAs improve signal quality and fast-slow MAs capture trend changes well. But it also has lags and false signals. Improvements can be made by optimizing parameters, adding filters, applying stop loss etc. Overall, it is suitable for trending markets and a good starter strategy to learn.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|59|fastLength|
|v_input_2|82|fastLengthL|
|v_input_3|96|slowLength|
|v_input_4|95|slowLengthL|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-07 00:00:00
end: 2023-10-07 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/


//@version=2
strategy("OptimizedSisy4x", overlay=true,pyramiding=0,default_qty_type=strategy.cash,default_qty_value=20000,scale=true,initial_capital=10000,currency=currency.USD)
fastLength = input(59)
fastLengthL = input(82)

slowLength = input(96)
slowLengthL = input(95)
price = close

mafast = ema(price, fastLength)
mafastL= ema(price, fastLengthL)
maslow = ema(price, slowLength)
maslowL = ema(price, slowLengthL)



if (crossover(mafastL, maslowL))
    strategy.entry("SYS-LONG", strategy.long, comment="long")


if (crossunder(mafast, maslow))
    strategy.entry("SYS-SHORT", strategy.short, comment="short")
Target = 6250 
Stop = 3500
Q = 100



strategy.exit("Out Long", "SYS-LONG", qty_percent=Q, profit=Target, loss=Stop)
strategy.exit("Out Short", "SYS-SHORT", qty_percent=Q, profit=Target ,loss=Stop)

//plot(strategy.equity, title="equity", color=red, linewidth=2, style=areabr)
```

> Detail

https://www.fmz.com/strategy/428692

> Last Modified

2023-10-08 13:59:27
