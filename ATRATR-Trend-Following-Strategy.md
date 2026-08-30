
> Name

ATR Trend Following Strategy ATR-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy uses average true range (ATR) to capture price trends, and uses ATR to set stop loss levels to achieve trend tracking.
## Strategy Principle
1. Calculate the ATR value.
2. Determine the stop loss level based on the ATR value.
3. When the price breaks through the stop loss line, go long or short.
4. Lock in profits by dynamically adjusting stop loss levels.
## Strategic Advantages
- Use ATR to automatically adjust stop loss without manual intervention
- The strategy is simple, intuitive and easy to implement
- Avoid being trapped and stop losses in time
- Can take advantage of trends to make profits
- Trading frequency can be controlled by adjusting ATR parameters
## Strategy Risk
- Improper setting of ATR parameters may result in too loose or tight
- Inability to effectively identify the end of a trend
- There is a certain time lag
- May lose some profits due to reversal
## Optimization direction
- Optimize ATR cycle parameters
- Test different ATR multiples as stop loss distances
- Combine with other indicators to identify trend reversals
- Try machine learning parameter optimization
- Consider additional take-profit strategies
## Summarize
This strategy uses ATR to effectively capture the trend and dynamically adjust the stop loss to lock in profits. Optimizing parameter settings can improve strategy performance. However, the ATR lag problem cannot be completely avoided. Overall, this strategy is a simple and practical trend following solution.
|| 

## Overview

This strategy uses Average True Range (ATR) to capture price trends and sets stops based on ATR for trend following.

## How it Works

1. Calculate ATR value. 

2. Determine stop loss level based on ATR.

3. Enter long/short when price breaks stop level.  

4. Lock in profits by adjusting stops dynamically.

## Advantages

- ATR automatically adjusts stops, no manual intervention needed
- Simple and intuitive logic, easy to implement
- Helps avoid being trapped, timely stop loss
- Profits from riding trends  
- Trade frequency controlled via ATR parameters

## Risks

- Poor ATR parameters can cause stops to be too Loose or Tight
- Unable to effectively identify trend end  
- Some time lag exists
- Reversals may cut profits

## Optimization Directions 

- Optimize ATR period parameter
- Test different ATR multiples for stop distance
- Add filters to detect trend reversal
- Explore machine learning for parameter optimization
- Consider additional profit taking mechanisms

## Conclusion

The strategy effectively catches trends using ATR and locks in profits with dynamic stops. Fine tuning parameters can improve performance. But ATR lag cannot be completely eliminated. Overall a simple and practical trend following solution.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|5|nATRPeriod|
|v_input_2|3.5|nATRMultip|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-14 00:00:00
end: 2023-09-20 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

strategy(title="ATR Strategy", overlay = true,  commission_type=strategy.commission.percent,commission_value=0.075)
//credits to HPotter for the orginal code
nATRPeriod = input(5)
nATRMultip = input(3.5)
xATR = ta.atr(nATRPeriod)
nLoss = nATRMultip * xATR
xATRTrailingStop = iff(close > nz(xATRTrailingStop[1], 0) and close[1] > nz(xATRTrailingStop[1], 0), math.max(nz(xATRTrailingStop[1]), close - nLoss),
                    iff(close < nz(xATRTrailingStop[1], 0) and close[1] < nz(xATRTrailingStop[1], 0), math.min(nz(xATRTrailingStop[1]), close + nLoss), 
                        iff(close > nz(xATRTrailingStop[1], 0), close - nLoss, close + nLoss)))
pos =	iff(close[1] < nz(xATRTrailingStop[1], 0) and close > nz(xATRTrailingStop[1], 0), 1,
	    iff(close[1] > nz(xATRTrailingStop[1], 0) and close < nz(xATRTrailingStop[1], 0), -1, nz(pos[1], 0))) 
color = pos == -1 ? color.red: pos == 1 ? color.green : color.blue 
plot(xATRTrailingStop, color=color, title="ATR Trailing Stop")

barbuy = close > xATRTrailingStop 
barsell = close < xATRTrailingStop 

strategy.entry("Long", strategy.long, when = barbuy) 
strategy.entry("Short", strategy.short, when = barsell) 

barcolor(barbuy? color.green:color.red)


```

> Detail

https://www.fmz.com/strategy/427470

> Last Modified

2023-09-21 15:13:47
