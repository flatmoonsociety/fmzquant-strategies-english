
> Name

Heiken-Ashi-and-Ichimoku-Kinko-Hyo-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy uses a combination of the Sea, Air and Ichimoku indicators to determine trend direction and follow the trend. Sea and air smooth K-line data reduces noise. The Ichimoku Balance Sheet comprehensively determines the strength of the trend through various signals such as conversion lines and baselines. Combined with dual indicators to improve strategy stability.
## Strategy Principle
Calculate the closing prices of sea and air, and draw conversion lines, baselines and other Ichimoku Balance Sheet indicators. Go long when the closing price is higher than the previous two days and above the upper edge of the cloud chart and the delay line. Go short when the closing price is lower than the previous two days and below the lower edge of the cloud chart and the delay line. The intersection of the conversion line and the base line of the Ichimoku Balance Meter also serves as an auxiliary signal.
## Advantage Analysis
- Filter false breakthroughs from air and sea to improve signal quality
- Multiple indicator signals of Ichimoku balance mutually verify each other
- Delay line to avoid being trapped and ensure profit taking
- Follow the trend, hold positions for a long time, and have large profit potential
## Risk Analysis
- The smoothness of sea and air indicators cannot be perfectly optimized
- Ichimoku parameter settings have a significant impact on the results
- If you hold a position for too long, your losses may expand.
- The transaction frequency is low, not suitable for short-term trading
Smoothing parameters can be appropriately adjusted, position holding periods can be shortened, Ichimoku balance table parameters can be optimized, etc. to control risks.
## Optimization direction
- Test different sea and air smoothing parameters
- Optimize the period parameters of the Ichimoku Balance Table
- Set up re-entry strategy after exit
- Test parameter robustness in different varieties
## Summarize
This strategy combines multiple indicators to determine the trend direction and has strong retracement control capabilities. The effect can be further improved by adjusting parameters and other methods.
||

## Overview

This strategy combines Heiken Ashi and Ichimoku Kinko Hyo indicators to determine trend direction and follow the trend. Heiken Ashi smoothing reduces noise. Ichimoku uses multiple signals like conversion and base lines to assess trend strength. The combination improves strategy stability.

## Strategy Logic

Calculate Heiken Ashi close price and plot Ichimoku indicators like conversion line, base line etc. Go long when close is higher than previous two days and above Ichimoku top edge and lagging line. Go short when close is lower than previous two days and below Ichimoku bottom edge and lagging line. Conversion and base line crosses also provide secondary signals.

## Advantages 

- Heiken Ashi filters false breakouts improving signal quality
- Ichimoku uses multiple validating signals 
- Lagging line avoids whipsaws ensuring profit taking 
- Following the trend leads to longer holding and bigger profits

## Risks

- Heiken Ashi smoothing cannot be perfectly optimized
- Ichimoku parameters significantly impact results
- Long holding risks increasing losses
- Lower trade frequency unsuitable for short term

Risks can be controlled by adjusting smoothness, holding period, optimizing Ichimoku parameters etc.

## Enhancements

- Test different Heiken Ashi smoothing parameters
- Optimize Ichimoku period parameters
- Strategize re-entry rules after exit
- Test robustness across different products  

## Conclusion

This strategy comprehensively uses multiple indicators to determine trend direction with controlled drawdowns. Performance can be further improved via tuning parameters etc.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|9|Tenkan Sen Periods|
|v_input_2|24|Kijun Sen Periods|
|v_input_3|51|Senkou Span B Periods|
|v_input_4|24|Displacement|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-18 00:00:00
end: 2023-09-17 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3

strategy("Heiken Ashi + Ichimoku Kinko Hyo Strategy", shorttitle="HaI", overlay=true, default_qty_type=strategy.percent_of_equity, max_bars_back=1000, default_qty_value=100, calc_on_order_fills= true, calc_on_every_tick=true, pyramiding=0)

hahigh = security(heikinashi(syminfo.tickerid), timeframe.period, high)
halow = security(heikinashi(syminfo.tickerid), timeframe.period, low)

TenkanSenPeriods = input(9, minval=1, title="Tenkan Sen Periods")
KijunSenPeriods = input(24, minval=1, title="Kijun Sen Periods")
SenkouSpanBPeriods = input(51, minval=1, title="Senkou Span B Periods")
displacement = input(24, minval=1, title="Displacement")
donchian(len) => avg(lowest(len), highest(len))
TenkanSen = donchian(TenkanSenPeriods)
KijunSen = donchian(KijunSenPeriods)
SenkouSpanA = avg(TenkanSen, KijunSen)
SenkouSpanB = donchian(SenkouSpanBPeriods)
SenkouSpanH = max(SenkouSpanA[displacement - 1], SenkouSpanB[displacement - 1])
SenkouSpanL = min(SenkouSpanA[displacement - 1], SenkouSpanB[displacement - 1])
ChikouSpan = close[displacement-1]

plot(TenkanSen, color=blue, title="Tenkan Sen", linewidth = 2)
plot(KijunSen, color=maroon, title="Kijun Sen", linewidth = 3)
plot(close, offset = -displacement, color=orange, title="Chikou Span", linewidth = 2)
sa=plot (SenkouSpanA, offset = displacement, color=green,  title="Senkou Span A", linewidth = 2)
sb=plot (SenkouSpanB, offset = displacement, color=red,  title="Senkou Span B", linewidth = 3)
fill(sa, sb, color = SenkouSpanA > SenkouSpanB ? green : red)

longCondition = hahigh > max(hahigh[1],hahigh[2]) and close>ChikouSpan and close>SenkouSpanH and (TenkanSen>=KijunSen or close>KijunSen)
if (longCondition)
    strategy.entry("Long",strategy.long)

shortCondition = halow < min(halow[1],halow[2]) and close<ChikouSpan and close<SenkouSpanL and (TenkanSen<=KijunSen or close<KijunSen)
if (shortCondition)
    strategy.entry("Short",strategy.short)

closelong = halow < min(halow[1],halow[2]) and (TenkanSen<KijunSen or close<TenkanSen or close<KijunSen or close<SenkouSpanH or close<ChikouSpan)
if (closelong)
    strategy.close("Long")

closeshort = hahigh > max(hahigh[1],hahigh[2]) and (TenkanSen>KijunSen or close>TenkanSen or close>KijunSen or close>SenkouSpanL or close>ChikouSpan)
if (closeshort)
    strategy.close("Short")
```

> Detail

https://www.fmz.com/strategy/427137

> Last Modified

2023-09-18 15:13:35
