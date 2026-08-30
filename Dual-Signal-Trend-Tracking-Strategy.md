
> Name

Dual-Signal-Trend-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/152c854182209303462.png)
[trans]

## Overview
This strategy uses a combination of dual EMA and Awesome Oscillator indicators to identify and track trends. Among them, EMA quickly determines the direction of the recent trend, and Awesome Oscillator filters out false breakthroughs to provide entry opportunities. The strategy name "Dual Signal Trend Following Strategy" accurately summarizes the main functionality of the strategy.
## Strategy Principle
This strategy mainly uses two technical indicators, Double EMA and Awesome Oscillator, to filter signals. The specific logic is as follows:
1. Calculate the 2-period and 20-period EMAs. When the 2-period EMA breaks through the 20-period EMA from bottom to top, it is judged to be an upward trend; when the 2-period EMA breaks through the 20-period EMA from top to bottom, it is judged to be a downtrend.
2. Calculate the Awesome Oscillator, which is obtained by subtracting the slow moving average from the fast moving average, and then subtracting the MACD histogram from the fast moving average to obtain the histogram. When the AO histogram changes from red to blue, it is considered a buy signal, and when it changes from blue to red, it is a sell signal.
3. Only when EMA shows an upward trend and AO also shows a buy signal, the final buy signal is generated; only when EMA shows a downward trend and AO shows a sell signal at the same time, the final sell signal is generated.
4. Through this dual signal filtering mechanism, false breakthrough operations can be effectively reduced and the mid-term direction of the trend can be tracked.
## Advantage Analysis
This strategy has the following advantages:
1. Dual-line joint filtering can reduce erroneous transactions caused by noise. EMA determines the direction of the general trend, and AO filters entry opportunities. The combination of the two can improve the reliability of the signal.
2. The response to Sensitivity is extremely fast and can capture short-term trend reversals in a timely manner. The 2-period EMA is extremely sensitive to breakthroughs and can quickly determine whether the trend has changed in the near future.
3. Awesome Oscillator filters MACD again, which can effectively identify false breakthroughs in the trend and avoid unnecessary reverse operations.
4. The strategic direction is clear and the mid-term trend is tracked. EMA determines the basic trend direction, and AO further filters to ensure that transactions are in line with the general trend direction, and can continue to capture the mid-term trend market.
5. The selection of strategy parameters is reasonable. The 2-period and 20-period EMA capture price changes in different periods. The 5-period and 34-period AO parameters have been optimized to better identify short-term morphological characteristics.
## Risk Analysis
There are also some risks with this strategy:
1. In a volatile market, EMA and AO may send out more false signals, leading to unnecessary short transactions. The risk of misjudgment can be reduced by adjusting the EMA cycle parameters.
2. AO may lag behind EMA in some cases, resulting in a time difference in signal occurrence. AO parameters can be appropriately optimized to respond to breakthroughs faster.
3. The setting of EMA and AO parameters that take into account short- and medium-term characteristics requires high data quality and computing power, and needs to be adjusted according to the characteristics of different varieties.
4. Frequent transactions will incur more handling fees and slippage costs. The strategy exit criteria can be appropriately relaxed and the holding period extended.
5. The strategy does not consider the general cycle trend and key support and resistance levels, and more factors should be combined to ensure the correct trading direction.
## Optimization direction
This strategy can be optimized through the following aspects:
1. Introduce trend judgment indicators to assist EMA in judging the general trend direction, such as commonly used moving average ribbons, ATR and other indicators to supplement judgment.
2. Add key support and resistance level identification mechanisms, such as Fibonacci retracement lines, which only send signals near key levels. Avoid opening positions at unfavorable positions.
3. Optimize the combination of EMA and AO parameters to improve the combination effect of the two. For example, use a quasi-genetic algorithm to automatically find the optimal parameter pair.
4. Add stop loss Exit mechanism. When the price breaks through the recent Swing High/Low, stop the loss in time and leave the market to control single losses.
5. Preliminary data set verification, using historical data to evaluate the effectiveness of the strategy. Test whether stable profits can be made and whether the backtest results are in line with expectations.
6. Real offer simulation parameter adjustment, gradually adjust parameters to improve the effect of real offer indicators. Verify the robustness of parameters and obtain a better stable parameter combination.
## Summarize
The overall idea of ​​this strategy is clear. EMA is used to determine the general trend direction, and the combination of AO filtering signals uses two indicators for double verification. It can effectively identify trends and track mid-term market conditions. However, there are also certain risks and shortcomings, and testing needs to continue to be optimized to improve stability. The key is to choose the appropriate varieties and parameters and apply them in conjunction with the trader's style and rules. Overall, this strategy is reasonable and has practical value.
||


## Overview

This strategy combines dual EMA and Awesome Oscillator indicators to identify and track trends. EMA quickly judges short-term trend direction while Awesome Oscillator filters out false breakouts and provides entry timing. The strategy name "Dual Signal Trend Tracking Strategy" accurately summarizes its main functionality.

## Strategy Logic 

This strategy mainly utilizes two technical indicators, dual EMA and Awesome Oscillator, to filter signals with the following logic:

1. Calculate 2-period and 20-period EMA. When 2-period EMA breaks 20-period EMA upward, it signals an uptrend. When 2-period EMA breaks 20-period EMA downward, it signals a downtrend.

2. Calculate Awesome Oscillator, which is MACD histogram smoothed by fast EMA minus slow EMA. When AO histogram changes from red to blue, it is a buy signal. When it changes from blue to red, it is a sell signal.

3. Only when EMA shows uptrend and AO shows a buy signal at the same time, a final buy signal is generated. Only when EMA shows downtrend and AO shows a sell signal, a final sell signal is generated. 

4. Through this dual signal filtering mechanism, false breakouts can be reduced and mid-term trends can be tracked.

## Advantage Analysis

The advantages of this strategy are:

1. Dual line filtering reduces noisy trades caused by errors. EMA judges overall trend while AO filters entry timing. Combining the two improves signal reliability.

2. Extremely fast response sensitivity quickly captures short-term reversals. 2-period EMA is very sensitive to breakouts and can quickly determine if recent trends have changed.

3. Awesome Oscillator further filters MACD to effectively identify false breakouts in trends and avoid unnecessary reverse trades.

4. The strategy has a clear direction to track mid-term trends. EMA determines the basic trend while AO filters signals to ensure trading along overall trends.

5. Reasonable parameter selection. 2-period and 20-period EMA capture price changes over different timeframes. AO parameters 5 and 34 are optimized to identify short-term patterns.

## Risk Analysis

Some risks also exist:

1. In ranging markets, EMA and AO may generate more false signals, causing unnecessary short trades. Adjusting EMA period can reduce errors.

2. AO may sometimes lag EMA, causing signal time delays. AO parameters can be optimized for faster response.

3. EMA and AO combing short and mid-term features require quality data and computing power. Parameters should be adjusted for different products. 

4. Frequent trading leads to higher commissions and slippage costs. Exit criteria can be relaxed to extend holding periods.

5. The strategy does not consider long-term trends and key support/resistance levels. More factors should be combined to ensure correct trade direction.

## Optimization Directions

The strategy can be optimized through several aspects:

1. Introduce trend indicators like moving average ribbons and ATR to assist EMA in determining overall trend.

2. Add key support/resistance detection like Fibonacci retracements, generating signals only around key levels to avoid bad entry positions.

3. Optimize EMA and AO parameter combinations to improve combo effects. For example, use genetic algorithms to find optimal parameter pairs.

4. Add stop loss exits. Exit when price breaks recent Swing High/Low to control single trade loss. 

5. Backtest on historical data to evaluate strategy performance, check if stable profitability meets expectations.

6. Paper trade to gradually adjust parameters and improve live performance. Test parameter robustness to find better stable parameter sets.

## Conclusion

The overall strategy idea is clear, combining EMA for overall trend and AO for signal filtering. It can effectively identify and track trends but also has some risks and limitations for further optimization and testing to improve stability. The key is choosing suitable products and parameters combined with proper trading principles and styles. Overall this strategy has sound logic and practical value.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|14|(?●═════ 2/20 EMA ═════●)Length|
|v_input_int_2|34|(?●═════  Awesome Oscillator AC ═════●)Length Slow|
|v_input_int_3|5|Length Fast|
|v_input_int_4|15|MA|
|v_input_int_5|15|EMA|
|v_input_int_6|15|WMA|
|v_input_bool_1|true|trading WMA|
|v_input_bool_2|false|trading MA|
|v_input_bool_3|false|trading EMA|
|v_input_bool_4|false|(?●═════ MISC ═════●)Trade reverse|
|v_input_int_7|true|(?●═════ Time Start ═════●)From Day|
|v_input_int_8|true|From Month|
|v_input_int_9|2005|From Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-26 00:00:00
end: 2023-11-01 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 27/04/2022
// This is combo strategies for get a cumulative signal. 
//
// First strategy
// This indicator plots 2/20 exponential moving average. For the Mov 
// Avg X 2/20 Indicator, the EMA bar will be painted when the Alert criteria is met.
//
// Second strategy
//    This indicator plots the oscillator as a histogram where blue denotes 
//    periods suited for buying and red . for selling. If the current value 
//    of AO (Awesome Oscillator) is above previous, the period is considered 
//    suited for buying and the period is marked blue. If the AO value is not 
//    above previous, the period is considered suited for selling and the 
//    indicator marks it as red.
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


AC(nLengthSlow,nLengthFast,nLengthMA,nLengthEMA,nLengthWMA,bShowWMA,bShowMA,bShowEMA) =>
    pos = 0.0
    xSMA1_hl2 = ta.sma(hl2, nLengthFast)
    xSMA2_hl2 = ta.sma(hl2, nLengthSlow)
    xSMA1_SMA2 = xSMA1_hl2 - xSMA2_hl2
    xSMA_hl2 = ta.sma(xSMA1_SMA2, nLengthFast)
    nRes =  xSMA1_SMA2 - xSMA_hl2
    xResWMA = ta.wma(nRes, nLengthWMA)
    xResMA = ta.sma(nRes, nLengthMA)
    xResEMA = ta.ema(nRes, nLengthEMA)
    xSignalSeries = bShowWMA ? xResWMA :
                     bShowMA ? xResMA : 
                      bShowEMA ? xResEMA : na
    pos :=  xSignalSeries[2] < 0 and xSignalSeries[1] > 0? 1:
    	     xSignalSeries[2] > 0 and xSignalSeries[1] < 0 ? -1 : nz(pos[1], 0)
    pos

strategy(title='Combo 2/20 EMA & Bill  Awesome Oscillator (AC)', shorttitle='Combo', overlay=true)
var I1 = '●═════ 2/20 EMA ═════●'
Length = input.int(14, minval=1, group=I1)
var I2 = '●═════  Awesome Oscillator (AC) ═════●'
nLengthSlow = input.int(34, minval=1, title="Length Slow", group=I2)
nLengthFast = input.int(5, minval=1, title="Length Fast", group=I2)
nLengthMA = input.int(15, minval=1, title="MA", group=I2)
nLengthEMA = input.int(15, minval=1, title="EMA", group=I2)
nLengthWMA = input.int(15, minval=1, title="WMA", group=I2)
bShowWMA = input.bool( defval=true, title="trading WMA", group=I2)
bShowMA = input.bool( defval=false, title="trading MA", group=I2)
bShowEMA = input.bool( defval=false, title="trading EMA", group=I2)
var misc = '●═════ MISC ═════●'
reverse = input.bool(false, title='Trade reverse', group=misc)
var timePeriodHeader = '●═════ Time Start ═════●'
d = input.int(1, title='From Day', minval=1, maxval=31, group=timePeriodHeader)
m = input.int(1, title='From Month', minval=1, maxval=12, group=timePeriodHeader)
y = input.int(2005, title='From Year', minval=0, group=timePeriodHeader)
StartTrade = time > timestamp(y, m, d, 00, 00) ? true : false
posEMA20 = EMA20(Length)
prePosAC = AC(nLengthSlow,nLengthFast,nLengthMA,nLengthEMA,nLengthWMA,bShowWMA,bShowMA,bShowEMA)
iff_1 = posEMA20 == -1 and prePosAC == -1 and StartTrade ? -1 : 0
pos = posEMA20 == 1 and prePosAC == 1 and StartTrade ? 1 : iff_1
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

https://www.fmz.com/strategy/430896

> Last Modified

2023-11-02 17:02:06
