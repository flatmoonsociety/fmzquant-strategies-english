
> Name

Double moving average crossover trading trend following strategy MACD-Crossover-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/115bd4eafb6a07a28a2097367e82334521bd2f6a42e05de763c75b84695093a0.png)
[trans]

## Overview
The Double Moving Average Crossover trading strategy is a trend following strategy. It utilizes the crossover of the fast moving average (MACD) and the slow moving average as buy and sell signals. When the fast moving average sweeps up from the slow moving average, a buy signal is generated; when the fast moving average sweeps down from the slow moving average, a sell signal is generated.
## Strategy Principle
This strategy is based on the MACD indicator. The MACD indicator is the difference between two moving averages with different parameters, reflecting price momentum changes. Specifically, it is the difference obtained by subtracting the slow moving average (the default parameter is the 26-day line) from the fast moving average (the default parameter is the 12-day line), which is called the MACD column. In order to eliminate shocks, the DEA line or signal line is introduced into the MACD indicator, which is generally the 9-day weighted moving average of MACD.
When the MACD column breaks through the DEA line from bottom to top and enters the positive area, it means that the short-term average sweeps the long-term average, indicating that the stock price trend has turned upward, generating a buy signal. When MACD falls below the DEA line from top to bottom and enters the negative area, it indicates that the short-term average line sweeps downwards from the long-term average line, and the stock price trend turns downward, generating a sell signal.
This strategy uses the intersection of the MACD column and the DEA line to determine the timing of buying and selling. Buy when the MACD column sweeps up the DEA line and sell when it sweeps down.
## Advantage Analysis
This strategy has the following advantages:
1. captured Ability to follow the trend and seize changes in price trends in a timely manner.
2. Simple and clear, easy to understand and implement.
3. The parameters are relatively fixed and do not need to be adjusted frequently.
4. Applicable to different time periods.
## Risk Analysis
There are also some risks with this strategy:
1. Whipsaws may generate multiple false signals, that is, triggering buy and sell orders repeatedly in sideways trading. 
2. There is a certain lag in lagging, and the best opportunity for price changes may be missed.
3. over optimization Parameters are easy to be over-optimized, and the actual effect may be poor.
In order to reduce risks, parameters can be adjusted appropriately or used in combination with other indicators, such as volume and price indicators, volatility indicators, etc. In addition, reasonable stop loss and take profit strategies are also important.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Parameter optimization. Different parameter combinations can be tested to find the best parameters. But be careful to avoid over-optimization.
2. Combined with other indicators. Volume price indicators, volatility indicators, etc. can be introduced to form a more powerful combination strategy.
3. Stop loss and take profit strategy. Setting reasonable stop loss and profit points can effectively control risks.
4. Adaptability optimization. This strategy can be applied to different markets and time periods and can be adjusted according to actual conditions.
## Summarize
The double moving average crossover strategy achieves low-cost trend following trading by capturing changes in price trends. It is simple, practical and easy to implement, making it an entry-level strategy suitable for novices. However, this strategy also has certain flaws, and attention needs to be paid to preventing risks. Through continuous optimization and improvement, the actual effect of this strategy can be made better, and it is worth recommending.
||

## Overview

The MACD crossover trading strategy is a trend-following strategy. It uses the crossover of fast and slow moving average lines as buy and sell signals. When the fast moving average line crosses above the slow moving average line, a buy signal is generated. When the fast moving average line crosses below the slow moving average line, a sell signal is generated.

## Strategy Principle  

This strategy is based on the MACD indicator. The MACD indicator is the difference between two moving average lines with different parameters, reflecting the changes in the momentum of prices. Specifically, it is the difference between the fast moving average line (default parameter is 12-day line) and the slow moving average line (default parameter is 26-day line), called the MACD bar. To eliminate oscillations, the MACD indicator also introduces a DEA line or signal line, usually the 9-day weighted moving average of the MACD.

When the MACD bar breaks through the DEA line from bottom up and enters the positive area, it indicates that the short-term average line crosses above the long-term average line, indicating that the price trend turns to upward and a buy signal is generated. When the MACD falls from top to bottom through the DEA line and enters the negative area, it indicates that the short-term average line crosses below the long-term average line and the price trend turns to downward, generating a sell signal.

The strategy uses the crossover of the MACD bar and the DEA line to determine the timing of buying and selling. It buys when the MACD bar crosses above the DEA line and sells when the MACD bar crosses below the DEA line.

## Advantage Analysis

The advantages of this strategy include:

1. Ability to follow the trend and capture price changes in a timely manner. 
2. Simple and easy to understand and implement.
3. Relatively fixed parameters without frequent adjustment.
4. Applicable to different timeframes.

## Risk Analysis  

This strategy also has some risks:

1. May generate multiple false signals or whipsaws in sideways markets.  
2. Has some lag and may miss the best timing of price changes. 
3. Parameters are easily overoptimized and actual results may be poor.

To reduce risks, parameters can be adjusted, or combined with other indicators like volume and volatility indicators. In addition, proper stop loss and take profit strategies are also important.

## Optimization Directions

This strategy can be optimized in the following aspects:

1. Parameter optimization to find the optimal parameters while avoiding overoptimization.

2. Combining with other indicators to form more powerful combination strategies.  

3. Setting proper stop loss and take profit points to effectively control risks.

4. Adaptive optimization to apply this strategy to different markets and timeframes based on actual conditions.

## Conclusion

The MACD crossover trading strategy captures trend changes at a low cost by following price trends. It is simple, practical and easy to implement, making it a suitable starter strategy for beginners. But this strategy also has some flaws. By constantly optimizing and improving, the actual effect of this strategy can be better. It is worth recommending.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|fastLength|
|v_input_2|40|slowlength|
|v_input_3|4|MACDLength|
|v_input_4|2011|From Year|
|v_input_5|true|From Month|
|v_input_6|true|From Day|
|v_input_7|9999|To Year|
|v_input_8|12|To Month|
|v_input_9|31|To Day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-29 00:00:00
end: 2024-01-04 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("MACD Strategy by Forbes",default_qty_type=strategy.percent_of_equity, default_qty_value=100, overlay=false)

fastLength = input(20)
slowlength = input(40)
MACDLength = input(4)

// === INPUT BACKTEST RANGE ===
FromYear  = input(defval = 2011, title = "From Year", minval = 2009)
FromMonth = input(defval = 1, title = "From Month", minval = 1, maxval = 12)
FromDay   = input(defval = 1, title = "From Day", minval = 1, maxval = 31)
ToYear    = input(defval = 9999, title = "To Year", minval = 2009)
ToMonth   = input(defval = 12, title = "To Month", minval = 1, maxval = 12)
ToDay     = input(defval = 31, title = "To Day", minval = 1, maxval = 31)

// === FUNCTION EXAMPLE ===
start     = timestamp(FromYear, FromMonth, FromDay, 00, 00)  // backtest start window
finish    = timestamp(ToYear, ToMonth, ToDay, 23, 59)        // backtest finish window
window()  => true // create function "within window of time"

MACD = ema(close, fastLength) - ema(close, slowlength)
aMACD = ema(MACD, MACDLength)
delta = MACD - aMACD

// Plot colors
col_grow_above = #26A69A
col_grow_below = #FFCDD2
col_fall_above = #B2DFDB
col_fall_below = #EF5350

f1 = plot(MACD,color=red)
s1 = plot(aMACD,color=blue)
plotColor = if delta > 0
    delta > delta[1] ? lime : green
else 
    delta < delta[1] ? maroon : red

plot(delta, color=plotColor, style=columns)

if (crossover(delta, 0))
    strategy.entry("Buy", true, when=window(), comment="Buy")

if (crossunder(delta, 0))
    strategy.close_all(when=window())

//plot(strategy.equity, title="equity", color=red, linewidth=2, style=areabr)
```

> Detail

https://www.fmz.com/strategy/437785

> Last Modified

2024-01-05 15:32:06
