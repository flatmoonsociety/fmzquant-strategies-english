
> Name

Trend-Trading-Strategy-Based-on-Triple-Hull-Moving-Averages-and-Ichimoku-Kinko-Hyo
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/137e15f95009f0b312e.png)
[trans]

## Overview
This strategy combines two indicators, the Hull Moving Average and the Ichimoku Balance Sheet, to implement a trend following trading system. This system can capture short- and medium-term trends and conduct trend trading.
## Strategy Principle
This strategy uses the Hull Moving Average to determine the price trend direction. The Hull Moving Average is an indicator optimized for the moving average to respond more quickly to price changes. The strategy here uses a triple Hull moving average system, including 6-period, 3-period and 1.5-period Hull MA.
In addition, the strategy also incorporates the transition lines and delay lines of the Ichimoku Balance Sheet. These two indicators reflect the mid- to long-term trend of prices. The strategy combines the Triple Hull MA with the Ichimoku Balance Sheet indicator to form a trading signal.
Specifically, the strategy calculates a triple Hull MA: n1, n2, n2ma. And two indicators of the Ichimoku Balance Sheet: leadLine1 and leadLine2. Then post1 and post2 are calculated as the final trading indicators.
When post1 crosses post2 above, go long; when post1 crosses post2 below, go short. In this way, you can track and capture the short-term and medium-term price trends and conduct trend trading.
## Advantage Analysis
This strategy has the following advantages:
1. Combine dual indicators to improve system stability.
2. Using Hull MA has fast response and can capture trend changes.
3. The Ichimoku Balance Sheet indicator can filter out false breakthroughs.
4. Using multiple Hull MAs, you can effectively track the short-term and medium-term price trends.
5. The strategy logic is simple and clear, easy to understand and optimize.
## Risk Analysis
This strategy also has some risks:
1. In a volatile market, multiple false signals may appear.
2. Improper parameter settings may lead to poor strategy performance.
3. Avoid using this strategy when major news is released.
Countermeasures:
1. Parameters can be adjusted appropriately to filter out some noise.
2. It is recommended to optimize parameters and find the best parameter combination.
3. Avoid trading around the time of major news releases.
## Optimization direction
This strategy can also be optimized from the following aspects:
1. Try Hull MA combinations with different length periods.
2. Test the indicators that increase or decrease the Ichimoku Balance Sheet.
3. Smoothly optimize the trading indicators post1 and post2.
4. Add stop loss logic to control single loss.
## Summarize
This strategy comprehensively uses Hull MA and Ichimoku Balance Sheet indicators to build a simple and practical trend following trading system. The strategy responds quickly and can effectively capture short- and medium-term price trends. This system deserves further testing and optimization, and better trading performance can be achieved by adjusting parameters and adding other filtering indicators.
||

## Overview

This strategy combines the Hull Moving Average and Ichimoku Kinko Hyo indicators to implement a trend-following trading system. The system can capture medium-term trends for trend trading.  

## Strategy Logic

This strategy uses the Hull Moving Average to determine the direction of the price trend. The Hull MA is an optimized version of the moving average that can respond more quickly to price changes. The strategy here employs a triple Hull MA system, containing 6-period, 3-period and 1.5-period Hull MAs.

In addition, the strategy also incorporates the Ichimoku Kinko Hyo conversion and lagging span lines. These two indicators reflect the medium to long term trend of the prices. The strategy combines the triple Hull MA and Ichimoku indicators to generate trading signals. 

Specifically, the strategy calculates the triple Hull MA: n1, n2, n2ma. As well as two Ichimoku indicators: leadLine1 and leadLine2. It then computes post1 and post2 as the final trading metrics.

When post1 crosses over post2 upward, go long. When post1 crosses below post2, go short. This allows us to track and capture price medium-term trends for trend trading.

## Advantage Analysis  

The advantages of this strategy include:

1. Combining dual indicators improves system stability.
2. Hull MA responds fast and can capture trend changes.  
3. Ichimoku filters out false breakouts.
4. The multiple Hull MAs can effectively track medium-term price trends.
5. The strategy logic is simple and easy to understand and optimize.

## Risk Analysis

There are also some risks with this strategy:

1. It may generate multiple false signals during ranging markets.  
2. Inadequate parameter settings can lead to poor performance.
3. Avoid using this strategy around major news events.

Countermeasures:

1. Adjust parameters to filter out noise.
2. Optimize parameters to find the best combination.  
3. Avoid trading around significant news releases.

## Optimization Directions

This strategy can also be improved in the following aspects:

1. Test Hull MA combinations of different lengths.
2. Add or reduce Ichimoku indicators.  
3. Smooth optimizations for trading metrics post1 and post2. 
4. Incorporate stop loss to limit per trade loss.

## Conclusion

This strategy combines the Hull MA and Ichimoku Kinko Hyo indicators to build a simple and practical trend following system. With fast responses, it can effectively capture medium-term price trends. Further testing and optimization, through parameter tuning and adding filters, can lead to better trading performance.
[/trans]]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|6|Hull MA period|
|v_input_2|9|Conversion Line Periods|
|v_input_3|26|Base Line Periods|
|v_input_4|52|Lagging Span 2 Periods|
|v_input_5|26|Displacement|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-17 00:00:00
end: 2023-12-24 00:00:00
period: 30m
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
//                                                HULL & ICHIMOKU & MATHS
strategy("3 HULLs & ICHIMOKU divided by PRICE", shorttitle="3H&I/P", overlay=true, default_qty_type=strategy.percent_of_equity, max_bars_back=720, default_qty_value=100, calc_on_order_fills=true, calc_on_every_tick=true, pyramiding=0)
keh=input(title="Hull MA period",defval=6)
p=ohlc4[1]
n2ma=2*wma(p,round(keh/2))
nma=wma(p,keh)
diff=n2ma-nma
sqn=round(sqrt(keh))
n2ma1=2*wma(p[1],round(keh/2))
nma1=wma(p[1],keh)
diff1=n2ma1-nma1
sqn1=round(sqrt(keh))
n1=wma(diff,sqn)
n2=wma(diff1,sqn)
conversionPeriods = input(9, minval=1, title="Conversion Line Periods")
basePeriods = input(26, minval=1, title="Base Line Periods")
laggingSpan2Periods = input(52, minval=1, title="Lagging Span 2 Periods")
displacement = input(26, minval=1, title="Displacement")
donchian(len) => avg(lowest(len), highest(len))
conversionLine = donchian(conversionPeriods)
baseLine = donchian(basePeriods)
leadLine1 = avg(conversionLine, baseLine)
leadLine2 = donchian(laggingSpan2Periods)
post1=((n1[1]*3)+leadLine1)/p
post2=((n2[1]*3)+leadLine2)/p
if (post1<post2)
    strategy.entry("buy", strategy.long, comment="BUY")
if (post1>post2)
    strategy.entry("sell", strategy.short, comment="SELL")
```

> Detail

https://www.fmz.com/strategy/436509

> Last Modified

2023-12-25 13:40:10
