
> Name

Trend-Trading-Strategy-Based-on-Multiple-Moving-Averages
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/12f22b560707cc1cfe5.png)
[trans]

## Overview
This strategy calculates moving averages of multiple different periods and combines the golden cross pattern to determine the trend direction and implement trend following transactions. The main function is to discover turning points in price trends and issue buy and sell signals.
## Strategy Principle
This strategy is based on the 35-period EMA as the main indicator for judging buy and sell. When the price goes above the 35EMA, a buy signal is generated; when the price goes below the 35EMA, a sell signal is generated. In addition, this strategy also draws 8 EMA bands composed of EMAs with different periods to assist in determining the trend direction. The EMA with a lower period is closer to the price and can capture price changes faster; the EMA with a higher period follows price changes more slowly and can filter out some noise. The EMA bands clearly depict the main trend direction of the price.
This strategy mainly relies on the 35EMA to determine the main price trend. A trading signal is generated when the price crosses above or below the 35EMA. The EMA band mainly plays a role in assisting judgment and optimizing entry timing.
## Advantage Analysis
This strategy combines a balance between trend judgment and frequent trading. The 35EMA can basically determine the change of the main trend direction without being too lagging behind. It can basically generate trading signals near the price turning point. The trend channel formed by the EMA band can help determine buying and selling opportunities and optimize the timing of entry.
Compared with single EMA indicator judgment, this strategy can provide a more comprehensive and clear trend judgment. The combination of EMAs of different periods not only ensures the judgment of the direction of the large-cycle trend, but also smooths the impact of some short-cycle market noise through the combination of high- and low-frequency EMAs.
Users can adjust parameters by themselves, change the period of the main trading indicator 35EMA, or the EMA period in the EMA band, and optimize their own trading style. Overall, this strategy provides a relatively accurate and comprehensive trend trading solution.
## Risk Analysis
The main risk of this strategy lies in the user's parameter selection. If the EMA period selected is too short, the trading frequency and trading risk will increase. If the EMA period is too long, the price turning point will be missed and entry into the market will not be possible in time.
Another major risk is that during consolidation, the EMA indicator will produce multiple false signals. At this time, users need assistance in judging the trend direction to avoid blind entry.
The last risk point is that in violent market conditions, indicators will lag behind and fail to issue buy and sell signals in time. At this time, users need to make judgments in advance and cannot completely rely on indicator signals.
## Optimization direction
The main optimization direction of this strategy is to adjust the EMA parameters to adapt to different markets and trader styles. Specifically, you can start from the following aspects:
1. Adjust the cycle parameters of the main trading indicator 35EMA to optimize the timing of obtaining trading signals.
2. Adjust each EMA period parameter in the EMA band to optimize the judgment of the trend.
3. Add other auxiliary indicators for combined judgment, such as BOLL channel, KDJ indicator, etc.
4. Combine with trading volume indicators to avoid entering the market when prices fluctuate violently but trading volume does not increase.
Through parameter adjustment and combination of multiple indicators, the stability of the strategy and the accuracy of signal acquisition can be further improved. Thereby reducing transaction risks and obtaining better returns.
## Summarize
This strategy achieves a relatively accurate and comprehensive trend-following trading plan by calculating multiple EMAs of different periods and supplementing it with EMA band judgment. It not only considers the timeliness of capturing price turning points, but also comprehensively judges the trends at different levels, and strikes a balance between the pursuit of trading frequency and system stability. Through parameter adjustment and optimization, this strategy can adapt to different market environments, asset types and trader styles. It provides users with a relatively mature and powerful basic solution for quantitative trading.
||

## Overview  

This strategy calculates multiple moving averages of different periods and combines golden cross patterns to determine trend direction for trend following trading. The main functionality is to identify price trend reversal points and generate buy and sell signals.

## Strategy Principle   

The core of this strategy is the 35-period EMA which serves as the primary indicator for buy and sell signals. When price crosses above the 35EMA, a buy signal is generated. When price crosses below the 35EMA, a sell signal is generated. In addition, the strategy plots an EMA ribbon consisting of 8 EMAs of different periods to aid in determining trend direction. Shorter period EMAs stay closer to price for detecting changes more rapidly, while longer period EMAs lag price changes more slowly to filter some noise. The EMA ribbon clearly depicts the major trend direction of price.   

This strategy mainly relies on the 35EMA to determine the major trend. Trading signals are generated when price crosses above or below the 35EMA. The EMA ribbon plays an auxiliary role in confirming the trend and optimizing entry timing.  

## Advantage Analysis   

This strategy strikes a balance between trend following and frequent trading. The 35EMA can basically judge changes in the major trend direction without too much lag, and generates trading signals around significant turning points. The EMA ribbon forms a trend channel for confirming opportunities to enter long or short positions with better timing.  

Compared to using a single EMA indicator, this multi-EMA approach provides more comprehensive and clearer trend determination. The combination of different period EMAs ensures judging the longer-term trend direction while smoothing some short-term market noise through integrating high and low frequency EMAs.  

Users can tweak parameters on their own to change the main 35EMA period or the EMAs in the ribbon to optimize for their own trading style. Overall, this strategy offers a relatively accurate and versatile solution for trend trading.  

## Risk Analysis  

The main risk lies in the user's choice of parameters. Using EMA periods that are too short increases trade frequency and risk. Periods that are too long may cause missing major turning points and lag entries.  

Another key risk is during range-bound markets, the EMA indicator can generate multiple false signals. Users need to apply additional trend analysis to avoid blind entries.  

Finally, during strong trending markets, indicator lag may delay buy and sell signals. Users should anticipate turning points instead of purely relying on signals.  

## Optimization Directions  

The main ways to optimize this strategy focus on adjusting EMA parameters to suit different markets and trading styles:  

1. Fine tune the 35EMA period for better timing of trade signals  
2. Adjust EMA ribbon periods for better trend judgment   
3. Incorporate other supporting indicators like BOLL bands and KDJ for confirmation   
4. Add volume measures to avoid acting in volatile markets with no volume increase  

Through parameter tuning and combining signals from multiple indicators, further improvements in stability and signal accuracy can be achieved. This reduces trading risks and achieves better returns.  

## Conclusion   

This strategy provides a relatively accurate and versatile trend following solution through calculating multiple EMAs and using the EMA ribbon. It balances capturing turning points promptly and judging multi-timeframe trends holistically for a good mix of trade frequency and system stability. Through optimization it adapts across market environments, asset types and trading styles. It offers users a sophisticated and robust foundation for quantitative trading.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Show Buy & Sell Strategy|
|v_input_2|true|Show EMA Cross - need to active B&S Strategy|
|v_input_3|35|Length EMA Cross - need to active B&S Strategy|
|v_input_4_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-30 00:00:00
end: 2023-12-06 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//
// @author d3nv3r 
// @inspiration [LazyBear]
// List of all my indicators: https://github.com/d3nv3r0ne/tradingview
//
// Inputs : Show Buy&Sell Signals
// Inputs : Show EMA in White for the Buy&Sell Signals
// Inputs : Choose the length of the EMA for the B&S signals
// 
// How to use it : 
// Any chart
// copy all and paste the content into the Pine Editor Tab at the bottom of the tradingview pannel
// [Save As...] and [Add to Chart] in top-right of the Pine Editor
//
//@version=4
strategy(shorttitle = "35EMA_X_B/S_RIBBON", title="35EMA Cross BuyAndSell Strategy + RIBBON [d3nv3r]", overlay=true)

//
// Variables inputs
//
useBSstrategy = input(true, title="Show Buy & Sell Strategy")
showMABS = input(true, title="Show EMA Cross - need to active B&S Strategy")
lengthBS = input(title="Length EMA Cross - need to active B&S Strategy", type=input.integer, defval=35, minval=1)
src = input(close, title="Source")

//
// Variables
// Ribbon EMA + EMA B/S 
//
lenRib1 = 20
lenRib2 = 25
lenRib3 = 30
lenRib4 = 35
lenRib5 = 40
lenRib6 = 45
lenRib7 = 50
lenRib8 = 55

//
// Variables
// Quadruple SMA + SMA B/S 
//
maBS = ema(src, lengthBS)
rib1 = ema(src, lenRib1)
rib2 = ema(src, lenRib2)
rib3 = ema(src, lenRib3)
rib4 = ema(src, lenRib4)
rib5 = ema(src, lenRib5)
rib6 = ema(src, lenRib6)
rib7 = ema(src, lenRib7)
rib8 = ema(src, lenRib8)

//
// Variables color
//
colorEMAX = #FFFFFF
colorRib1 = #FFFF00
colorRib2 = #FFD700
colorRib3 = #FFC800
colorRib4 = #FFC800
colorRib5 = #FFC800
colorRib6 = #FF4500
colorRib7 = #FF1500
colorRib8 = #FF0000

//
// Variables Buy/Sell
//
longCondition = crossover(close,maBS)
shortCondition = crossunder(close,maBS)

//
// Logic Buy/Sell
//
if (useBSstrategy)
    if (longCondition)
        strategy.entry("Long", strategy.long)
    if (shortCondition)
        strategy.entry("short", strategy.short)

//
// Plot Quadruple SMA + SMA B/S
//
plot(showMABS and maBS ? maBS : na, color=colorEMAX, transp=0, linewidth=2)
plot(rib1, color=colorRib1, transp=15, linewidth=1)
plot(rib2, color=colorRib2, transp=15, linewidth=1)
plot(rib3, color=colorRib3, transp=15, linewidth=1)
plot(rib4, color=colorRib4, transp=15, linewidth=1)
plot(rib5, color=colorRib5, transp=15, linewidth=1)
plot(rib6, color=colorRib6, transp=15, linewidth=1)
plot(rib7, color=colorRib7, transp=15, linewidth=1)
plot(rib8, color=colorRib8, transp=15, linewidth=1)
```

> Detail

https://www.fmz.com/strategy/434525

> Last Modified

2023-12-07 10:50:37
