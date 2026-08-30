
> Name

Dual-Moving-Average-Crossover-Combined-with-RSI-Indicator-Quantitative-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/150b97cd28da910a46f.png)
[trans]

# 

## Overview
This strategy combines the double moving average crossover and the RSI indicator to identify trend direction and overbought and oversold conditions. It goes long when the buying conditions are met and closes the position when the selling conditions are met. This strategy aims to use moving average crossovers to determine the direction of the trend, while using the RSI indicator to avoid going long at the top of the market and short at the bottom of the market, thereby achieving better returns.
## Strategy Principle
When the fast 9-period moving average crosses the slow 50-period moving average, it means that the short-term trend is rising and the long-term trend is rising, which is a typical bull signal. At the same time, if the RSI indicator is greater than 5 points in the previous period and less than 70, it indicates that it is in the area before overbought, and it is a more appropriate time to go long.
When the fast 9-period moving average crosses below the slow 50-period moving average, it indicates that the market is in a short market and needs to be closed.
## Advantage Analysis
- Use the cross of double moving averages to determine the general trend and avoid being misled by false breakthroughs
- RSI indicator avoids making wrong decisions at market turning points
- The moving average period can be flexibly adjusted to adapt to different varieties and time dimensions
- Controllable stop loss strategy
## Risk Analysis
- Decisions made when moving averages cross are not timely and may result in losses
- Improper setting of RSI parameters may lead to missing the best entry opportunity
- Need to pay attention to whether the trading volume can support the price trend
- Irrational market conditions caused by emergencies require manual intervention
## Optimization direction
- Optimize the parameters of RSI to achieve the best results
- Avoid false signals by combining volume indicators
- Test the best moving average parameters according to different varieties and time dimensions
- Appropriately relax the stop loss range to avoid being trapped
## Summarize
This strategy uses the cross of double moving averages to determine the direction and RSI to avoid chasing highs and lows, and can effectively use the medium and long-term trends to obtain stable returns. However, we also need to be alert to the lag of moving average crossover signals and adjustments to RSI parameters, and at the same time pay attention to the relationship between price and trading volume. Through continuous testing and optimization, this strategy is expected to achieve better results.
||

## Overview

This strategy combines dual moving average crossover and RSI indicator to identify trend direction and overbought/oversold situations. It goes long when the buying conditions are met and closes positions when the selling conditions are triggered. The goal is to use moving average crossover to determine trend direction while utilizing RSI indicator to avoid wrongly buying at tops and selling at bottoms, thus generating better profits.

## Strategy Logic  

When the fast 9-period moving average crosses above the slow 50-period moving average, it signals an uptrend in shorter timeframe overlapping with an uptrend in longer timeframe, which is a typical bullish signal. Meanwhile, if RSI is greater than the previous period by 5 points and less than 70, it means the asset is approaching but not yet in the overbought territory, making it a good timing to go long.

When the fast 9-period moving average crosses below the slow 50-period moving average, it signals the beginning of a bearish market and existing long positions should be closed.

## Advantage Analysis

- Dual moving averages help determine overall market direction and avoid false breakout
- RSI indicator prevents wrong moves at turning points  
- Flexibility in adjusting moving average periods to suit different symbols and timeframes
- Controllable stop loss strategy

## Risk Analysis  

- Crossover signal may lag and cause some losses
- Improper RSI parameter setting may miss best entry timing
- Need to watch trading volume to see if it supports price move
- Black swan events require manual intervention 

## Optimization Directions

- Optimize RSI parameters for best results
- Incorporate trading volume to avoid false signals
- Test optimal moving average periods based on symbol and timeframe
- Loosen stop loss to avoid being stopped out early

## Summary

This strategy utilizes dual moving average crossover to determine direction and RSI to avoid chasing tops and bottoms. It can effectively ride medium- to long-term trends for steady profits. But the lagging nature of crossover signals and tuning of RSI parameters should be watched out for. Also need to correlate price with volume. With continuous testing and optimization, this strategy shows promise for even better results.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Show Date Range|
|v_input_2|14|length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-14 00:00:00
end: 2023-11-20 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © joshuajcoop01

//@version=5
strategy("Bitpanda Coinrule Template",
         overlay=true,
         initial_capital=1000,
         process_orders_on_close=true,
         default_qty_type=strategy.percent_of_equity,
         default_qty_value=30,
         commission_type=strategy.commission.percent,
         commission_value=0.1)

showDate = input(defval=true, title='Show Date Range')
timePeriod = time >= timestamp(syminfo.timezone, 2020, 1, 1, 0, 0)
notInTrade = strategy.position_size <= 0


// RSI
length = input(14)
vrsi = ta.rsi(close, length)

// Moving  Averages for Buy Condition
buyFastEMA = ta.ema(close, 9)
buySlowEMA = ta.ema(close, 50)
buyCondition1 = ta.crossover(buyFastEMA, buySlowEMA)


increase = 5
if ((vrsi > vrsi[1]+increase) and buyCondition1 and vrsi < 70 and timePeriod)
    strategy.entry("Long", strategy.long)


// Moving  Averages for Sell Condition
sellFastEMA = ta.ema(close, 9)
sellSlowEMA = ta.ema(close, 50)
plot(request.security(syminfo.tickerid, "60", sellFastEMA), color = color.blue)
plot(request.security(syminfo.tickerid, "60", sellSlowEMA), color = color.green)


condition = ta.crossover(sellSlowEMA, sellFastEMA)
//sellCondition1 = request.security(syminfo.tickerid, "60", condition)

strategy.close('Long', when = condition and timePeriod)




```

> Detail

https://www.fmz.com/strategy/432767

> Last Modified

2023-11-21 12:09:50
