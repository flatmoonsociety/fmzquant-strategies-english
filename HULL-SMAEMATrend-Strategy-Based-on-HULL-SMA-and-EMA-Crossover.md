
> Name

Trend-Strategy-Based-on-HULL-SMA-and-EMA-Crossover
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/ebb708c9919b59d40c.png)

[trans]

## Overview
This strategy determines the direction of the market trend and generates buy and sell signals by calculating the intersection of the HULL smoothed moving average and the exponential moving average. It is a short- to medium-term trend following strategy.
## Strategy Principle
1. Calculate the 5-day HULL smoothed moving average (HULL SMA). HULL SMA is calculated by weighted moving average and the square root of the period, which can respond to price changes faster.
2. Calculate the 5-day exponential moving average (EMA). EMA calculates the average line by giving greater weight to recent prices, which is more sensitive than SMA.
3. Determine the intersection of HULL SMA and EMA to generate buy and sell signals.
- When the HULL SMA crosses above the EMA, a buy signal is generated. Indicates that the short-term trend breaks upward from the long-term trend, indicating that prices will rise.
- When the HULL SMA crosses below the EMA, a sell signal is generated. Indicates that the short-term trend is beginning to turn and prices will fall.
4. Use HULL SMA as the fast line and EMA as the slow line. Based on the cross pattern of the two moving averages, judge the changes in the short-term and medium-term market trends and generate trading signals.
## Advantage Analysis
1. HULL SMA is sensitive to price changes and can detect trend changes earlier.
2. EMA has the ability to smooth noise and track long-term trends.
3. The fast line breaks through the slow line to generate a signal, which can seize the turning point of the trend and enter the market in time.
4. By adjusting the moving average parameters, you can adapt to transactions in different periods.
5. Can judge rising and falling trends at the same time, and flexibly capture two-way market conditions.
## Risk Analysis
1. There may be many false signals in a volatile market.
2. Unable to judge the strength of the trend, and may suffer repeated losses in a weak trend.
3. The gap between the moving averages is too large, and part of the market may be missed.
4. Improper setting of fast and slow line parameters will affect the quality of trading signals.
5. The trading frequency may be too high, increasing transaction costs and slippage risk.
It can be improved by combining other indicators to filter signals, assess trend strength, optimize parameter settings, and control risks.
## Optimization direction
1. Add indicator filtering, such as MACD, RSI, etc. to determine buying and selling opportunities.
2. Add trend strength indicators, such as ADX, to avoid trading in weak trends.
3. Optimize the moving average parameters and find the best parameter combination.
4. Set a stop-loss strategy to control single losses.
5. Considering the number of transactions and cost control, adjust the frequency of opening positions.
6. Combine with more time period analysis to identify cross-cycle trend signals.
7. Develop an automatic parameter optimization program to dynamically find optimal parameters.
## Summarize
This strategy determines the market trend through the intersection of fast HULL SMA and slow EMA, and is a typical moving average crossover strategy. Compared with traditional moving averages, this strategy uses a more sensitive HULL SMA, which can detect trend changes earlier. However, parameter settings still need to be optimized and supplemented by other technical indicators to reduce false signals. If paired with sound risk and capital management, this strategy can become a highly efficient short- to medium-term trend following strategy.
||


## Overview

This strategy generates buy and sell signals by calculating the crossover between the HULL Smoothed Moving Average line and the Exponential Moving Average line to determine market trend direction. It belongs to the category of medium-term trend-following strategies.

## Strategy Logic

1. Calculate the 5-period HULL Smoothed Moving Average (HULL SMA). HULL SMA responds faster to price changes by using weighted moving averages and the square root of the period. 

2. Calculate the 5-period Exponential Moving Average (EMA). EMA gives more weight to recent prices and is more sensitive than SMA in tracking the trend.

3. Generate buy and sell signals based on the crossover between HULL SMA and EMA.

  - When HULL SMA crosses above EMA, a buy signal is generated, indicating the short-term trend breaks out above the long-term trend, suggesting an upward price movement.  

  - When HULL SMA crosses below EMA, a sell signal is generated, indicating the short-term trend turning down, suggesting a downward price movement.

4. Use HULL SMA as the fast line and EMA as the slow line to determine changes in short-term and medium-term trends based on the crossover, generating trading signals. 

## Advantage Analysis  

1. HULL SMA is sensitive to price changes and can detect trend changes earlier.

2. EMA smoothes market noise and tracks long-term trends.

3. Crossover signals catch trend turning points in a timely manner.

4. Parameters can be adjusted for different trading timeframes.  

5. Captures upside and downside trends flexibly.

## Risk Analysis

1. More false signals may occur during range-bound markets.

2. Unable to determine trend strength, may lead to repeated losses in weak trends.

3. Price movements between the averaging intervals may be missed.  

4. Improper parameter settings affect signal quality.

5. High trading frequency increases costs and slippage risks.

Improvements can be made via signal filtering, evaluating trend strength, parameter optimization, risk management, etc.

## Optimization Directions

1. Add indicators like MACD, RSI for signal confirmation.

2. Incorporate trend strength indicators like ADX to avoid trading weak trends.

3. Optimize moving average parameters for best combinations. 

4. Implement stop loss to control single trade loss.

5. Manage trade frequency and costs.

6. Incorporate multi-timeframe analysis to identify cross-cycle trends.

7. Develop auto parameter optimization programs.

## Summary

This strategy judges the trend based on the crossover between the fast HULL SMA and slow EMA. It is a typical moving average crossover system. Compared to traditional moving averages, the more responsive HULL SMA provides earlier trend change detection. But parameters and supplemental indicators should be optimized to reduce false signals. With proper risk and money management, this strategy can be an efficient medium-term trend following system.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|5|Hull EMA Value|
|v_input_1|5|EMA Value|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-23 00:00:00
end: 2023-10-29 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("HULL EMA Crossover", overlay = true, process_orders_on_close = true)

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © spiritedPerson95700

inSession = true


HULL_INP = input.int(5, "Hull EMA Value")
EMA_INP = input(5, "EMA Value")

/// Indicator
HULL_EMA = ta.hma(close, HULL_INP)
EMA = ta.ema(close, EMA_INP)

prevSignal = ''
if (prevSignal == '')  
    prevSignal := HULL_EMA > EMA ? 'buy' : 'sell'

/// buy and sell signal
buy = ta.crossover(HULL_EMA, EMA)
short = ta.crossover(EMA, HULL_EMA)

sell = short
cover = buy

if inSession
    if buy 
        prevSignal := 'na'
        strategy.entry("long", direction = strategy.long, comment = "Buy")

    if sell
        prevSignal := 'na'
        strategy.close("long", comment = "Sell")

    if short
        strategy.entry("short", direction = strategy.short, comment = "Short")

    if cover
        strategy.close("short", comment = "Cover")


plot(HULL_EMA, color = color.green)
plot(EMA, color = color.blue)

// if ( hour(time) == 15 and minute(time) > 25  )  
//     strategy.close("long", comment="EOD")
//     strategy.close("short", comment="EOD")
//     buy := false
//     sell := false
//     prevSignal := ''

```

> Detail

https://www.fmz.com/strategy/430563

> Last Modified

2023-10-30 14:36:25
