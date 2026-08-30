
> Name

Dynamic RSI indicator trading strategy Dynamic-RSI-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/15e79a6e1d9b48e65bd.png)
[trans]

## Overview
This strategy builds a trading strategy by calculating the RSI indicator and setting the overbought and oversold ranges, combined with dynamic stop loss and target profit exit. Go short when the RSI indicator crosses the oversold range, go long when it falls below the oversold range, and set a trailing stop loss and target profit to exit the position.
## Strategy Principle
This strategy uses the 14-day RSI indicator to determine the technical form of the market. The RSI indicator reflects the ratio of rising and falling momentum over a period of time and is used to determine whether the market is overbought or oversold. The RSI length in this strategy is 14. When the RSI goes above 70, the market is considered overbought, and you go short; when the RSI goes below 30, the market is considered oversold, and you go long.
In addition, this strategy also uses a dynamic trailing stop loss mechanism. When holding a long position, the trailing stop price is 97% of the closing price; when holding a short position, the trailing stop price is 103% of the closing price. This way you can lock in most of your profits while avoiding your stop loss being knocked out.
Finally, this strategy also uses a target profit mechanism. The position will be exited when the profit of the position reaches 20%. This can lock in some profits and avoid profit taking.
## Advantage Analysis
This strategy has the following advantages:
1. Use the RSI indicator to determine overbought and oversold conditions and seize market turning points in time.
2. Using dynamic trailing stop loss can effectively control risks
3. Set a target profit level to lock in part of the profit
4. The strategy idea is clear and easy to understand, with fewer parameters and easy to operate.
5. Can easily optimize parameters such as RSI length, overbought and oversold levels, stop loss range, etc.
## Risk Analysis
This strategy also has some risks that need attention:
1. The possibility of the RSI indicator giving false signals, which can lead to unnecessary losses
2. The probability of the stop loss being breached, which will expand the loss
3. The target profit is set too low and it is impossible to make enough profits by holding the position.
The above risks can be solved by optimizing the RSI parameters, adjusting the stop loss range, and appropriately relaxing the target profit requirements.
## Optimization direction
This strategy can be optimized from the following directions:
1. Optimize RSI indicator parameters, adjust overbought and oversold judgment criteria, and reduce the probability of false signals.
2. Add other indicator filters to avoid false signals caused by a single degree of RSI.
3. Dynamically optimize the target profit level so that the strategy can be flexibly adjusted according to market conditions
4. Combine with trading volume indicators to avoid low-volume false breakthroughs
5. Add machine learning algorithm to automatically optimize parameters
## Summarize
The overall idea of ​​this strategy is clear. It uses the RSI indicator to determine overbought and oversold, and cooperates with dynamic stop loss and target profit exit. The advantages are easy to understand and implement, risk control is in place, and strong scalability. The next step can be to optimize the signal quality and dynamically adjust parameters to make the strategy more intelligent.
||

## Overview 

This strategy builds a trading system using RSI indicator to determine overbought and oversold levels, together with dynamic trailing stop loss and profit target exit. It goes short when RSI crosses above overbought level and goes long when RSI crosses below oversold level. Trailing stop loss and profit target exit are used to close positions.

## Strategy Logic

This strategy uses 14-period RSI indicator to judge market technical patterns. RSI reflects the ratio of rising and falling power over a period of time, to tell if the market is overbought or oversold. The RSI length here is 14. When RSI crosses above 70, the market is considered overbought, and we go short. When RSI crosses below 30, the market is considered oversold, and we go long.

In addition, this strategy uses dynamic trailing stop loss mechanism. When holding long position, trailing stop price is set at 97% of closing price. When holding short position, trailing stop price is 103% of closing price. This locks in most profits while avoiding being stopped out by market noise. 

Finally, this strategy uses profit target exit. When position profit reaches 20%, it will be closed. This locks in some profits and avoids profit retracement.  

## Advantage Analysis

The advantages of this strategy include:

1. Using RSI indicator to determine overbought/oversold market effectively
2. Adopting dynamic trailing stop loss to control risk 
3. Setting proper profit target to lock in profits
4. Clear logic and few parameters, easy to implement for live trading
5. Easy to optimize parameters like RSI length, overbought/oversold levels, stop loss percentage etc.

## Risk Analysis  

Some risks of this strategy to note:

1. Potential false signals from RSI, causing unnecessary losses
2. Probability of stop loss being hit, enlarging losses
3. Profit target set too low, unable to hold position long enough to earn adequate profits

To cope with these risks, optimizing RSI parameters, adjusting stop loss percentage, relaxing profit target requirements reasonably can help.  

## Optimization Directions

Some directions to optimize the strategy:

1. Optimize RSI parameters and overbought/oversold judge standards to reduce false signals
2. Add other indicator filters to avoid erroneous signals caused by single RSI
3. Dynamically optimize profit target according to market conditions  
4. Incorporate trading volume indicators to avoid low volume false breakouts
5. Introduce machine learning algorithms to auto-tune parameters  

## Summary 

The strategy has clear logic of using RSI to determine overbought/oversold market, with dynamic stops and profit taking. Its pros are easy understanding and implementation, good risk control, and high extensibility. Next step is to enhance signal quality, auto-tune parameters etc to make strategy more intelligent.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|RSI Length|
|v_input_2|3|Trailing Stop Percentage (%)|
|v_input_3|20|Profit Target Percentage (%)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-04 00:00:00
end: 2024-02-03 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Modified RSI-Based Trading Strategy", overlay=true)

// RSI settings
rsiLength = input(14, title="RSI Length")
overboughtLevel = 70
oversoldLevel = 30

// User-defined parameters
trailingStopPercentage = input(3, title="Trailing Stop Percentage (%)")
profitTargetPercentage = input(20, title="Profit Target Percentage (%)")

rsiValue = ta.rsi(close, rsiLength)

var float trailingStopLevel = na
var float profitTargetLevel = na

// Entry criteria
enterLong = ta.crossover(rsiValue, oversoldLevel)
enterShort = ta.crossunder(rsiValue, overboughtLevel)

// Exit criteria
exitLong = ta.crossover(rsiValue, overboughtLevel)
exitShort = ta.crossunder(rsiValue, oversoldLevel)

// Trailing stop calculation
if (strategy.position_size > 0)
    trailingStopLevel := close * (1 - trailingStopPercentage / 100)

if (strategy.position_size < 0)
    trailingStopLevel := close * (1 + trailingStopPercentage / 100)

// Execute the strategy
if (enterLong)
    strategy.entry("Buy", strategy.long)

if (exitLong or ta.crossover(close, trailingStopLevel) or ta.change(close) > profitTargetPercentage / 100)
    strategy.close("Buy")

if (enterShort)
    strategy.entry("Sell", strategy.short)

if (exitShort or ta.crossunder(close, trailingStopLevel) or ta.change(close) < -profitTargetPercentage / 100)
    strategy.close("Sell")

// Plot RSI and overbought/oversold levels
plot(rsiValue, title="RSI", color=color.blue)
hline(overboughtLevel, "Overbought", color=color.red, linestyle=hline.style_dashed)
hline(oversoldLevel, "Oversold", color=color.green, linestyle=hline.style_dashed)

```

> Detail

https://www.fmz.com/strategy/441010

> Last Modified

2024-02-04 17:36:41
