
> Name

RSI Double Cross Reversal Strategy RSI-Dual-Cross-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/10b768e77f595f1576d.png)

[trans]

### Overview
This strategy is a trend following strategy based on the double cross reversal principle of the RSI indicator. It uses RSI line crossovers of different periods as buy and sell signals, and combines it with the RSI indicator to determine whether it is currently overbought or oversold to further confirm the validity of the trading signal.
### Strategy Principles
This strategy is mainly based on the two RSI indicator lines on the 5th and 11th. When the faster RSI (5-day line) breaks through the slower RSI (11-day line) from bottom to top and at the same time the 6-day RSI is below 30, a buy signal is generated; when the faster RSI falls below the slower RSI from top to bottom and at the same time the 6-day RSI is above 70, a sell signal is generated.
This strategy plots both the 30 and 70 levels. 30 represents the oversold area, and 70 represents the overbought area. The basic idea of ​​the RSI indicator is that when it is in the overbought and oversold zone, it means that the asset is overvalued, and you should consider taking profits or waiting for a correction opportunity; when RSI is in the oversold zone, it means that the asset is undervalued, and you should consider buying to establish a long position. Therefore, this strategy adds 6-day RSI to determine whether it is in the overbought and oversold area, which can filter out some false signals and improve the reliability of the signal.
When buy and sell signals are generated, this strategy will place long and short orders respectively. So it is a two-way trading strategy that can track both uptrends and downtrends.
### Strategic Advantages
1. Using the double-fork principle, higher reliability
2. Combine RSI judgments of different periods to avoid false signals
3. Two-way trading is possible, suitable for tracking market trends
4. The performance of RSI indicator is stable and the space for parameter optimization is large.
### Risks and Solutions
1. The double cross signal lags behind and may miss part of the rise or fall.
Solution: Appropriately shorten the period parameter of faster RSI to make the signal more sensitive
2. There may be more false signals in trending markets
Solution: Adjust the parameters of overbought and oversold judgment areas to avoid false signals in trending markets.
3. The probability of RSI indicator divergence or failure
Solution: Use in combination with other indicators to avoid the probability of a single failure of RSI
### Optimization direction
1. Period parameter optimization: adjust the period parameters of faster and slower RSI to find the best parameter combination
2. Optimization of overbought and oversold parameters: adjust the parameters of overbought and oversold judgment areas to improve signal accuracy
3. Combine with other indicators: combine moving averages or volatility indicators to form a comprehensive trading system
### Summarize
This strategy is based on the RSI double cross reversal idea and is a relatively reliable trend following strategy. It uses multi-period RSI judgment to avoid certain false signals, thus having high practical effect. Through parameter optimization and indicator combination, this strategy is expected to achieve better performance. Overall, this strategy has clear ideas and strong practicability, and deserves special attention and subsequent optimization.
||


### Overview  

This strategy is a trend following strategy based on the dual cross reversal principle of the RSI indicator. It uses crossovers between RSI lines of different periods as buy and sell signals, while also incorporating RSI indicator judgments on whether the current situation is overbought or oversold to further confirm the validity of trading signals.

### Strategy Logic

The strategy is mainly based on the 5-day and 11-day two RSI indicator lines. When the faster RSI (5-day line) breaks through the slower RSI (11-day line) upward while the 6-day RSI is below 30 at the same time, a buy signal is generated; When the faster RSI breaks through the slower RSI downward while the 6-day RSI is above 70 at the same time, a sell signal is generated.  

The strategy also draws 30 and 70 horizontal lines, with 30 representing the oversold area and 70 representing the overbought area. The basic idea of the RSI indicator is that when in the overbought/oversold area, it means the asset is over/under valued and one should consider taking profit/buying opportunities. Therefore, the strategy incorporates judgments on the 6-day RSI to see if it is in the OBOS region to filter out some false signals and improve reliability.

When buy and sell signals are generated, the strategy will place long and short orders accordingly. So it is a dual directional trading strategy that can track both uptrends and downtrends.  

### Advantages  

1. High reliability due to dual cross principle
2. Avoid false signals by incorporating multi-period RSI
3. Dual directional trading suitable for trend following  
4. RSI indicator is stable with large optimization space

### Risks and Solutions   

1. Dual cross signals lag and may miss some ups and downs  
Solution: Shorten faster RSI period parameter to make signals more sensitive  

2. More false signals may occur in trending markets  
Solution: Adjust OBOS parameter to avoid false signals in trends

3. Divergence or failure probabilities of RSI indicator  
Solution: Combine with other indicators to avoid sole failure probability  

### Optimization Directions   

1. Period parameter optimization: Adjust faster and slower RSI periods, find best combination

2. OBOS parameter optimization: Adjust OBOS parameters to improve signal accuracy  

3. Combine with other indicators: Incorporate MA, volatility indicators etc to form comprehensive system

### Conclusion   

This strategy is a reliable trend following strategy based on the RSI dual cross reversal logic. Its multi-period RSI design can avoid certain false signals and thus has good practical results. Through parameter optimization and indicator combinations, the strategy has potential for even better performance. In summary, the strategy has clear logic and strong practicality, and is worth key attention and further optimization.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|5|MA 1|
|v_input_2|11|MA 1|
|v_input_3|6|MA 1|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-15 00:00:00
end: 2023-11-21 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © email_analysts
// This code gives indication on the chart to go long or short based on RSI crossover strategy. 
//Default value has been taken as 5 and 11, with 6 being used to identify highs & lows.
//@version=4
strategy("RSITrendStrategy", overlay=false)
len1 = input(title="MA 1", defval = 5)
len2 = input(title="MA 1", defval = 11)
len3 = input(title="MA 1", defval = 6)

h1 = hline(30.)
h2 = hline(70.)
///fill(h1, h2, color = color.new(color.blue, 80))
sh = rsi(close, len1)
ln = rsi(close, len2)
rs = rsi(close, len3)
p1 = plot(sh, color = color.red)
p2 = plot(ln, color = color.green)
p3 = plot(rs, color = color.white)

mycol = sh > ln ? color.lime : color.red
fill(p1, p2, color = mycol)

buy = (sh[1] < ln[1] and sh > ln and rs[1] < 30) 
if (buy)
    strategy.entry("long", strategy.long)

sell = (sh[1] > ln[1] and sh < ln and rs[1] > 70)
if (sell)
    strategy.entry("short", strategy.short)
```

> Detail

https://www.fmz.com/strategy/432885

> Last Modified

2023-11-22 14:59:07
