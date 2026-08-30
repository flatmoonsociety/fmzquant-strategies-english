
> Name

Triple-EMA-Crossover-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/10932b61f00228dfbaf.png)
[trans]

## Overview
The triple EMA overlay breakthrough strategy uses the triple exponential moving average indicator to determine the market trend direction and enter the market at the trend breakthrough point. This strategy also combines the K-line shape to determine the quality of the signal.
## Strategy Principle
This strategy is mainly based on the following principles:
1. Use three EMA lines of different periods (200-day line, 50-day line, and 20-day line) to determine the market's general trend, mid-term trend, and short-term trend.
2. When the short-term trend EMA (20-day line) breaks above the mid-term EMA (50-day line) upward, a buy signal is generated; when it breaks downward, a sell signal is generated.
3. Combined with the K-line shape, judge the reliability of the breakthrough signal. Only when the closing price of the second K line is higher (lower) than the highest price (lowest price) of the previous day, it is considered a reliable breakthrough.
4. Set take-profit and stop-loss points to avoid risks that exceed the reasonable fluctuation range.
## Strategic Advantages
1. Use multiple EMA indicators to judge trends and improve the accuracy of judgment.
2. Combine K-line patterns to filter misleading signals to avoid unnecessary trading risks.
3. Set take-profit and stop-loss points to effectively control single losses.
## Strategy Risk
1. In a volatile market, the EMA indicator produces a large number of misleading signals and cannot effectively judge market trends.
2. The combination of single indicators is simple and has poor judgment on complex market conditions.
3. Without considering transaction costs, it may not be profitable in a high-fee market.
## Strategy optimization
1. Other indicators such as MACD and KDJ can be introduced to form a combination of indicators to improve the accuracy of judgment.
2. Testing and optimization can be carried out according to different varieties and cycle parameters, so that the strategy parameters are more in line with the characteristics of the varieties.
3. Trading volume indicators can be introduced to avoid misleading signals of low volume.
## Summarize
The overall idea of ​​the triple EMA overlay breakthrough strategy is clear and easy to understand. Use EMA to determine the primary and secondary market trends and find entry opportunities when the trend turns. However, this strategy has certain limitations and cannot handle complex market conditions well. It is recommended to use it in combination with other indicators and optimize parameters to adapt to a wider market environment.
||

## Overview

The Triple EMA Crossover Breakout strategy uses triple exponential moving average (EMA) indicators to determine market trend direction and enter at trend breakout points. It also combines candlestick patterns to filter signal reliability. 

## Strategy Logic

The strategy is mainly based on the following principles:

1. Use three EMAs with different periods (200-day, 50-day, 20-day) to determine major, medium-term and short-term market trends.  

2. When the short-term EMA (20-day) crosses above the medium-term EMA (50-day), a buy signal is generated. When it crosses below, a sell signal is generated.

3. Combine candlestick patterns to check signal reliability. Only when the closing price of the second candle is higher (lower) than the previous candle's high (low) price, the breakout is considered reliable.  

4. Set stop loss and take profit levels to limit risks beyond reasonable price fluctuations.

## Advantage Analysis 

1. Using multiple EMAs improves trend judgment accuracy.  

2. Filtering fake signals with candlestick patterns avoids unnecessary trading risks.

3. Stop loss and take profit controls single trade loss effectively.

## Risk Analysis

1. In ranging markets, EMAs may generate excessive fake signals and fail to determine market direction.  

2. The single indicator system has limited capacity in complex market situations.

3. It ignores trading costs which could lead to unprofitability in high-fee markets.

## Optimization

1. Introduce other indicators like MACD and KDJ to form a combined system and improve judgment accuracy.  

2. Optimize parameters through backtesting for specific symbols and timeframes to make the strategy fit better.

3. Add trading volume to avoid low-volume fake signals.

## Conclusion

The Triple EMA Crossover Breakout Strategy has clear, easy-to-understand logic to determine market trends and find entry timing using EMA crossovers. But it also has some limitations in dealing with complex market situations. It's recommended to combine with other indicators and optimize parameters to adapt to more diverse trading environments.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0.5|ENTRY LEVEL 1|
|v_input_2|0.25|ENTRY LEVEL 2|
|v_input_3|false|ENTRY LEVEL 3|
|v_input_4|-0.35|STOP LEVEL|
|v_input_5|0.88|TP LEVEL|
|v_input_6|false|Don't Use EMA|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-21 00:00:00
end: 2023-12-27 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("GHG RETRACEMENT MODE 1", overlay=true)

entryLevel1 = input(0.5, "ENTRY LEVEL 1")
entryLevel2 = input(0.25, "ENTRY LEVEL 2")
entryLevel3 = input(0.0, "ENTRY LEVEL 3")

stopLevel = input(-0.35, "STOP LEVEL")
tpLevel = input(0.88, "TP LEVEL")
dontUseEma = input(false, "Don't Use EMA")


get_level(level, level100, level0) =>
    level * (level100 - level0) + level0

buySignal = close[2] < open[2] and close[1] > open[1] and close[0] > open[0] and high[0] > open[2] and high[1] < high[2]
sellSignal = close[2] > open[2] and close[1] < open[1] and close[0] < open[0] and low[0] < open[2] and low[1] > low[2]

if buySignal and (close[0] > ta.ema(close, 200) or dontUseEma)
    l = label.new(bar_index, na)
    entryPrice1 = get_level(entryLevel1, high[0], low[2])
    entryPrice2 = get_level(entryLevel2, high[0], low[2])
    entryPrice3 = get_level(entryLevel3, high[0], low[2])
    
    exitPrice = get_level(tpLevel, high[0], low[2])
    stopPrice = get_level(stopLevel, high[0], low[2])
    
    strategy.order("BUY 1", strategy.long, comment="BUY 1", limit=entryPrice1)
    strategy.exit("exit", "BUY 1", limit=high[0], stop=stopPrice)
    strategy.order("BUY 2", strategy.long, comment="BUY 2", limit=entryPrice2)
    strategy.exit("exit", "BUY 2", limit=high[0], stop=stopPrice)

    label.set_text(l, "Buy => " + str.tostring(close[2]) + "\nSL=> " + str.tostring(stopPrice) + "\nTP => " + str.tostring(exitPrice) )
    label.set_color(l, color.green)
    label.set_yloc(l, yloc.belowbar)
    label.set_style(l, label.style_label_up)
    
if sellSignal and (close[0] < ta.ema(close, 200) or dontUseEma)
    a = label.new(bar_index, na)
    entryPrice1 = get_level(entryLevel1, low[0], high[2])
    entryPrice2 = get_level(entryLevel2, low[0], high[2])
    entryPrice3 = get_level(entryLevel3, low[0], high[2])
    
    exitPrice = get_level(tpLevel, low[0], high[2])
    stopPrice = get_level(stopLevel,low[0], high[2])
    
    strategy.order("SELL 1", strategy.short, comment="SELL 1", limit=entryPrice1)
    strategy.exit("exit", "SELL 1", limit=low[0], stop=stopPrice) 
    strategy.order("SELL 2", strategy.short, comment="SELL 2", limit=entryPrice2)
    strategy.exit("exit", "SELL 2", limit=low[0], stop=stopPrice) 

    label.set_text(a,"Sell => " + str.tostring(close[2]) + "\nSL=> " + str.tostring(stopPrice) + "\nTP => " + str.tostring(exitPrice) )
    label.set_color(a, color.red)
    label.set_yloc(a, yloc.abovebar)
    label.set_style(a, label.style_label_down)
   

```

> Detail

https://www.fmz.com/strategy/436884

> Last Modified

2023-12-28 15:56:54
