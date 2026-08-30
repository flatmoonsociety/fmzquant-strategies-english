
> Name

Quantitative-Trading-Strategy-Based-on-Moving-Average
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/7d84b64d03795abc452d50ae84f7c1f3ac22978581565ee8b4fd616f06b47324.png)
[trans]

## Overview
This strategy calculates moving averages of different periods and determines their golden crosses and dead crosses to form trading signals, which is a typical trend following strategy. The weighted moving average WMA and the adaptive moving average ALMA are mainly used.
## Strategy Principle
This strategy first calculates the short- and medium-term moving averages ma1 and ma2 of the price, where the ma1 period is shorter and the ma2 period is longer. Then calculate the difference ma3 between ma1 and ma2, and then calculate the smoothed moving average ma4 for ma3. When MA3 crosses above MA4, a buy signal is generated, and when MA3 crosses below, a sell signal is generated.
In this way, ma3 reflects the short- and medium-term trend direction of the price, and ma4 filters out some of the noise in ma3 to form a more reliable trading signal. The period ratio of ma1 and ma2 is set by the parameter maLen, and users can get the best parameter combination according to different market adjustment cycles.
## Strategic Advantages
This strategy has the following advantages:
1. Using adaptive moving average ALMA and weighted moving average WMA can better adapt to market changes.
2. Apply multi-period price averaging method to make trading signals more reliable.
3. The parameters are adjustable, users can optimize it for different markets, and it has a wide range of applications.
4. The strategic ideas are clear, easy to understand and easy to implement.
5. Can achieve good results in both trending and oscillating markets.
## Risks and Solutions
There are also some risks with this strategy:
1. In violent market changes, the moving average strategy is prone to problems such as unclear trading signals and delays. It can be optimized by adjusting the moving average period and parameters.
2. Pure trend following strategies are prone to losses during the shock and consolidation phase. Can be combined with other indicators as filter conditions.
3. Improper parameter settings may lead to excessive trading in ultra-short cycles. Appropriate parameters should be chosen carefully.
## Strategy optimization
This strategy can be optimized from the following aspects:
1. Test more types of moving averages, such as linear moving averages, weighted moving averages, etc.
2. Add a stop-loss mechanism based on indicators such as volatility and price channels.
3. Combined with multiple time period analysis, adopt rolling optimization parameters.
4. Add machine learning algorithms to realize automatic optimization of parameters.
## Summarize
This strategy forms a trading signal based on the golden cross of the moving average. Apply adaptive moving averages and multi-time period price averages to make signals more accurate and reliable. This strategy has adjustable parameters, wide application, simple and clear ideas, good results in trending markets, and high practical value.
||

## Overview

This strategy generates trading signals based on the golden cross and dead cross of moving averages with different cycles. It belongs to a typical trend-following strategy. Weighted Moving Average (WMA) and Adaptive Moving Average (ALMA) are mainly used.

## Strategy Logic  

The strategy first calculates the medium-term and short-term moving averages, ma1 and ma2, of the price, where ma1 has a shorter cycle and ma2 has a longer cycle. Then it calculates the difference between ma1 and ma2 as ma3, and further computes the smoothed moving average ma4 of ma3. When ma3 crosses over ma4 upwards, a buy signal is generated. When it crosses downwards, a sell signal is generated.

Thus, ma3 reflects the medium-term trend of the price, and ma4 filters some noise from ma3 to form a more reliable trading signal. The cycles of ma1 and ma2 are set by the parameter maLen. Users can optimize parameters to achieve the best setting for different markets.

## Advantages

The advantages of this strategy include:

1. Using ALMA and WMA that can better adapt to market changes.
2. Applying multi-cycle price averaging to make trading signals more reliable. 
3. The adjustable parameters can be optimized for different markets with wide applicability.
4. The strategy logic is simple and easy to implement.  
5. It can achieve good performance in both trending and sideways markets.

## Risks and Solutions

There are also some risks for this strategy:

1. The signals may become unclear and delayed for volatile market conditions. This can be solved by optimizing the cycles and parameters of the moving averages.
2. As a pure trend-following strategy, it may lead to losses during range-bound markets. Other indicators can be added as filters.  
3. Improper parameter settings may cause over-trading due to ultra short cycles. Appropriate parameters should be carefully selected.

## Optimization

The strategy can be optimized from the following aspects:

1. Test more types of moving averages, like LMA, WMA, etc.
2. Add stop loss mechanisms based on volatility, price channels, etc. 
3. Adopt multi-timeframe analysis with rolling optimization of parameters.
4. Increase machine learning algorithms for automatic parameter optimization.

## Conclusion  

The strategy generates trading signals based on the golden cross and dead cross of moving averages. By using ALMA and multi-cycle price averaging, the signals become more precise and reliable. The adjustable parameters make it widely applicable. Also, the logic is simple and clear and performs well in trending markets. Therefore, it has high practical value.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|30|ma period|
|v_input_2|0|mode: wma|ema|alma|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-08 00:00:00
end: 2024-01-15 00:00:00
period: 10m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Oracle Move Strategy", overlay=true)

maLen = input(30, "ma period")
mode =  input(defval="wma", options=["alma", "ema", "wma"])
price = close

ma(src, len) =>
     mode=="alma"  ? alma(src, len, 0.85, 6) :
     mode=="ema"? ema(src, len) : 
     wma(src, len)
    

ma1 = ma(price, floor(maLen / 2))
ma2 = ma(price, maLen)
ma3 = 2.0 * ma1 - ma2
ma4 = ma(ma3, floor(sqrt(maLen)))

//plot(ma1, color = red)
//plot(ma2, color = green)
plot(ma3, color = blue)
plot(ma4, color = orange)


mafast = ma3
maslow = ma4

if (crossover(mafast, maslow))
    strategy.entry("MA2CrossLE", strategy.long, comment="MA2CrossLE")

if (crossunder(mafast, maslow))
    strategy.entry("MA2CrossSE", strategy.short, comment="MA2CrossSE")

//plot(strategy.equity, title="equity", color=red, linewidth=2, style=areabr)
```

> Detail

https://www.fmz.com/strategy/438975

> Last Modified

2024-01-16 17:37:13
