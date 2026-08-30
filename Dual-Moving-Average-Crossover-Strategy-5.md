
> Name

Dual-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/18d6d545a7e83002ff8.png)
[trans]

### Overview
This strategy uses simple moving average crossovers and average true volatility indicators to generate buy and sell signals, and is a trend following strategy. Mainly use the intersection of the 50-day moving average and the 100-day moving average to determine the trend, and use the ATR indicator to set stop loss points to control risks.
### Strategy Principles
1. Calculate the 50-day simple moving average SMA1 and the 100-day simple moving average SMA2
2. When SMA1 crosses above SMA2, a buy signal is issued; when SMA1 crosses below SMA2, a sell signal is issued.
3. Calculate the 14-day ATR indicator
4. ATR multiplied by the set multiplier as the stop loss point
5. When a buy signal is issued, the closing price minus the stop loss point is used as the stop loss selling point; when a sell signal is issued, the closing price plus the stop loss point is used as the stop loss buying point.
It can be seen that this strategy mainly relies on the trend judgment ability of the moving average and the risk control ability of the ATR indicator. The basic principles are simple and clear, easy to understand and implement.
### Strategic Advantages
1. The principle is clear and easy to implement, suitable for beginners
2. Use moving averages to determine the main trend and effectively track the trend.
3. ATR stop loss can effectively control the losses caused by individual giant earthquakes
4. Parameters can be easily adjusted to adapt to different market environments.
### Strategy Risk
1. In a volatile market, the moving average generates a large number of false signals, making it easy to miss the reversal point.
2. The ATR indicator is not sensitive enough to the rapidly changing market, which may cause losses beyond expectations.
3. The settings of indicator parameters and ATR multipliers depend on experience. Improper settings may affect strategy performance.
4. The double moving average itself has a large lag and may miss the turning point.
Risk control methods:
1. Appropriately shorten the moving average period to make the indicator more sensitive
2. Dynamically adjust the ATR multiplier to make stop loss more flexible
3. Combine with other indicators to filter false signals
4. Operate on the basis of large-level structural judgments
### Strategy optimization direction
1. Try other types of moving averages, such as exponential moving averages for better filtering
2. ATR can be replaced by dynamic stop loss methods such as Keltner channels.
3. Add trading volume and other auxiliary indicators to filter signals
4. Determine key trend points based on wave theory, support and resistance levels, etc.
### Summarize
This strategy is a typical trend following strategy. It uses moving averages to determine the trend direction, and ATR sets stop loss to control risks. The principle is simple, clear, and easy to master. However, there is a certain risk of hysteresis and false signals. It can be improved through parameter adjustment, indicator optimization, and combining more factors to make the strategy more adaptable to the changing market environment. In general, this strategy is suitable for beginners to practice and optimize, but it needs to be treated with caution in actual combat.
||

### Overview

This strategy uses simple moving average crossovers and average true range indicator to generate buy and sell signals. It belongs to trend following strategies. It mainly uses 50-day and 100-day moving average crossovers to determine the trend and sets stop loss based on ATR to control risks.  

### Strategy Logic   

1. Calculate 50-day simple moving average SMA1 and 100-day simple moving average SMA2
2. When SMA1 crosses over SMA2, a buy signal is generated. When SMA1 crosses below SMA2, a sell signal is generated.  
3. Calculate 14-day ATR 
4. ATR multiplied by a set factor is used as stop loss point
5. When a buy signal is triggered, the closing price minus the stop loss point is the stop loss sell point. When a sell signal is triggered, the closing price plus the stop loss point is the stop loss buy point.

It can be seen that this strategy mainly relies on the trend judging capability of moving averages and the risk control capability of ATR. The logic is simple and easy to understand and implement.  

### Advantages

1. Simple logic easy to implement, suitable for beginners
2. Moving averages can effectively track trends 
3. ATR stop loss can effectively control losses from individual black swan events
4. Parameters can be easily adjusted for different market environments

### Risks

1. Many false signals may be triggered during range-bound markets, missing reversal points
2. ATR may not react sensitively enough to fast changing markets, leading to larger than expected losses  
3. The parameter settings and ATR multiplier rely on experience. Improper settings may affect strategy performance
4. The dual moving averages themselves have lagging effect, may miss turning points

Risk Management:

1. Shorten moving average periods to make the indicator more sensitive 
2. Dynamically adjust ATR multiplier for more flexible stop loss
3. Add other indicators to filter false signals
4. Operate based on larger time frame structure judgments 

### Optimization Directions 

1. Try other types of moving averages, like EMAs that filter better
2. Consider dynamic stop loss with Keltner Channels etc. to replace ATR
3. Add supporting indicators like volume to filter signals
4. Identify trend key points with concepts like Elliott Waves, support resistance etc.  

### Summary

This is a typical trend following strategy, using moving averages to determine trend direction and ATR stop loss to control risks. The logic is simple and easy to grasp. But it has certain lagging and false signal risks. Improvements can be made through parameter tuning, indicator optimization, incorporating more factors etc. to make the strategy more adaptive. Overall this strategy is suitable for beginner practice and optimization, but need to be careful when apply it in actual trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|50|50 SMA Length|
|v_input_int_2|100|100 SMA Length|
|v_input_int_3|14|ATR Length|
|v_input_int_4|4|ATR Multiplier|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-27 00:00:00
end: 2024-01-03 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("SMA and ATR Strategy", overlay=true)

// Step 1. Define strategy settings
lengthSMA1 = input.int(50, title="50 SMA Length")
lengthSMA2 = input.int(100, title="100 SMA Length")
atrLength = input.int(14, title="ATR Length")
atrMultiplier = input.int(4, title="ATR Multiplier")

// Step 2. Calculate strategy values
sma1 = ta.sma(close, lengthSMA1)
sma2 = ta.sma(close, lengthSMA2)
atr = ta.atr(atrLength)

// Step 3. Output strategy data
plot(sma1, color=color.blue, title="50 SMA")
plot(sma2, color=color.red, title="100 SMA")

// Step 4. Determine trading conditions
longCondition = ta.crossover(sma1, sma2)
shortCondition = ta.crossunder(sma1, sma2)

longStopLoss = close - (atr * atrMultiplier)
shortStopLoss = close + (atr * atrMultiplier)

// Step 5. Execute trades based on conditions
if (longCondition)
    strategy.entry("Buy", strategy.long)
    strategy.exit("Sell", "Buy", stop=longStopLoss)

if (shortCondition)
    strategy.entry("Sell", strategy.short)
    strategy.exit("Buy", "Sell", stop=shortStopLoss)

```

> Detail

https://www.fmz.com/strategy/437640

> Last Modified

2024-01-04 15:03:14
