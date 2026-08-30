
> Name

Buy-Sell-on-Candle-Close-Strategy based on K-line closing price
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/2eff4313d3a2aa09eed358539c343bdd697c9020ca9f03b115825ba076d88c61.png)
[trans]

## Overview
This strategy determines whether to trigger a buy or sell signal by comparing the closing price of the current K line and the previous K line.
Specifically, if the closing price of the current K line is higher than the highest price of the previous K line, a buy signal is triggered; if the closing price of the current K line is lower than the lowest price of the previous K line, a sell signal is triggered.
## Strategy Principle
1. Get the historical high and low prices of a specified time period (such as daily, hourly, etc.)
2. Calculate stop loss distance and take profit distance
   - Stop loss distance = the highest price of the previous K line - the lowest price of the previous K line
   - Take profit distance = Stop loss distance * 3 (set to a stop loss and take profit ratio of 1:3)
3. Determine the relationship between the closing price of the current K line and the highest price and lowest price of the previous K line
   - If the current closing price > the highest price of the previous K line, a buy signal is triggered
   - If the current closing price < the lowest price of the previous K line, a sell signal is triggered
4. Set stop loss and take profit after entering the market
   - After buying, set the stop loss to the lowest price of the previous K line - the stop loss distance, and the take profit to the highest price of the previous K line + the take profit distance
   - After selling, set the stop loss to the highest price of the previous K line + the stop loss distance, and the take profit to the lowest price of the previous K line - the take profit distance.
The above is the basic trading logic of this strategy.
## Advantage Analysis
- The strategic ideas are clear and simple, easy to understand and implement
- Use K-line information to determine the trend direction
- There is a stop-loss and stop-profit mechanism to control risks
## Risk Analysis
- Judging only based on the K-line shape of one time period may produce more false signals
- Not taking into account more factors such as changes in trading volume, volatility, etc.
- The stop-loss and stop-profit settings may be inappropriate, and there are risks if the distance is too large or too small.
## Optimization direction
- Combine more factors to confirm entry signals, such as trading volume, moving average, etc.
- Optimize the stop loss and take profit algorithm to make the stop loss more reasonable and the take profit more sufficient
- Parameter settings for different varieties may need to be adjusted
- Can test the effects of longer term cycles
## Summarize
The overall idea of ​​this strategy is simple and clear. It uses K-line closing price information to determine the trend direction, and at the same time sets stop loss and profit to control risks. It can be used as a basic strategy for stock and digital currency trading. However, based only on the K-line shape of a single time period, it is easy to produce false signals, and there is still a lot of room for optimization. It is necessary to further consider combining more factors and adjusting parameters to improve the strategy effect.
||

## Overview

This strategy triggers buy/sell signals by comparing the closing prices of the current candle and previous candle. 

Specifically, if the current candle closes above the highest price of the previous candle, a buy signal is triggered. If the current candle closes below the lowest price of the previous candle, a sell signal is triggered.

## Strategy Logic

1. Get historical highest and lowest prices of the specified timeframe (e.g. daily, hourly) 
2. Calculate stop loss and take profit distances
   - Stop loss distance = Previous candle highest - Previous candle lowest
   - Take profit distance = Stop loss distance * 3 (1:3 risk-reward ratio)
3. Determine the relationship between current close and previous high/low
   - If current close > previous candle highest, trigger buy signal
   - If current close < previous candle lowest, trigger sell signal
4. Set stop loss and take profit after entry
   - After buying, set stop loss at previous candle lowest - stop loss distance, take profit at previous candle highest + take profit distance
   - After selling, set stop loss at previous candle highest + stop loss distance, take profit at previous candle lowest - take profit distance

The above is the basic trading logic of this strategy.

## Advantage Analysis

- Simple and clear strategy idea, easy to understand and implement
- Use candlestick information to determine trend direction  
- Have stop loss and take profit mechanism to control risk

## Risk Analysis

- Judgment based solely on one timeframe may generate more false signals 
- Does not consider more factors like volume change, volatility etc.
- Stop loss and take profit settings could be inappropriate, too wide or too tight are both risky

## Optimization Directions

- Combine more factors to confirm entry signal, like volume, moving average etc.  
- Optimize stop loss and take profit algorithms to have more reasonable stop loss and sufficient take profit
- Parameter tuning may be needed for different products  
- Longer timeframe can be tested  

## Summary

The strategy idea is simple and clear overall, using candlestick closing price to determine trend direction and also has stop loss/take profit to control risk, it can serve as a basic strategy for stocks and crypto trading. But with judgment solely based on one timeframe, it tends to generate false signals more easily. There is still much room for improvement by incorporating more factors and tuning parameters to enhance strategy performance.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-08 00:00:00
end: 2024-01-07 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Buy/Sell on Candle Close", overlay=true)

var float prevLowest = na
var float prevHighest = na
var float slDistance = na
var float tpDistance = na

// Specify the desired timeframe here (e.g., "D" for daily, "H" for hourly, etc.)
timeframe = "D"

// Fetching historical data for the specified timeframe
pastLow = request.security(syminfo.tickerid, timeframe, low, lookahead=barmerge.lookahead_on)
pastHigh = request.security(syminfo.tickerid, timeframe, high, lookahead=barmerge.lookahead_on)

if bar_index > 0
    prevLowest := pastLow[1]
    prevHighest := pastHigh[1]

currentClose = close

if not na(prevLowest) and not na(prevHighest)
    slDistance := prevHighest - prevLowest
    tpDistance := 3 * slDistance // Adjusted for 1:3 risk-reward ratio

// Buy trigger when current close is higher than previous highest
if not na(prevLowest) and not na(prevHighest) and currentClose > prevHighest
    strategy.entry("Buy", strategy.long)
    strategy.exit("Buy TP/SL", "Buy", stop=prevLowest - slDistance, limit=prevHighest + tpDistance)

// Sell trigger when current close is lower than previous lowest
if not na(prevLowest) and not na(prevHighest) and currentClose < prevLowest
    strategy.entry("Sell", strategy.short)
    strategy.exit("Sell TP/SL", "Sell", stop=prevHighest + slDistance, limit=prevLowest - tpDistance)

plot(prevLowest, color=color.blue, title="Previous Lowest")
plot(prevHighest, color=color.red, title="Previous Highest")






```

> Detail

https://www.fmz.com/strategy/438017

> Last Modified

2024-01-08 11:11:18
