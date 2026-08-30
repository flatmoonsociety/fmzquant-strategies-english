
> Name

Quantitative-Strategy-Based-on-Reversal-and-Comparative-Relative-Strength
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/460a60e7e69ca8f514.png)
[trans]

## Overview
This strategy first combines the reversal strategy proposed by Ulf Jensen on page 183 of his book "How I Tripled My Money in the Futures Market" with the Comparative Relative Strength Indicator, combined to obtain stronger signals. The combined strategy is called "Combined Quantitative Strategy Based on Reversal and Relative Strength."
The main idea of ​​this strategy is to use multiple factors for judgment at the same time, combine the two signals of reversal factor and comparative relative strength, and only buy or sell when both signals are sent at the same time to improve the stability of the strategy.
## Strategy Principle
The first part is the reversal strategy. This strategy goes long under the following conditions: the closing prices of the last two days have risen continuously, and the 9-day Stochastic slow line is below 50. The conditions for closing the position are: the closing prices of the last two days have fallen continuously, and the 9-day Stochastic Express line is above 50.
The second part compares relative strength indicators. This indicator calculates the moving average of the N-day closing price change rate of the target stock and the underlying index, and compares it with the pre-set buying band, selling band and liquidation band. When the indicator crosses the buying band above, go long, when it crosses below the selling band, go short, when it goes long, it crosses the closing band, it closes the position, when it goes short, it goes above the closing band, it closes the position.
This combination strategy will judge the signals of the two parts at the same time. Only when both send the same signal (double buy or double sell), the corresponding buying or selling operation will be carried out.
## Advantage Analysis
This strategy combines the Reversal Factor and the Relative Strength Factor to take advantage of both. The reversal strategy can capture short-term extreme points; the relative strength strategy can capture the main trend of the market. Both send signals at the same time, which can improve the reliability of the signal and filter out erroneous signals caused by part of the noise.
In addition, the Stochastic indicator, as an overbought and oversold distinction indicator, can better judge reversal points. Combining trend indicators such as moving averages can also form a more mature combination strategy.
## Risk Analysis
The biggest risk of the reversal strategy is that it is impossible to determine the time when the market will reverse, and it may continue to move in the opposite direction after a loss. At this time, the relative strength indicator can come into play to determine whether the general trend has changed.
The risk of the relative strength strategy is that the indicator parameters are not set properly, resulting in too many false signals. At this time, the reversal strategy can play a filtering role and reduce unnecessary transactions.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Test more reversal factors and find better reversal strategies. Currently using only a simple N-day new high/new low statistical strategy.
2. Test and optimize the parameters of the relative strength index to find the best parameter combination. The current parameter settings are subjective and may not be optimal.
3. Add a stop loss strategy. This strategy currently does not set a stop loss. Adding a reasonable stop loss can control the risk of loss.
4. You can test different underlying indexes, and then calculate the relative strength with the target stock to find the best matching index.
## Summarize
This strategy combines reversal factors and relative strength factors for trading, and can use the advantages of both to improve signal quality. It is a relatively mature combination strategy. There is still a lot of room for optimization of this strategy, and better results can be obtained through parameter optimization, stop-loss strategies and adjustments to strategy combinations.
||


## Overview

This strategy first combines the reversal strategy proposed by Ulf Jensen on page 183 of his book "How I Tripled My Money in the Futures Market" with the comparative relative strength indicator to obtain stronger signals. The combined strategy is called "Quantitative Strategy Based on Reversal and Comparative Relative Strength".

The main idea of this strategy is to judge by multiple factors at the same time. By combining the reversal factor and the comparative relative strength signal, it will only place buy or sell orders when both give the same signal, in order to improve the stability of the strategy.

## Strategy Principle 

The first part is a reversal strategy. The strategy goes long when: the closing price has risen continuously for the last two days, and the 9-day Stochastic slow line is below 50. The closing condition is: the closing price has fallen continuously for the last two days, and the 9-day Stochastic fast line is above 50.

The second part is the comparative relative strength indicator. This indicator calculates the moving average of the N-day closing price change rate between the target stock and the benchmark index, and compares it with the preset buy zone, sell zone and close zone. It goes long when the indicator crosses above the buy zone, goes short when it falls below the sell zone, and closes positions when long and the indicator falls below the close zone, and when short and the indicator rises above the close zone.

This combined strategy judges the signals of both parts at the same time. It will only place buy or sell orders when both give the same signal (both buy or both sell).

## Advantage Analysis

This strategy combines the advantages of reversal factors and relative strength factors. The reversal strategy can capture extremes in the short term; the relative strength strategy can grasp the main trend of the broader market. Signals from both strategies can improve reliability and filter out some false signals caused by noise.

In addition, the Stochastic indicator, as an indicator for distinguishing overbought and oversold zones, can better determine reversal points. Using it in combination with trend indicators like moving averages can form a more mature combined strategy.

## Risk Analysis

The biggest risk of reversal strategies is that they cannot determine the timing of market reversals, which may lead to continued losses after the market reversal. In this case, the relative strength indicator can come into play to judge whether the major trend has changed.

The risk of the relative strength strategy lies in inappropriate parameter settings, which may generate too many false signals. In this case, the reversal strategy can play a role in filtering to reduce unnecessary trades.

## Optimization Directions

This strategy can be optimized in the following aspects:

1. Test more reversal factors to find better reversal strategies. The current one uses just a simple N-day new high/low statistics strategy.

2. Test and optimize parameters for the relative strength indicator to find the optimal parameter combination, since current settings are subjective and likely not optimized.

3. Add stop loss strategies. Currently there is no stop loss, adding reasonable stop loss can control downside risk.

4. Test different benchmark indices to calculate relative strength to the target stock and find the best matching index.

## Conclusion

This strategy combines reversal factors and relative strength factors for trading. It utilizes the advantages of both to improve signal quality and is a relatively mature combined strategy. There is still much room for optimization by parameters tuning, adding stop loss strategies, and adjusting the strategy combination methods to achieve even better results.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Length|
|v_input_2|true|KSmoothing|
|v_input_3|3|DLength|
|v_input_4|50|Level|
|v_input_5|BTC_USDT:swap|b|
|v_input_6|10|LengthCRS|
|v_input_7|0.9988|BuyBand|
|v_input_8|0.996|SellBand|
|v_input_9|0.9975|CloseBand|
|v_input_10|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-06 00:00:00
end: 2023-12-12 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 30/10/2019
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
// Comparative Relative Strength Strategy for ES
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

CRS(a, b, len, BuyBand, SellBand, CloseBand) =>
    pos = 0.0
    as = security(a, timeframe.period, close) 
    bs = security(b, timeframe.period, close) 
    nRes = sma(as/bs, len)
    pos := iff(nRes > BuyBand, 1,
	         iff(nRes < SellBand, -1,
	          iff(pos[1] == 1 and nRes < CloseBand, 0,
    	       iff(pos[1] == -1 and nRes > CloseBand, 0, nz(pos[1], 0)))))
    pos

strategy(title="Combo Backtest 123 Reversal & Comparative Relative Strength", shorttitle="Combo", overlay = true)
Length = input(14, minval=1)
KSmoothing = input(1, minval=1)
DLength = input(3, minval=1)
Level = input(50, minval=1)
//-------------------------
a = syminfo.tickerid 
b = input("BTC_USDT:swap", type=input.symbol) 
LengthCRS = input(10) 
BuyBand = input(0.9988, step = 0.0001)
SellBand = input(0.9960, step = 0.0001)
CloseBand = input(0.9975, step = 0.0001)
reverse = input(false, title="Trade reverse")
posReversal123 = Reversal123(Length, KSmoothing, DLength, Level)
posCRS = CRS(a, b, LengthCRS, BuyBand, SellBand, CloseBand)
pos = iff(posReversal123 == 1 and posCRS == 1 , 1,
	   iff(posReversal123 == -1 and posCRS == -1, -1, 0)) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1 , 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	 
if (possig == 0) 
    strategy.close_all()
barcolor(possig == -1 ? #b50404: possig == 1 ? #079605 : #0536b3 )
```

> Detail

https://www.fmz.com/strategy/435275

> Last Modified

2023-12-13 17:17:10
