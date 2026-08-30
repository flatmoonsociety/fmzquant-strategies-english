
> Name

Dual-Moving-Average-Reversal-Tracking-System
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/72f3bdd0a9d34e27fa265a69d6ac3db6714ddaa6daca08decc4cc95f11b7e5ac.png)
[trans]


## Overview
The dual-line tracking reversal moving average system combines the 123 pattern reversal strategy and the Ichimoku Balance Sheet strategy, aiming to explore reversal opportunities, track trends, and obtain excess returns.
## Strategy Principle
This strategy consists of two sub-strategies:
1. 123 pattern reversal strategy
This strategy trades based on price patterns. The specific logic is:
- When the closing price rises for two consecutive days and the 9-day slow K-line is below 50, go long
- When the closing price falls for two consecutive days and the 9-day fast K-line is above 50, go short
This strategy uses the price to break through the closing price of the previous day to determine the reversal, and uses the stock K-line combination indicator to filter out shock consolidation.
2. Ichimoku balance table strategy
This strategy is based on trading the five-line crossover of the Ichimoku Balance Sheet. The specific logic is:
- Go long when the closing price is above the baseline
- Go short when the closing price is below the conversion line
Among them, the base line is the midpoint of the highest price and the lowest price in the past 26 days, and the conversion line is the midpoint of the highest price and the lowest price in the past 9 days. This strategy uses a moving average crossover system to uncover trends.
The final strategy is merged based on the signals of the two sub-strategies, opening a position when they are bullish or bearish in the same direction, and closing a position when they are in different directions.
## Advantage Analysis
- Combining reversals and trends, you can capture reversal opportunities and track trends with flexible strategies.
- The 123 pattern is simple and practical, and can effectively identify critical reversal points.
- The parameters of the Ichimoku balance table have been optimized and the risk of breakthrough is small.
- The merger of two different types of strategies can achieve strategy optimization.
## Risk Analysis
- The reversal strategy is easy to be trapped and there is a risk of loss. The trading cycle can be appropriately shortened or stop loss can be added to control risks.
- The Ichimoku Balance Sheet is easily trapped in volatile market conditions. You can adjust parameters appropriately or add filtering conditions to reduce unnecessary transactions.
- When two strategies are combined, improper parameter matching may result in too frequent or sparse signals, which requires careful testing and optimization.
## Optimization direction
- Test more indicator combinations and find better filtering methods. For example, combined with energy indicators, etc.
- Optimize the parameters of the Ichimoku balance meter to make it more suitable for specific product characteristics.
- Add stop loss mechanism. Position stop loss can be set based on ATR.
- Add money management module to achieve risk control.
- Collect more data in backtesting, conduct multi-faceted testing of strategies, discover problems and continuously optimize.
## Summarize
The dual-line tracking reversal moving average system comprehensively uses the advantages of reversal and trend strategies to achieve excess returns through parameter optimization and strategy merger. This strategy has certain trading advantages, but there are also risks of being trapped and stopped. We need to continue to optimize the strategy logic during backtesting and supplement it with strict risk management measures to improve the stability and real performance of the strategy. Generally speaking, this strategy provides us with a good idea, which is to use different types of strategies to combine to obtain better overall results.
|| 

## Overview

The Dual Moving Average Reversal Tracking System integrates the 123 reversal pattern strategy and the Ichimoku strategy to identify reversal opportunities and track trends for excess returns. 

## Strategy Logic

The strategy consists of two sub-strategies:

1. 123 Reversal Pattern Strategy

This strategy trades based on price patterns. The logic is:

- Go long when the close price rises for two consecutive days and the 9-day slow stochastic is below 50.  

- Go short when the close price falls for two consecutive days and the 9-day fast stochastic is above 50.

It uses the breakout of previous day's close to determine reversals and uses stochastics to filter noise.

2. Ichimoku Strategy 

This strategy trades based on the five lines crossover of Ichimoku. The logic is:

- Go long when close price is above the baseline.

- Go short when close price is below the conversion line.

Where the baseline is the midpoint of the highest high and lowest low over the past 26 days, and the conversion line is the midpoint of the highest high and lowest low over the past 9 days. It uses moving average crossovers to identify trends.

The final strategy combines the signals from the two sub-strategies, entering when both signal long or short and exiting when they disagree.

## Advantage Analysis

- Combines reversal and trend-following, flexible in catching reversals and trends.

- 123 pattern is simple and effective in identifying reversals. 

- Ichimoku parameters are optimized, with lower breakout risk.

- Combining two different strategies can achieve optimization.

## Risk Analysis

- Reversal strategies are prone to traps and losses. Consider shorter holding periods or add stop loss to control risks.

- Ichimoku can experience whipsaws in range-bound markets. Fine-tune parameters or add filters to reduce unnecessary trades.

- Incompatible parameters when combining strategies may lead to too frequent or sparse signals. Require careful testing and optimization. 

## Optimization Directions

- Test more indicators for better filters, e.g. incorporating volume.

- Optimize Ichimoku parameters to fit instrument characteristics.

- Add stop loss mechanisms, e.g. set exits based on ATR. 

- Add money management module for risk control.

- Collect more data for robust backtesting, discover issues and iterate.

## Conclusion

The Dual Moving Average Reversal Tracking System combines the strengths of reversal and trend-following strategies through optimization and combination for alpha generation. It has trading merits but risks like whipsaws and stop loss exist. We need to keep improving the logic in backtests and implement proper risk control for stability and real-world performance. Overall it provides a good approach of combining different strategies for better overall results.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Length|
|v_input_2|true|KSmoothing|
|v_input_3|3|DLength|
|v_input_4|50|Level|
|v_input_5|9|conversionPeriods|
|v_input_6|26|basePeriods|
|v_input_7|52|laggingSpan2Periods|
|v_input_8|26|displacement|
|v_input_9|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-07 00:00:00
end: 2023-11-06 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 26/11/2020
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
//  Ichimoku Strategy
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

middleDonchian(Length) =>
    lower = lowest(Length)
    upper = highest(Length)
    avg(upper, lower)    
    
Ichimoku2c(conversionPeriods, basePeriods,laggingSpan2Periods,displacement) =>
    pos = 0.0
    Tenkan = middleDonchian(conversionPeriods)
    Kijun =  middleDonchian(basePeriods)
    xChikou = close
    SenkouA = middleDonchian(laggingSpan2Periods)
    SenkouB = (Tenkan[basePeriods] + Kijun[basePeriods]) / 2
    pos := iff(close < SenkouA[displacement], -1,
              iff(close > SenkouB, 1, nz(pos[1], 0))) 
    pos

strategy(title="Combo Backtest 123 Reversal & Ichimoku2c", shorttitle="Combo", overlay = true)
Length = input(14, minval=1)
KSmoothing = input(1, minval=1)
DLength = input(3, minval=1)
Level = input(50, minval=1)
//-------------------------
conversionPeriods = input(9, minval=1),
basePeriods = input(26, minval=1)
laggingSpan2Periods = input(52, minval=1),
displacement = input(26, minval=1)
reverse = input(false, title="Trade reverse")
posReversal123 = Reversal123(Length, KSmoothing, DLength, Level)
posIchimoku2c = Ichimoku2c(conversionPeriods, basePeriods,laggingSpan2Periods,displacement)
pos = iff(posReversal123 == 1 and posIchimoku2c == 1 , 1,
	   iff(posReversal123 == -1 and posIchimoku2c == -1, -1, 0)) 
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

https://www.fmz.com/strategy/431407

> Last Modified

2023-11-07 16:00:33
