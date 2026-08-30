
> Name

Schaff-Trend-Cycle-with-Double-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/153c91721c7a2ba8662.png)
[trans]

## Overview
This strategy is called "Follow the trend and break through the moving average crossover strategy". The main idea is to combine the trend indicators and the moving average crossover to judge long and short positions. Specifically, this strategy uses the Schaff Trend Cycle (STC) indicator and the double moving average crossover. When the STC direction breaks through the overbought and oversold zone, the price is higher than the short-term exponential moving average, and the short-term exponential moving average is higher than the long-term exponential moving average, go long; otherwise, go short.
## Strategy Principle
This strategy is mainly based on two technical indicators:
1. Trend-following indicator: STC indicator, which determines the trend direction. STS indicators include MACD indicator, Stoch indicator and STC indicator line. When the STC line breaks upward from the 0-25 range, it is a long signal; when it breaks downward from the 75-100 range, it is a short signal.
2. Moving average crossover: the intersection of the fast simple moving average (default period 35) and the slow simple moving average (default period 200). When the fast line crosses the slow line, it is a long signal, and when the fast line crosses the slow line, it is a short signal.
The trading signal judgment logic of this strategy is as follows:
1. Long signal: When the STC indicator breaks through the 25 line upward, and the fast simple moving average is higher than the slow simple moving average, and the price is higher than the fast simple moving average, go long.
2. Short signal: When the STC indicator breaks through the 75 line downwards, and the fast simple moving average is lower than the slow simple moving average, and the price is lower than the fast simple moving average, go short.
## Advantage Analysis
This strategy has the following advantages:
1. Combining trend indicators and moving average indicators, trading signals are more reliable. The STC indicator determines the direction of the general trend, and the double moving average determines the specific entry.
2. The moving average parameters are adjustable. The moving average parameters can be adjusted according to the market and the strategy optimized.
3. Risks are controllable. The STC indicator determines overbought and oversold areas to avoid chasing highs and buying lows in extreme areas. Target Stop sets a Take Profit and Stop Loss range of 400 pips.
## Risk Analysis
This strategy also has certain risks:
1. The STC indicator may have a false breakthrough. It needs to be judged based on the price entity.
2. Moving average crossovers may produce more false signals. The moving average period parameters need to be adjusted.
3. Only do one-sided transactions. Space is limited. Two-way transactions can be considered.
4. There is no slippage risk in foreign exchange margin trading. Slippage may be larger in real trading.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Adjust STC parameters to optimize overbought and oversold judgments.
2. Optimize the moving average period and improve the reliability of cross signals.
3. Add other filter indicators to filter out false breakthroughs. For example, Bollinger Bands.
4. Add two-way transaction logic. Reduce space risks.
5. Add stop loss logic. Control single losses.
## Summarize
This strategy comprehensively uses trend indicators and moving average crossover indicators to determine the trend direction and specific entry points. Under certain risk control conditions, better returns can be obtained. The strategy model is simple, clear and easy to understand. It is also easy to adjust parameters and optimize functions according to different markets. It is suitable for beginners to learn and apply.
||


## Overview

This strategy is named "Schaff Trend Cycle with Double Moving Average Crossover Strategy". The main idea is to determine long and short positions based on the Schaff Trend Cycle (STC) indicator and double moving average crossover. Specifically, when the STC breaks out of the overbought or oversold areas, the price is above the fast exponential moving average, and the fast EMA is above the slow EMA, a long position is opened. Conversely, a short position is opened. 

## Strategy Logic

The strategy relies primarily on two technical indicators:

1. Trend indicator: STC indicator to determine trend direction. The STC includes the MACD, Stochastic, and STC indicator line. An upward breakout from the 0-25 zone signals a bullish trend, while a downward breakout from the 75-100 zone signals a bearish trend.

2. Moving average crossover: Fast simple moving average (default period 35) crosses above/below the slow SMA (default period 200). A bullish signal triggered when the fast SMA crosses above the slow SMA. A bearish signal triggered on the opposite crossover.

The trading signal logic is defined as follows: 

1. Long signal: STC breaks above the 25 line, fast SMA is above slow SMA, and close price is above fast SMA.

2. Short signal: STC breaks below 75 line, fast SMA is below slow SMA, and close price is below fast SMA.


## Advantage Analysis 

The advantages of this strategy include:

1. Reliable trading signals from combining trend and moving average indicators. STC determines overall trend, while double MAs generate specific entry signals.  

2. Customizable moving average periods. MA periods can be optimized for different market conditions.

3. Controllable risk. STC identifies overbought/oversold levels to avoid buying tops and selling bottoms. Target stops set 400 point profit/loss range.


## Risk Analysis

There are some risks to consider:

1. Potential for STC false breakouts. Needs to be confirmed by price action.  

2. More false signals from MA crosses. Requires tuning of MA periods.

3. Only trades in one direction at a time. Limits space for open positions. Consider allowing dual-directional trading.  

4. No handling of spread risk in margin FX trading. Spread could be substantial in live trading.


## Optimization

Possible optimization paths include:

1. Adjust STC overbought/oversold parameters.

2. Optimize MA periods to improve crossover signal reliability.  

3. Add additional filters like Bollinger Bands to reduce false breakout trades.  

4. Implement dual-directional trading logic to increase capacity.

5. Add stop loss logic to control loss per trade.


## Conclusion

In summary, this strategy combines trend and moving average crossover indicators to determine trend direction and timing of entries. With proper risk controls, it can achieve good returns. The straightforward logic makes it easy to understand and optimize across different market conditions, well-suited for beginners.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|23|MACD Fast Length|
|v_input_2|50|MACD Slow Length|
|v_input_3|10|Cycle Length|
|v_input_4|3|1st %D Length|
|v_input_5|3|2nd %D Length|
|v_input_6|true|Highlight Breakouts ?|
|v_input_7|400|Target/stop|
|v_input_8|35|SMA1|
|v_input_9|200|SMA2|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-11 00:00:00
end: 2023-12-11 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
// Shaff Trend Cycle coded by Alex Orekhov (everget)
// Strategy and its additional conditions provided by greenmask
// Schaff Trend Cycle script may be freely distributed under the MIT license.
strategy("STC", shorttitle="STC")

fastLength = input(title="MACD Fast Length", type=input.integer, defval=23)
slowLength = input(title="MACD Slow Length", type=input.integer, defval=50)
cycleLength = input(title="Cycle Length", type=input.integer, defval=10)
d1Length = input(title="1st %D Length", type=input.integer, defval=3)
d2Length = input(title="2nd %D Length", type=input.integer, defval=3)
src = close
highlightBreakouts = input(title="Highlight Breakouts ?", type=input.bool, defval=true)

macd = ema(src, fastLength) - ema(src, slowLength)
k = nz(fixnan(stoch(macd, macd, macd, cycleLength)))
d = ema(k, d1Length)
kd = nz(fixnan(stoch(d, d, d, cycleLength)))
stc = ema(kd, d2Length)
stc := 	stc > 100 ? 100 : stc < 0 ? 0 : stc
stcColor = not highlightBreakouts ? (stc > stc[1] ? color.green : color.red) : #ff3013
stcPlot = plot(stc, title="STC", color=stcColor, transp=0)
upper = 75
lower = 25
transparent = color.new(color.white, 100)
upperLevel = plot(upper, title="Upper", color=color.gray)
hline(50, title="Middle", linestyle=hline.style_dotted)
lowerLevel = plot(lower, title="Lower", color=color.gray)

fill(upperLevel, lowerLevel, color=#f9cb9c, transp=90)

upperFillColor = stc > upper and highlightBreakouts ? color.green : transparent
lowerFillColor = stc < lower and highlightBreakouts ? color.red : transparent

fill(upperLevel, stcPlot, color=upperFillColor, transp=80)
fill(lowerLevel, stcPlot, color=lowerFillColor, transp=80)
strategy.initial_capital = 50000
ordersize=floor(strategy.initial_capital/close)
targetvalue = input(title="Target/stop", type=input.integer, defval=400)

ma1length = input(title="SMA1", type=input.integer, defval=35)
ma2length = input(title="SMA2", type=input.integer, defval=200)
ma1 = ema(close,ma1length)
ma2 = ema(close,ma2length)

bullbuy = crossover(stc, lower) and ma1>ma2 and close>ma1
bearsell = crossunder(stc, upper) and ma1<ma2 and close<ma1

if (bullbuy)
    strategy.entry("Riposte", strategy.long, ordersize)
    strategy.exit( "Riposte close", from_entry="Riposte", qty_percent=100, profit=targetvalue,loss=targetvalue)

if (bearsell)
    strategy.entry("Riposte", strategy.short, ordersize)
    strategy.exit( "Riposte close", from_entry="Riposte", qty_percent=100, profit=targetvalue,loss=targetvalue)

//plotshape(bullbuy,  title= "Purple", location=location.belowbar, color=#006600, transp=0, style=shape.circle, size=size.tiny, text="Riposte")
//plotshape(bearsell,  title= "Purple", location=location.abovebar, color=#006600, transp=0, style=shape.circle, size=size.tiny, text="Riposte")















```

> Detail

https://www.fmz.com/strategy/435160

> Last Modified

2023-12-12 17:43:19
