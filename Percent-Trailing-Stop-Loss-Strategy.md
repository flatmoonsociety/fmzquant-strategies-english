
> Name

Percent-Trailing-Stop-Loss-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy implements a configurable percentage trailing stop mechanism for controlling trading risk. It allows you to set the stop loss percentage of long and short positions, and continuously track the highest or lowest price in a favorable direction starting from the entry price, thereby achieving dynamic stop loss.
## Strategy Principle
The main logic of this strategy is:
1. Enter the stop loss percentage for long and short positions
2. When taking a long position: Continue to track the low point and calculate the stop loss line based on the lowest price.
3. When taking a short position: Continue to track the high point and calculate the stop loss line based on the highest price.
4. When the price touches the stop loss line, stop the loss immediately and exit the current position.
The strategy allows customizing the stop loss percentage, for example setting it to 10%. When taking a long position, it will calculate 10% above the lowest price in real time as the stop loss line; when taking a short position, it will calculate 10% below the highest price as the stop loss line.
In this way, the stop-loss line will continue to move in a favorable direction, realizing dynamic tracking of stop-loss, protecting profits to the greatest extent and controlling risks at the same time.
## Strategic Advantages
- Realize automatic tracking and stop loss, no manual operation required
- Dynamic stop loss line to protect profits to the maximum extent
- Customizable stop loss percentage to adapt to various trading varieties
- Contributes to risk control and reduces unexpected losses
- Suitable for a variety of trading strategies and easy to integrate
## Strategic risks and responses
- The tracking speed is slow and there is a risk of being unable to stop losses.
- Stop loss that is too loose may cause losses to expand
- Stop loss that is too tight may cause excessive stop loss
How to deal with it:
1. Optimize stop loss percentage and balance stop loss effect
2. Combined with other stop loss methods, such as time stop loss
3. Optimize stop loss parameters based on market volatility
4. Maintain stop loss consistency and avoid changing parameters too arbitrarily.
## Strategy optimization direction
Points that this strategy can optimize:
1. Use machine learning algorithms to dynamically optimize stop loss parameters
2. Automatically adjust the stop loss width based on indicators such as maximum retracement
3. Set the stop loss position based on indicators such as moving averages
4. Choose different parameter configurations according to volatility conditions
5. Set a partial stop loss and then adjust the take profit position to make a profit
## Summarize
This strategy provides an effective percentage trailing stop loss method that can dynamically adjust the stop loss line. It can protect profits to the maximum extent and can also effectively control risks. Through parameter optimization, indicator integration, etc., the stop loss strategy can be made more intelligent and optimized.
|| 

## Overview

This strategy implements a configurable percentage trailing stop loss to manage trade risk. It allows setting long and short stop loss percentage from entry price for dynamic stop loss tracking.

## Strategy Logic

The main logic is:

1. Input long and short stop loss percentage
2. For longs: continually track lows and calculate stop loss line 
3. For shorts: continually track highs and calculate stop loss line
4. Exit positions when price touches stop loss line

The strategy allows customizing stop percentage, e.g. 10%. For longs, it dynamically calculates 10% above the low as the stop line. For shorts, 10% below the high.

This way, the stop line keeps moving favorably to maximize profit protection while controlling risk.

## Advantages

- Automates trailing stop loss without manual intervention
- Dynamic stop line protects profits as much as possible
- Customizable stop loss percentage for different instruments
- Helps control risk and reduce outsized losses  
- Easy to integrate into other strategies

## Risks and Mitigation 

- Slow trailing risks inability to stop out
- Stop loss too loose can increase losses
- Stop loss too tight risks over-frequent stops

Mitigations:

1. Optimize stop percentage to balance effectiveness
2. Incorporate other stop types like time-based stops
3. Tune stop based on market volatility  
4. Maintain stop consistency, avoid arbitrary changes

## Enhancement Opportunities

Enhancement opportunities:

1. Machine learning to dynamically optimize stop  
2. Auto-adjust based on max drawdown metrics
3. Incorporate indicators like moving averages for stop placement
4. Use different configurations based on volatility regime  
5. Set profit stops after partial stops to lock in profits

## Conclusion

This strategy provides an effective percentage trailing stop method to dynamically adjust stop loss. It maximizes profit protection while controlling risk. Enhancements through parameter optimization, indicator integration can make the stops more intelligent.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|Long Trailing Stop (%)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-19 00:00:00
end: 2023-09-18 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// © theCrypster

//@version=4
strategy("Percent Trailing Stop %", overlay=true)

//ENTER SOME SETUP TRADES FOR TSL EXAMPLE
longCondition = crossover(sma(close, 10), sma(close, 20))
if (longCondition)
    strategy.entry("My Long Entry Id", strategy.long)

shortCondition = crossunder(sma(close, 10), sma(close, 20))
if (shortCondition)
    strategy.entry("My Short Entry Id", strategy.short)
    

//TRAILING STOP CODE
trailStop = input(title="Long Trailing Stop (%)", type=input.float, minval=0.0, step=0.1, defval=10) * 0.01

longStopPrice = 0.0
shortStopPrice = 0.0
longStopPrice := if strategy.position_size > 0
    stopValue = close * (1 - trailStop)
    max(stopValue, longStopPrice[1])
else
    0
shortStopPrice := if strategy.position_size < 0
    stopValue = close * (1 + trailStop)
    min(stopValue, shortStopPrice[1])
else
    999999

//PLOT TSL LINES
plot(series=strategy.position_size > 0 ? longStopPrice : na, color=color.red, style=plot.style_linebr, linewidth=1, title="Long Trail Stop", offset=1, title="Long Trail Stop")
plot(series=strategy.position_size < 0 ? shortStopPrice : na, color=color.red, style=plot.style_linebr, linewidth=1, title="Short Trail Stop", offset=1, title="Short Trail Stop")


//EXIT TRADE @ TSL
if strategy.position_size > 0
    strategy.exit(id="Close Long", stop=longStopPrice)
if strategy.position_size < 0
    strategy.exit(id="Close Short", stop=shortStopPrice)

```

> Detail

https://www.fmz.com/strategy/427301

> Last Modified

2023-09-19 21:18:39
