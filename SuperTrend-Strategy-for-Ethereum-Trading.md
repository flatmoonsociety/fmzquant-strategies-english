
> Name

SuperTrend-Strategy-for-Ethereum-Trading based on super trend Ethereum trading strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/4c6c2d08e3e761c461f5d94b233c7d078c7278e513d36c9e6630be7c604bb3e0.png)
[trans]
## Overview
This strategy is based on the super trend indicator and combines ATR to dynamically set stop loss lines to profit from the strong trend of Ethereum. It works on the ETH/USD trading pair on the Coinbase exchange.
## Strategy Principle
This strategy uses a classic trend following indicator, the Super Trend Indicator, to determine trend direction. The Super Trend Indicator consists of two curves, namely:
1. Uptrend stop loss line, hold long orders in the rising trend;
2. Downtrend stop loss line, hold short orders in the downtrend.
When the price changes from an upward trend to a downward trend, a short position is opened; when the price changes from a downward trend to an upward trend, a long position is opened.
In addition, the strategy also uses the ATR indicator to dynamically adjust the position of the stop loss line. Specifically, the position of the rising stop loss line is the average of the highest price and the lowest price minus ATR multiplied by a coefficient; the position of the falling stop loss line is the average of the highest price and the lowest price plus ATR multiplied by a coefficient. This allows you to adjust the stop loss line based on market volatility.
After the entry signal is sent, if the price returns to the stop loss line, stop loss exit will be carried out.
## Strategic Advantages
This is a relatively mature trend following strategy with the following advantages:
1. Use the super trend indicator to determine the trend direction, which has high reliability;
2. Applying ATR to adaptively adjust the stop loss line can effectively control risks;
3. The strategy logic is simple and clear, easy to understand and modify;
4. Can make profits in the highly volatile digital currency market.
## Strategy Risk
There are also some risks with this strategy:
1. There is a probability that the super trend indicator will make a wrong judgment, which may lead to unnecessary losses;
2. The ATR stop loss may be too aggressive and will be stopped by price reversal;
3. The digital currency market is highly volatile, and the probability of the stop loss being breached is high;
4. Exchanges with higher transaction fees will affect the final profit.
In order to reduce the above risks, the ATR coefficient can be appropriately adjusted, or combined with other indicators to filter trading signals. You can also consider leaving a certain buffer in the stop loss position.
## Strategy optimization direction
There is room for further optimization of this strategy:
1. More indicator combinations can be introduced to improve the accuracy of signals;
2. The optimal values of ATR coefficient and length parameters can be studied;
3. You can set the risk stop loss ratio to dynamically adjust the position size;
4. The effectiveness of the strategy can be tested on more digital currency trading pairs.
## Summarize
Overall, this strategy is a mature and reliable trend following strategy. It uses the super trend indicator to determine the trend direction, and uses ATR to adjust the stop loss position to control risks while making profits. This strategy is suitable for high-volatility digital currency transactions, and works better on mainstream currencies such as Ethereum. Through further optimization, the strategy can be applied in a wider range of markets and obtain more stable excess returns.
|| 

## Overview

This strategy is based on the SuperTrend indicator and uses ATR to dynamically set stop loss lines to profit from strong trends in Ethereum. It can run on the ETH/USD trading pair on Coinbase exchange.  

## Strategy Logic

The strategy uses a classic trend-following indicator - SuperTrend indicator to determine the trend direction. The SuperTrend indicator consists of two lines:  

1. Uptrend stop loss line to hold long positions in uptrends;
2. Downtrend stop loss line to hold short positions in downtrends.

When price turns from uptrend to downtrend, open short position. When price turns from downtrend to uptrend, open long position.

In addition, the strategy utilizes the ATR indicator to dynamically adjust the stop loss line. Specifically, the uptrend stop loss line position is the average of highest high and lowest low minus ATR multiplied by a coefficient; the downtrend stop loss line position is the average of highest high and lowest low plus ATR multiplied by a coefficient. This allows adjusting the stop loss based on market volatility.  

After entry signals are triggered, if price breaks back above the stop loss line, stop out with loss. 

## Advantages

This is a relatively mature trend following strategy with the following advantages:

1. Use SuperTrend indicator to determine trend direction reliably;  
2. Apply adaptive ATR stop loss to effectively control risks;
3. Simple and clear strategy logic, easy to understand and modify; 
4. Profitable in the high volatility cryptocurrency market.

## Risks

There are also some risks with this strategy:

1. Probability of SuperTrend indicator judging wrongly exists, may cause unnecessary losses;
2. ATR stop loss may be too aggressive, stopped out by price reversals;
3. High volatility in crypto markets increases probability of stop loss being hit;
4. Higher transaction fees on some exchanges impacts final profitability.

To mitigate the above risks, ATR coefficient can be adjusted, or add filters with other indicators. Stop loss buffer can also be considered.

## Improvement Directions 

There is room for further improvements:

1. Introduce more indicators to improve signal accuracy;  
2. Research optimal values for ATR length and coefficient;
3. Implement dynamic position sizing based on risk-reward ratio;
4. Test strategy effectiveness across more crypto trading pairs.

## Conclusion

Overall this is a mature and reliable trend following strategy. It uses SuperTrend indicator to determine trend direction and adapts stop loss with ATR to control risks while profiting. The strategy works well for high volatility cryptocurrencies like Ethereum. Further optimizations can expand its application across more markets for steady outperformance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|21|ATR Period|
|v_input_2|6.2|ATR Multiplier|
|v_input_3|false|Take Wicks into Account ?|
|v_input_4|false|Start from Specific Date ?|
|v_input_5|2019|Start Year|
|v_input_6|true|Start Month|
|v_input_7|true|Start Day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-01 00:00:00
end: 2024-01-07 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4 
strategy("SuperTrend Strategy", 
     overlay=true, 
     initial_capital=2e3, 
     process_orders_on_close=true, 
     commission_type=strategy.commission.percent, 
     commission_value=0.1 
     ) 
  
length = input(title="ATR Period", type=input.integer, defval=21) 
mult = input(title="ATR Multiplier", type=input.float, step=.25, defval=6.2) 
wicks = input(title="Take Wicks into Account ?", type=input.bool, defval=false) 
  
useDate = input(title="Start from Specific Date ?", defval=false) 
yearStart = input(title="Start Year", defval=2019) 
monthStart = input(title="Start Month", minval=1, maxval=12, defval=1) 
dayStart = input(title="Start Day", minval=1, maxval=31, defval=1) 
  
startTime = timestamp(yearStart, monthStart, dayStart, 0, 0) 
startFrom = useDate ? time(timeframe.period) >= startTime : true 
  
atr = mult * ta.atr(length) 
  
longStop = hl2 - atr 
longStopPrev = nz(longStop[1], longStop) 
longStop := (wicks ? low[1] : close[1]) > longStopPrev ? math.max(longStop, longStopPrev) : longStop 
  
shortStop = hl2 + atr 
shortStopPrev = nz(shortStop[1], shortStop) 
shortStop := (wicks ? high[1] : close[1]) < shortStopPrev ? math.min(shortStop, shortStopPrev) : shortStop 
  
dir = 1 
dir := nz(dir[1], dir) 
dir := dir == -1 and (wicks ? high : close) > shortStopPrev ? 1 : dir == 1 and (wicks ? low : close) < longStopPrev ? -1 : dir 
  
longColor = color.green 
shortColor = color.red 
  
plot(dir == 1 ? longStop : na, title="Long Stop", style=plot.style_linebr, linewidth=2, color=longColor) 
plotshape(dir == 1 and dir[1] == -1 ? longStop : na, title="Long Start", location=location.absolute, style=shape.circle, size=size.tiny, color=longColor, transp=0) 
  
plot(dir == 1 ? na : shortStop, title="Short Stop", style=plot.style_linebr, linewidth=2, color=shortColor) 
plotshape(dir == -1 and dir[1] == 1 ? shortStop : na, title="Short Start", location=location.absolute, style=shape.circle, size=size.tiny, color=shortColor, transp=0) 
  
longCondition = dir[1] == -1 and dir == 1 
if longCondition and startFrom 
    strategy.entry("Long", strategy.long, stop=longStop) 
else 
    strategy.cancel("Long") 
  
shortCondition = dir[1] == 1 and dir == -1 
if shortCondition and startFrom 
    strategy.entry("Short", strategy.short, stop=shortStop) 
else 
    strategy.cancel("Short")
    
```

> Detail

https://www.fmz.com/strategy/438035

> Last Modified

2024-01-08 14:35:37
