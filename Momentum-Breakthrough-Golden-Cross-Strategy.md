
> Name

Momentum-Breakthrough-Golden-Cross-Strategy Momentum-Breakthrough-Golden-Cross-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/d3c6e7cf2064e3fbcf9ca45bfecf62e54de603f3eb50c5b88366cc6d54e6ee4c.png)
[trans]
## Overview
This is a quantitative trading strategy that combines MACD, RSI and EMA moving averages. It uses the MACD golden cross to go long, the RMSI high reversal and the price falling below the EMA moving average as a stop-loss exit method to achieve the effect of tracking the long-term market trend.
## Strategy Principle
This strategy is mainly based on the following three indicators for trading signal judgment and strategy implementation:
1. MACD: Calculate fast line, slow line and MACD column. The strategy uses the golden cross of the fast and slow lines to judge the buying time.
2. RSI: Calculate the 14-period RSI value and set the overbought and oversold lines. The strategy uses the weekly RSI high reversal to avoid the risk of overbought.
3. EMA: Calculate the 50-day EMA. The strategy sets a stop loss point when the price falls below the moving average to control the risk of loss.
A buy signal is generated when the MACD fast line breaks above the slow line from below to form a golden cross. At the same time, it is required that the weekly RSI indicator at this time is higher than 50, which means it is in an overbought state, which is helpful to grasp the upward trend of this round of market. Finally, the actual buy operation will not be executed until the price is above the 50-day EMA.
If the price falls below the 50-day EMA moving average or the MACD fast and slow line crosses, stop loss and liquidation operations will be executed.
## Advantage Analysis
This strategy combines the advantages of the three indicators MACD, RSI and EMA to achieve a better breakthrough tracking function.
1. The MACD Golden Cross has a certain advance nature and can capture the market’s buying opportunities earlier.
2. Based on the weekly RSI, it can effectively filter out the short-term overbought phenomenon and grasp the medium and long-term rising trend of this round.
3. EMA stop loss can promptly stop the sudong market and effectively control DD.
4. Overall, this strategy can successfully capture breakthrough opportunities in the medium and long term, and can earn good returns after the market breaks through upward.
## Risk Analysis
The following risks need to be noted:
1. The MACD Golden Cross has a certain degree of lag and may miss the best buying point in the market.
2. The parameter settings of RSI and EMA need to be repeatedly tested and optimized, otherwise they may fail.
3. The best buying point for a market breakthrough does not necessarily occur at the golden cross moment, and there is a certain timing risk.
4. If the stop loss setting is too loose, it may lead to greater DD. If the stop loss setting is too strict, it may be easily broken by a breakthrough positive line.
## Optimization direction
This strategy also has the following optimization directions:
1. You can test and optimize the MACD parameter combination to find a better balance point.
2. RSI cycles and overbought and oversold lines can also be parameter optimized.
3. The moving period of EMA can also be adjusted appropriately to find better parameters.

4. The buying opportunity can be confirmed twice based on advanced technical indicators, such as a combination of KDJ indicators, etc.
5. You can test the stop loss and exit strategy, using percentage moving stop loss or quantitative stop loss strategy to make the stop loss more intelligent.
## Summarize
Generally speaking, this strategy is a relatively typical tracking medium and long-term strategy. It combines multiple indicators such as MACD, RSI and EMA to judge the buying time in order to obtain a better entry point. At the same time, stop-loss measures will be taken to control trading risks. This strategy is suitable for medium and long-term tracking investors, and there is room for further optimization. If the parameters are adjusted properly, considerable benefits can be obtained.
||

## Overview

This is a quantitative trading strategy that combines MACD, RSI and EMA moving average. It uses MACD golden cross for long entry, RMSI overbought reversal and price breakout below EMA as stop loss exit to track the middle-to-long term trends in the market.  

## Principles

The strategy mainly uses the following three indicators for trading signal judgment and strategy implementation:

1. MACD: Calculate fast line, slow line and MACD histogram. The strategy judges the timing of entry by the golden cross of fast and slow lines.  

2. RSI: Calculate the 14-period RSI and set the overbought/oversold line. The strategy utilizes the RSI overbought reversal on weekly timeframe to avoid overbought risk.

3. EMA: Calculate the 50-day EMA line. The strategy sets the stop loss point by the price breakout below this line to control the risk of loss.

A buy signal is generated when the MACD fast line crosses above the slow line from below forming a golden cross. At the same time, require the weekly RSI indicator to be above 50, indicating an overbought state, which helps to grasp the upward trend of this round of market. Finally, a long entry will only be executed when the price is above the 50-day EMA line.  

If the price breaks below the 50-day EMA or a MACD dead cross occurs, a stop loss exit will be executed.

## Advantage Analysis 

The advantage of this strategy combines MACD, RSI and EMA indicators to achieve good breakthrough tracking capability:

1. MACD golden cross has some lead characteristic that can capture the buy timing of the market earlier. 

2. Based on weekly RSI, it can effectively filter out short-term overbought scenarios and grasp the middle-to-long term uptrend.  

3. The EMA stop loss can make timely stop losses on sudden down trends, effectively controlling DD.

4. Overall, this strategy can smoothly capture middle-to-long term breakthrough opportunities and gain decent returns after the market breaks out upwards.


## Risk Analysis   

Pay attention to the following risks:

1. MACD golden cross has some lagging properties that may miss the optimal entry point of the market.  

2. The parameter settings of RSI and EMA need repeated testing and optimization, otherwise they may become invalid. 

3. The best buying point of a breakthrough market does not necessarily appear at the moment of golden cross, there is some timing risk.  

4. A stop loss set too loose may lead to larger DD, while a stop loss set too tight may easily be broken by breakthrough yang line.

## Optimization Directions

There are still several optimization directions for this strategy:

1. Test and optimize the MACD parameter combination to find a better balance point.

2. The RSI cycle and overbought/oversold line can also be optimized.  

3. The moving cycle of EMA can also be adjusted appropriately to find better parameters.

4. Secondary confirmation of the entry timing can be made based on advanced technical indicators, such as the KDJ indicator.

5. Test stop loss exit strategies by adopting percentage-based moving stop loss or quantitative stop loss to make the stop loss smarter.

## Conclusion

In general, this strategy is a typical mid-to-long term tracking strategy. It combines multiple indicators such as MACD, RSI and EMA to judge the timing of entry in order to obtain a better entry point. It also adopts stop loss measures to control trading risks. The strategy suits middle-to-long term tracking investors, and there is still room for further optimization. With proper parameter tuning, decent returns can also be obtained.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|5|Fast Length|
|v_input_2|13|Slow Length|
|v_input_3|9|Signal Length|
|v_input_4|21|EMA Length|
|v_input_5|14|RSI Length|
|v_input_6|50|RSI Overbought Level|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("MACD, EMA, and RSI Strategy", overlay=true)

// Input for MACD
fastLength = input(5, title="Fast Length")
slowLength = input(13, title="Slow Length")
signalLength = input(9, title="Signal Length")

// Input for EMA
emaLength = input(21, title="EMA Length")

// Input for RSI
rsiLength = input(14, title="RSI Length")
rsiOverbought = input(50, title="RSI Overbought Level")

// Calculate MACD on the weekly timeframe
[macdLine, signalLine, _] = ta.macd(close, fastLength, slowLength, signalLength)

// Calculate 50-day EMA
ema50 = ta.ema(close, emaLength)

// Calculate RSI on the weekly timeframe
rsi = ta.rsi(close, rsiLength)

// Condition for Buy Entry
buyCondition = ta.crossover(macdLine, 0) and dayofweek == dayofweek.monday and rsi > rsiOverbought

// Condition for Sell Exit
sellCondition = ta.crossunder(close, ema50) or ta.crossunder(macdLine, 0)

// Execute Buy Entry on the next day's open
if buyCondition
    strategy.entry("My Long Entry Id", strategy.long)

// Execute Sell Exit on the next day's open
if sellCondition
    strategy.close("My Long Entry Id")

// Plotting MACD and EMA
plot(macdLine - signalLine, title="MACD Histogram", color=color.blue, style=plot.style_histogram)
hline(0, "Zero Line", color=color.gray)
plot(ema50, title="50-day EMA", color=color.red)

// Plotting RSI
hline(rsiOverbought, "RSI Overbought", color=color.red)
plot(rsi, title="RSI", color=color.green)

```

> Detail

https://www.fmz.com/strategy/440313

> Last Modified

2024-01-29 11:27:31
