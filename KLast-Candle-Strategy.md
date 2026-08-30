
> Name

Last-Candle-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/4d2b6eea5c7ae3d67be44045bb0e9e1d1059efdedcb57ea55f8d36439efe7b4a.png)
[trans]

## Overview
The last K-line strategy is a trend following strategy. It determines the direction of the market trend by analyzing the relationship between the closing price and the opening price of the last K-line, thereby generating trading signals.
## Strategy Principle
The core logic of this strategy is:
1. Calculate the opening price and closing price of the last K line
2. If the opening price is lower than the closing price, it is judged as an upward trend and a buy signal is generated.
3. If the opening price is higher than the closing price, it is judged to be a downward trend and a sell signal is generated.
4. Open a long or short position based on the generated trading signal.
5. Set stop loss and take profit prices, exit strategy
Specifically, in the strategy, the trend direction is determined based on the price comparison results by requesting the opening price and closing price data of the last K line. If it is an upward trend, open a long order with a market price order when the K line closes; if it is a downward trend, open a short order with a market price order when the K line closes.
Then set the stop loss and take profit prices. The stop-loss price for long orders is the opening price of the K-line multiplied by a coefficient, and the take-profit price is the current closing price. The opposite is true for short orders. When the price triggers stop loss or take profit, the corresponding position will be closed and exited.
## Advantage Analysis
- The strategy logic is simple and clear, easy to understand and implement
- Use the last K-line to determine the trend and capture the recent price trend
- There are both stop loss and take profit to limit downside risk
## Risk Analysis
- There may be a correction or shock in the last K line, increasing the probability of whipsaw
- Judging the trend based solely on the last K-line may lead to trapping, and should be judged in combination with trend indicators.
- Insufficient backtest data may lead to overfitting
Risks can be reduced by combining trend indicator confirmation, optimizing stop-loss and take-profit logic, and expanding the backtesting cycle and market environment.
## Optimization direction
- Can combine MA, MACD and other indicators to filter entry opportunities
- Stop loss range can be set based on ATR
- Machine learning models can be introduced to determine the trend direction
- Can optimize stop loss and take profit strategies, such as trailing stop loss, batch take profit, etc.
## Summarize
Finally, the K-line strategy is a simple trend following strategy. It quickly determines the trend direction and trades through the last K line. The strategy logic is simple, easy to implement, and conforms to the trend tracking idea. At the same time, stop loss and take profit are set to control risks. However, it is easy to get trapped by relying solely on the last K line, so it should be used in conjunction with trend indicators. In addition, this strategy has a lot of room for expansion, and more technical indicators or machine learning models can be introduced to improve performance.
||


## Overview

The Last Candle strategy is a trend following strategy that determines market trend direction based on the relationship between the closing price and opening price of the last candlestick, and generates trading signals accordingly.  

## Strategy Logic

The core logic of this strategy is:

1. Calculate the opening price and closing price of the last candlestick
2. If the opening price is lower than the closing price, judge it as an uptrend and generate a buy signal  
3. If the opening price is higher than the closing price, judge it as a downtrend and generate a sell signal
4. Enter long or short positions based on the trading signals 
5. Set stop loss and take profit prices to exit positions

Specifically, the strategy requests the opening price and closing price data of the last candlestick, and determines the trend direction based on price comparison. If it is an uptrend, a market order to buy will be placed when the candlestick closes. If it is a downtrend, a market order to sell will be placed.

After that, stop loss and take profit prices are set. For long positions, the stop loss price is the opening price of that candlestick multiplied by a coefficient, and take profit price is the current closing price. For short positions it is the opposite. When price triggers either stop loss or take profit, the corresponding position will be closed.

## Advantage Analysis 

- Simple and clear strategy logic, easy to understand and implement
- Captures latest price change trend by using last candlestick 
- Has both stop loss and take profit to limit downside risk

## Risk Analysis

- Last candlestick may have pullback or sideways, increasing whipsaw probability
- Judging trend merely based on last candle may cause being trapped, should incorporate trend indicators
- Insufficient backtesting data may lead to overfitting

Risks can be reduced by incorporating trend indicators for confirmation, optimizing stop loss/take profit logic, expanding backtest period and market environments.

## Optimization Directions

- Incorporate MA, MACD etc. to filter entry timing
- Use ATR to set stop loss percentage 
- Introduce machine learning models to determine trend direction
- Optimize stop loss/take profit strategies, like trailing stop loss, partial take profits etc.

## Conclusion

The Last Candle strategy is a simple trend following strategy. It quickly judges trend direction using the last candlestick and trades accordingly. The logic is simple and easy to implement, aligning with the idea of trend following. Stop loss and take profit are also set to control risks. However, just relying on the last candlestick could easily get trapped, so it should be used together with trend indicators. Also, there is still large room for improving this strategy, by introducing more technical indicators or machine learning models.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-14 00:00:00
end: 2023-12-20 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Last Candle Strategy with Date Range", overlay=true)

// Define the start and end dates for the backtest
startDate = timestamp(2015, 01, 01, 00, 00)
endDate = timestamp(2023, 11, 24, 23, 59)

// Check if the current bar is within the specified date range
withinDateRange = time >= startDate and time <= endDate

// If outside the date range, skip the strategy logic
if (not withinDateRange)
    strategy.close_all()

// Calculate the opening and closing values for the last candle
lastCandleOpen = request.security(syminfo.tickerid, "D", open[1], lookahead=barmerge.lookahead_on)
lastCandleClose = request.security(syminfo.tickerid, "D", close[1], lookahead=barmerge.lookahead_on)

// Determine the trade direction based on the last candle
tradeDirection = lastCandleOpen < lastCandleClose ? 1 : -1  // 1 for buy, -1 for sell

// Plot the last candle's opening and closing values on the chart
plot(lastCandleOpen, color=color.blue, title="Last Candle Open")
plot(lastCandleClose, color=color.red, title="Last Candle Close")

// Execute strategy orders
if (withinDateRange)
    if (tradeDirection == 1)
        strategy.entry("Buy", strategy.long)

    if (tradeDirection == -1)
        strategy.entry("Sell", strategy.short)

// Set stop loss and take profit
stopLoss = 0.01 * lastCandleOpen
takeProfit = close

// Exit strategy
strategy.exit("StopLoss/Profit", from_entry="Buy", loss=stopLoss, profit=takeProfit)
strategy.exit("StopLoss/Profit", from_entry="Sell", loss=stopLoss, profit=takeProfit)


```

> Detail

https://www.fmz.com/strategy/436112

> Last Modified

2023-12-21 12:15:23
