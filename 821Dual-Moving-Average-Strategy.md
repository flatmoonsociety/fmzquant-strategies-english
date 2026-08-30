
> Name

8-period and 21-period moving average strategy Dual-Moving-Average-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/100b186d80b89b8f627.png)
 [trans]

## Overview
This strategy uses dual moving averages, an 8-period and a 21-period moving average. When the short-term moving average crosses the long-term moving average, go long; when the short-term moving average crosses below the long-term moving average, go short.
This strategy also introduces the slope indicator of the moving average to filter out some trendless intervals and only generate trading signals when the trend is obvious.
## Strategy Principle
The core of this strategy lies in the intersection of the short-term moving average and the long-term moving average. Short-term moving averages can capture price changes faster, while long-term moving averages have a better filtering effect on noise. When the short-term line crosses the long-term line, it shows that the bull trend has been established, and you can make profits by going long; when the short-term line crosses below the long-term line, it shows that the short trend has been established, and you can make profits by going short.
This strategy also sets a slope threshold. A long signal is generated only when the slope is greater than the positive threshold, and a short signal is generated only when the slope is less than the negative threshold. This can filter out some intervals with no obvious trend and make the quality of trading signals higher.
Specifically, the trading signal generation logic of this strategy is:
1. Calculate 8-period and 21-period simple moving averages
2. Detect the cross signals between the two
3. Calculate the slope of the 21-period moving average. The slope is calculated by the arctangent function atan.
4. Only when the slope exceeds the set positive threshold, a long signal is generated
5. Only when the slope is lower than the set negative threshold, a short signal is generated
## Advantage Analysis
This strategy has the following advantages:
1. The strategy is simple, easy to understand and implement
2. Introducing the slope indicator can filter out intervals with no obvious trend and improve signal quality.
3. Using double moving averages can give full play to their respective advantages and improve stability.
4. Parameters can be adjusted according to the market to adapt to different trading varieties
5. The program implementation is simple and convenient for secondary development and optimization.
## Risks and Solutions
There are also some risks with this strategy:
1. The market has a range of violent fluctuations, and many false signals may appear.
2. Double-line crossing itself may generate more false alarm signals
3. There is a certain degree of lag and it is impossible to immediately catch the trend turning point
In response to these risks, optimization can be carried out from the following aspects:
1. Adjust the parameters of the moving average to adapt to market characteristics
2. Optimize the slope threshold and improve the robustness of parameters
3. Add a stop-loss mechanism to control single losses
4. Combine with other indicators for filtering to improve signal quality
5. Use adaptive parameter settings to make the strategy more robust
## Optimization direction
This strategy can also be optimized from the following directions:
1. Use adaptive moving averages to adjust parameters according to market fluctuations
2. Increase correlation analysis of trading volume to avoid generating false signals during consolidation
3. Combine with volatility indicators to enhance the quality and timeliness of signals
4. Add machine learning algorithms to realize automatic optimization of parameters
5. Combine with deep learning technology to explore more complex non-linear price models
## Summarize
This double moving average strategy is generally simple and practical. It captures different trend characteristics through the parameters of two periods of diffs and fuses them together to generate trading signals. At the same time, the introduction of slope threshold improves the signal quality. This strategy can be used as a basic strategy and expanded, and there is still a lot of room for optimization and expansion capabilities.
||

## Overview

This strategy employs dual moving averages, specifically 8-period and 21-period ones. It generates long signals when the shorter MA crosses over the longer one, and short signals when the shorter MA crosses below the longer one.  

The strategy also incorporates the slope of the moving average line to filter out some non-trending periods and only produce signals when a trend is more apparent.

## Principles

The core of this strategy lies in the crossover of the short-term and long-term moving averages. The shorter MA can capture trend changes faster, while the longer MA has better noise filtering effects. The establishment of an uptrend is suggested when the shorter MA crosses over the longer MA, leading to a long signal; the establishment of a downtrend is suggested when the shorter MA crosses below the longer MA, leading to a short signal.

The strategy also sets a slope threshold. Only when the slope is greater than the positive threshold value will a long signal be generated. Only when the slope is less than the negative threshold value will a short signal be generated. This helps filter out zones where no pronounced trend exists, resulting in trading signals of higher quality. 

Specifically, the logic for generating trading signals is:

1. Calculate the 8-period and 21-period simple moving averages  
2. Detect crossover signals between the two
3. Calculate the slope of the 21-period moving average line using the arctangent function atan
4. Only generate long signals when the slope exceeds a preset positive threshold
5. Only generate short signals when the slope falls below a preset negative threshold

## Advantage Analysis 

The advantages of this strategy include:

1. The strategy idea is simple and easy to understand/implement
2. Incorporating slope index helps filter out non-trending periods and improves signal quality
3. Employing dual moving averages allows both to play to their strengths, improving robustness
4. Parameters can be adjusted to suit different trading instruments  
5. Simple program implementation facilitates further optimization

## Risk Analysis

Some risks also exist with this strategy:  

1. More false signals may occur during violent market fluctuations
2. Crossover itself tends to produce some false signals 
3. There is some degree of lag, unable to instantly capture trend reversals

Some ways to optimize based on these risks:

1. Adjust MA parameters to suit market characteristics
2. Optimize slope threshold to improve robustness
3. Add stop loss mechanisms to control single loss
4. Incorporate other indicators to filter signals 
5. Employ adaptive parameter setting to improve robustness

## Optimization Directions

Some directions for optimizing the strategy:

1. Employ adaptive MAs, adjusting parameters based on volatility
2. Incorporate volume analysis to avoid errors during consolidation
3. Add volatility index to enhance quality and timeliness 
4. Add machine learning for automatic parameter optimization
5. Leverage deep learning to uncover more complex nonlinear patterns

## Conclusion

In summary, this dual MA strategy is simple and practical. By capturing different trend characteristics through the two period parameters and combining them to generate trading signals. Meanwhile, incorporating the slope threshold improves signal quality. This strategy can serve as a basic one for extensions, with ample optimization space and potential.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|7|Angle|
|v_input_2|2|Angle Period|
|v_input_3|10|ATR Period|
|v_input_4|6|Angle Level|
|v_input_5_close|0|MA Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-09 00:00:00
end: 2024-01-16 00:00:00
period: 10m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//written by sixpathssenin
//@version=4
strategy(title="Dual Moving Average",initial_capital=10000,overlay=true)

ma1= sma(close,8)
ma2= sma(close,21)

angleCriteria = input(title="Angle", type=input.integer, defval=7, minval=1, maxval=13)

i_lookback   = input(2,     "Angle Period", input.integer, minval = 1)
i_atrPeriod  = input(10,    "ATR Period",   input.integer, minval = 1)
i_angleLevel = input(6,     "Angle Level",  input.integer, minval = 1)
i_maSource   = input(close, "MA Source",    input.source)

f_angle(_src, _lookback, _atrPeriod) =>
    rad2degree = 180 / 3.141592653589793238462643  //pi 
    ang = rad2degree * atan((_src[0] - _src[_lookback]) / atr(_atrPeriod)/_lookback)
    ang
_angle = f_angle(ma2, i_lookback, i_atrPeriod)

plot(ma1,color=#FF0000)
plot(ma2,color=#00FF00)

crosso=crossover(ma1,ma2) 
crossu=crossunder(ma1,ma2)

_lookback = 15

f_somethingHappened(_cond, _lookback) =>
    bool _crossed = false
    for i = 1 to _lookback
        if _cond[i]
            _crossed := true
    _crossed
    
longcrossed = f_somethingHappened(crosso,_lookback)
shortcrossed = f_somethingHappened(crossu,_lookback)

long = longcrossed and _angle > angleCriteria
short= shortcrossed and _angle < -(angleCriteria)


if(long)
    strategy.entry("Long",strategy.long)
if(short)
    strategy.entry("short",strategy.short)
    

```

> Detail

https://www.fmz.com/strategy/439106

> Last Modified

2024-01-17 17:45:45
