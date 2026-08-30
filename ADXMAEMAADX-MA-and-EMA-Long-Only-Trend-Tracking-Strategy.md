
> Name

ADX-MA-and-EMA-Long-Only-Trend-Tracking-Strategy based on ADXMA and EMA
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/136162f76aea28bf1f8.png)
 [trans]
## Overview
This strategy mainly uses the ADX indicator to determine the trend, and combines MA and EMA with two moving averages with different parameter settings to build a long-only trend following strategy. When ADX rises, the long direction is prompted, and when the price breaks through the upward MA and EMA, a long position is opened; when ADX falls or the price falls below one of the MA or EMA, the position is closed.
## Strategy Principle
This strategy mainly uses ADX to determine market trends and strength. ADX determines the existence and strength of a trend by calculating the extent and direction of price changes. When ADX rises, it means that it is in an upward trend; when ADX falls, it means that the trend is weakening.
This strategy also uses two moving averages MA and EMA with different parameter settings to assist in judgment. They can effectively filter out the randomness of prices and show the main trend direction of prices. When the price rises and breaks through the MA and EMA, it is a long signal; when the price falls below it, it is a closing signal.
Combining the characteristics of ADX and moving averages, this strategy constructs a trading signal to determine the direction of the trend: open a long position when ADX rises and the price breaks through the upward MA and EMA, close the position when ADX falls or the price falls below the MA/EMA, realizing a long-only trend following strategy.
## Strategic advantage analysis
This strategy mainly has the following advantages:
1. Use ADX to judge the strength of the trend, which can reduce the occurrence of invalid transactions and track the trend;
2. Filtering by combining moving averages with two different parameter settings can effectively identify trends;
3. Only go long to avoid slippage losses caused by frequent reverse operations of 29797;
4. The admission conditions are strict and risks can be effectively controlled;
5. Implemented a long-only long-term trend following strategy.
## Strategy risk analysis
There are also some risks with this strategy:
1. The ADX indicator lags behind and may miss the best entry opportunity;
2. Only go long and cannot take advantage of the falling market to make profits;
3. When the trend changes, there is a certain risk of loss;
4. Improper parameter settings can also affect strategy performance.
Corresponding solutions:
1. Appropriately adjust the parameters of ADX to reduce lag;
2. Stop loss strategies can be set to control single losses;
3. Test and optimize parameters and select the best parameters.
## Strategy optimization direction
This strategy can also be optimized from the following aspects:
1. Add stop-loss strategies to better control risks;
2. Increase position management and dynamically adjust positions according to market conditions;
3. Test optimization parameters and find the best parameter combination;
4. Add machine learning algorithms and dynamically optimize parameters;
5. Construct a Martingale long strategy to reduce the impact of the profit-loss ratio.
## Summarize
The overall strategy is a long-only trend tracking strategy that uses ADX to determine trend strength and assists in constructing filtering signals with two moving averages. It effectively controls the occurrence of invalid transactions and achieves the effect of tracking trends. It is a relatively stable long-only strategy. Through certain optimization adjustments, the stability and profitability of the strategy can be further enhanced.
||

## Overview

This strategy mainly uses the ADX indicator to judge the trend and combines the MA and EMA moving averages with different parameter settings to build a long-only trend tracking strategy. When ADX rises, it indicates a long direction. When the price breaks through the upward MA and EMA, open long positions. When ADX falls or the price falls below MA or EMA, close positions.

## Strategy Principle  

The strategy mainly uses ADX to judge market trend and strength. ADX calculates the degree and direction of price changes to determine the existence and strength of the trend. When ADX rises, it means that it is currently in an upward trend. When ADX falls, it means the trend is weakening.

The strategy also uses two moving averages, MA and EMA, with different parameter settings as auxiliary judgment. They can effectively filter the randomness of prices and show the main trend direction of prices. When prices rise and break through MA and EMA, it is a long signal. When prices fall and break through, it is a closing signal.

Combining the characteristics of ADX and moving averages, the strategy builds trading signals to judge the trend direction: go long when ADX rises and prices break through the upward MA and EMA, and close positions when ADX falls or prices break through MA/EMA. It implements a long-only trend tracking strategy.

## Advantage Analysis

The main advantages of this strategy are:

1. Use ADX to judge the trend strength, reduce invalid trades and track trends.
2. Combining two moving averages with different parameter settings can effectively identify trends.  
3. Only long positions avoid frequent reverse operations and slippage loss. 
4. Strict entry conditions can effectively control risks.
5. Implement a long-only trend tracking strategy.

## Risk Analysis  

There are also some risks:  

1. ADX indicator has lag, possibly missing the best entry point.
2. Only long positions cannot profit from falling markets. 
3. There is a certain loss risk when trends change.
4. Improper parameter settings also affect strategy performance.

Solutions:

1. Adjust ADX parameters to reduce lag reasonably.
2. Set stop loss to control single loss.
3. Test and optimize parameters to select the best.

## Optimization

The strategy can be optimized from the following aspects:

1. Add a stop loss strategy to better control risks.
2. Add position management to dynamically adjust positions based on market conditions.  
3. Test and optimize parameters to find the best combination.
4. Add machine learning algorithms to dynamically optimize parameters. 
5. Build martingale strategies to reduce the impact of profit ratio.

## Conclusion  

In general, this is a long-only trend tracking strategy that uses ADX to judge the trend strength and two moving averages as auxiliary filters. It effectively controls the occurrence of invalid trades and achieves the effect of tracking trends. It is a relatively stable long-only strategy. With some optimizations, the strategy's stability and yield can be further enhanced.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|ADX Smoothing|
|v_input_2|14|DI Length|
|v_input_3|50|MA Period|
|v_input_4|50|EMA Period|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-22 00:00:00
end: 2024-01-28 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("ADX, MA, and EMA Long Strategy - ADX Trending Up", shorttitle="ADX_MA_EMA_Long_UpTrend", overlay=true)
adxlen = input(14, title="ADX Smoothing")
dilen = input(14, title="DI Length")
maPeriod = input(50, title="MA Period")
emaPeriod = input(50, title="EMA Period")
dirmov(len) =>
    up = change(high)
    down = -change(low)
    plusDM = na(up) ? na : (up > down and up > 0 ? up : 0)
    minusDM = na(down) ? na : (down > up and down > 0 ? down : 0)
    truerange = rma(tr, len)
    plus = fixnan(100 * rma(plusDM, len) / truerange)
    minus = fixnan(100 * rma(minusDM, len) / truerange)
    [plus, minus]
adx(dilen, adxlen) =>
    [plus, minus] = dirmov(dilen)
    sum = plus + minus
    100 * rma(abs(plus - minus) / (sum == 0 ? 1 : sum), adxlen)
sig = adx(dilen, adxlen)
maValue = sma(close, maPeriod)
emaValue = ema(close, emaPeriod)
longCondition = sig > sig[1] and close > maValue and close > emaValue
if (longCondition)
    strategy.entry("Long", strategy.long)
exitCondition = sig < sig[1] or  close < maValue or close < emaValue
if (exitCondition)
    strategy.close("Long")
plot(maValue, color=color.blue, title="MA")
plot(emaValue, color=color.orange, title="EMA")
plot(sig, color=color.red, title="ADX")

```

> Detail

https://www.fmz.com/strategy/440314

> Last Modified

2024-01-29 11:30:15
