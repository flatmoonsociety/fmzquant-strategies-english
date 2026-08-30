
> Name

SAR Alternating Timeframe Trading StrategySAR-Alternating-Timeframe-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/12bcc0884d447e70b37.png)
 [trans]

## Overview
This strategy is a trading strategy based on alternate operations of the SAR indicator in different time periods. The strategy will calculate the SAR indicator in the 15-minute, daily, weekly and monthly time frames respectively, and conduct trading operations in the weekly time frame. Go long when the weekly SAR indicator crosses the highest price, and go short when it crosses the lowest price.
## Strategy Principle
### SAR indicator calculation
The SAR indicator stands for Parabolic SAR, which determines the trend direction of the market by calculating the relationship between current price and historical price. When the price breaks through the SAR point, it indicates a trend reversal.
This strategy calculates SAR values ​​under the 15-minute, daily, weekly and monthly time frames. The calculation formula is:
```
SAR = SAR前值 + 加速因子(最高价 - SAR前值) # 多头趋势
SAR = SAR前值 + 加速因子(最低价 - SAR前值) # 空头趋势
```

Among them, the initial value of the acceleration factor is set to 0.02, which will gradually increase to a maximum of 0.2 as the trend continues.
### Trading Strategy
The strategy issues trading signals on the weekly time frame. When the weekly SAR crosses the highest price, go long and set the stop loss to the SAR value. When the SAR falls below the lowest price, go short and set the stop loss to the SAR value.
This strategy determines the trend in a higher-level time frame and sets a more precise stop loss position to make profits more efficiently.
## Advantage Analysis
- Use SAR to determine trend reversal points and accurately locate entry points
- Operate in advanced time frames and follow the general trend
- The stop loss point is close to the SAR, effectively controlling risks
## Risks and Solutions
- The SAR indicator has a lag and may reverse after exceeding the stop loss point. The solution is to appropriately relax the stop loss distance.
- When the trend is huge, the accelerating FACTOR of SAR will gradually amplify, and a large-volume breakthrough may appear. The solution is to limit the FACTOR maximum value.
- In the advanced time frame, if the cycle is too long, the retracement time will be long. Risks can be avoided by reducing positions.
## Optimization ideas
- Optimize entry conditions, such as filtering signals in combination with other indicators
- Optimize stop loss strategies, such as trailing stop loss, range stop loss, etc.
- Optimize position management, such as fixed shares, dynamic adjustments, etc.
- Operate on higher-level time frames, such as quarterly lines and annual lines
- Combined with machine learning algorithm to dynamically optimize parameters
## Summarize
The overall idea of ​​this strategy is clear. By judging the trend in a high time frame, it can effectively follow the general direction. At the same time, the SAR indicator can more accurately locate the turning point of the trend, and also control the stop loss risk to a small level. Subsequent optimization can be carried out from aspects such as entry conditions, stop loss strategies, and position management to make the strategy more stable and efficient.
||

## Overview 

This strategy is based on the alternating operations of the SAR indicator across different timeframes. The strategy calculates the SAR indicator in 15-minute, daily, weekly and monthly timeframes, and trades in the weekly timeframe. It goes long when the weekly SAR crosses above the highest price and goes short when crossing below the lowest price.  

## Principles

### SAR Indicator Calculation

The Parabolic SAR (SAR) indicator represents parabolic SAR, which judges the trend direction by calculating the relationship between the current price and historical prices. When the price breaks through the SAR point, it indicates a trend reversal.

This strategy calculates SAR values in 15-minute, daily, weekly and monthly timeframes, respectively. The formula is:  

```
SAR = Previous SAR + Acceleration Factor * (Highest Price - Previous SAR) # Uptrend 
SAR = Previous SAR + Acceleration Factor * (Lowest Price - Previous SAR) # Downtrend
```

The initial acceleration factor is set at 0.02, and will gradually increase up to a maximum of 0.2 as the trend extends.  

### Trading Strategy 

The strategy generates trading signals in the weekly timeframe. It goes long when the weekly SAR crosses above the highest price, with SAR value as the stop loss. It goes short when SAR crosses below the lowest price, with SAR as the stop loss.  

By determining the trend on a higher timeframe and setting a more precise stop loss level, the strategy aims to profit more efficiently.  

## Advantages

- SAR indicator accurately locates trend reversal points for entering the market
- Trading in higher timeframes follows the major trend 
- Stop loss stuck to SAR effectively controls risks

## Risks & Solutions

- SAR lag may cause trend to reverse after hitting stop loss. Solution is to allow wider stop loss distance.  
- Acceleration factor may expand dramatically on huge trends, causing stop loss to be penetrated. Solution is to limit maximum factor size.
- Long drawdown periods during long cycles on higher timeframes. Solution is to reduce position sizes.

## Improvement Areas

- Optimize entry conditions, e.g. combine with other indicators  
- Enhance stop loss mechanisms, e.g. trailing stop loss, zone stop loss
- Refine position sizing rules, e.g. fixed fractional, dynamic adjustment
- Operate on even higher timeframes, e.g. quarterly, annually
- Dynamically optimize parameters via machine learning

## Conclusion  

The strategy has clear logic of riding trends on higher timeframes using SAR indicator to locate reversals and set stop loss. Entry signals and risk management could be further improved. With optimizations in areas like entries, stops and position sizing, it can become more stable and profitable.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|15|Resolution|
|v_input_2|D|Resolution|
|v_input_3|W|Resolution|
|v_input_4|M|Resolution|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-09 00:00:00
end: 2024-01-15 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy ("SAR alternating timeframe", overlay=true)

//resolution
res1=input("15", title="Resolution")
res2=input("D", title="Resolution")
res3=input("W", title="Resolution")
res4=input("M", title="Resolution")

//output functions
out = sar(0.02,0.02,0.2)

// request.security
SAR1 = request.security(syminfo.tickerid, res1, out)
SAR2 = request.security(syminfo.tickerid, res2, out)
SAR3 = request.security(syminfo.tickerid, res3, out)
SAR4 = request.security(syminfo.tickerid, res4, out)

//Plots
//plot(SAR1 , title="SAR 15", color = red, linewidth = 2)
//plot(SAR2 , title="SAR D", color = green, linewidth = 3)
plot(SAR3 , title="SAR W", color =blue, linewidth = 4)
//plot(SAR4 , title="SAR W", color =purple, linewidth = 5))


/////////////////////////////////////////////////////////////////////
//trade
if (SAR3 >= high)
    strategy.entry("ParLE", strategy.long, stop=SAR3, comment="ParLE")
else
    strategy.cancel("ParLE")

if (SAR3 <= low)
    strategy.entry("ParSE", strategy.short, stop=SAR3, comment="ParSE")
else
    strategy.cancel("ParSE")


```

> Detail

https://www.fmz.com/strategy/438932

> Last Modified

2024-01-16 14:18:20
