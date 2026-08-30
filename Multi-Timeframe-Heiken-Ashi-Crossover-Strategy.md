
> Name

Multi-Timeframe-Heiken-Ashi-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy is based on the smoothed convergence and divergence average indicators of three time periods. When the indicators of different periods are bullish or bearish in the same direction, a trading signal is generated. The purpose is to use multiple time frames to confirm trends and reduce the probability of false signals.
## Principle
The Heiken Ashi indicator is different from ordinary K-lines. Its calculation method can smooth the price curve and identify trends more accurately.
This strategy uses the smoothed convergence and divergence average indicators of three time periods: daily, weekly and monthly. When the three are bullish in the same direction, that is, when the fire candle lines of all time periods are green, a buy signal is generated; when the three are bearish in the same direction, that is, when the fire candle lines are all red, a sell signal is generated.
After entering the market, as long as the smoothed convergence and divergence average line turns in any time period, a closing signal will be generated.
## Advantages
1. Multi-time frame verification can reduce false signals and enhance stability.
2. The smoothed average convergence and divergence indicator can identify trends and reduce noise.
3. The rules are simple, clear and easy to implement.
4. Flexible selection of time period combinations to adapt to different varieties.
5. No parameter optimization, extremely easy to operate.
## Risks and Solutions
1. Due to multiple restrictions, trading opportunities may be missed. Conditional restrictions can be reduced.
2. The lag problem of the smoothed average convergence and difference still exists, which may delay the signal. Can be combined with other indicators for optimization.
3. Without a stop loss, the risk cannot be controlled. A trailing stop loss strategy can be added.
4. The profit and loss ratio is fixed and lacks flexibility. Dynamic stop-profit and stop-loss can be set.
5. Based only on indicators, it is easy to produce false signals. A volume and price confirmation mechanism can be added.
## Optimization ideas
1. Test by adding more time frames, such as 15 minutes or 60 minutes.
2. Optimize the parameters of the smoothed average line of similarity and difference to improve sensitivity.
3. Add a trailing stop loss strategy to control risks.
4. Research on adding market structure indicators to avoid the shock range.
5. Add new re-entry conditions and extend the holding period.
## Summarize
This strategy takes advantage of the multi-time period smoothed average convergence and divergence indicators to achieve trend tracking, but it is easy to generate false signals based only on indicators. It can be improved by adding more indicators, stop loss strategies, optimization parameters, etc. to make the strategy more reliable. Overall, the multi-time frame verification idea is worth learning from.
|| 

## Overview

This strategy uses Heiken Ashi candles across three timeframes to generate signals when all timeframes align bullish or bearish. It aims to confirm trend using multiple timeframes to reduce false signals.

## Principles

Heiken Ashi candles differ from regular candles by smoothing price action for easier trend identification.

The strategy employs daily, weekly and monthly Heiken Ashi candles. When all three align bullish, with green candles, long signal is generated. When all red candles, short signal is generated.

Exits when any timeframe flips direction after entry.

## Advantages  

1. Multi-timeframe confirmation reduces false signals and enhances robustness.

2. Heiken Ashi smooths noise to identify trend.

3. Simple straightforward rules easy to implement. 

4. Flexible timeframes adaptable to different products.

5. No parameter optimization required, very easy to use.

## Risks and Mitigations

1. Strict conditions may miss opportunities. Can relax condition requirements.

2. Heiken Ashi lag remains, potentially delaying signals. Can optimize with additional indicators.

3. No stop loss inability to control risk. Can add moving stop loss.

4. Fixed risk-reward lacks flexibility. Can implement dynamic stops. 

5. Indicator-only prone to false signals. Can add price-volume confirmation.

## Enhancement Opportunities

1. Test additional timeframes like 15m or 60m.

2. Optimize Heiken Ashi parameters for sensitivity.

3. Add moving stop loss for risk control.

4. Incorporate market structure indicators to avoid ranges.

5. Develop re-entry conditions to extend holding period.

## Summary

The strategy taps into Heiken Ashi across timeframes for trend following, but indicator-only design prone to false signals. Improvements can be made via additional indicators, stops, parameter optimization to make it more reliable. Overall the multi-timeframe confirmation is a useful concept.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|D|TM 1|
|v_input_2|W|TM 2|
|v_input_3|M|TM 3|
|v_input_4|true|longA|
|v_input_5|false|shortA|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-01 00:00:00
end: 2023-03-23 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
args: [["v_input_5",true]]
*/

//@version=4
strategy("Heiken Ashi MTF Strategy")
ha_t = heikinashi(syminfo.tickerid)

res = input('D', title="TM 1")
ha_open = security(ha_t, res, open)
ha_close = security(ha_t, res, close)
ha_dif = ha_open-ha_close
ha_diff=iff(ha_dif > 0, 1, iff(ha_dif<0, 2, 3))

res2 = input('W', title="TM 2")
ha_open2 = security(ha_t, res2, open)
ha_close2 = security(ha_t, res2, close)
ha_dif2 = ha_open2-ha_close2
ha_diff2=iff(ha_dif2 > 0, 1, iff(ha_dif2<0, 2, 3))

res3 = input('M', title="TM 3")
ha_open3 = security(ha_t, res3, open)
ha_close3 = security(ha_t, res3, close)
ha_dif3 = ha_open3-ha_close3
ha_diff3=iff(ha_dif3 > 0, 1, iff(ha_dif3<0, 2, 3))

plot(15, title="TF1", color=iff(ha_diff==1, color.red, iff(ha_diff==2, color.green, color.white)), style=plot.style_circles, linewidth=5, join=true)
plot(14, title="TF2", color=iff(ha_diff2==1, color.red, iff(ha_diff2==2, color.green, color.white)), style=plot.style_circles, linewidth=5, join=true)
plot(13, title="TF3", color=iff(ha_diff3==1, color.red, iff(ha_diff3==2, color.green, color.white)), style=plot.style_circles, linewidth=5, join=true)


short = ha_diff ==1 and ha_diff2==1 and ha_diff3 ==1
long = ha_diff ==2 and ha_diff2==2 and ha_diff3 ==2

exitlong = ha_diff ==1 or ha_diff2==1 or ha_diff3 ==1
exitshort = ha_diff ==2 or ha_diff2==2 or ha_diff3 ==2

longA = input(true)
shortA = input(false)

if(longA)
    strategy.entry("long",1,when=long)
    strategy.close("long",when=exitlong)
if(shortA)
    strategy.entry("short",0,when=short)
    strategy.close("short",when=exitshort)
```

> Detail

https://www.fmz.com/strategy/427188

> Last Modified

2023-09-18 21:50:05
