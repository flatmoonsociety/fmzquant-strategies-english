
> Name

Dual-Moving-Average-Crossover-and-Bull-Bear-Power-Balance-Combination-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/b045e4b81279b20a43.png)
[trans] 

## Overview
This strategy first uses the 2-period and 20-period exponential moving averages to construct a double moving average indicator to determine whether the price breaks through the moving average as a basic judgment for entering the market. At the same time, the auxiliary judgment indicator "long-short power balance indicator" further identifies the relative power of longs and shorts and filters out misoperations. The two indicators are combined to form the final trading signal.
## Strategy Principle
1. 2/20 moving average indicator
    - Calculate 2-period and 20-period exponential moving averages (EMA)
    - Send a trading signal when the closing price breaks from one side of the moving average to the other
    - Breaking through the 20 moving average is a signal to confirm the trend
    - Breaking through the 2 moving average is a signal to determine the specific entry point
2. Long and short power balance indicator
    - Calculate the long power value and short power value separately
    - Compare the size of the two to get the relative strength of the long and short forces
    - Strong direction serves as an auxiliary judgment for market entry
3. Comprehensive judgment of two indicators
    - Double moving average indicator determines the direction of the general trend
    - Long and short power balance indicator for local area judgment
    - When the two judgment results are consistent, a trading signal is issued
## Advantage Analysis
The biggest advantage of this combination strategy is to combine indicators of different varieties to achieve more reliable trading judgments. Specifically, it has the following advantages:
1. Use the double moving average to determine the general direction and avoid being deceived by local fluctuations.
2. Use the long-short power balance indicator to judge local areas and accurately grasp the specific entry point.
3. The two indicators verify each other, which can filter out certain misoperations and reduce transaction risks.
4. Parameter settings are flexible and can be optimized for different market varieties.
5. The strategic ideas are simple and clear, easy to understand and facilitate later optimization.
## Risk Analysis
There are also some risks that need to be noted in this strategy:
1. The lag in the signal sent by the indicator may lead to the stop loss point being too deep
2. The double moving average indicator is sensitive to parameter settings.
3. The long-short balance indicator is slightly less accurate in judging short-term market conditions.
4. Under special market conditions (common false signals of breakthroughs), the two indicators may have deviations in judgment.
Countermeasures:
1. Appropriately shorten the position period, or set an appropriate trailing stop loss
2. Test different parameter combinations and find the optimal parameters
3. Refer to other indicators for confirmation.
4. Optimize parameters according to variety characteristics
## Optimization direction
This strategy can be optimized in the following aspects:
1. Test more moving average indicator parameter combinations
2. Add stop loss strategy and control single stop loss
3. Combined with volatility indicators to improve parameter adaptive capabilities
4. Add machine learning models to achieve dynamic parameter optimization
5. Try different trend-following indicators to replace the long-short balance indicator
6. Develop a visual interface to facilitate users to test different parameters
## Summarize
This strategy uses the double moving average indicator to determine the general trend, and uses the long-short power balance indicator to assist in determining the entry opportunity. The two indicators verify each other and can effectively reduce the probability of misoperation. The selection of strategy parameters is flexible and can be optimized and adjusted for different varieties. Overall, the strategy is relatively simple and practical, and is worth learning and using by investors. Through further optimization in the future, the effect of the strategy can be further improved.
||

## Overview

This strategy first uses the dual moving average lines of 2-period and 20-period EMA to determine if price breaks through the moving averages, as a basic criterion for entering the market. At the same time, the auxiliary indicator "Bull Bear Power Balance Indicator" further identifies the relative power between bulls and bears to avoid mis-operations. The two types of indicators jointly generate the final trading signal.

## Strategy Principle

1. Dual Moving Average Indicator 
    - Calculate 2-period and 20-period Exponential Moving Average (EMA) 
    - Generate trading signals when closing price breaks through from one side of the moving averages to the other
    - Breaking through 20-EMA determines the trend direction  
    - Breaking through 2-EMA determines specific entry point

2. Bull Bear Power Balance Indicator
    - Separately calculate bull power value and bear power value
    - Compare the two values to determine relative strength between bulls and bears
    - The stronger direction serves as an auxiliary judgment for entry

3. Combined judgment of the two indicators
    - Dual moving average indicator judges major trend direction 
    - Bull bear power balance indicator makes local regional judgment
    - Issue trading signals when both indicators give consistent judgment

## Advantage Analysis

The biggest advantage of this combination strategy is to integrate indicators of different varieties to achieve more reliable trading judgment. Specifically, it has the following advantages:

1. Using dual moving average to determine major direction, avoid being deceived by local fluctuations
2. Use the bull bear power balance indicator for local regional judgment to accurately grasp specific entry point  
3. Two types of indicators verify each other and can filter out some mis-operations to reduce trading risks
4. Flexible parameter settings that can be optimized for different market varieties  
5. The strategy idea is simple and clear, easy to understand, and easy to optimize later

## Risk Analysis  

Some risks of this strategy need to be noted:

1. The lag of indicator signals may lead to over deep stop loss points
2. Dual moving average indicator is sensitive to parameter settings  
3. Bull bear balance indicator has slightly lower accuracy in judging short-term trends
4. Judgment deviation may occur for both indicators under special market conditions (common false breakout signals)

Countermeasures:

1. Appropriately shorten holding period or set appropriate moving stop loss
2. Test different parameter combinations to find optimal parameters  
3. Refer to other indicators for confirmation
4. Optimize parameters based on characteristics of different varieties

## Optimization Directions   

The strategy can be further optimized in the following aspects:

1. Test more moving average indicator parameter combinations
2. Increase stop loss strategies to control single stop loss
3. Incorporate volatility indicators to improve parameter self-adaptability  
4. Add machine learning models to achieve dynamic parameter optimization
5. Try different trend-following indicators to replace bull bear power balance
6. Develop visual interfaces for easy user testing of different parameters  

## Conclusion  

This strategy judges the major trend through dual moving average indicator and uses bull bear power balance indicator to assist in determining entry timing. The two indicators verify each other and can effectively reduce the probability of mis-operations. The strategy parameters are flexible and can be optimized for different varieties. Overall, the strategy is simple and practical, worth learning and using by most investors. Subsequent optimizations can further improve strategy performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|14|(?●═════ 2/20 EMA ═════●)Length|
|v_input_float_1|-15|(?●═════  Bull And Bear Balance ═════●)SellLevel|
|v_input_float_2|15|BuyLevel|
|v_input_bool_1|false|(?●═════ MISC ═════●)Trade reverse|
|v_input_int_2|true|(?●═════ Time Start ═════●)From Day|
|v_input_int_3|true|From Month|
|v_input_int_4|2005|From Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-01 00:00:00
end: 2024-01-07 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 23/05/2022
// This is combo strategies for get a cumulative signal. 
//
// First strategy
// This indicator plots 2/20 exponential moving average. For the Mov 
// Avg X 2/20 Indicator, the EMA bar will be painted when the Alert criteria is met.
//
// Second strategy
//    This new indicator analyzes the balance between bullish and
//    bearish sentiment.
//    One can cay that it is an improved analogue of Elder Ray indicator.
//    To get more information please see "Bull And Bear Balance Indicator" 
//    by Vadim Gimelfarb. 
//
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
EMA20(Length) =>
    pos = 0.0
    xPrice = close
    xXA = ta.ema(xPrice, Length)
    nHH = math.max(high, high[1])
    nLL = math.min(low, low[1])
    nXS = nLL > xXA or nHH < xXA ? nLL : nHH
    iff_1 = nXS < close[1] ? 1 : nz(pos[1], 0)
    pos := nXS > close[1] ? -1 : iff_1
    pos


BBB(SellLevel,BuyLevel) =>
    pos = 0.0
    value = close < open ? 
              close[1] > open ?  math.max(close - open, high - low) : high - low : 
                 close > open ? 
                  close[1] > open ? math.max(close[1] - low, high - close) : math.max(open - low, high - close) :
                   high - close > close - low ? 
                     close[1] > open ? math.max(close[1] - open, high - low) :high - low : 
                      high - close < close - low ? 
                         close > open ? math.max(close - low, high - close) : open - low : 
                           close > open ? math.max(close[1] - open , high - close) :
                             close[1] < open ? math.max(open - low, high - close) : high - low
    
    value2 =close < open ? 
              close[1] < open ?  math.max(high - close[1], close - low) : math.max(high - open, close - low) : 
               close > open ? 
                 close[1] > open ?  high - low : math.max(open - close[1], high - low) : 
                  high - close > close - low ? 
                   close[1] < open ? math.max(high - close[1], close - low) : high - open : 
                     high - close < close - low ? 
                      close[1] > open ?  high - low : math.max(open - close, high - low) : 
                       close[1] > open ? math.max(high - open, close - low) :
                         close[1] < open? math.max(open - close, high - low): high - low
    nBBB = value2 - value
    pos :=  nBBB < SellLevel ? -1 :
    	     nBBB >= BuyLevel ? 1 : nz(pos[1], 0) 
    pos

strategy(title='Combo 2/20 EMA & Bull And Bear Balance', shorttitle='Combo', overlay=true)
var I1 = '●═════ 2/20 EMA ═════●'
Length = input.int(14, minval=1, group=I1)
var I2 = '●═════  Bull And Bear Balance ═════●'
SellLevel = input.float(-15, step=0.01, group=I2)
BuyLevel = input.float(15, step=0.01, group=I2)
var misc = '●═════ MISC ═════●'
reverse = input.bool(false, title='Trade reverse', group=misc)
var timePeriodHeader = '●═════ Time Start ═════●'
d = input.int(1, title='From Day', minval=1, maxval=31, group=timePeriodHeader)
m = input.int(1, title='From Month', minval=1, maxval=12, group=timePeriodHeader)
y = input.int(2005, title='From Year', minval=0, group=timePeriodHeader)
StartTrade = time > timestamp(y, m, d, 00, 00) ? true : false
posEMA20 = EMA20(Length)
prePosBBB = BBB(SellLevel,BuyLevel)
iff_1 = posEMA20 == -1 and prePosBBB == -1 and StartTrade ? -1 : 0
pos = posEMA20 == 1 and prePosBBB == 1 and StartTrade ? 1 : iff_1
iff_2 = reverse and pos == -1 ? 1 : pos
possig = reverse and pos == 1 ? -1 : iff_2
if possig == 1
    strategy.entry('Long', strategy.long)
if possig == -1
    strategy.entry('Short', strategy.short)
if possig == 0
    strategy.close_all()
barcolor(possig == -1 ? #b50404 : possig == 1 ? #079605 : #0536b3)
```

> Detail

https://www.fmz.com/strategy/438067

> Last Modified

2024-01-08 17:09:48
