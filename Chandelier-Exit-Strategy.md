
> Name

Chandelier-Exit-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1cbb20b898e9c99d3f1.png)

[trans]

## Overview
This strategy utilizes the Chandelier indicator to determine the direction and strength of price breakouts, thereby generating buy and sell signals. It only performs buy operations.
## Strategy Principle
This strategy is based on the Chandelier indicator, which sets stop loss lines based on the highest price, lowest price and average true fluctuation range of the price. Specifically, the strategy calculates the 22-day average true volatility and multiplies it by a coefficient (default is 3). Then set the long-term stop loss line and the short-term stop loss line based on this value. When the strategy holds a long position, if the price falls below the long-term stop loss line, a sell signal will be generated; if the price exceeds the short-term stop loss line when the short position is held, a buy signal will be generated.
This strategy only operates on buys. Specifically, it generates a buy signal when the price breaks above the last long-term stop loss level. Then when the price falls below the short-term stop loss line, a sell signal is generated and the position is closed.
## Advantage Analysis
- Use the chandelier indicator to set dynamic stop loss lines to effectively control risks
- Combined with price breakthroughs to generate trading signals, you can capture the trend of prices Features
- Only carry out buying operations, realizing a strategy to avoid market reversal at both ends
- Alert reminders triggered by multiple conditions are set up to monitor the status of the strategy in real time
## Risk Analysis
- The Chandelier indicator is sensitive to fluctuations and may falsely report signals if there are abnormal price fluctuations.
- Without setting a stop loss after buying, the risk of loss cannot be effectively controlled.
- Failure to consider trailing take profit and unable to lock in profits
Risk resolution:
1. Combine with other indicators to filter signals to avoid false alarms
2. Set a stop loss line to limit the maximum loss ratio
3. Add a tracking take-profit mechanism and consider dynamically adjusting the sell line or partially exiting the market.
## Optimization direction
1. You can test different parameter settings and optimize the timing of buying and selling.
2. You can add confirmation of other indicators to avoid false alarm signals.
3. You can consider buying and selling at the same time
4. Stop loss and take profit mechanisms can be set up
## Summary
This strategy utilizes the Chandelier indicator’s dynamic stop lines to identify price reversal opportunities. It only buys when the price breaks through the long stop loss line upwards, and sells when the price falls below the short stop loss line, realizing a simple strategy of unilateral operation and avoiding reversal at both ends of the market. This strategy effectively controls risk, but there are no stop loss and take profit settings. We can optimize this strategy by adding other indicator filters and setting stop loss and take profit to make it more robust.
||

## Overview
This strategy uses the Chandelier Exit indicator to determine the direction and momentum of price breakouts and generate buy and sell signals. It only performs buy operations.

## Strategy Logic  
This strategy is based on the Chandelier Exit indicator which sets stop-loss lines based on the highest high, lowest low and the Average True Range. Specifically, it calculates a 22-day ATR and multiples it by a coefficient (default 3) to derive values for long and short stop lines. The strategy generates a sell signal when price breaks below the long stop when long, and a buy signal when price breaks above the short stop when short.

The strategy only performs buy operations. It triggers a long entry when price breaks above the previous long stop line, and creates an exit signal when price falls below the short stop line, closing the long position.

## Advantage Analysis
- Utilizes dynamic stop loss lines from Chandelier Exit to effectively control risks
- Combines price breakouts to capture trending moves  
- Implements a strategy that avoids upside/downside reversals by only buying
- Alert conditions trigger notifications to monitor strategy status

## Risk Analysis
- Chandelier Exit is sensitive to volatility expansion which may cause false signals  
- No stop loss in place after buying to limit loss
- No profit taking mechanism to lock in gains

Risk Mitigations:
1. Add filter with other indicators to avoid false signals
2. Implement stop loss to limit maximum loss %  
3. Incorporate trailing profit stops, such as dynamic adjustment of sell line or partial exits

## Enhancement Opportunities 
1. Test different parameter sets to optimize entries and exits
2. Add indicator filters to confirm signals and avoid false signals
3. Consider allowing both buy and sell operations
4. Introduce stop loss and take profit mechanisms

## Conclusion
This strategy identifies reversal opportunities using the dynamic stop lines from the Chandelier Exit indicator. It buys on upside breaks of the long stop line and sells when prices falls below the short stop line, implementing a simple one-sided strategy that avoids upside/downside reversals. It effectively controls risk but lacks stop loss and take profit provisions. Optimization opportunities include adding filters and stop loss/profit taking mechanisms to make the strategy more robust.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|22|ATR Period|
|v_input_float_1|3|ATR Multiplier|
|v_input_2|true|Show Buy/Sell Labels ?|
|v_input_3|true|Use Close Price for Extremums ?|
|v_input_4|true|Highlight State ?|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-28 00:00:00
end: 2024-01-04 00:00:00
period: 10m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Chandelier Exit Strategy", overlay=true)

length = input(title='ATR Period', defval=22)
mult = input.float(title='ATR Multiplier', step=0.1, defval=3.0)
showLabels = input(title='Show Buy/Sell Labels ?', defval=true)
useClose = input(title='Use Close Price for Extremums ?', defval=true)
highlightState = input(title='Highlight State ?', defval=true)

atr = mult * ta.atr(length)

longStop = (useClose ? ta.highest(close, length) : ta.highest(length)) - atr
longStopPrev = nz(longStop[1], longStop)
longStop := close[1] > longStopPrev ? math.max(longStop, longStopPrev) : longStop

shortStop = (useClose ? ta.lowest(close, length) : ta.lowest(length)) + atr
shortStopPrev = nz(shortStop[1], shortStop)
shortStop := close[1] < shortStopPrev ? math.min(shortStop, shortStopPrev) : shortStop

var int dir = 1
dir := close > shortStopPrev ? 1 : close < longStopPrev ? -1 : dir

var color longColor = color.green
var color shortColor = color.red

longStopPlot = plot(dir == 1 ? longStop : na, title='Long Stop', style=plot.style_linebr, linewidth=2, color=color.new(longColor, 0))
buySignal = dir == 1 and dir[1] == -1
plotshape(buySignal ? longStop : na, title='Long Stop Start', location=location.absolute, style=shape.circle, size=size.tiny, color=color.new(longColor, 0))
plotshape(buySignal and showLabels ? longStop : na, title='Buy Label', text='Buy', location=location.absolute, style=shape.labelup, size=size.tiny, color=color.new(longColor, 0), textcolor=color.new(color.white, 0))

shortStopPlot = plot(dir == 1 ? na : shortStop, title='Short Stop', style=plot.style_linebr, linewidth=2, color=color.new(shortColor, 0))
sellSignal = dir == -1 and dir[1] == 1
plotshape(sellSignal ? shortStop : na, title='Short Stop Start', location=location.absolute, style=shape.circle, size=size.tiny, color=color.new(shortColor, 0))
plotshape(sellSignal and showLabels ? shortStop : na, title='Sell Label', text='Sell', location=location.absolute, style=shape.labeldown, size=size.tiny, color=color.new(shortColor, 0), textcolor=color.new(color.white, 0))

changeCond = dir != dir[1]
alertcondition(changeCond, title='Alert: CE Direction Change', message='Chandelier Exit has changed direction!')
alertcondition(buySignal, title='Alert: CE Buy', message='Chandelier Exit Buy!')
alertcondition(sellSignal, title='Alert: CE Sell', message='Chandelier Exit Sell!')

// Define initial capital
initial_capital =25

// Trigger buy order and close buy order on sell signal
if buySignal
    strategy.entry("Buy", strategy.long, qty = initial_capital / close)

if sellSignal
    strategy.close("Buy")

```

> Detail

https://www.fmz.com/strategy/437792

> Last Modified

2024-01-05 15:57:51
