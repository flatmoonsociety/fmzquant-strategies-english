
> Name

Quantitative-Reversal-Index-Strategy-Integrating-Dual-Trend-Signals
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/fd22f4107d505d18b3.png)
[trans]

## Overview
The name of this strategy is "Reversal Index Quantitative Strategy Fusion of Dual Trend Signals". It combines two different strategic signals, one is a short-term reversal signal based on the stochastic indicator, and the other is a long-term trend signal based on trading volume. The two are combined to form a stable entry signal.
## Strategy Principle
This strategy consists of two parts. The first part uses the 9-day Stoch indicator to generate short-term reversal signals. Specifically, if the closing price is higher than the previous day, go long when the 9-day fast line is below 50 and the slow line is above 50; if the closing price is lower than the previous day, go short when the 9-day fast line is above 50 and the slow line is below 50. In this way, the golden cross of the Stoch indicator is used to form a short-term reversal signal.
The second part uses the Negative Volume Index (NVI) to form a long-term trend signal. The calculation formula of NVI is: if the trading volume on the current day is less than the previous day, the closing price change rate of the current day is accumulated; if the trading volume on the current day is greater than or equal to the previous day, the value of the previous day remains unchanged. Long-term trend signals are formed through the moving averages of the NVI indicator.
Finally, this strategy combines both signals. An entry signal is formed only when the short-term reversal signal and the long-term trend signal are in the same direction. This helps filter out false signals and enhances stability.
## Advantage Analysis
The biggest advantage of this strategy is the stability of the signal. Short-term reversal signals can capture short-term adjustments in the market, while long-term trend signals ensure that the general trend remains unchanged. The combination of the two greatly enhances the stability of the signal and can effectively filter short-term signals with a high false alarm rate.
In addition, this strategy has fewer parameters and is easy to optimize. Users only need to adjust the parameters of NVI to adapt to the characteristics of different markets.
## Risk Analysis
The biggest risk with this strategy is the possible time lag between the two signals. There may be a certain lag between the short-term reversal signal and the long-term trend signal, which will cause the two signals to be inconsistent for a period of time and fail to form a stable entry signal.
In addition, the NVI indicator is also sensitive to abnormally large trading volume changes, which may lead to incorrect long-term trend judgments.
In order to reduce these risks, the NVI indicator parameters can be appropriately adjusted, or a stop loss can be added to control a single loss.
## Optimization direction
This strategy can mainly be optimized from the following aspects:
1. Optimize the parameters of the Stoch indicator and improve the reversal capturing ability.
2. Optimize the length cycle of the NVI indicator and enhance the ability to identify long-term trends.
3. Add trading volume filtering conditions to eliminate false signals of abnormal trading volume.
4. Add a stop-loss strategy to control single losses.
## Summarize
This strategy designs a stable entry mechanism based on the ideas of short-term reversal and long-term trend, which can effectively control the false alarm rate and enhance the stability of the signal. The next step can be to optimize parameters and add filtering conditions to further improve the stability of the strategy.
||


## Overview

The strategy is named "Quantitative Reversal Index Strategy Integrating Dual Trend Signals". It integrates signals from two different strategies - a short-term reversal signal based on the Stochastic indicator and a long-term trend signal based on volume, combining them into a stable entry signal.

## Principles

The strategy consists of two parts. The first part uses the 9-day Stoch to generate short-term reversal signals. Specifically, it goes long when the close is higher than the previous close and the Stoch 9-day fast line is below 50 while the slow line is above 50; it goes short when the close is lower than the previous close and the Stoch 9-day fast line is above 50 while the slow line is below 50. This way, the Stoch's golden cross and death cross form short-term reversal signals.  

The second part uses the Negative Volume Index (NVI) to form long-term trend signals. The NVI calculation formula is that if the volume of the day is less than the previous day, the rate of change of the closing price of the day is accumulated; if the volume of the day is greater than or equal to the previous day, the previous day's value remains unchanged. Long-term trend signals are formed through the moving average of the NVI indicator.

Finally, the strategy combines the two types of signals. Only when the short-term reversal signal and long-term trend signal are in the same direction will an entry signal be formed. This helps filter out false signals and enhance stability.

## Advantage Analysis

The biggest advantage of this strategy is the stability of signals. The short-term reversal signal captures short-term market adjustments, while the long-term trend signal ensures the big trend remains unchanged. The combination of the two greatly enhances the stability of the signals and can effectively filter out false signals that have a higher rate from the short-term ones.

In addition, the strategy has few parameters and is easy to optimize. Users only need to adjust the parameters of the NVI to adapt to the characteristics of different markets.

## Risk Analysis

The biggest risk of this strategy is that there may be a time lag between the two types of signals. There may be some lag between the short-term reversal signal and long-term trend signal, which will lead to inconsistent signals for a period of time, unable to form a stable entry signal.

In addition, the NVI indicator is also sensitive to abnormal surges in trading volume, which can lead to wrong judgments of long-term trends.  

To mitigate these risks, the parameters of the NVI indicator can be adjusted accordingly, or stop loss can be added to control the loss per trade.

## Optimization

The main aspects for optimizing this strategy include:

1. Optimize the parameters of the Stoch indicator to improve reversal capturing capability.  

2. Optimize the cycle length of the NVI indicator to enhance long-term trend identification capability. 

3. Add trading volume filters to eliminate false signals from abnormal trading volumes.

4. Add stop loss strategies to control per trade loss.

## Conclusion  

The strategy is designed with a stable entry mechanism based on the idea of short-term reversal and long-term trend to effectively control the false positive rate and enhance signal stability. Next steps for optimization include adjusting parameters, adding filter conditions, etc. to further improve the stability of the strategy.  
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|---- 123 Reversal ----|
|v_input_2|14|Length|
|v_input_3|true|KSmoothing|
|v_input_4|3|DLength|
|v_input_5|50|Level|
|v_input_6|true|---- Negative Volume Index ----|
|v_input_7|50|EMA_Len|
|v_input_8|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-18 00:00:00
end: 2023-12-21 05:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 29/03/2021
// This is combo strategies for get a cumulative signal. 
//
// First strategy
// This System was created from the Book "How I Tripled My Money In The 
// Futures Market" by Ulf Jensen, Page 183. This is reverse type of strategies.
// The strategy buys at market, if close price is higher than the previous close 
// during 2 days and the meaning of 9-days Stochastic Slow Oscillator is lower than 50. 
// The strategy sells at market, if close price is lower than the previous close price 
// during 2 days and the meaning of 9-days Stochastic Fast Oscillator is higher than 50.
//
// Second strategy
// The theory behind the indexes is as follows: On days of increasing 
// volume, you can expect prices to increase, and on days of decreasing 
// volume, you can expect prices to decrease. This goes with the idea of 
// the market being in-gear and out-of-gear. Both PVI and NVI work in similar 
// fashions: Both are a running cumulative of values, which means you either 
// keep adding or subtracting price rate of change each day to the previous day`s 
// sum. In the case of PVI, if today`s volume is less than yesterday`s, don`t add 
// anything; if today`s volume is greater, then add today`s price rate of change. 
// For NVI, add today`s price rate of change only if today`s volume is less than 
// yesterday`s.
//
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
Reversal123(Length, KSmoothing, DLength, Level) =>
    vFast = sma(stoch(close, high, low, Length), KSmoothing) 
    vSlow = sma(vFast, DLength)
    pos = 0.0
    pos := iff(close[2] < close[1] and close > close[1] and vFast < vSlow and vFast > Level, 1,
	         iff(close[2] > close[1] and close < close[1] and vFast > vSlow and vFast < Level, -1, nz(pos[1], 0))) 
	pos


NVI(EMA_Len) =>
    pos = 0.0
    nRes = 0.0
    xROC = roc(close, EMA_Len)
    nRes := iff(volume < volume[1], nz(nRes[1], 0) + xROC, nz(nRes[1], 0))
    nResEMA = ema(nRes, EMA_Len)
    pos := iff(nRes > nResEMA, 1,
    	     iff(nRes < nResEMA, -1, nz(pos[1], 0))) 
    pos

strategy(title="Combo Backtest 123 Negative Volume Index", shorttitle="Combo", overlay = true)
line1 = input(true, "---- 123 Reversal ----")
Length = input(14, minval=1)
KSmoothing = input(1, minval=1)
DLength = input(3, minval=1)
Level = input(50, minval=1)
//-------------------------
line2 = input(true, "---- Negative Volume Index ----")
EMA_Len = input(50, minval=1)
reverse = input(false, title="Trade reverse")
posReversal123 = Reversal123(Length, KSmoothing, DLength, Level)
posNVI = NVI(EMA_Len)
pos = iff(posReversal123 == 1 and posNVI == 1 , 1,
	   iff(posReversal123 == -1 and posNVI == -1, -1, 0)) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1 , 1, pos))	   
if (possig == 1 ) 
    strategy.entry("Long", strategy.long)
if (possig == -1 )
    strategy.entry("Short", strategy.short)	 
if (possig == 0) 
    strategy.close_all()
barcolor(possig == -1 ? #b50404: possig == 1 ? #079605 : #0536b3 )
```

> Detail

https://www.fmz.com/strategy/436645

> Last Modified

2023-12-26 15:47:36
