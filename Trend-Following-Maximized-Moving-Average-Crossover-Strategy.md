
> Name

Trend-Following-Maximized-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/13c2c7d06cf1eb377e8.png)

[trans]

## Overview
This strategy uses the intersection of two moving averages of different periods to trade, and is a trend following strategy. The strategy uses short-term and long-term moving average crossover buy and sell signals to trade in trending markets.
## Strategy Principle
This strategy uses a 9-period short-term moving average SMA and a 50-period long-term moving average LMA. When the short-term moving average crosses the long-term moving average from below, a buy signal is generated; when the short-term moving average crosses below the long-term moving average from above, a sell signal is generated.
At the same time, the strategy also introduces the RSI indicator to judge the strength of the trend. Only when the RSI is greater than the set threshold (default 55), a trading signal will be generated. This avoids false signals when the RSI is in oversold territory.
Each transaction of the strategy accounts for 30% of the total funds, and only one order is opened at a time. A 0.1% transaction fee is taken into account.
## Advantage Analysis
- This strategy uses the trend signal formed by the crossing of the moving average to effectively track the trend market.
- Introducing the RSI indicator to judge the strength of the trend can avoid false signals when the trend is blocked.
- The default parameters have been optimized to obtain more stable returns in a variety of markets.
- Reasonable fund management to avoid excessive single losses.
## Risk Analysis
- When the market is in a volatile adjustment, this strategy is prone to produce false signals and cannot make profits.
- Trend-following strategies cannot make profits when there is no clear trend.
- Improper parameter settings may lead to frequent transactions and increase transaction fees.
- Failure to consider the impact of emergencies may result in late stop loss.
Risks can be reduced by optimizing parameters, combining other indicators to determine profit opportunities, strictly managing funds, and setting stop losses.
## Optimization direction
- You can test different moving average combinations to find optimal parameters.
- Other indicators can be introduced to determine the trend, such as MACD, etc.
- Dynamic stop loss can be set to control single losses.
- The fund management ratio can be adjusted according to different markets.
- Can be combined with trading volume indicators to determine trend strength.
## Summarize
This strategy captures trend opportunities through a simple moving average crossover system. The default parameters have been optimized, the income is stable, and it is suitable for automated trading. Strategy stability and profitability can be further improved by introducing other auxiliary indicators, optimizing parameters, and improving stop loss. Generally speaking, this strategy uses trend crossover signals to trade and works better in markets with obvious trends.
|| 

## Overview

This strategy uses the crossover of two moving averages with different periods to generate trading signals. It belongs to trend following strategies. The strategy captures trending opportunities by using signals when a shorter period MA crosses a longer period MA.

## Strategy Logic

The strategy uses a 9-period short term MA (SMA) and a 50-period long term MA (LMA). When the SMA crosses above the LMA, a buy signal is generated. When the SMA crosses below the LMA, a sell signal is generated. 

The strategy also incorporates the RSI indicator to gauge the strength of the trend. Trading signals are only generated when RSI is above a threshold (default 55). This avoids incorrect signals when RSI is in overbought zones.

The strategy trades 30% of total capital each time, with only one position open at a time. 0.1% commission is accounted for.

## Advantage Analysis

- Captures trending opportunities effectively using MA crossover trend signals.
- Incorporating RSI avoids incorrect signals when trend stalls. 
- Default parameters are optimized and produce steady returns across various markets.
- Reasonable capital management avoids oversized position sizing.

## Risk Analysis

- Prone to whipsaws and incorrect signals during range-bound markets without a trend.
- No profits without a significant trend as a trend following strategy.
- Excessive trading and commissions if parameters not tuned properly. 
- Lack of stop loss exposes strategy to events risk.

Risks can be reduced via parameter optimization, using other indicators, strict capital management, and stop loss.

## Enhancement Opportunities

- Test different MA combinations to find optimal parameters.
- Incorporate other indicators like MACD to confirm trend. 
- Implement dynamic stop loss to control loss per trade.
- Adjust position sizing based on different markets.
- Use volume indicators to gauge trend strength.

## Conclusion

The strategy captures trending opportunities using simple MA crossover system. Default parameters are optimized with steady returns, suitable for algorithmic trading. Further improvements can be made by adding other indicators, optimizing parameters, and implementing stop loss. Overall, it is an effective trend following strategy for trending markets using crossover signals.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|From Month|
|v_input_2|true|From Day|
|v_input_3|2020|From Year|
|v_input_4|true|Thru Month|
|v_input_5|true|Thru Day|
|v_input_6|2112|Thru Year|
|v_input_7|true|Show Date Range|
|v_input_8|50|MA long period|
|v_input_9|9|MA short period|
|v_input_10|55|RSI Trigger|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-16 00:00:00
end: 2023-10-16 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © relevantLeader16058

//@version=4
strategy(shorttitle='Maximized Moving Average Crossing ',title='Maximized Moving Average Crossing (by Coinrule)', overlay=true, initial_capital=1000,  default_qty_type = strategy.percent_of_equity, default_qty_value = 30, commission_type=strategy.commission.percent, commission_value=0.1)

//Backtest dates
fromMonth = input(defval = 1,    title = "From Month",      type = input.integer, minval = 1, maxval = 12)
fromDay   = input(defval = 1,    title = "From Day",        type = input.integer, minval = 1, maxval = 31)
fromYear  = input(defval = 2020, title = "From Year",       type = input.integer, minval = 1970)
thruMonth = input(defval = 1,    title = "Thru Month",      type = input.integer, minval = 1, maxval = 12)
thruDay   = input(defval = 1,    title = "Thru Day",        type = input.integer, minval = 1, maxval = 31)
thruYear  = input(defval = 2112, title = "Thru Year",       type = input.integer, minval = 1970)

showDate  = input(defval = true, title = "Show Date Range", type = input.bool)

start     = timestamp(fromYear, fromMonth, fromDay, 00, 00)        // backtest start window
finish    = timestamp(thruYear, thruMonth, thruDay, 23, 59)        // backtest finish window
window()  => time >= start and time <= finish ? true : false       // create function "within window of time"

//MA inputs and calculations
inlong=input(50, title='MA long period')
inshort=input(9, title='MA short period')

MAlong = sma(close, inlong)
MAshort= sma(close, inshort)

// RSI inputs and calculations
lengthRSI = (14)

RSI = rsi(close, lengthRSI)
RSI_Signal = input(55, title = 'RSI Trigger', minval=1)

//Entry and Exit
bullish = crossover(MAshort, MAlong)
bearish = crossunder(MAshort, MAlong)

strategy.entry(id="long", long = true, when = bullish and RSI > RSI_Signal and window())
strategy.close(id="long", when = bearish and window())

 
plot(MAshort, color=color.purple, linewidth=2)
plot(MAlong, color=color.red, linewidth=2)
```

> Detail

https://www.fmz.com/strategy/429460

> Last Modified

2023-10-17 13:05:29
