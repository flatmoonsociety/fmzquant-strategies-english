
> Name

Inside-Bar-Failure-Strategy
> Author

ChaoZhang

> Strategy Description


[trans]

## Strategy Principle
This strategy trades based on the destruction of the inward K-line. When the inward K line appears, if the high and low points of the next K line break through the high and low points of the inward K line, a trading signal will be generated.
The specific transaction logic is:
1. Determine whether the first two K lines form an inward direction, that is, the high and low points of the second K line are within the first K line.
2. If the highest point of the third K-line exceeds the second K-line and the closing price is higher than the lowest point of the second K-line, a long signal will be generated.
3. If the lowest point of the third K-line is lower than the second K-line, and the closing price is lower than the highest point of the second K-line, a short signal will be generated.
4. You can close the position by a certain number of K lines (such as 3) in advance.
This strategy attempts to capture the trend movement after inward disruption. Inward direction represents short-term consolidation, while damage may start a new trend.
## Strategic Advantages
- The inside direction is easy to identify and the damage signal is clear
- Positions can be closed a certain period in advance to avoid reversal
- The rules are simple, intuitive and easy to implement
## Strategy Risk
- Further verification of the effectiveness of the destruction is required
- Inward formation and destruction are less common
- Possible trades in sub-optimal directions following the general trend
## Summarize
This strategy attempts to capture trend opportunities brought about by inward disruptions. However, the trading frequency is low and the risk-return ratio needs to be evaluated. It can be considered to be used in combination with other factors to optimize the trading effect.

||


## Strategy Logic

This strategy trades based on inside bar breakdowns. If the high/low of the bar following an inside bar penetrates the prior inside bar's range, trade signals are generated. 

The logic is:

1. Check if the prior 2 bars formed an inside bar i.e. bar 2's high/low within bar 1's range

2. If bar 3 high exceeds bar 2 high, and closes above bar 2 low, go long

3. If bar 3 low breaks bar 2 low, and closes below bar 2 high, go short 

4. Optionally close orders X bars later (e.g. 3 bars)

It aims to capture trends emerging from inside bar consolidations. Inside bars represent short-term balances, and breakdowns can kickstart new trends.

## Advantages

- Inside bars easy to identify, breakdowns give clear signals

- Closing orders early avoids whipsaws

- Simple and intuitive rules

## Risks

- Need to further validate signal effectiveness 

- Inside bar formation and breakdowns less common

- Could trade against major trend

## Summary

This strategy attempts to capitalize on trends from inside bar breakdowns. But the lower frequency of trading needs evaluation of risk-reward. Combining with other factors could improve performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|3|Look Forward|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-07 00:00:00
end: 2022-10-31 00:00:00
period: 4d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Inside Bar Failure", overlay=true)

forward = input(defval=3, title="Look Forward")

longCondition = if (high[2] > high[1] and low[2] < low[1] and low < low[1] and high < high[1] and close > low[1])
    x = true
if (longCondition)
    strategy.entry("Long", strategy.long)

shortCondition = if (high[2] > high[1] and low[2] < low[1] and high > high[1] and low > low[1] and close < high[1])
    y = true
if (shortCondition)
    strategy.entry("Short", strategy.short)
    
if (longCondition[forward])
    strategy.close("Long")
if (shortCondition[forward])
    strategy.close("Short")
```

> Detail

https://www.fmz.com/strategy/426807

> Last Modified

2023-09-14 16:43:52
