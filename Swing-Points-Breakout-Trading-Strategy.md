
> Name

Swing-Points-Breakout-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

This strategy trades trend breakouts by identifying price swing highs and lows. This strategy belongs to the trend following strategy and is designed to capture price fluctuations caused by medium and long-term trends.
Strategy principle:
1. Calculate the swing high and swing low for the specified period.
2. When the price exceeds the swing high, make a buy operation.
3. When the price breaks below the swing low, sell.
4. Set the stop loss point to the previous swing low (long order) or the previous swing high (short order) to control risk.
5. When the price falls below the stop loss point again, stop the loss and exit the position.
The advantages of this strategy include:
1. Identifying swing points can effectively determine trends. Trend trading is a high-win-probability operation.
2. Breaking through the swing point causes price behaviors to accelerate, which is helpful for tracking the trend.
3. Stop loss points are set at key support and resistance levels to control risks.
Risks of this strategy include:
1. There is often a lag in identifying swing points, and the best entry point may be missed.
2. If the stop loss point is too close, it is easy to be hit by the volatile market. The stop loss range should be widened.
3. Breakthroughs can easily form a head effect, and stop losses must be set to deal with pullbacks.
In short, the swing point breakout strategy takes trend breakout operations by tracking the mid- to long-term trend. This strategy can achieve a higher winning rate, but attention must be paid to the selection of entry points and the setting of stop loss points to optimize the strategy effect. Investors should consider the risk characteristics of this strategy and use appropriate fund management methods to obtain long-term stable returns.
||



This strategy identifies swing highs and lows in price to trade breakouts in the trending direction. It is a trend-following strategy that aims to capture price swings during sustained trends.

Strategy Logic:

1. Identify swing highs and lows over a specified period. 

2. Go long when price breaks above swing high.

3. Go short when price breaks below swing low. 

4. Set stop loss at previous swing low (for long) or swing high (for short) to control risk.

5. If price reverses below stop loss, exit the position.

Advantages:

1. Swing points effectively identify trends. Trend trading has high win rate.

2. Breaking swing points accelerates price behaviors, good for trend following.

3. Stops at key support/resistance levels manage risk.

Risks:

1. Swing points often lag, risk missing best entry timing. 

2. Stops being too tight get hit by market noise. Consider widening range.

3. Breakouts prone to head fakes. Need stops to defend pullbacks.

In summary, the swing points breakout strategy follows medium/long-term trends using trend-based breakout trading. It can achieve high win rate but requires careful entry timing and stop loss placement to optimize performance. Investors should consider its risks and apply appropriate money management for long-term steady gains.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|leftBars|
|v_input_2|true|rightBars|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-12 00:00:00
end: 2023-09-11 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Swing Points", overlay=true)


leftBars = input(1)
rightBars=input(1)
sl = pivotlow(low, leftBars, rightBars)
sh = pivothigh(high, leftBars, rightBars)

last_sh=na
last_sh:= sh!=0 ? sh : nz(last_sh[1])

last_sl=na
last_sl:= sl!=0 ? sl : nz(last_sl[1])


EMA = ema(close,55)

longCondition = sh and high > EMA
shortCondition = sl and close < EMA
exitLongCondition = sl < sh[1]
exitShortCondition = sh > sl[1]

if longCondition 
    strategy.entry("swinghigh", strategy.long, stop=last_sh)
    
if shortCondition 
    strategy.entry("swinglow", strategy.short, stop=last_sl)
   
if exitLongCondition
    strategy.exit("stoplong", "swinghigh", stop = last_sl )

if exitShortCondition
    strategy.exit("stopshort", "swinglow", stop = last_sh )
    
plot(EMA,linewidth = 4)
```

> Detail

https://www.fmz.com/strategy/426480

> Last Modified

2023-09-12 14:40:56
