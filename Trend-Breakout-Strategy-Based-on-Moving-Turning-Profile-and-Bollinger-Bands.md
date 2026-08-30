
> Name

Trend-Breakout-Strategy-Based-on-Moving-Turning-Profile-and-Bollinger-Bands
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
This strategy is based on the volatility zone indicator and introduces the moving turning contour to find potential trend breakthrough points. It works by calculating a forward-moving fluctuation band and issuing a trading signal when the price breaks through the forward-moving fluctuation band. This strategy combines the powerful trend identification ability of the fluctuation zone with the early warning ability provided by the moving turning contour, aiming to find more effective entry points.
## Strategy Principle
1. Calculate the midline, upper line and lower line of ordinary fluctuation bands
2. Move the midline, upper line and lower line of the fluctuation band forward by a certain period
3. A buy signal is issued when the price breaks through the forward moving upper line from bottom to top.
4. When the price breaks through the forward moving lower line from top to bottom, a sell signal is issued
5. After entering the market, use the reverse fluctuation band line as the stop loss level.
## Advantage Analysis
1. The moving turning contour provides early warning and can detect trend turning points earlier.
2. Combined with the trend identification ability of the fluctuation zone indicator itself, it improves the accuracy of the signal.
3. Set the stop loss position in advance to effectively control risks
4. Combining trends and bands, you can establish a position in a better position
## Risk Analysis
1. Improper parameter settings may lead to too many error signals
2. Moving reversal contours may preis a breakout and form a stop-loss
3. It is necessary to further combine trend judgment to avoid being trapped in a volatile market
4. There is a certain lag and the turning point cannot be fully grasped.
## Optimization direction
1. Test different combinations of price data and parameters
2. Add additional filtering conditions to avoid false breakthroughs
3. Combine trend indicators to determine the general direction and avoid being trapped.
4. Optimize the stop loss strategy and adjust the stop loss range according to the market
5. Try to test the effect on different varieties and cycles
6. Can be combined with other indicators to find more accurate entry points
## Summarize
This strategy makes full use of the advantages of the fluctuation zone itself and improves the timeliness of entry by moving the turning contour. On the basis of optimizing the parameter combination, adding filter conditions and further considering the trend situation, this strategy can become a stronger breakthrough system. Overall, this strategy is simple and practical and deserves further testing and optimization to achieve better backtesting and real-time results.
|| 

## Overview

This strategy incorporates a forward shifted Bollinger Bands as a moving turning profile to identify potential trend breakout points. It generates trading signals when price breaks through the forward shifted bands. Combining the trend identification strength of BB and early warning of turning points from the shifted bands aims to discover more effective entries.

## Strategy Logic

1. Calculate standard BB with middle line, upper and lower bands.

2. Shift BB lines forward by a set period.

3. Signal long entry when price breaks above forward shifted upper band.

4. Signal short entry when price breaks below forward shifted lower band. 

5. Set stop loss at opposite BB line after entry.

## Advantage Analysis

1. Moving turning profile provides early warning for trend reversals.

2. Combines with BB's inherent trend identification ability for higher signal accuracy.

3. Preset stop loss positions allows effective risk control.

4. Can build positions at advantageous prices when combined with trend and swing analysis.

## Risk Analysis

1. Improper parameter tuning may generate excessive false signals.

2. Moving turning profile may have premature breakout and mid-way stop loss.

3. Needs further trend analysis to avoid whipsaws in ranging markets.

4. Has some lag, may not fully capture turning points.

## Optimization Directions

1. Test different price inputs and parameter combinations.

2. Add filters to avoid false breakouts.

3. Incorporate trend analysis to avoid being trapped.

4. Optimize stops based on market conditions.

5. Test effectiveness across different instruments and timeframes. 

6. Combine with other indicators for more accurate entries.

## Summary

This strategy fully utilizes the inherent advantages of Bollinger Bands and improves entry timing via the moving turning profile. With optimized parameters, additional filters, and further trend analysis, it can become a robust breakout system. Overall, a simple and practical strategy worth further testing and optimization for improved performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_hl2|0|source: hl2|high|low|open|close|hlc3|hlcc4|ohlc4|
|v_input_2|20|length|
|v_input_3|true|mult|
|v_input_4|26|x_offset|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-11 00:00:00
end: 2023-09-18 00:00:00
period: 15m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("LAGging span leaves Bollinger Bands strategy" , shorttitle="LagBB" , overlay=true)
source = input( hl2 )
length = input(20, minval=1)
mult = input( 1.0, minval=0.0, maxval=50)
x_offset = input( 26 ,minval=0 , maxval=244 )

basis = sma(source, length)
dev = mult * stdev(source, length)
upper = basis + dev
lower = basis - dev
buyEntry = crossover(source, upper[x_offset] )
sellEntry = crossunder(source, lower[x_offset] )
if (crossover(source, upper[x_offset] ))
    strategy.entry("LE", strategy.long, stop=lower, oca_name="BollingerBands",  comment="LE")
else
    strategy.cancel(id="LE")
if (crossunder(source, lower[x_offset] ))
    strategy.entry("SE", strategy.short, stop=upper, oca_name="BollingerBands",  comment="SE")
else
    strategy.cancel(id="SE")
//plot(strategy.equity, title="equity", color=color.red, linewidth=2, style=plot.style_areabr)
plot( upper , color=#cccc00 , transp=50 , offset=x_offset )
plot( basis , color=#cccc00 , offset=x_offset )
plot( lower , color=#cccc00 , transp=50 , offset=x_offset )
```

> Detail

https://www.fmz.com/strategy/427245

> Last Modified

2023-09-19 13:29:51
