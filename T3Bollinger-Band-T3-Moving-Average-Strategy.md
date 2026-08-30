
> Name

Bollinger-Band-T3-Moving-Average-Strategy for shock breakthrough of Bollinger Band T3 moving average strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/5a0c6e0fef0c3f0026.png)

[trans]


## Overview
This strategy makes full use of the trend judgment function of the moving average and the overbought and oversold judgment of the Bollinger Bands, supplemented by the T3 smoothing moving average to filter shocks, so as to timely judge the form and enter the market when the trend turns. In the shock range, the Bollinger Bands are used to identify overbought and oversold areas to perform reverse operations and achieve ultra-short-term trading.
## Strategy Principle
This strategy mainly uses three sets of moving averages to identify trends and judge trading signals. The first is the T3 moving average, which plays a filtering role through multiple exponential smoothings, which can effectively filter price shocks and determine the trend direction. The second is the medium-term moving average. Here, the SMA moving average with a length of 20 is used to determine the medium-term trend direction. Finally, there is the fast and slow moving averages, which are T3 moving averages with lengths of 50 and 200 respectively. If the fast line is greater than the slow line, it indicates an upward trend, otherwise it is a downward trend.
The judgment of trading signals is that when the mid-term moving average crosses golden cross, go long in conjunction with the upward trend; when the mid-term moving average crosses dead cross, go short in conjunction with the downward trend. In addition, the upper and lower rails of Bollinger Bands are also used to judge the situation. If the price breaks through the upper rails, a stop profit will be considered, and if the price breaks below the lower rails, a stop loss will be considered.
Specifically, the condition for going long is that the mid-term moving average crosses the mid-term T3 moving average, and the fast line is greater than the slow line. After going long, if the price breaks through the upper Bollinger Band or the mid-term moving average crosses the T3 moving average, stop loss will be considered; the condition for going short is that the mid-term moving average crosses the T3 moving average, and the fast line is smaller than the slow line. After going short, if the price falls below the lower Bollinger Band or the mid-term moving average crosses the T3 moving average, stop loss will be considered.
## Strategic Advantages
- Use multiple sets of moving averages to give full play to their respective advantages, T3 smoothing and denoising, mid-term SMA to judge the trend, and fast and slow moving averages to judge the long-term trend.
- The upper and lower rails of Bollinger Bands determine overbought and oversold areas to reduce the risk of losses.
- The combination of trading signals is strict, which can effectively filter out shock and misleading
## Strategy Risk
- Improper setting of T3 moving average parameters may not allow effective filtering and may also cause lag.
- Improper Bollinger Band parameter settings may cause the upper and lower rails to be invalid.
- Improper selection of the moving average period may lead to incorrect judgment of the trend direction.
- The setting of take-profit and stop-loss points when breaking through the upper and lower rails is not accurate, and the profit may be taken too early or the stop-loss too late.
Optimization method:
- Adjust T3 moving average parameters to achieve smooth denoising and hysteresis balance
- Adjust the Bollinger Bands parameters so that the upper and lower rails wrap around the normal fluctuation range
- Test the moving average parameters of different periods and find the period parameters suitable for the variety
- Optimize take profit and stop loss points based on backtest results
## Strategy optimization direction
- Add trend strength judgment, such as ADX, to avoid being trapped by trend turning points
- Add volatility indicator and adjust parameters according to market fluctuations
- Add trailing stop loss and trailing stop loss to allow more profits to flow out
- You can consider the breakout strategy, and then track the stop loss after breaking through the upper and lower rails
## Summarize
Generally speaking, this strategy uses moving averages to systematically determine trends and Bollinger Bands to identify overbought and oversold areas. It can timely determine the pattern and enter the market when the trend turns, and can effectively control risks. However, attention needs to be paid to parameter adjustment and optimization in order to truly exert the effect of the strategy. If further optimized by combining trend strength indicators, volatility indicators, and trailing stop loss technology, the strategy can be made more flexible and intelligent.
||

## Overview

This strategy makes full use of the trend judgment of moving averages and overbought/oversold judgment of Bollinger Bands. With the smoothing of T3 moving average, it can identify the trend reversal timely and enter the market. In the oscillation zone, it uses the Bollinger Bands to identify overbought/oversold areas for counter trend trading. So it realizes ultra short-term trading.

## Strategy Logic

The strategy mainly uses three groups of moving averages to identify the trend and generate trading signals. First is the T3 moving average, which can filter price fluctuations through exponential smoothing and judge the trend direction. Second is the middle-term moving average, here uses 20-period SMA to determine the middle-term trend. Last is the fast and slow moving averages, 50-period and 200-period T3 moving averages respectively. When fast line is greater than slow line, it indicates an upward trend, otherwise downward trend.

The trading signals are generated when the middle-term SMA crosses over the middle-term T3 upward combining with an upward trend, go long. When the middle-term SMA crosses below the middle-term T3 downward combining with a downward trend, go short. In addition, the Bollinger Bands can be used for profit taking and stop loss. If price breaks through the upper band, consider taking profit. If price breaks through the lower band, consider stop loss.

Specifically, the long condition is middle SMA crosses over middle T3 upward, and fast MA is greater than slow MA. If price breaks through the upper Bollinger band or middle SMA crosses below T3, consider taking profit. The short condition is middle SMA crosses below middle T3 downward, and fast MA is less than slow MA. If price breaks through the lower Bollinger band or middle SMA crosses above T3, consider stop loss.

## Advantages

- Fully utilize the advantages of multiple moving averages, T3 for smoothing, middle SMA for trend, fast and slow MAs for long-term trend 
- Bollinger Bands upper and lower bands judge overbought/oversold levels, reduce loss risk
- Strict trading signals combination, avoid misleading by fluctuations

## Risks

- Improper T3 parameters may fail to smooth or cause lagging
- Improper Bollinger Bands parameters may cause invalid bands
- Wrong moving average periods lead to wrong trend direction
- Inaccurate breakout points for profit taking and stop loss, may exit too early or too late 

Improvements:
- Adjust T3 parameters for balancing smoothing and lagging
- Adjust Bollinger Bands parameters to cover normal fluctuation range
- Test different moving average periods to find suitable ones for the asset
- Optimize take profit and stop loss points based on backtest results

## Optimization Directions

- Add trend strength indicator like ADX to avoid reverse at trend turning points
- Add volatility indicator to adjust parameters based on market volatility
- Add trailing stop loss to allow more profits to run out
- Consider breakout strategy, trailing stop loss after breaking bands

## Summary

In summary, this strategy uses moving averages systematically to determine the trend, and identifies overbought/oversold levels with Bollinger Bands. It can enter the market timely at trend reversals, and also effectively controls risks. But parameters tuning and optimization are important for the strategy to truly perform well. Further combining with trend strength, volatility, and trailing stop loss can make the strategy more robust and intelligent.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|length|
|v_input_2|2.5|StdDev|
|v_input_3|false|Offset|
|v_input_4|true|Stop Loss|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-25 00:00:00
end: 2023-11-01 00:00:00
period: 10m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy(shorttitle="BB T3 Strategy", title="BB T3 Strategy", overlay=true)

//T3
b = 0.7
c1 = -b*b*b
c2 = 3*b*b+3*b*b*b
c3 = -6*b*b-3*b-3*b*b*b
c4 = 1+3*b+b*b*b+3*b*b

t3(len) => c1 * ema(ema(ema(ema(ema(ema(close, len), len), len), len), len), len) + c2 * ema(ema(ema(ema(ema(close, len), len), len), len), len) + c3 * ema(ema(ema(ema(close, len), len), len), len) + c4 * ema(ema(ema(close, len), len), len)
//T3 end

length = input(20, minval=1)

mult = input(2.5, minval=0.001, maxval=50, title="StdDev")
basis = t3(length)
basisDev = t3(length/10)

dev = mult * stdev(basisDev,length)
upper = basis + dev
lower = basis - dev
offset = input(0, "Offset", type = input.integer, minval = -500, maxval = 500)
plot(basis, "Basis", color=#872323, offset = offset)
p1 = plot(upper, "Upper", color=color.teal, offset = offset)
p2 = plot(lower, "Lower", color=color.teal, offset = offset)
fill(p1, p2, title = "Background", color=#198787, transp=95)

stoploss = input(true, "Stop Loss")

basisSma = sma(close, length)
p3 = plot(basisSma, color=color.blue, title="MA", offset=offset)

fastT3 = t3(50)
slowT3 = t3(200)

crossUp = crossover(basisSma, basis)
crossDown = crossunder(basisSma, basis)
bollBounce = crossover(close, upper)
bollReject = crossunder(close, lower)
underBasis = crossunder(close, basis)
overBasis = crossover(close, basis)

trendUp = fastT3 > slowT3
trendDown = fastT3 < slowT3

strategy.entry("long", strategy.long, when=(trendUp and crossUp), stop=(stoploss ? high+syminfo.mintick : na))
strategy.close("long", when=(bollBounce or crossDown or underBasis))
strategy.entry("short", strategy.short, when=(trendDown and crossDown), stop=(stoploss ? low-syminfo.mintick : na))
strategy.close("short", when=(bollReject or crossUp or overBasis))

```

> Detail

https://www.fmz.com/strategy/430869

> Last Modified

2023-11-02 15:45:31
