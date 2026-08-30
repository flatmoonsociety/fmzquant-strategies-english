
> Name

Trend-Reversal-Strategy-Based-on-Moving-Averages
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/b86dd9e64e4c5482b22360a28e99ca2da2c4bb53cc0e1748c350ae420381209f.png)
[trans]

## Overview
The main idea of ​​this strategy is to trade short-term retracements in the direction of the long-term trend. Specifically, the 200-day simple moving average is used to determine the long-term trend direction, and the 10-day simple moving average is used to determine the short-term trend direction. When the price is above the 200-day line, it is a long market, and when the price is below the 200-day line, it is a short market. In the long market, when the price falls to the 10-day line, go long; in the short market, when the price rises to the 10-day line, go short.
## Strategy Principle
This strategy uses the 200-day simple moving average and the 10-day simple moving average to determine market trends. When the price crosses the 200-day line, it is considered to have entered the long market, and when the price crosses the 200-day line, it is considered to have entered the short market. In the bull market, if the price falls near the 10-day line, it means that it has encountered a short-term adjustment. At this time, the goal is to follow the long-term bull trend and continue to rise. In the short market, if the price rises near the 10-day line, it means that it has encountered a short-term rebound. At this time, the goal is to go short and follow the long-term short trend to continue to fall.
Specifically, when the following conditions are met, go long and enter the market: the price is higher than the 200-day line, the price is lower than the 10-day line, and there is no previous position. When the following conditions are met, close the position and exit the market: the price is higher than the 10-day line, and you previously held a long position. In order to prevent huge losses, a FAILSAFE stop loss is set. If the retracement from the highest point exceeds 10%, stop the loss and exit directly.
It can be seen that the trading logic of this strategy is mainly based on the golden cross of the moving average. It performs retracement buying and trend following take profit in the trend direction after judging the long and short moving average. It is a typical trend following strategy.
## Advantage Analysis
The biggest advantage of this strategy is to follow trends with low capital costs and pursue excess returns. The specific advantages are as follows:
1. Using a combination of long and short-term moving averages to determine the trend direction of primary and secondary levels can effectively lock in medium and long-term trend opportunities and avoid being misled by short-term market conditions.
2. Using the short-term retracement approach can minimize the purchase cost and obtain higher profit margins.
3. Set up a FAILSAFE stop-loss mechanism to effectively control single losses and protect the security of account funds.
4. Allows you to follow the profit-taking exit, fully explore the medium and long-term trend opportunities, and obtain excess Alpha.
5. Use purely mechanical trading methods to avoid the influence of subjective emotions and make the strategy easier to implement.
## Risk Analysis
This strategy mainly involves the following risks:
1. Backtest data fitting risk. Actual market conditions may differ from historical data, resulting in discounted real trading results.
2. Risk of false breakthrough. The probability of a reversal and correction when the price only touches the moving average is high, which can easily lead to the accumulation of small losses.
3. Trend reversal risk. A sudden reversal in the mid- to long-term trend is a common situation, and holding a position at this time can easily cause large losses.
The countermeasures are as follows:
1. Increase the sample size and use more historical data for robustness verification to ensure reliable results.
2. Optimize parameters and adjust the moving average system parameter combination to ensure the quality of trading signals.
3. Appropriately relax the stop loss line, give the price some room for correction, and avoid being too sensitive to stop loss.
## Optimization direction
This strategy can be further optimized from the following aspects:
1. Adding filtering conditions, such as transaction volume filtering, can effectively reduce unnecessary transactions caused by false breakthroughs.
2. Combined with other indicators, such as KDJ, MACD, etc., to form an indicator combination, which can improve the quality of trading signals.
3. Test different holding times, optimize take-profit and stop-loss strategies, and further improve indicators such as Sharpe ratio.
4. Dynamically adjust parameters according to market conditions to form an adaptive parameter optimization mechanism to make the strategy more robust.
5. Add an algorithmic trading module and use machine learning and other methods to automatically generate trading signals to reduce human intervention.
## Summarize
The overall idea of ​​this strategy is clear and easy to implement. It can track medium and long-term trends at low cost and obtain stable Alpha. However, there is also a certain risk of arbitrage, and further optimization is needed to improve stability. In general, this strategy is designed from the perspective of trend tracking and is worthy of further research and application. If the parameters are adjusted properly, good real-time results should be obtained.
||

## Overview

The main idea of this strategy is to trade short-term pullbacks along the direction of the long-term trend. Specifically, the 200-day simple moving average is used to determine the direction of the long-term trend, and the 10-day simple moving average is used to determine the direction of the short-term trend. When the price is above the 200-day line, it is a bull market. When the price is below the 200-day line, it is a bear market. In a bull market, go long when the price drops to the 10-day line. In a bear market, go short when the price rises to the 10-day line.

## Strategy Logic  

This strategy uses the 200-day simple moving average and the 10-day simple moving average to determine market trend. When the price crosses above the 200-day line, it is considered entering a bull market. When the price crosses below the 200-day line, it is considered entering a bear market. In a bull market, if the price drops to around the 10-day line, it means encountering a short-term correction. At this time, go long, targeting the continuation of the long-term bullish trend. In a bear market, if the price rises to around the 10-day line, it means encountering a short-term rebound. At this time, go short, targeting the continuation of the long-term bearish trend.   

Specifically, when the following conditions are met, go long to enter the market: price is above the 200-day line, price is below the 10-day line, and there was no previous position. When the following conditions are met, close the position to exit the market: price is above the 10-day line, and there was a previous long position. To prevent huge losses, a FAILSAFE stop loss is set. If the retracement from the highest point exceeds 10%, directly stop loss to exit.  

It can be seen that the trading logic of this strategy is mainly based on the golden cross and death cross of moving averages. It enters based on pullbacks and exits based on trend tracking in the direction determined by long and short moving averages, which belongs to a typical trend tracking strategy.   

## Advantage Analysis

The biggest advantage of this strategy is low-cost trend tracking to pursue excess returns. The specific advantages are as follows:

1. Using a combination of long-term and short-term moving averages to determine the direction of primary and secondary trends can effectively lock in medium and long-term trend opportunities and avoid being misled by short-term market movements.

2. By entering based on short-term pullbacks, the entry cost can be minimized to obtain relatively high profit potential.  

3. The FAILSAFE stop loss mechanism can effectively control single losses to protect account funds.  

4. Allowing trend tracking exits can fully tap medium and long-term trend opportunities for alpha excess returns.
   
5. The adoption of a fully automated trading method avoids subjective emotional impact and makes the strategy easier to implement.

## Risk Analysis   

The main risks of this strategy are:   

1. Backtest overfitting risk. Actual market conditions may differ from historical data, resulting in reduced actual trading performance.
   
2. Risk of false breakouts. The probability of prices reversing near the moving averages is relatively large, which can easily lead to small accumulated losses.  

3. Risk of trend reversal. Sudden reversals in medium and long-term trends are common, which can easily lead to relatively large losses when holding positions.

The counter measures are:

1. Increase sample size and use more historical data for robustness testing to ensure reliable results.
   
2. Optimize parameters by adjusting the combination of moving average system parameters to ensure signal quality.  

3. Widen stop loss lines appropriately to allow some price retracements to avoid oversensitive stop losses.  

## Optimization Directions   

This strategy can be further optimized in the following aspects:  

1. Add filtering conditions such as volume filtering to effectively reduce unnecessary trading caused by false breakouts. 

2. Incorporate other indicators such as KDJ and MACD to form combo signals to improve trade signal quality.   

3. Test different holding periods and optimize take profit and stop loss strategies to further improve Sharpe ratio etc.  

4. Dynamically adjust parameters based on market conditions to form an adaptive parameter optimization mechanism to make the strategy more robust.

5. Add algorithmic trading modules using machine learning etc to automatically generate trading signals to reduce human intervention.  

## Summary  

The overall logic of this strategy is clear and easy to implement for low-cost tracking of medium and long-term trends to achieve steady alpha. But there are also risks of getting caught on the wrong side of the trend which requires further optimization to improve robustness. In general, this strategy is designed from a trend tracking perspective and is worth further research and application. With proper parameter tuning, it should produce good live trading results.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|200|(?Strategy Parameters)MA 1 Length|
|v_input_int_2|10|MA 2 Length|
|v_input_float_1|0.1|Stop Loss Percent|
|v_input_bool_1|false|Exit On Lower Close|
|v_input_1|timestamp(01 Jan 1995 13:30 +0000)|(?Time Filter)Start Filter|
|v_input_2|timestamp(1 Jan 2099 19:30 +0000)|End Filter|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-21 00:00:00
end: 2024-02-20 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © irfanp056
// @version=5

strategy("Simple Pullback Strategy", 
     overlay=true, 
     initial_capital=100000,
     default_qty_type=strategy.percent_of_equity, 
     default_qty_value=1000, // 100% of balance invested on each trade
     commission_type=strategy.commission.cash_per_contract, 
     commission_value=0.005) // Interactive Brokers rate

// Get user input
i_ma1           = input.int(title="MA 1 Length", defval=200, step=10, group="Strategy Parameters", tooltip="Long-term MA")
i_ma2           = input.int(title="MA 2 Length", defval=10, step=10, group="Strategy Parameters", tooltip="Short-term MA")
i_stopPercent   = input.float(title="Stop Loss Percent", defval=0.10, step=0.1, group="Strategy Parameters", tooltip="Failsafe Stop Loss Percent Decline")
i_lowerClose    = input.bool(title="Exit On Lower Close", defval=false, group="Strategy Parameters", tooltip="Wait for a lower-close before exiting above MA2")
i_startTime     = input(title="Start Filter", defval=timestamp("01 Jan 1995 13:30 +0000"), group="Time Filter", tooltip="Start date & time to begin searching for setups")
i_endTime       = input(title="End Filter", defval=timestamp("1 Jan 2099 19:30 +0000"), group="Time Filter", tooltip="End date & time to stop searching for setups")

// Get indicator values
ma1 = ta.sma(close, i_ma1)
ma2 = ta.sma(close, i_ma2)

// Check filter(s)
f_dateFilter = true

// Check buy/sell conditions
var float buyPrice = 0
buyCondition    = close > ma1 and close < ma2 and strategy.position_size == 0 and f_dateFilter
sellCondition   = close > ma2 and strategy.position_size > 0 and (not i_lowerClose or close < low[1])
stopDistance    = strategy.position_size > 0 ? ((buyPrice - close) / close) : na
stopPrice       = strategy.position_size > 0 ? buyPrice - (buyPrice * i_stopPercent) : na
stopCondition   = strategy.position_size > 0 and stopDistance > i_stopPercent

// Enter positions
if buyCondition
    strategy.entry(id="Long", direction=strategy.long)

if buyCondition[1]
    buyPrice := open

// Exit positions
if sellCondition or stopCondition
    strategy.close(id="Long", comment="Exit" + (stopCondition ? "SL=true" : ""))
    buyPrice := na

// Draw pretty colors
plot(buyPrice, color=color.lime, style=plot.style_linebr)
plot(stopPrice, color=color.red, style=plot.style_linebr, offset=-1)
plot(ma1, color=color.blue)
plot(ma2, color=color.orange)
```

> Detail

https://www.fmz.com/strategy/442417

> Last Modified

2024-02-21 17:03:31
