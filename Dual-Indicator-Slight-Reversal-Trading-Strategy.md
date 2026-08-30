
> Name

Dual-Indicator-Slight-Reversal-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/2fdceeadb11ba95a5af88111b7285f4fb2cf471b18c9498a6e36114a198c4e70.png)

[trans]

## Overview
The dual-indicator slight reversal trading strategy is a short-term trading strategy that combines momentum indicators and trend indicators. This strategy first uses a reversal indicator to generate trading signals, and then combines it with a trend indicator to generate more reliable trading signals. This strategy is designed to capture short-term price reversals and trade against the backdrop of short- and medium-term trends.
## Principle
This strategy consists of two sub-strategies.
The first sub-strategy is the 123 reversal strategy. It monitors prices for signs of a pullback from highs. Specifically, it generates a buy signal when: the previous two days' closing price fell, the current day's closing price is higher than the previous day's closing price, and the Stochastic slow line is below 50. It generates a sell signal when the closing price of the previous two days is higher, the closing price of the current day is lower than the closing price of the previous day, and the Stochastic line is above 50.
The second sub-strategy is the ergodic stochastic indicator (EMDI). It is a trend indicator that identifies the direction of the mid- to long-term trend. It combines the ideas of moving averages and MACD, and uses the intersection of the one-time exponentially smoothed moving average and the fast and slow lines of MACD to generate buy and sell signals.
This strategy combines the signals of two sub-strategies. The strategy will only open a position when both sub-strategies generate consistent signals. In other words, it only trades when there is a slight reversal in the short term and strong medium and long-term trend support.
## Advantages
- Combining multiple indicators can effectively filter out false signals and improve signal reliability.
- The combination of reversal strategy and trend strategy can not only capture short-term opportunities but also avoid contrarian trading.
- The parameter settings using the Stochastic indicator are more robust and can reduce whipsaws. 
- The smoothing parameters of the Ergodic indicator are set reasonably and the trend can be better identified.
- The trading frequency of this strategy is moderate, so you can get more trading opportunities without trading too frequently.
- Suitable for short- and medium-term transactions with flexible time periods.
## Risk
- Reversal signals may contain false positives and require verification by trend indicators.
- The trading frequency is not high and some short-term opportunities may be missed.
- After the reversal, it may reverse again, so you need to stop the loss in time.  
- Improper parameter settings may have a greater impact on transaction results.
- Too much reliance on technical indicators may lead to the risk of model overfitting.
## Optimization direction
- You can test different parameter settings and optimize the performance of sub-strategies.
- More indicators can be introduced to build a multi-factor model.  
- Can be combined with machine learning methods to achieve dynamic parameter optimization.
- You can study different stop loss methods to control risks.
- You can study the opportunity cost and adjust the trading frequency of the strategy.
- Ability to test strategy robustness in different market environments.
## Summarize
The dual-indicator slight reversal trading strategy attempts to capture short-term price reversal opportunities on the medium and short-term lines through a combination of reversal and trend indicators. It can effectively filter false positive signals and control trading risks to a certain extent. However, this strategy also has some problems, such as the possibility of missing short-term opportunities, parameter sensitivity, and the risk of over-fitting. The stability and profitability of this strategy can be further enhanced by introducing more indicators, optimizing parameter settings, adjusting trading frequency, and testing in different markets. Generally speaking, the dual-indicator slight reversal trading strategy is a simple and practical quantitative strategy idea that is worth exploring and applying.
|| 

## Overview

The Dual Indicator Slight Reversal Trading Strategy combines momentum and trend-following indicators for short-term trading. The strategy first generates trading signals using a reversal indicator, then combines it with a trend-following indicator to produce more reliable signals. It aims to capture short-term price reversals within the context of medium-term trends.

## Principle 

The strategy consists of two sub-strategies. 

The first is the 123 Reversal strategy. It monitors if a peak reversal pattern occurs. Specifically, it will generate a long signal if the closing price of the prior two days drops and the current closing price is higher than the previous closing price, with the Stochastic slow line below 50. It will generate a short signal if the closing prices of the prior two days rise and the current closing price is lower than the previous closing price, with the Stochastic fast line above 50.

The second is the Ergodic indicator, which is a trend-following indicator identifying the direction of medium to long term trends. It incorporates the ideas of moving averages and MACD, using single exponential smoothed moving averages and MACD's fast and slow lines crossovers to generate trading signals.

The strategy combines the signals from the two sub-strategies. It will only open a position when the two sub-strategies generate consistent signals. That is, it only trades when there is a short-term slight reversal along with a strong medium to long term trend. 

## Advantages

- Combining multiple indicators can effectively filter false signals and improve reliability.

- Combining reversal and trend-following provides both short-term opportunities and avoids counter-trend trades.

- The Stochastic parameter settings are quite robust to reduce whipsaws.

- The smoothing parameters of the Ergodic indicator are reasonably set to better identify trends.

- The trading frequency is appropriate, capturing adequate opportunities without overtrading.

- Suitable for medium-term trading with flexible timeframes.

## Risks

- Reversal signals may produce false signals and need validation from trend indicators.

- The low trading frequency may miss some short-term opportunities. 

- There could be reversals after reversals, requiring timely stop loss.

- Inappropriate parameter settings may significantly impact results.

- Relying too much on technical indicators risks overfitting. 

## Enhancement

- Test different parameter settings to optimize sub-strategies.

- Introduce more indicators to build multi-factor models.

- Apply machine learning for dynamic parameter optimization. 

- Research different stop loss methods to control risks.

- Study opportunity costs and adjust strategy trading frequency.

- Test strategy robustness across different market regimes.

## Conclusion

The Dual Indicator Slight Reversal Trading Strategy attempts to capture short-term reversal opportunities on medium-term timeframes using combinations of reversal and trend-following indicators. It can effectively filter false signals and control risks to some extent. However, issues like missing short-term opportunities, parameter sensitivity, and overfitting risks remain. Further enhancing stability and profitability can be achieved by incorporating more indicators, optimizing parameters, adjusting trading frequency, and testing across markets. Overall, the strategy represents a simple and practical quantitative approach worth exploring and applying.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Length|
|v_input_2|true|KSmoothing|
|v_input_3|3|DLength|
|v_input_4|50|Level|
|v_input_5|32|r|
|v_input_6|5|s|
|v_input_7|5|u|
|v_input_8|3|SmthLen|
|v_input_9|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-09 00:00:00
end: 2023-10-16 00:00:00
period: 15m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 28/07/2020
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
// This is one of the techniques described by William Blau in his book "Momentum,
// Direction and Divergence" (1995). If you like to learn more, we advise you to
// read this book. His book focuses on three key aspects of trading: momentum, 
// direction and divergence. Blau, who was an electrical engineer before becoming 
// a trader, thoroughly examines the relationship between price and momentum in 
// step-by-step examples. From this grounding, he then looks at the deficiencies 
// in other oscillators and introduces some innovative techniques, including a 
// fresh twist on Stochastics. On directional issues, he analyzes the intricacies 
// of ADX and offers a unique approach to help define trending and non-trending periods. 
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


EMDI(r,s,u,SmthLen) =>
    pos = 0
    xEMA = ema(close, r)
    xEMA_S = close - xEMA
    xEMA_U = ema(ema(xEMA_S, s), u)
    xSignal = ema(xEMA_U, u)
    pos := iff(xEMA_U > xSignal, 1,
    	     iff(xEMA_U < xSignal, -1, nz(pos[1], 0)))
    pos

strategy(title="Combo Backtest 123 Reversal & Ergodic MDI", shorttitle="Combo", overlay = true)
Length = input(14, minval=1)
KSmoothing = input(1, minval=1)
DLength = input(3, minval=1)
Level = input(50, minval=1)
//-------------------------
r = input(32, minval=1)
s = input(5, minval=1)
u = input(5, minval=1)
SmthLen = input(3, minval=1)
reverse = input(false, title="Trade reverse")
posReversal123 = Reversal123(Length, KSmoothing, DLength, Level)
posEMDI = EMDI(r,s,u,SmthLen)
pos = iff(posReversal123 == 1 and posEMDI == 1 , 1,
	   iff(posReversal123 == -1 and posEMDI == -1, -1, 0)) 
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

https://www.fmz.com/strategy/429488

> Last Modified

2023-10-17 15:45:09
