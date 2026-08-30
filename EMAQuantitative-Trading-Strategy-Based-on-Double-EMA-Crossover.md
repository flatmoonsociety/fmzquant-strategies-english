
> Name

Quantitative-Trading-Strategy-Based-on-Double-EMA-Crossover
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/17df18e531d65a4fe64.png)
[trans]

## Overview
This strategy determines the market trend by calculating the intersection of the EMA moving averages of two different periods and generates trading signals accordingly. When the short-period EMA crosses the long-period EMA, it is considered that the market has entered an upward trend, and this strategy will open a long position; when the short-period EMA crosses below the long-period EMA, it is considered that the market has entered a downward trend, and the strategy will close the position and exit.
## Strategy Principle
This strategy mainly applies the golden cross and dead cross theory of double EMA moving average. The double EMA moving average is divided into long-term EMA and short-term EMA. The short-term EMA parameters are set to 10 days, and the long-term EMA parameters are set to 21 days.
When the short-term EMA crosses above the long-term EMA, a buy signal is generated; when the short-term EMA crosses below the long-term EMA, a sell signal is generated. This strategy also sets a growth rate threshold. A long position will be opened only when the growth rate exceeds the threshold, and a long position will be closed when the decline exceeds the threshold.
Specifically, the buying condition is that the short-term EMA is higher than the long-term EMA, and the stock price growth rate exceeds the set positive threshold; the closing condition is that the short-term EMA is lower than the long-term EMA, and the stock price growth rate is lower than the set negative threshold.
## Strategic Advantages
- The golden cross and dead cross theory using double EMA moving average is relatively simple and reliable
- Added growth rate threshold setting to avoid wrong transactions when growth is weak
- The maximum loss ratio can be strictly controlled
- EMA moving average parameters can be flexibly adjusted, suitable for different periods
## Risk Analysis
- EMA moving average has hysteresis and may miss the price reversal point
- Moving average crossovers have a certain hysteresis, which may result in losing the best opportunity to open a position.
- Need to rely on parameter optimization. Improper parameter setting may lead to frequent transactions or insufficient signals.
## Optimization direction
- Optimize in combination with other indicators, such as MACD, KD, etc., to improve signal accuracy
- Add stop loss strategies, such as trailing stop loss, to ensure profit maximization
- Optimize EMA cycle parameters and set the best parameters for different varieties
- Combine real-time data and machine learning methods for dynamic parameter adjustment and optimization
## Summarize
This strategy is relatively simple and reliable overall. It judges the price trend through double EMA crossover and sets the growth rate threshold to send trading signals. Compared with a single moving average crossover, some false signals can be filtered out. However, the EMA moving average itself has a hysteresis problem. Combining it with other indicators or dynamic parameter adjustment can further improve the strategy effect.
|| 


## Overview

This strategy generates trading signals by calculating the crossover between two EMA lines of different periods to determine market trends. It will open long positions when the shorter period EMA crosses over the longer period EMA, indicating an uptrend, and it will close positions when the shorter period EMA crosses below the longer period EMA, indicating a downtrend.  

## Principles  

The strategy mainly applies the golden cross and death cross theory of double EMA lines. The double EMA lines consist of a long EMA and a short EMA. The short EMA parameter is set to 10 days and the long EMA parameter is set to 21 days.  

When the short EMA crosses over the long EMA, a buy signal is generated. When the short EMA crosses below the long EMA, a sell signal is generated. The strategy also sets growth rate thresholds, opening long positions only when growth exceeds a positive threshold and closing positions only when decline exceeds a negative threshold.   

Specifically, the buy condition is when the short EMA is higher than the long EMA and the stock growth rate exceeds the positive threshold. The close position condition is when the short EMA is lower than the long EMA and the stock growth rate falls below the negative threshold.  

## Advantages  

- Utilizes the golden cross and death cross theory of double EMA lines for simplicity and reliability
- Adds growth rate thresholds to avoid erroneous trades during weak growth  
- Can strictly control maximum loss ratio
- EMA period parameters can be flexibly adjusted for different cycles  

## Risk Analysis   

- EMA lines have lagging effects, possibly missing price reversal points
- Line crossovers have some lag, possibly missing best entry points  
- Relies on parameter optimization, improper settings may cause overtrading or insufficient signals  

## Optimization Directions  

- Combine with other indicators like MACD, KD etc. to improve signal accuracy
- Add stop loss strategies like trailing stop loss to maximize profits
- Optimize EMA period parameters for best settings across different products   
- Incorporate real-time data and machine learning methods for dynamic parameter adjustment and optimization
  

## Summary  

The overall strategy is relatively simple and reliable, using double EMA crossovers to determine price trends and setting growth rate thresholds to generate trading signals. Compared to single line crossovers, it can filter out some false signals. But EMA lines themselves have lagging issues. Combining other indicators or dynamic parameter adjustment can further improve strategy performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|false|Use Start Time Limiter?|
|v_input_2|2016|Start From Year|
|v_input_3|5|Start From Month|
|v_input_4|true|Start From Day|
|v_input_5|false|Start From Hour|
|v_input_6|false|Start From Minute|
|v_input_7|10|lenght0|
|v_input_8|21|lenght1|
|v_input_9|0.05|Threshold Up|
|v_input_10|-0.165|Threshold Down|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-14 00:00:00
end: 2023-11-20 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy(title="ema(ema10-21)", overlay=true, pyramiding = 0, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, initial_capital = 15000, commission_type = strategy.commission.percent, commission_value = 0.2)

useTimeLimit    = input(defval = false, title = "Use Start Time Limiter?")
startYear       = input(defval = 2016, title = "Start From Year",  minval = 0, step = 1)
startMonth      = input(defval = 05, title = "Start From Month",  minval = 0,step = 1)
startDay        = input(defval = 01, title = "Start From Day",  minval = 0,step = 1)
startHour       = input(defval = 00, title = "Start From Hour",  minval = 0,step = 1)
startMinute     = input(defval = 00, title = "Start From Minute",  minval = 0,step = 1)

startTimeOk() => true

lenght0 = input(10)
lenght1 = input(21)

source = close

EmaShort = ema(ema(source, lenght0), lenght0)
EmaLong = ema(ema(source, lenght1),lenght1)
plot(EmaShort, color=red)
plot(EmaLong, color=purple)

growth = ((EmaShort-EmaLong)*100)/((EmaShort+EmaLong)/2)
thresholdUp = input(defval=0.05, title="Threshold Up", type=float, step=0.01)
thresholdDown = input(defval=-0.165, title="Threshold Down", type=float, step=0.001)

if( startTimeOk() )
    buy_condition = EmaShort > EmaLong and growth > thresholdUp
    buy_exit_condition = EmaShort < EmaLong and growth < thresholdDown
    strategy.entry("buy", strategy.long, comment="buy", when=buy_condition)
    strategy.close(id='buy', when=buy_exit_condition)
```

> Detail

https://www.fmz.com/strategy/432763

> Last Modified

2023-11-21 11:41:40
