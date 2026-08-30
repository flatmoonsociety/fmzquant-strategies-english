
> Name

Wealth-Creation-Composite-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/fa126af7ee4a52aae7e56116ea78b66010f296a9a3957545ebe8cb7cfb425b0a.png)
[trans]

## Overview
This strategy is a comprehensive trading strategy that aims to make profits in the short to medium term. It integrates the 123 reversal strategy and the magic oscillator strategy to take advantage of both and obtain more reliable trading signals.
## Strategy Principle
The strategy consists of two parts:
**123 Reversal Strategy**
This part of the strategy is adapted from the reversal strategy described on page 183 of the book "How I Tripled My Money in the Futures Market". It goes long if the closing price is higher than the previous day's closing price for 2 consecutive days and the 9-day slow stochastic line is below 50; it goes short if the closing price is lower than the previous day's closing price for 2 consecutive days and the 9-day stochastic fast line is above 50.
**Magic Oscillator Strategy**
This part of the strategy uses the Magic Oscillator indicator, which compares the current value of AO with the value of the previous period. If the current AO value is higher than the previous period, it is considered suitable for long selling, and the column is displayed in blue; if the current AO value is not higher than the previous period, it is deemed suitable for short selling, and the column is displayed in red.
The comprehensive signal generation rule is: if the 123 reversal strategy and the magic oscillator strategy send out buy signals at the same time, then a long strategy is adopted; if both send out sell signals at the same time, a short strategy is adopted.
## Advantage Analysis
The biggest advantage of this comprehensive strategy is that it integrates the advantages of two different types of strategies, which can improve the reliability and stability of the signal.
Specifically, the 123 reversal strategy is more suitable in the short to medium term and can capture reversal opportunities. The Magic Oscillator strategy pays more attention to short-term trends and has higher sensitivity. The two complement each other and can filter out some false signals, while also capturing better entry opportunities at different stages.
In addition, this strategy comprehensively uses K-line information and oscillator indicators, taking into account the information of the price market itself and the relationship between volume and price, and is relatively comprehensive and three-dimensional.
## Risk Analysis
The biggest risk of this strategy is that combining multiple strategies also means combining their own risks.
123 Reversal strategies by themselves do not completely avoid the risk of being trapped in volatile markets. The Magic Oscillator strategy is also sensitive to short-term market fluctuations. If the two send wrong signals, the damage will be multiplied by two.
In addition, parameter settings will also affect the strategy effect. It requires repeated testing and optimization to find the best parameter combination.
To avoid risks, you can appropriately adjust the strategic position size and reduce the risk exposure of a single transaction. In addition, a stop loss line can be set to avoid further losses.
## Optimization direction
This strategy can be further optimized from the following aspects:
1. Test and optimize parameters to find the optimal parameter combination
2. Add other indicators or filtering conditions to further improve signal quality
3. Combine different time periods for multi-time frame optimization
4. Add dynamic stop loss strategy to better control risks
5. Consider actual transaction costs and set entry and exit conditions
6. Consider the direction of the large-scale trend and avoid counter-trend operations
## Summarize
This strategy combines the advantages of 123 reversal and magic oscillator strategies to improve signal reliability while retaining a certain degree of flexibility and sensitivity to market changes. However, it is still necessary to further optimize parameters and strictly control risks in order to make stable profits in the real market. Overall, this strategy has good short- and medium-term trading potential and is worthy of further research and application.
||


## Overview

This strategy is a composite trading strategy that aims to profit in the medium to short term. It integrates the 123 Reversal strategy and Awesome Oscillator strategy to leverage the strengths of both and obtain more reliable trading signals.

## Strategy Logic

The strategy consists of two parts:

**123 Reversal Strategy** 

This part is adapted from the reversal strategy described on page 183 of the book "How I Tripled My Money in the Futures Market" by Ulf Jensen. It goes long when the close price is higher than the previous close for 2 consecutive days and the 9-day Slow Stochastic is below 50. It goes short when the close price is lower than the previous close for 2 consecutive days and the 9-day Fast Stochastic is above 50.

**Awesome Oscillator Strategy**

This part uses the Awesome Oscillator indicator, which compares the AO current value to the previous one. If the current AO value is higher than the previous, it indicates a good opportunity to go long and the histogram bar color is blue. If the current AO value is not higher than the previous, it indicates a good chance to go short and the bar color is red.

The combined signal is generated as follows: if the 123 Reversal and Awesome Oscillator strategies both give buy signals, adopt a long strategy; if both give sell signals, adopt a short strategy.

## Advantage Analysis 

The biggest advantage of this composite strategy is that it combines the strengths of two different types of strategies, improving the reliability and stability of trading signals.

Specifically, the 123 Reversal strategy is more applicable in the medium to short term and can capture reversal opportunities. The Awesome Oscillator strategy focuses more on short-term trends and is more sensitive. The two strategies complement each other, help filter out false signals, and capture better entry opportunities in different stages.

In addition, this strategy comprehensively utilizes K-line information and an oscillator indicator, taking into account both price action itself and the volume-price relationship for a more well-rounded approach.

## Risk Analysis

The biggest risk of this strategy is that combining multiple strategies also compounds their individual risks. 

The 123 Reversal strategy itself cannot completely avoid the risk of being stuck in a range-bound market. The Awesome Oscillator strategy is also sensitive to short-term market fluctuations. Incorrect signals from both strategies will be amplified.

In addition, parameter settings also affect strategy performance. Extensive testing and optimization is needed to find the optimum parameters.

To mitigate risks, properly size positions to limit downside on individual trades. Also set stop loss orders to prevent losing more.

## Optimization Directions

The strategy can be further optimized in the following aspects:

1. Test and optimize parameters to find the optimal parameter combination.

2. Add other indicators or filters to further improve signal quality. 

3. Optimize across different timeframes for a multi-timeframe approach.

4. Add dynamic stops to better control risks.

5. Consider actual transaction costs and define entry/exit criteria.  

6. Consider the major trend direction to avoid countertrend trading.

## Conclusion

This strategy combines the strengths of the 123 Reversal and Awesome Oscillator strategies, enhancing signal reliability while retaining flexibility and sensitivity to market changes. Further parameter optimization and strict risk control are needed for stable profits in live trading. Overall, this strategy has good potential for medium to short-term trading and is worth researching and applying.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|---- 123 Reversal ----|
|v_input_2|14|Length|
|v_input_3|true|KSmoothing|
|v_input_4|3|DLength|
|v_input_5|50|Level|
|v_input_6|true|---- Awesome Oscillator (AC) ----|
|v_input_7|34|Length Slow|
|v_input_8|5|Length Fast|
|v_input_9|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-01 00:00:00
end: 2023-10-31 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 09/08/2021
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
Reversal123(Length, KSmoothing, DLength, Level) =>
    vFast = sma(stoch(close, high, low, Length), KSmoothing) 
    vSlow = sma(vFast, DLength)
    pos = 0.0
    pos := iff(close[2] < close[1] and close > close[1] and vFast < vSlow and vFast > Level, 1,
	         iff(close[2] > close[1] and close < close[1] and vFast > vSlow and vFast < Level, -1, nz(pos[1], 0))) 
	pos


BWAC(nLengthSlow,nLengthFast) =>
    pos = 0.0
    xSMA1_hl2 = sma(hl2, nLengthFast)
    xSMA2_hl2 = sma(hl2, nLengthSlow)
    xSMA1_SMA2 = xSMA1_hl2 - xSMA2_hl2
    xSMA_hl2 = sma(xSMA1_SMA2, nLengthFast)
    nRes =  xSMA1_SMA2 - xSMA_hl2
    pos:= iff(nRes > nRes[1], 1,
             iff(nRes < nRes[1], -1, nz(pos[1], 0)))  
    pos

strategy(title="Combo Backtest 123 Reversal & Awesome Oscillator (AC)", shorttitle="Combo", overlay = true)
line1 = input(true, "---- 123 Reversal ----")
Length = input(14, minval=1)
KSmoothing = input(1, minval=1)
DLength = input(3, minval=1)
Level = input(50, minval=1)
//-------------------------
line2 = input(true, "---- Awesome Oscillator (AC) ----")
nLengthSlow = input(34, minval=1, title="Length Slow")
nLengthFast = input(5, minval=1, title="Length Fast")
reverse = input(false, title="Trade reverse")
posReversal123 = Reversal123(Length, KSmoothing, DLength, Level)
posBWAC = BWAC(nLengthSlow,nLengthFast)
pos = iff(posReversal123 == 1 and posBWAC == 1 , 1,
	   iff(posReversal123 == -1 and posBWAC == -1, -1, 0)) 
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

https://www.fmz.com/strategy/430763

> Last Modified

2023-11-01 16:28:55
