
> Name

Dual-Reversal-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/17f94b2113065fe22c3.png)

[trans]

## Overview
The double reversal trading strategy combines the two sub-strategies of "123 reversal" and "N K-line continuous decline" to achieve the effect of efficiently capturing trading opportunities when the trend reverses. This strategy is more suitable for medium and long-term trading.
## Strategy Principle
### 123 reverse
The principle of the "123 reversal" sub-strategy is:
Go long when the closing prices of the current two days are inverse (that is, if the closing price of the previous day is higher than the previous two days, then the current closing price is lower than the previous day), and the fast stochastic indicator of the 9-day stock K-line is lower than 50, go long; when the closing prices of the current two days are inverse (that is, if the closing price of the previous day is lower than the previous two days, then the current closing price is higher than the previous day), and the fast stochastic indicator of the 9-day stock K-line is higher than 50, go short.
This sub-strategy achieves the effect of efficiently capturing trend reversal by judging the reversal of the closing prices of the previous two days and combining it with the stochastic indicator to determine the timing of trend reversal.
### N K lines fell continuously
The principle of the "N K-lines falling continuously" sub-strategy is:
Count whether the closing prices of the recent N K lines have fallen continuously. If the decline reaches N K lines, a short signal will be generated.
This sub-strategy determines the timing of trend reversal by judging the continuous decline of a certain number of K lines.
### Dual combination signal
The double reversal trading strategy combines the above two sub-strategies. When both generate long or short signals at the same time, the order will actually be placed.
This can filter out some false positive signals and make trading signals more reliable. At the same time, combining reversal signals and continuous falling signals can more accurately determine the timing of trend reversal.
## Strategic advantage analysis
The double reversal trading strategy has the following advantages:
1. By combining multiple sub-strategies, false signals can be effectively filtered and the reliability of the signal can be improved.
2. The 123 reversal strategy can accurately determine the trend reversal point in the short term. The continuous decline of N K lines can determine the reversal of the mid- to long-term trend. The two are used together to capture short-term trading opportunities at the medium and long-term level.
3. Using stock K-line indicators, the parameters can be adjusted flexibly and are suitable for different varieties.
4. The strategic ideas are simple and clear, easy to understand and follow, and suitable for beginners to learn.
5. The parameters of sub-strategies can be customized, which can be optimized for different varieties to improve the adaptability of the strategy.
## Strategy risk analysis
There are also some risks associated with the double reversal trading strategy:
1. False alarms may occur with reversal signals. Although combined signals can reduce the risk of false alarms, they cannot be completely avoided. Recommended to be used in conjunction with a stop loss strategy.
2. The sub-strategy uses simple indicators and may not be able to adapt to complex market conditions. You can consider introducing more technical indicators or machine learning to improve strategy adaptability.
3. Sub-strategy parameters need to be optimized for different varieties, otherwise over-fitting problems may occur.
4. Reversal strategies are more suitable for the medium and long term, and there is a risk of arbitrage in the short term. The holding period should be adjusted appropriately.
5. Reversal signals may appear in the small-scale adjustment stage of the trend. Trend judgment should be combined to ensure that the strategy direction is consistent with the general trend.
## Strategy optimization direction
This double reversal trading strategy can be optimized from the following aspects:
1. Introduce more technical indicator judgments, form a multi-factor model, and improve the strategy's adaptability to complex market conditions. For example, moving averages, Bollinger Bands and other indicators are introduced for combination.
2. Add machine learning model judgment and use machine learning to model multi-dimensional features to improve signal accuracy. For example, random forest or neural network is introduced to judge the K line.
3. Optimize parameter settings and conduct parameter training for different varieties to improve the adaptability of parameters. For example, genetic algorithm is used to optimize parameter combinations.
4. Combine with the stop loss strategy to control the single stop loss and strengthen the risk control of the strategy. Stop loss positions can also be subject to data-driven optimization.
5. Develop a dynamic position management mechanism to dynamically adjust the position size based on market conditions and sub-strategy results to reduce risks.
6. Introduce a trend judgment module to avoid signals generated by sub-strategies that are inconsistent with the general trend. For example, the moving average is introduced to determine the trend.
## Summarize
The double reversal trading strategy achieves efficient capture of trend reversal opportunities by combining the two sub-strategies of 123 reversal and N K-line continuous decline. This strategy is more suitable for medium and long-term positions, can effectively filter false positive signals, and provides more reliable trading opportunities when the trend reverses. However, this strategy also has certain limitations. It needs to introduce more technical indicators for optimization, and cooperate with stop loss and position management mechanisms to reduce risks, so as to adapt to a more complex market environment. Generally speaking, the double reversal trading strategy provides a simple and direct trend reversal strategy idea, and is a good material for beginners to understand and learn strategic trading. With the introduction of more optimization methods, this strategy can become a very practical quantitative trading strategy.
|| 

## Overview

The dual reversal trading strategy combines the "123 reversal" and "N consecutive bars down" sub-strategies to efficiently capture trading opportunities when trend reversal occurs. This strategy is more suitable for medium and long term trading.

## Strategy Logic

### 123 Reversal 

The "123 reversal" sub-strategy is based on the principle:

Go long when the closing price of the previous two days shows a reverse (i.e. if previous close is higher than the close before previous day, current close is lower than previous close), and the 9-day fast stochastic is lower than 50; 

Go short when the closing price of the previous two days shows a reverse (i.e. if previous close is lower than the close before previous day, current close is higher than previous close), and the 9-day fast stochastic is higher than 50.

This sub-strategy identifies trend reversal by judging the reverse of previous two closing prices combined with stochastic indicator.

### N Consecutive Bars Down

The "N consecutive bars down" sub-strategy is based on the principle: 

Count the recent N bars and see if the closing prices show consecutive downward movement. If yes, a short signal is generated.

This sub-strategy identifies trend reversal by consecutive downward price movement.

### Combination of Signals 

The dual reversal trading strategy combines the two sub-strategies by only taking actual positions when both long or short signals are triggered at the same time.

This helps filter out some false signals and makes the trading signals more reliable. The combination of reversal and consecutive down signals can also more accurately identify trend reversal timing.

## Advantage Analysis

The dual reversal trading strategy has the following advantages:

1. Combining multiple sub-strategies helps filter out false signals effectively and improves reliability of signals.

2. The 123 reversal strategy can accurately identify short term trend reversal points. The N bar consecutive down strategy looks at medium-long term reversal. The two complement each other and capture short term opportunities at medium-long term levels.

3. Using technical indicators from stock charts makes the strategy flexible to adjust parameters for different products. 

4. The strategy logic is simple and easy to understand and track, suitable for beginners to learn.

5. Customizable parameters of sub-strategies allow optimization for different products, improving adaptability.

## Risk Analysis

There are also some risks associated with the dual reversal trading strategy:

1. Reversal signals may give false signals sometimes. Although the combined signals reduce false signals, the risk cannot be completely eliminated. It's recommended to use stops.

2. The sub-strategies use simple indicators and may not adapt well to complex market situations. More technical indicators or machine learning could be introduced to improve adaptability.

3. Sub-strategy parameters need optimization for different products, otherwise overfitting problems may occur.

4. Reversal strategies fit better for medium-long term. There are risks of being stopped out in the short term. Proper position holding period should be adjusted.

5. Reversal signals may come during range-bound corrections in a trend. Overall trend should be confirmed to ensure consistency with the major trend.

## Optimization Directions

The dual reversal trading strategy can be optimized in the following aspects:

1. Introduce more technical indicators, build a multi-factor model to improve adaptability to complex market situations. For example, combining with moving average, Bollinger bands etc.

2. Add machine learning models to take advantage of multi-dimensional features and improve signal accuracy. For example, introduce random forest or neural networks.

3. Optimize parameters for different products through training to improve adaptability. Genetic algorithm can be used to search for optimal parameter combinations.

4. Incorporate stop loss strategies to control single trade risks. Stop loss levels can also be data-driven optimized.

5. Develop dynamic position sizing mechanisms based on market conditions and sub-strategy signals to lower risks.

6. Introduce trend filtering modules to avoid signal contradictions with the overall trend. Simple moving averages can be used to determine trends.

## Conclusion

The dual reversal trading strategy efficiently captures trend reversals by combining the 123 reversal and N consecutive bars down sub-strategies. It fits better for medium-long term holdings and can filter out false signals to provide reliable trading opportunities during trend reversals. But there are also some limitations that need addressing through introducing more technical indicators and optimization, together with stop loss and position sizing to lower risks, in order to adapt to more complex market environments. Overall, it provides a simple and straightforward approach for trend reversal trading and serves as good learning materials for beginners to understand and learn about quantitative trading strategies. With more optimization techniques, it can become a very practical quantitative trading strategy.

[/trans]


> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|---- 123 Reversal ----|
|v_input_2|14|Length|
|v_input_3|true|KSmoothing|
|v_input_4|3|DLength|
|v_input_5|50|Level|
|v_input_6|true|---- N Bars Down ----|
|v_input_7|4|nLength|
|v_input_8|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-24 00:00:00
end: 2023-10-28 03:00:00
period: 10m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 24/03/2021
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
// Evaluates for n number of consecutive lower closes. Returns a value 
// of 1 when the condition is true or 0 when false.
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


NBD(nLength) =>
    pos = 0.0
    nCounter = 0
    nCounter :=  iff(close[1] <= open[1], nz(nCounter[1],0)+1,
                   iff(close[1] > open[1], 0, nCounter))
    C2 = iff(nCounter >= nLength, 1, 0)
    posprice = 0.0
    posprice := iff(C2== 1, close, nz(posprice[1], 0)) 
    pos := iff(posprice > 0, -1, 0)
    pos

strategy(title="Combo Backtest 123 Reversal & N Bars Down", shorttitle="Combo", overlay = true)
line1 = input(true, "---- 123 Reversal ----")
Length = input(14, minval=1)
KSmoothing = input(1, minval=1)
DLength = input(3, minval=1)
Level = input(50, minval=1)
//-------------------------
line2 = input(true, "---- N Bars Down ----")
nLength = input(4, minval=1)
reverse = input(false, title="Trade reverse")
posReversal123 = Reversal123(Length, KSmoothing, DLength, Level)
posNBD = NBD(nLength)
pos = iff(posReversal123 == 1 and posNBD == 1 , 1,
	   iff(posReversal123 == -1 and posNBD == -1, -1, 0)) 
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

https://www.fmz.com/strategy/430768

> Last Modified

2023-11-01 16:49:36
