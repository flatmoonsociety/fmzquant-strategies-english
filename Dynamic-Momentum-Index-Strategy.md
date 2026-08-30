
> Name

Dynamic-Momentum-Index-Strategy
> Author

ChaoZhang

> Strategy Description


[trans]

## Strategy Principle
This strategy trades based on the Dynamic Oscillator Indicator (DMI). DMI determines trends by calculating the percentage deviation of price from moving averages of different lengths.
The specific transaction logic is:
1. Calculate the percentage deviation of the price from the long-term moving average (such as 200 days) as the 1st DMI
2. Calculate the percentage deviation of the price from the mid-cycle moving average (such as 50 days) as the second DMI
3. Calculate the percentage deviation of the price from the short-term moving average (such as the 20th) as the 3rd DMI
4. When the 3rd DMI is higher than the 1st DMI, it is bearish; when the 3rd DMI is lower than the 2nd DMI, it is bullish.
5. Generate trading signals based on DMI relationships
DMI determines the turning point of market trends by dynamically comparing the relative strengths of different moving average periods. Parameter optimization can be adapted to different cycles.
## Strategic Advantages
- DMI combined with multi-cycle judgment is more comprehensive
- Compare relative strengths and avoid absolute numerical judgments
- Flexible adjustment of cycle parameters to suit the market
## Strategy Risk
- DMI has a certain lag and may miss the turning point
- Need to set cycle parameters carefully
- Multiple invalid signals may be generated
## Summarize
The DMI strategy determines turning points by comparing the strength and weakness of multiple moving average periods. It can adapt to different market environments through parameter optimization. However, hysteresis exists and other indicators need to be assisted for judgment.

||

## Strategy Logic 

This strategy trades based on the Dynamic Momentum Index (DMI). DMI measures the percentage deviation between price and moving averages of different lengths to determine trend.

The trading logic is:

1. Calculate percentage deviation of price from a long MA (e.g. 200-day) as 1st DMI

2. Calculate deviation from a medium MA (e.g. 50-day) as 2nd DMI  

3. Calculate deviation from a short MA (e.g. 20-day) as 3rd DMI

4. When 3rd DMI is higher than 1st DMI, bearish. When 3rd DMI is lower than 2nd DMI, bullish.

5. Trade signals generated based on DMI relationship

By comparing relative strength dynamically across MA periods, DMI aims to identify trend turning points. Parameters can be optimized for different cycles.

## Advantages

- DMI combines multi-period lookback for robustness

- Compares relative strength vs. absolute levels 

- Flexible MA periods for market adaption

## Risks

- DMI has lag and may miss reversals

- Careful optimization of period parameters 

- Prone to multiple false signals

## Summary

DMI judges turning points by comparing multi-MA period strength dynamics. Optimization can suit different market environments. But lag limitations necessitate additional filters.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|200|LengthFirst|
|v_input_2|50|LengthSecond|
|v_input_3|20|LengthThird|
|v_input_4|true|ShowFirst|
|v_input_5|true|ShowSecond|
|v_input_6|true|ShowThird|
|v_input_7|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-14 00:00:00
end: 2023-09-13 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 31/06/2018
// The related article is copyrighted materialfrom Stocks & Commodities Dec 2009
// My strategy modification.
//
// You can change long to short in the Input Settings
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="CMOaDisparity Index Backtest")
LengthFirst = input(200, minval=1)
LengthSecond = input(50, minval=1)
LengthThird = input(20, minval=1)
ShowFirst = input(type=bool, defval=true)
ShowSecond = input(type=bool, defval=true)
ShowThird = input(type=bool, defval=true)
reverse = input(false, title="Trade reverse")
xEMAFirst = ema(close,LengthFirst)
xEMASecond  = ema(close,LengthSecond)
xEMAThird  = ema(close,LengthThird)
xResFirst = 100 * (close - xEMAFirst) / close
xResSecond = 100 * (close - xEMASecond) / close
xResThird = 100 * (close - xEMAThird) / close
pos = iff(xResThird > xResFirst, -1,
       iff(xResThird < xResSecond, 1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue ) 
plot(ShowFirst ? xResFirst : na, color=red, title="DIX 1")
plot(ShowSecond ? xResSecond : na, color=blue, title="DIX 2")
plot(ShowThird ? xResThird : na, color=green, title="DIX 3")
```

> Detail

https://www.fmz.com/strategy/426799

> Last Modified

2023-09-14 16:15:42
