
> Name

Daily K-line breakout strategyDaily-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/16de630a330e35a2b5f.png)

[trans]

### Overview
The daily K-line breakout strategy is a simple trend following strategy based on the daily K-line. It judges the market trend by observing the relationship between the closing price and the opening price of the previous day's K-line, thereby generating trading signals.
### Strategy Principles
The core logic of this strategy is:
If the K-line entity of the previous day is green (the closing price is higher than the opening price), it means that the previous day was an upward trend, and this strategy will go long when the market opens the next day; if the K-line entity of the previous day is red (the closing price is lower than the opening price), it means that the previous day was a downward trend, and this strategy will go short when the market opens the next day.
In this simple way, the strategy can determine the market trend within the latest K-line cycle and trade accordingly. This allows you to follow recent market trends and achieve trend following trading.
Specifically, the strategy's trading signals are generated as follows:
1. At the opening of each trading day, obtain the K-line data of the previous day
2. Compare the opening price and closing price of the previous day's K-line
3. If the opening price is lower than the closing price (green K line), a long signal is generated, and you will go long in proportion to the available funds.
4. If the opening price is higher than the closing price (red K line), a short signal is generated, and the short position is made in proportion to the available funds.
5. Use Stop Loss to Exit Long and Short Positions
Through this logic, the strategy can capture the price trend within a shorter period to make profits.
### Strategic Advantages
This strategy mainly has the following advantages:
1. **Simple and clear**. The core logic directly compares the K-line entity color, which is very concise and easy to understand and implement.
2. **Follow the trends**. Able to determine the trend direction of the latest trading day and follow the price trend of a shorter period.
3. **Flexible adjustment**. You can adjust the profit and risk characteristics of the strategy by adjusting parameters such as position ratio and stop loss range.
4. **Easy to optimize**. If you add multiple cycle judgments, data fitting, etc., you can continue to optimize and improve the stability of the strategy.
### Risks and Improvements
This strategy also has some risks and areas that can be optimized:
1. **Catch rebound risk**. The strategy only looks at the single-day K-line entity, which may catch a rebound rather than a trend in a volatile market. This can be optimized by adding more K lines or indicators as consolidation judgments.
2. **Short Risk**. Short selling has bottomless risks, and strict stop loss is required to control losses.
3. **Parameter optimization**. Parameters such as stop loss width and position size can continue to be optimized to balance income risks.
4. **Integration of technical indicators**. More technical indicators can be added to judge and improve the stability of the strategy.
### Summarize
The daily K-line breakthrough strategy judges the market trend through a simple and effective daily comparison method, and can seize the short-term trend for trading. The advantage of the strategy is that it is simple, clear and easy to operate, but there is also the risk of being intercepted by rebound. By further optimizing parameter settings and adding more technical indicators, the stability and reliability of the strategy can be improved.

||


### Overview

The daily breakout strategy is a simple trend following strategy based on daily candlestick charts. It generates trading signals by observing the relationship between the previous day's opening and closing prices to determine market momentum.  

### Strategy Logic  

The core logic of this strategy is:

If the previous day's candlestick body is green (closing price higher than opening price), it indicates an upward trend on that day. The strategy will go long at the next day's opening. If the previous day's candlestick body is red (closing price lower than opening price), it indicates a downward trend. The strategy will go short at the next day's opening.  

By this simple way, the strategy can identify the market momentum within the recent one candlestick cycle and make trades accordingly. This allows the strategy to follow the latest market trend.

Specifically, the strategy generates trading signals as follows:  

1. Get the previous trading day's candlestick data at market open each day  
2. Compare the opening and closing prices of that candlestick
3. If open < close (green candlestick), generate long signal, go long at a percentage of available funds  
4. If open > close (red candlestick), generate short signal, go short at a percentage of available funds
5. Use stop loss to exit positions  

Through this logic, the strategy can capitalize on short-term price trends.

### Advantages  

The main advantages of this strategy include:  

1. **Simplicity** - The core logic directly compares candlestick color and is very simple and clear.  
2. **Trend following** - It identifies the trend direction of the latest trading day, following shorter-term momentum. 
3. **Flexibility** - Parameters like position sizing, stop loss can be adjusted to modify risk vs. reward.  
4. **Optimization potential** - More enhancements can be added, like multiple timeframe analysis and data fitting to improve robustness.  

### Risks and Improvements

Some risks and improvement areas:

1. **Whipsaw risk** - It only looks at the daily candle, so may falsely buy pullbacks instead of actual trend in ranging markets. Additional timeframe or indicators can be added to judge consolidation.  
2. **Shorting risk** - Short positions have unlimited downside risk. Strict stop loss needs to be implemented.
3. **Parameter tuning** - Fine tune stop loss level, position sizing etc. to achieve better risk-adjusted returns.  
4. **Add indicators** - Incorporate more technical indicators to improve robustness and stability.

### Conclusion  

The daily breakout strategy identifies market momentum through simple and effective comparison of daily candlesticks, allowing it to trade in the direction of shorter-term trends. While simple and easy to implement, it has whipsaw risks. Further optimizations on parameters and additional indicators can enhance strategy reliability.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-26 00:00:00
end: 2023-08-30 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Daily Candle Strategy", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=0.0)

// Input parameters
initialCapital = 10000
riskFactor = 3500

// Calculate the opening and closing values for the last day's candle
lastDayOpen = request.security(syminfo.tickerid, "D", open[1], lookahead=barmerge.lookahead_on)
lastDayClose = request.security(syminfo.tickerid, "D", close[1], lookahead=barmerge.lookahead_on)

// Determine the color of the last day's candle
lastDayColor = lastDayOpen < lastDayClose ? color.green : color.red

// Plot the last day's candle on the chart
plotshape(series=na, color=lastDayColor, style=shape.triangledown, location=location.abovebar)

// Calculate trade size based on available capital at last day's closing
availableCapital = strategy.equity
tradeSize = availableCapital / riskFactor

// Trading conditions
buyCondition = lastDayColor == color.green
sellCondition = lastDayColor == color.red

// Execute strategy orders with calculated trade size
strategy.entry("Buy", strategy.long, qty=tradeSize, when=buyCondition)
strategy.entry("Sell", strategy.short, qty=tradeSize, when=sellCondition)

// Exit strategy
stopLoss = 0.001 * lastDayOpen * tradeSize
strategy.exit("StopLoss/Profit", from_entry="Buy", loss=stopLoss)
strategy.exit("StopLoss/Profit", from_entry="Sell", loss=stopLoss)

// Plot stop loss level on the chart
plot(stopLoss, color=color.red, linewidth=2, title="Stop Loss")


```

> Detail

https://www.fmz.com/strategy/437411

> Last Modified

2024-01-02 13:57:42
