
> Name

Strategy-Based-on-5-10-20-Day-EMA-Crossover-Using-Super-Trend-Confirmation
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/124e1b5c8ab66817e1b.png)
 [trans]

## Overview
This strategy generates buy and sell signals by calculating the 5-, 10-, and 20-day exponential moving averages (EMA), combined with overtrend indicators. When the 5-day line crosses the 10-day line, and both the 5-day and 10-day lines cross above the 20-day line, a buy signal is generated; when the 10-day line crosses below the 5-day line, and both the 5-day and 10-day lines cross below the 20-day line, a sell signal is generated.
## Strategy Principle
1. Calculate the 5-day EMA, 10-day EMA and 20-day EMA.
2. Calculate supertrend indicators.
3. When the 5-day EMA is greater than the 10-day EMA, and both the 5-day EMA and the 10-day EMA are greater than the 20-day EMA, that is, the 5-day line and the 10-day line cross the 20-day line, generating a buy signal.  
4. When the 10-day EMA is less than the 5-day EMA, and both the 5-day EMA and the 10-day EMA are less than the 20-day EMA, that is, the 5-day line and the 10-day line cross below the 20-day line, generating a sell signal.
5. At the same time, combined with the super-trend indicator to determine the market trend, a buy signal will be generated only when the super-trend indicator shows a downward trend, and a sell signal will be generated when the trend is upward.

## Strategic Advantages
1. Simple and effective, easy to understand and implement.  
2. Combined with three moving averages and super trends, the signal judgment is more accurate and reliable.  
3. Use the three moving averages of the 5th, 10th and 20th to have a comprehensive vision and accurately judge short-term, medium-term and long-term trends.
4. Avoid being manipulated by large-scale market making by considering the combination of super-trend judgment technology and short- and medium-term moving average technology.
5. The configurable parameters are flexible and can be adjusted and optimized for different varieties and market conditions.
6. Detect trading opportunities accurately and have a high profit-loss ratio.
7. Simple to implement, easy to understand, easy to expand and customize.
## Strategy Risk
1. In a market with severe market fluctuations, there are many false signals, and it is easy to make mistakes in exit timing. 
2. The moving average system is very sensitive to parameters, and improper parameter settings may lead to losses.
3. There is a lag in the long-short judgment of super trend, and it needs to be confirmed in combination with other technical indicators.
4. Unable to cope with extreme market conditions, such as plummets and instantaneous short jumps.
**Solutions for major risks:**
1. Combine with more technical indicators or fundamental analysis to confirm the signal again.  
2. Add a stop-loss strategy to avoid loss expansion.  
3. Optimize parameter settings by combining short-term and medium- and long-term indicators. 
4. Monitor the volatility of the index and the performance of super-trend indicators in real time, and intervene manually when necessary.
## Strategy optimization direction
1. Combine more moving average systems and technical indicators for judgment, such as MACD, KD, etc.
2. Add automatic stop loss and take profit strategies.
3. Optimize the parameters of super trend and moving average systems according to different varieties and market conditions.  
4. Add model evaluation and perform parameter optimization and strategy optimization based on historical data.
5. Add a machine learning prediction module to determine price trends and potential trading opportunities.

## Summarize
This strategy uses three moving averages on the 5th, 10th and 20th as well as super trend indicators to construct a trading strategy. The strategy is simple and efficient, and performs well in trend judgment and opportunity discovery. It also has strong customizability and scalability. There is a large space for optimization, and the strategy performance can be continuously improved by adjusting parameters, adding technical indicators, and adding machine learning to adapt to more complex market environments.
||

## Overview  

This strategy calculates the 5-day, 10-day and 20-day exponential moving average (EMA) lines and uses the Super Trend indicator to generate buy and sell signals. It generates buy signals when the 5-day EMA crosses above the 10-day EMA and both the 5-day and 10-day EMA cross above the 20-day EMA. It generates sell signals when the 10-day EMA crosses below the 5-day EMA and both the 5-day and 10-day EMA cross below the 20-day EMA.  

## Strategy Logic   

1. Calculate the 5-day EMA, 10-day EMA and 20-day EMA.  
2. Calculate the Super Trend indicator.
3. When 5-day EMA is greater than 10-day EMA, and both 5-day and 10-day EMA are greater than 20-day EMA, which means 5-day and 10-day EMA cross above 20-day EMA, generate buy signal.   
4. When 10-day EMA is less than 5-day EMA, and both 5-day and 10-day EMA are less than 20-day EMA, which means 5-day and 10-day EMA cross below 20-day EMA, generate sell signal.  
5. Also use Super Trend indicator to determine market trend. Generate buy signals only when Super Trend shows downward trend, and generate sell signals only when Super Trend shows upward trend.

## Advantages of the Strategy  

1. Simple and effective, easy to understand and implement.   
2. More accurate and reliable signals by combining three EMA lines and Super Trend indicator.
3. Comprehensive judgement on short-term, medium-term and long-term trends using 5-day, 10-day and 20-day EMA.  
4. Avoid being manipulated by combining technical and momentum indicators.  
5. Flexible adjustable parameters for different products and market conditions.  
6. Accurate detection of trading opportunities with high risk-reward ratio.  
7. Simple to understand, easy to extend and customize.  

## Risks of the Strategy   

1. More false signals may occur during violent market fluctuation. Exits may not be timely.  
2. EMA system is sensitive to parameters. Improper settings may lead to losses. 
3. Super Trend trend judgment has lagging effect. Needs confirmation from other indicators.  
4. Cannot cope with extreme market events like flash crash.  

**Solutions to Major Risks:**

1. Add more technical indicators or fundamental analysis to confirm signals.   
2. Add stop loss strategy to limit losses.
3. Optimize parameters by combining short-term and long-term indicators.  
4. Monitor index volatility and Super Trend performance. Manually intervene if necessary.  

## Directions for Strategy Optimization  

1. Add more EMA systems and technical indicators like MACD, KD etc.  
2. Add auto stop loss, take profit features.
3. Optimize Super Trend and EMA parameters based on different products and market conditions.   
4. Add backtesting to optimize parameters and strategy based on historical data.  
5. Add machine learning prediction model to forecast price trends and potential trading opportunities.

## Summary   

The strategy uses 5-day, 10-day and 20-day EMA together with Super Trend indicator. It is simple yet effective, performs great in trend identification and opportunity discovery. Highly customizable and extensible. Huge room for optimization via parameter tuning, adding more indicators and machine learning models to continuously improve strategy performance in more complex market environments.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|5|EMA 1|
|v_input_2|10|EMA 2|
|v_input_3|20|EMA 3|
|v_input_4|2|mult|
|v_input_5|14|len|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-12 00:00:00
end: 2023-12-18 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © aadilpatel07

//@version=4
strategy("5-10-20 Cross", overlay=true)
src = close, 
len1 = input(5, minval=1, title="EMA 1")
len2 = input(10, minval=1, title="EMA 2")
len3 = input(20, minval=1, title="EMA 3")

mult = input(type=input.float, defval=2)
len = input(type=input.integer, defval=14)
[superTrend, dir] = supertrend(mult, len)

ema1 = ema(src, len1)
ema2 = ema(src, len2)
ema3 = ema(src, len3)

//EMA Color
col1 = color.lime
col2 = color.blue
col3 = color.red

//EMA Plots
plot(series=ema1,color=col1, title="EMA1")
plot(series=ema2,color=col2, title="EMA2")
plot(series=ema3,color=col3, title="EMA3")

//plot SuperTrend
colResistance = dir == 1 and dir == dir[1] ? color.new(color.red, 100) : color.new(color.green, 100)
colSupport = dir == -1 and dir == dir[1] ? color.new(color.green, 0) : color.new(color.green, 10)
plot(superTrend, color = colResistance, linewidth=1)
plot(superTrend, color = colSupport, linewidth=1)

//longCondition = crossover(ema1, ema2) and crossover(ema1,ema3) and crossover(ema2,ema3)
longCondition = ema1 > ema2 and ema1 > ema3 and ema2 > ema3 and ema2 < ema1 and dir == -1
if (longCondition)
    strategy.entry("My Long Entry Id", strategy.long)

//shortCondition = crossover(ema2, ema1) and crossover(ema3,ema1) and crossover(ema3,ema2)
shortCondition = ema1 < ema2 and ema1 < ema3 and ema2 < ema3 and ema2 > ema1 and dir == 1
if (shortCondition)
    strategy.entry("My Short Entry Id", strategy.short)
```

> Detail

https://www.fmz.com/strategy/435828

> Last Modified

2023-12-19 10:39:36
