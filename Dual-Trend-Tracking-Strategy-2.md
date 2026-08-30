
> Name

Dual-Trend-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
The dual trend following strategy uses a combination of two different strategy signals to more accurately capture market trends and thereby obtain excess returns. This strategy first uses the 123 reversal strategy to determine the price reversal signal, and then combines the overbought and oversold indicators to determine the position direction, tracking the trend while avoiding being trapped.
## Strategy Principle
The strategy consists of two parts:
1. 123 reversal strategy
The 123 reversal strategy first determines the relationship between the closing prices of the previous two days. If the closing prices of the last two days are reversed (for example, the closing price of the previous day increased and the closing price of the previous two days fell), it means that the price may have a turning point.
Secondly, this strategy combines the Stoch indicator to determine the timing of buying and selling. When the Stoch fast line is lower than a certain level (such as 50) and the slow line is higher than the fast line, the market is considered oversold and a buy signal is generated; when the Stoch fast line is higher than a certain level (such as 50) and the slow line is lower than the fast line, the market is considered overbought and a sell signal is generated.
Therefore, while the 123 reversal strategy determines price reversal, it also needs Stoch indicator verification to generate a real buy and sell signal.
2. Overbought and oversold indicators
The overbought and oversold indicator directly uses the Stoch indicator. When the Stoch indicator is higher than a certain level (such as 90), it is considered that the market is overbought and a sell signal is generated; when the Stoch indicator is lower than a certain level (such as 20), the market is considered oversold and a buy signal is generated.
This indicator directly determines the overbought and oversold areas through the Stoch indicator to achieve the effect of tracking the trend.
Finally, this strategy combines the signals of the above two strategies - when the signals of the two strategies are in the same direction, the final buy or sell signal will be generated to capture the market trend more accurately.
## Strategic advantage analysis
The biggest advantage of the dual trend following strategy is that it can simultaneously verify price trends and overbought and oversold conditions to avoid errors in trading signals. The specific advantages are as follows:
1. Combining two strategy signals makes the verification mechanism more robust and can reduce losses caused by misjudgments of a single strategy.
2. The 123 reversal strategy determines price reversal signals and can capture potential trend turning points in a timely manner.
3. Overbought and oversold indicators can verify the current market conditions and avoid chasing highs and selling lows.
4. The two strategies can verify each other to avoid errors in trading signals, thus improving the stability of the strategy.
5. Using a combination of simple and effective indicators, the strategy logic is clear and easy to understand, making it easy to apply in practice.
## Strategy risk analysis
Although this strategy improves stability through combined verification, there are still certain risks that need to be noted:
1. The 123 reversal strategy cannot perfectly judge the price reversal point and may miss some reversal opportunities. Parameters can be adjusted appropriately to lower the threshold for judging reversal signals.
2. The overbought and oversold indicator is only based on a Stoch indicator and may produce wrong signals. Indicators such as moving averages can be added for verification.
3. The signals from the two strategies may cancel each other out, resulting in missed trading opportunities. Parameters can be adjusted appropriately to reduce the conditional constraints of the strategy combination.
4. The strategy is only based on historical data backtesting, and the parameters in the real market need to be continuously tested and optimized. A stop-loss mechanism should be added to control losses.
5. Parameters for different varieties and trading time periods need to be independently tested and optimized, and parameters cannot be completely reused.
## Strategy optimization direction
This strategy can be further optimized from the following aspects:
1. Optimize the parameters of the two strategies, find parameter combinations under different market conditions, and form a parameter pool for the optimization program to select.
2. Add filtering conditions based on indicators such as moving averages and Bollinger Bands to avoid false signals.
3. Add stop loss mechanisms, such as accelerated stop loss, trailing stop loss, time stop loss, etc., to control the maximum retracement of the strategy.
4. For different varieties, you can consider adding filters for trading volume or position quantity to avoid low-liquidity transactions.
5. The law of change of policy parameters over time can be studied, and machine learning methods can be used to automatically optimize parameters.
6. Optimize the number of entries and avoid high-frequency trading in markets without clear trends.
## Summarize
The dual trend following strategy combines the 123 reversal strategy and overbought and oversold indicators to accurately judge the price trend reversal while verifying whether it is currently overbought and oversold, thereby filtering out false signals and capturing the actual trend to bring excess returns. Compared with a single indicator strategy, this strategy is more stable and profitable. However, you still need to pay attention to controlling risks and stop losses in a timely manner. In the future, strategy performance can be continued to be improved through parameter optimization, adding filter conditions, automation, etc.

||

## Overview

The Dual Trend Tracking strategy combines two different strategy signals to more accurately capture market trends and generate excess returns. It first uses the 123 reversal strategy to determine price reversal signals, and then combines the overbought-oversold indicator to determine position direction, tracking trends while avoiding being trapped.

## Strategy Logic

The strategy consists of two parts:

1. 123 Reversal Strategy

   The 123 reversal strategy first judges the closing price relationship between the previous two days. If the closing prices reversed recently (e.g. the closing price rose yesterday and fell the day before), it indicates a potential turning point.

   It then combines the Stoch indicator to determine buy and sell timing. When the Stoch fast line is below a certain level (e.g. 50) and the slow line is above the fast line, it is considered oversold and generates a buy signal. When the Stoch fast line is above a certain level (e.g. 50) and the slow line is below the fast line, it is considered overbought and generates a sell signal.

   So the 123 reversal strategy requires confirmation from the Stoch indicator in addition to identifying price reversal to generate actual trading signals.

2. Overbought/Oversold Indicator

   The overbought/oversold indicator directly uses the Stoch indicator. When the Stoch indicator is above a certain level (e.g. 90), it is considered overbought and generates a sell signal. When the Stoch indicator is below a certain level (e.g. 20), it is considered oversold and generates a buy signal.

   This indicator judges overbought/oversold levels directly through the Stoch indicator to track trends.

Finally, the strategy combines the signals from the two strategies - only when the signals are in the same direction will final buy or sell signals be generated to more accurately capture market trends.

## Advantage Analysis

The biggest advantage of the Dual Trend Tracking strategy is that it can verify both price trends and overbought/oversold conditions to avoid wrong trading signals. Specific advantages:

1. Combining two strategy signals provides more robust verification and reduces losses caused by errors in a single strategy.

2. The 123 reversal strategy can capture potential trend reversal points in a timely manner.

3. The overbought/oversold indicator can verify current market conditions and avoid chasing highs and selling lows.

4. The two strategies can verify each other to avoid wrong signals, improving stability.

5. It combines simple and effective indicators with clear logic that is easy to understand and apply.

## Risk Analysis

Although the strategy improves stability through combined verification, some risks still exist:

1. The 123 reversal strategy cannot perfectly identify reversal points and may miss some opportunities. Fine-tune parameters to lower the reversal signal threshold.

2. The overbought/oversold indicator relies solely on one Stoch indicator and may generate false signals. Add MA lines etc. for verification.

3. The two strategy signals may cancel each other out and miss opportunities. Adjust parameters to reduce constraints.

4. The strategy is only backtested on historical data. Parameters need continuous optimization in live trading. Add stop loss mechanisms to control losses.

5. Parameters need independent testing and optimization for different products and trading periods. Do not directly copy parameters.

## Optimization Directions

The strategy can be further optimized in the following aspects:

1. Optimize parameters for both strategies to form parameter pools for optimization programs to select from under different market conditions.

2. Add filter conditions based on MA, Bollinger Bands etc. to avoid wrong signals. 

3. Add stop loss mechanisms such as trailing stop loss, move stop loss, time stop loss etc. to control maximum drawdown.

4. Consider adding filters on volume or positions for different products to avoid low liquidity.

5. Study the evolution of parameters over time and use machine learning to automatically optimize.

6. Optimize entry frequency to avoid overtrading in trendless markets. 

## Conclusion

The Dual Trend Tracking strategy accurately identifies trend reversals while verifying overbought/oversold levels by combining the 123 reversal and overbought/oversold strategies. This filters out wrong signals and captures actual trends for excess returns. It is more stable and profitable than single indicator strategies. But risks should be managed via timely stop loss. Future improvements can be made through parameter optimization, adding filters, automation etc.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|---- 123 Reversal ----|
|v_input_2|14|Length|
|v_input_3|true|KSmoothing|
|v_input_4|3|DLength|
|v_input_5|50|Level|
|v_input_6|true|---- Overbought/Oversold ----|
|v_input_7|10|LengthOO|
|v_input_8|0.92|BuyBand|
|v_input_9|0.5|SellBand|
|v_input_10|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-20 00:00:00
end: 2023-09-26 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 30/03/2021
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
// Simple Overbought/Oversold indicator
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


OO(Length,BuyBand,SellBand) =>
    pos = 0.0
    xOBOS = stoch(close, high, low, Length)
    nRes = iff(close > close[Length], xOBOS / 100, (100 - xOBOS) / 100)
    pos :=iff(nRes < SellBand, -1,
           iff(nRes > BuyBand, 1, nz(pos[1], 0))) 
    pos

strategy(title="Combo Backtest 123 Overbought/Oversold", shorttitle="Combo", overlay = true)
line1 = input(true, "---- 123 Reversal ----")
Length = input(14, minval=1)
KSmoothing = input(1, minval=1)
DLength = input(3, minval=1)
Level = input(50, minval=1)
//-------------------------
line2 = input(true, "---- Overbought/Oversold ----")
LengthOO = input(10, minval=1)
BuyBand = input(0.92, step = 0.01)
SellBand = input(0.5, step = 0.01)
reverse = input(false, title="Trade reverse")
posReversal123 = Reversal123(Length, KSmoothing, DLength, Level)
posOO = OO(LengthOO,BuyBand,SellBand)
pos = iff(posReversal123 == 1 and posOO == 1 , 1,
	   iff(posReversal123 == -1 and posOO == -1, -1, 0)) 
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

https://www.fmz.com/strategy/427985

> Last Modified

2023-09-27 16:14:25
