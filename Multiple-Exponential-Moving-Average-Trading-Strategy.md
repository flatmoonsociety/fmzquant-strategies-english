
> Name

Multiple-Exponential-Moving-Average-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/140aebfd27c87f8ca6a.png)
[trans]

## Overview
This strategy uses a combination of multiple Exponential Moving Averages (EMA) to identify potential market trade entry and exit points. By comparing the EMA trends of different periods, we can determine the current market trend, intervene in transactions at the beginning of the trend, and close positions at the end of the trend.
## Strategy Principle
This strategy uses 4 EMAs of different periods as core indicators, namely ultra-short-term EMA (default 8 periods), short-term EMA (default 13 periods), mid-term EMA (default 21 periods) and long-term EMA (default 55 periods). When the long-term EMA is below the other three EMAs, it is judged that the current situation may be in the early stage of an upward trend, and the strategy will open long positions at this time; when the long-term EMA is above the other three EMAs, it is judged that the current situation may be in the early stage of a downward trend, and the strategy will close all long positions at this time. Through this long and short arrangement and combination of EMA, we can identify trend turning points and capture the emerging trend.
EMA pays more attention to the recent price than the simple moving average (SMA), so the EMA trend is more sensitive and can respond to price changes more quickly. The crossover of EMAs of different periods reflects the strength of the trend at different time scales. The long-term EMA is the most stable and represents the big market trend; the short- and medium-term EMA is relatively sensitive and reflects the short- and medium-term market trends. Together they form the core logic of the strategy.
## Advantage Analysis (Advantage Analysis)
1. Wide applicability: This strategy is based on the EMA indicator of the price itself and is suitable for most products with good liquidity and relatively smooth trends, such as various futures, foreign exchange, mainstream digital currencies, etc.
2. Trend following: Judging the trend by comparing the position relationship of EMA of different periods, to a certain extent, it can capture the early stage of the trend and track the trend.
3. Flexible parameters: The period parameters of EMA can be flexibly adjusted according to the characteristics of the variety, Investment Horizon, etc., and have certain adaptability.
4. Clear logic: The strategy is based on a simple EMA long and short permutation and combination to generate trading signals. The logic is clear and easy to understand and implement.
## Risk Analysis
1. EMA delay: EMA is essentially a trend tracking indicator with a certain degree of delay, and more false signals may occur in volatile markets.
2. Parameter sensitivity: The selection of EMA cycle parameters has a great impact on the strategy performance, and after parameter optimization, it may not be able to maintain good performance on out-of-sample data.
3. Lack of filtering: This strategy lacks further filtering of trading signals. All signals will be traded after they are generated, and some low-quality transactions may occur.
4. Fixed positions: The current strategy is to fix 1 unit each time a position is opened, lacking risk-based dynamic position control, and risk management is not perfect.
## Optimization Direction
1. Introduce trend filtering: Based on the EMA signal, add trend strength filtering indicators such as ATR and ADX to filter out signals of weak trends and shock periods.
2. Introduce volatility filtering: On the basis of trend filtering, volatility filtering can be further introduced, such as Bollinger Band width, etc., to filter out low-quality signals that may be caused by high volatility.
3. Optimize stop loss: The current strategy lacks clear stop loss logic. After introducing trend and volatility filters, dynamic stop loss based on ATR or percentage can be added to control the maximum loss of a single transaction.
4. Dynamic positions: Based on the volatility of varieties, account value ratio, etc., the number of positions opened each time by the strategy can be dynamically controlled to pursue higher absolute returns while reducing risks.
5. Optimize parameters: The optimal parameters of EMA may be different for different varieties and different periods. Parameter optimization needs to be carried out according to the characteristics of the varieties to improve the applicability of the strategy.
## Summary
This strategy identifies trend turning points by comparing the long and short combinations of four EMAs with different periods, and captures the early stages of the trend. The idea is simple and clear. Its advantages include wide application range, clear logic, flexible parameters, and the ability to better track trends; however, it also has problems such as the inherent delay of the EMA indicator, sensitive parameters, lack of filtering, and fixed positions. In the future, the robustness and profitability of this strategy can be improved by introducing trend and volatility filtering, optimizing stop losses, dynamic positions, parameter optimization, etc., to make it more complete and reliable.
|| 

## Overview

This strategy combines multiple Exponential Moving Averages (EMAs) to identify potential entry and exit points in the market. By comparing the trends of EMAs with different periods, it determines the current market trend and enters trades at the beginning of the trend formation and closes positions at the beginning of the trend's end.

## Strategy Principle

This strategy uses 4 EMAs with different periods as core indicators, namely ultra-short-term EMA (default 8 periods), short-term EMA (default 13 periods), medium-term EMA (default 21 periods), and long-term EMA (default 55 periods). When the long-term EMA is below the other three EMAs, it is judged that the current market may be at the beginning of an upward trend, and the strategy opens a long position; when the long-term EMA is above the other three EMAs, it is judged that the current market may be at the beginning of a downward trend, and the strategy closes all long positions. The strategy identifies trend turning points by this combination of long and short EMA arrangements to capture nascent trends.

Compared to Simple Moving Average (SMA), EMA places more emphasis on recent prices and thus its trend is more sensitive and can react to price changes more quickly. The crossover of EMAs with different periods reflects the strength of trends on different time scales. The long-term EMA is the most stable and represents the significant market trend; the medium and short-term EMAs are relatively sensitive and reflect the short and medium-term market trends. They together constitute the core logic of this strategy.

## Advantage Analysis

1. Wide applicability: This strategy is based on the EMA indicator of the price itself and is applicable to most varieties with good liquidity and relatively smooth trends, such as various futures, forex, mainstream cryptocurrencies, etc.

2. Trend tracking: By comparing the position relationship of EMAs with different periods to determine the trend, it can capture the beginning of trend formation to a certain extent and track the trend.

3. Flexible parameters: The period parameters of EMA can be flexibly adjusted according to the characteristics of varieties, investment horizon, etc., and have certain adaptability.

4. Clear logic: The strategy generates trading signals based on a simple combination of long and short EMA arrangements, and the logic is clear and easy to understand and implement.

## Risk Analysis

1. EMA lag: EMA is essentially a trend-tracking indicator and has a certain lag, which may generate more false signals in a turbulent market.

2. Parameter sensitivity: The selection of EMA period parameters has a significant impact on the strategy performance, and the parameters optimized may not maintain good performance on out-of-sample data.

3. Lack of filtering: This strategy lacks further filtering of trading signals, and all generated signals will be traded, which may result in some low-quality trades.

4. Fixed position: Currently, the strategy opens a fixed 1 unit position each time, lacking dynamic position control based on risk, and risk management is not perfect enough.

## Optimization Direction

1. Introduce trend filtering: On the basis of EMA signals, add trend strength filtering indicators such as ATR and ADX to filter out signals from weak trends and turbulent periods.

2. Introduce volatility filtering: On the basis of trend filtering, volatility filtering such as Bollinger Band width can be further introduced to filter out low-quality signals that may be caused by high volatility.

3. Optimize stop-loss: Currently, the strategy lacks a clear stop-loss logic. After introducing trend and volatility filtering, dynamic stop-loss based on ATR or percentage can be added to control the maximum loss of a single trade.

4. Dynamic position: Based on the volatility of varieties, the proportion of account value, etc., the number of positions opened by the strategy each time can be dynamically controlled to pursue higher absolute returns while reducing risk.

5. Optimize parameters: For different varieties and different periods, the optimal parameters of EMA may be different, and parameter optimization needs to be performed separately according to the characteristics of varieties to improve the applicability of the strategy.

## Summary

This strategy identifies trend turning points by comparing the long and short arrangement combinations of 4 EMAs with different periods to capture the beginning of trend formation. The idea is simple and clear. Its advantages lie in its wide range of applicability, clear logic, and flexible parameters, and it can track trends well; but at the same time, it also has the inherent lag of EMA indicators, as well as problems such as parameter sensitivity, lack of filtering, and fixed position. In the future, the robustness and profitability of this strategy can be improved from aspects such as introducing trend and volatility filtering, optimizing stop-loss, dynamic position, and parameter optimization to make it more complete and reliable.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|8|Lowest EMA|
|v_input_int_2|13|Low EMA|
|v_input_int_3|21|Med EMA|
|v_input_int_4|55|High EMA|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-03-05 00:00:00
end: 2024-03-10 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © n1ghthawk

//@version=5
strategy("donmo's 4ema", overlay=true, margin_long=100, margin_short=100)

float long = na
float short = na

lowestEMAPeriodInput = input.int(8, "Lowest EMA")
lowEMAPeriodInput = input.int(13, "Low EMA")
medEMAPeriodInput = input.int(21, "Med EMA")
highEMAPeriodInput = input.int(55, "High EMA")

lowestEMA = ta.ema(close, lowestEMAPeriodInput)
lowEMA = ta.ema(close, lowEMAPeriodInput)
medEMA = ta.ema(close, medEMAPeriodInput)
highEMA = ta.ema(close, highEMAPeriodInput)


emaLongCondition = highEMA<medEMA and highEMA<lowEMA and highEMA<lowestEMA
emaShortCondition = highEMA>medEMA and highEMA>lowEMA and highEMA>lowestEMA

longCondition = ta.change(emaLongCondition)
shortCondition = ta.change(emaShortCondition)

notInTrade = strategy.position_size <= 0
if longCondition and emaLongCondition and notInTrade
    long:=high
    strategy.entry("EL", strategy.long)

if shortCondition and emaShortCondition
    short:=low
    strategy.close("EL")


plot(long+3,title = 'long', color = color.green, linewidth = 4, style = plot.style_cross)
plot(short-3,title = 'short', color = color.red, linewidth = 4, style = plot.style_cross)

plot(lowestEMA, title = "lowestEMA", color=color.blue)
plot(lowEMA, title = "lowEMA", color=color.green)
plot(medEMA, title = "medEMA", color=color.orange)
plot(highEMA, title = "highEMA", color=color.red)
```

> Detail

https://www.fmz.com/strategy/444387

> Last Modified

2024-03-11 16:17:20
