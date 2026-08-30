
> Name

Cross-Moving-Average-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/17bebcd04c5bf748668.png)
[trans]
## Overview
This strategy is a cross-moving average reversal strategy based on a simple moving average. It uses a simple moving average with a length of 1 and a length of 5. When the short-period moving average crosses the long-period moving average from below, it goes long and when it crosses below the long-period moving average, it goes short. It is a typical trend following strategy.
## Strategy Principle
This strategy calculates the 1-day simple moving average sma1 and the 5-day simple moving average sma5 of the close price, and enters long when sma1 crosses sma5, and enters short when sma1 crosses below sma5. After going long, set the stop loss at $5 below the entry price and the take profit at $150 above the entry price; after going short, set the stop loss at $5 above the entry price and the take profit at $150 below the entry price.
## Advantage Analysis
- Use double moving averages to determine the direction of the market trend and avoid entering the market in the opposite direction immediately after stopping the loss.
- The moving average parameters are simple and reasonable, and the backtest results are good
- The stop loss range is small and can withstand certain market fluctuations
- The take-profit range is large to obtain sufficient profits
## Risk Analysis
- The double moving average strategy is easy to be trapped, and the probability of stop loss is high when the market fluctuates.
- Unable to effectively track market trends, limited long-term profitability
- The parameter optimization space is limited and it is easy to over-optimize
- For specific trading varieties, parameters need to be adjusted for different varieties.
Optimization direction:
- Add other indicator filters to avoid false signals
- Dynamically adjust stop loss and take profit ranges
- Optimize moving average parameters
- Combined with volatility indicators to control position size
## Summarize
As a simple double moving average strategy, this strategy is simple to operate and easy to implement, and can quickly verify strategic ideas. However, its affordability and profit margin are relatively limited, and parameters and filtering conditions need to be optimized to adapt to more market environments. A first quant strategy for beginners, it contains the basic building blocks and serves as a simple framework for iterable improvements.
||

## Overview

This is a reversal strategy based on simple moving average crossover. It uses 1-day and 5-day simple moving averages. When the shorter SMA crosses above the longer SMA, it goes long. When the shorter SMA crosses below the longer SMA, it goes short. It's a typical trend following strategy.  

## Strategy Logic

The strategy calculates the 1-day SMA (sma1) and 5-day SMA (sma5) of the closing price. When sma1 crosses over sma5, it enters a long position. When sma1 crosses below sma5, it enters a short position. After opening a long position, the stop loss is set at 5 USD below the entry price and take profit at 150 USD above. For short positions, stop loss is 5 USD above entry and take profit 150 USD below.

## Advantage Analysis   

- Using double SMAs to determine market trend, avoiding loss trades after stop loss
- SMA parameters simple and reasonable, good backtest results  
- Small stop loss to withstand certain price fluctuations
- Big profit target to make enough money 

## Risk Analysis

- Double SMAs are prone to whipsaws, high probability of stop loss when choppy
- Hard to catch trending moves, limited profit for long term trades 
- Limited optimization space, easy to overfit
- Parameters need adjustment for different trading instruments

## Improvement Directions

- Add other filters to avoid wrong signals
- Dynamic stop loss and take profit  
- Optimize SMA parameters 
- Combine volatility index to control position sizing  

## Conclusion

This simple double SMA strategy is easy to understand and implement for fast strategy verification. But it has limited risk tolerance and profit potential. Further optimizations are needed in parameters and filters to adapt more market conditions. As a starter quant strategy, it contains basic building blocks for iterable improvements.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-02-19 00:00:00
end: 2024-02-19 00:00:00
period: 2d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Valeria 181 Bot Strategy Mejorado 2.21", overlay=true, margin_long=100, margin_short=100)
 
var float lastLongOrderPrice = na
var float lastShortOrderPrice = na

longCondition = ta.crossover(ta.sma(close, 1), ta.sma(close, 5))
if (longCondition)
    strategy.entry("Long Entry", strategy.long)  // Enter long

shortCondition = ta.crossunder(ta.sma(close, 1), ta.sma(close, 5))
if (shortCondition)
    strategy.entry("Short Entry", strategy.short)  // Enter short

if (longCondition)
    lastLongOrderPrice := close

if (shortCondition)
    lastShortOrderPrice := close

// Calculate stop loss and take profit based on the last executed order's price
stopLossLong = lastLongOrderPrice - 5  // 10 USDT lower than the last long order price
takeProfitLong = lastLongOrderPrice + 151  // 100 USDT higher than the last long order price
stopLossShort = lastShortOrderPrice + 5  // 10 USDT higher than the last short order price
takeProfitShort = lastShortOrderPrice - 150  // 100 USDT lower than the last short order price

// Apply stop loss and take profit to long positions
strategy.exit("Long Exit", from_entry="Long Entry", stop=stopLossLong, limit=takeProfitLong)

// Apply stop loss and take profit to short positions
strategy.exit("Short Exit", from_entry="Short Entry", stop=stopLossShort, limit=takeProfitShort)
```

> Detail

https://www.fmz.com/strategy/442222

> Last Modified

2024-02-20 13:59:46
