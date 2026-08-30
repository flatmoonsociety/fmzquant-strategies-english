
> Name

Moving-Average-Crossover-Long-Short-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/11eb458b6f407531342.png)
[trans]

## Overview
This strategy is a long- and short-term trading strategy based on moving averages. It uses a fast simple moving average (SMA) and a slow simple moving average, going long when the fast SMA crosses above the slow SMA and short when the fast SMA crosses below the slow SMA.
## Strategy Principle
This strategy uses two SMA indicators: a 20-day fast SMA and a 50-day slow SMA. When the short-term fast SMA crosses the long-term slow SMA from below, it means that the market trend has turned upward, and it is time to go long. When the fast SMA crosses the slow SMA from above, it means that the market trend has turned downward, and it is time to go short.
Specifically, if the fast SMA crosses above the slow SMA, open a long position. If the fast SMA crosses below the slow SMA, open a short position. Close the position when the opposite SMA cross occurs.
## Advantage Analysis
This SMA crossover strategy is simple to use, easy to understand and implement. Compared with other technical indicators, the SMA indicator has less delay and can capture trend changes more sensitively.
Using two fast and slow SMAs can play a filtering role. Fast SMA captures short-term trends, while slow SMA filters out noise. Their crossover helps capture turning points in mid- to long-term trends.
This strategy has low trading frequency and is suitable for long-term investors. It only opens positions when the SMA crosses, avoiding unnecessary trades.
## Risk Analysis
There may be some lag in this strategy. Due to the hysteresis of SMA itself, there is a certain lag in the time when this strategy generates signals sooner or later. This may result in the loss of some profits.
When the stock price jumps or the short-term trend reverses, the fast and slow SMA may send wrong signals, leading to unnecessary losses. At this time, the psychological quality of investors will be tested.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Adjust the period parameters of fast and slow SMA to optimize the crossover effect
2. Add filtering of other technical indicators, such as MACD, KD, etc., to improve signal accuracy
3. Add stop loss strategy to control single loss
4. Adjust parameters based on the characteristics of individual stocks.
## Summary
Overall, this strategy is a simple and practical long-term trading strategy. It uses the principle of moving average crossover to give trading signals at the turning point of the general trend. At the same time, combined with fast and slow SMA double moving average filtering, it can effectively reduce false signals. This strategy is easy to understand and implement, is suitable for most long-term investors, and is a recommended quantitative trading strategy. Through parameter optimization and the increase of auxiliary technical indicators, this strategy can achieve better strategy effects.
||

## Overview  
This strategy is a long-short trading strategy based on moving average crossover. It uses fast simple moving average (SMA) and slow SMA. When fast SMA crosses above slow SMA, go long. When fast SMA crosses below slow SMA, go short.  

## Strategy Logic
The strategy uses two SMA indicators: a 20-day fast SMA and a 50-day slow SMA. When short-term fast SMA crosses above long-term slow SMA from below, it indicates the market trend is turning bullish, so go long. When fast SMA crosses below slow SMA from above, it indicates the market trend is turning bearish, so go short.   

Specifically, if fast SMA crosses above slow SMA, open long position. If fast SMA crosses below slow SMA, open short position. Close position when the opposite SMA crossover occurs.  

## Advantage Analysis
This SMA crossover strategy is simple to use and understand. Compared to other technical indicators, SMA has smaller lagging and can capture trend changes more sensitively.  

Using double fast and slow SMA acts as a filter. Fast SMA captures short-term moves while slow SMA filters out noises. Their crossover helps capture mid-long term trend turning points.  

The strategy has relatively low trading frequency suitable for long-term investors. It only opens position on SMA crossovers, avoiding unnecessary trades. 

## Risk Analysis  
The strategy may have some lagging. Due to the lagging nature of SMA itself, there can be certain delay in the timing of signal generation. This may lead to loss of some profits.

When price gaps or short-term reversal occurs, fast and slow SMA may give out false signals, resulting in unnecessary losses. This tests investor's psychological quality.  

## Optimization  

The strategy can be optimized from the following aspects:

1. Adjust fast and slow SMA periods to optimize crossover effect   
2. Add other technical indicator filters e.g. MACD, KD to improve signal accuracy
3. Add stop loss to control single trade loss  
4. Adjust parameters based on individual stock characteristics   

## Conclusion
Overall this is a simple and practical long term trading strategy. It gives trading signals around major trend turning points based on the principle of moving average crossover. Coupling fast and slow double SMA acts as effective filter to reduce false signals. The strategy is easy to understand and implement, suitable for most long-term investors. It is a recommended quantitative trading strategy. Further improvements can be made through parameter tuning and adding complementary technical indicators.
[/trans]]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|SMA Veloce|
|v_input_2|50|SMA Lenta|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-14 00:00:00
end: 2023-12-21 00:00:00
period: 3m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © forsakenMaster81726

//@version=5
strategy("Il mio script", overlay=true)

// Imposta le medie mobili
fastLength = input(20, title="SMA Veloce")
slowLength = input(50, title="SMA Lenta")

smaFast = ta.sma(close, fastLength)
smaSlow = ta.sma(close, slowLength)

// Crossover SMA (Veloce sopra Lenta)
bullishCrossover = ta.crossover(smaFast, smaSlow)

// Crossunder SMA (Veloce sotto Lenta)
bearishCrossover = ta.crossunder(smaFast, smaSlow)

// Regole di trading
strategy.entry("Long", strategy.long, when=bullishCrossover)
strategy.close("Long", when=bearishCrossover)

strategy.entry("Short", strategy.short, when=bearishCrossover)
strategy.close("Short", when=bullishCrossover)

// Plot delle medie mobili sul grafico
plot(smaFast, color=color.green, title="SMA Veloce")
plot(smaSlow, color=color.red, title="SMA Lenta")

// Plot del prezzo
plot(close, color=color.blue, title="Prezzo")

```

> Detail

https://www.fmz.com/strategy/436254

> Last Modified

2023-12-22 15:13:50
