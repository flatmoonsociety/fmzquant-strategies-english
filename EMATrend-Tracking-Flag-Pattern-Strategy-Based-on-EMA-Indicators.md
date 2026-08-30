
> Name

Trend-Tracking-Flag-Pattern-Strategy-Based-on-EMA-Indicators
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/f46121bb0957b9326b.png)

[trans]

## Overview
This strategy mainly uses the EMA moving average indicator and the standard deviation indicator to determine the trend direction through the cross signal of the EMA moving average, and uses the standard deviation indicator to find breakthrough signals, thereby generating buy and sell signals. When the price breaks through the upper track, a buy signal is generated, and when the price breaks through the lower track, a sell signal is generated. It is a trend following type of strategy.
## Strategy Principle
The strategy mainly consists of three parts:
1. EMA moving average difference (s2): Calculate the difference between the fast EMA moving average (ema_range) minus the slow EMA moving average (ema_watch). This difference is used to determine the price trend direction.
2. Standard deviation upper and lower rails (s3): Based on the EMA moving average difference, multiples of the standard deviation are added to construct the upper and lower rail bands. The standard deviation multiple uses the golden section number 5.618.
3. Flag shapes and signals: When the price breaks through the upper rail from bottom to top, a buy signal is generated; when the price breaks through the lower rail from top to bottom, a sell signal is generated. At the same time, when a signal is generated, it is marked with a flag.
Through this combination of indicators, the trend direction of the price can be captured and buy and sell signals can be generated at key points, which is a typical trend following strategy.
## Advantage Analysis
This strategy has several advantages:
1. Use EMA moving average to determine the direction of the price trend, which can effectively track the trend.
2. Use the standard deviation indicator to construct upper and lower rails to avoid false signals at non-key points.
3. The flag signal is intuitive and clear, and you can clearly judge the buying and selling points.
4. Flexible parameter setting, the moving average period and standard deviation multiple can be adjusted.
5. Maximum drawdown control helps reduce risk.
## Risk Analysis
There are also some risks with this strategy:
1. The effect is better in trending markets, but it may produce more false signals in volatile markets.
2. If the standard deviation multiple is set too high, buying and selling opportunities will be missed.
3. Without a stop-loss strategy, a correction after a breakthrough may cause large losses.
In view of the above risks, the following methods can be used to optimize:
1. Increase the judgment of volatile markets and use other strategies instead in volatile markets.
2. Optimize the standard deviation parameters and find the best parameter combination.
3. Add a trailing stop to control losses on individual orders.
## Optimization direction
This strategy can be optimized from the following directions:
1. Add more indicator judgments, such as Bollinger Bands, to improve signal quality.
2. Optimize the moving average and standard deviation parameters to find the best parameter combination.
3. Add a stop loss strategy to reduce the risk of retracement.
4. Set the best buying and selling signal parameters according to different markets.
5. Add a machine learning algorithm to determine the overall market regime.
## Summarize
This strategy is a relatively typical trend following strategy as a whole, using EMA and standard deviation to build an indicator system and generating flag signals at key points. The advantage of the strategy is to capture the trend and use the standard deviation indicator to avoid false signals. The risk mainly lies in the false signals that shock the market and the risk of retracement caused by no stop loss. By adding judgment indicators, optimizing parameters and adding stop losses, the stability and profitability of the strategy can be further enhanced. Overall, the strategy framework is reasonable and has a lot of room for optimization.
|| 

## Overview

This strategy mainly uses EMA and standard deviation indicators to determine the trend direction through EMA cross signals and look for breakout signals with standard deviation to generate buy and sell signals. It belongs to the trend tracking type of strategy that generates buy signals when prices break through the upper rail and sell signals when prices break through the lower rail.

## Strategy Logic  

The strategy consists of three main parts:

1. EMA Difference (s2): Calculate the difference between fast EMA (ema_range) and slow EMA (ema_watch) to determine the price trend direction. 

2. Standard Deviation Channel (s3): Build upper and lower channel based on EMA difference with multiples of standard deviation. The standard deviation multiplier uses the golden ratio 5.618.

3. Flags and Signals: Generate buy signals when prices break through the upper rail from bottom up, and sell signals when prices break through the lower rail from top down. Flag shapes are used to mark the signals.  

Through this combination of indicators, it can capture the trend direction of prices and generate buy and sell signals at key points, which belongs to a typical trend tracking strategy.

## Advantage Analysis

The strategy has the following advantages:

1. EMA can effectively track trends.  
2. Standard deviation builds channels to avoid false signals.
3. Flag shapes make signals clear. 
4. Flexible parameter settings of moving averages and standard deviation multiples.  
5. Maximum drawdown control helps reduce risks.

## Risk Analysis  

There are also some risks:  

1. More false signals may occur in range-bound markets.
2. Too large standard deviation multiples may miss opportunities.  
3. No stop loss may lead to larger losses during retracements.

The solutions:

1. Add range-bound market judgment and use other strategies instead.
2. Optimize standard deviation parameters.
3. Add moving stop loss to control loss of individual trades.

## Optimization

The strategy can be optimized in the following directions:

1. Add more indicators like Bollinger Bands to improve signal quality.
2. Optimize moving average and standard deviation parameters. 
3. Add stop loss strategies to reduce drawdowns.
4. Set optimal buy/sell signal parameters according to different markets.
5. Add machine learning algorithms to determine overall market regime.  

## Conclusion  

In summary, this is a typical trend tracking strategy using EMA and standard deviation to build an indicator system and generate flag signals at key points. The advantages lie in catching trends and avoiding false signals with standard deviation. The main risks come from wrong signals in range-bound markets and drawdown risks due to no stop loss. By adding judgment indicators, optimizing parameters and adding stop loss, the strategy can be further enhanced in terms of stability and profitability. Overall, the strategy framework is reasonable and has great potential for optimization.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|5|ema_range|
|v_input_2|13|ema_watch|
|v_input_3_open|0|inval_a: open|high|low|close|hl2|hlc3|hlcc4|ohlc4|
|v_input_4_open|0|inval_b: open|high|low|close|hl2|hlc3|hlcc4|ohlc4|
|v_input_5|false|ratio|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-27 00:00:00
end: 2023-11-26 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("ROCKET_EWO", overlay=true)
ema_range = input(5)
ema_watch = input(13)
inval_a = input(open)
inval_b = input(open)
ratio = input(0)
max = 5000
s2=ta.ema(inval_a, ema_range) - ta.ema(inval_b, ema_watch)
c_color=s2 <= ratio ? 'red' : 'lime'
s3 = s2 + (ta.stdev(open, 1)) * 5.618
plotshape(s3, color=color.white, style=shape.cross, location=location.abovebar, size=size.auto, show_last=max, transp=30, offset= 0)
cr = s2 > 0
alertcondition(cr, title='[Rocket_EWO]', message='[Rocket_EWO]')
buy = s2 > 1
sell = s2 < -1
txt  = "?" + "\n"+ "\n"+ "\n"+ "\n"
plotshape(buy, color=color.lime, style=shape.triangleup, location=location.belowbar ,color=color.white, text=txt, size=size.normal, show_last=max, transp=1, offset= -3)
plotshape(not buy, color=color.red, style=shape.triangledown, location=location.belowbar, size=size.normal, show_last=max, transp=1, offset= 0)
signalperiod = time
s4 = ta.cross(s2, 0) ? time : na
colsig= s2 <= ratio ? color.red : color.lime
plotshape((time==s4)?7000:na,color=color.blue, style=shape.flag, location=location.abovebar, size=size.large, transp=1)

longCondition =  ta.crossover(s2, 1.618)
if (longCondition)
    strategy.entry("LONG Id", strategy.long)

shortCondition = ta.crossunder(s2, 1.618)
if (shortCondition)
    strategy.entry("SHORT Id", strategy.short)

strategy.close("LONG Id", when = s2 < 0.218)
// strategy.risk.max_drawdown(75, strategy.percent_of_equity)

```

> Detail

https://www.fmz.com/strategy/433424

> Last Modified

2023-11-27 15:30:29
