
> Name

Short-Term Scalable-Trend-Following-Strategy Based on Dual-Moving-Average-and-RSI-Based-Short-Term-Scalable-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/18fb6475229dbc77bb1.png)

[trans]
#### Overview
This strategy uses two moving averages (fast and slow) along with the Relative Strength Index (RSI) to identify short-term trends and overbought and oversold conditions in the market. When the fast moving average crosses the slow moving average from bottom to top, and the RSI is below the oversold level, the strategy opens a long position; when the fast moving average crosses the slow moving average from top to bottom, and the RSI is above the overbought level, the strategy opens a short position. The strategy uses moving average crossovers and RSI levels to identify entry and exit points to capture short-term price trends.
#### Strategy Principle
1. Calculate the fast moving average (default period is 5) and slow moving average (default period is 10).
2. Calculate the relative strength index RSI (default period is 7), and set overbought and oversold levels (default is 80 and 20 respectively).
3. Open a long position when the fast moving average crosses the slow moving average from bottom to top and the RSI is below the oversold level.
4. Open a short position when the fast moving average crosses the slow moving average from top to bottom and the RSI is above the overbought level.
5. Close the position when the fast moving average crosses the slow moving average again, or when the RSI exceeds the opposite overbought/oversold level.
#### Strategic Advantages
1. Combine the two indicators of moving average and RSI to improve the reliability and accuracy of the signal.
2. By capturing short-term trends, it is suitable for short-term trading in volatile markets.
3. Adjustable parameters, high flexibility, and easy to adapt to different market environments and trading styles.
4. The logic is clear and easy to understand and implement.
#### Strategy Risk
1. In a volatile market, frequent cross signals may lead to excessive transaction times and fee losses.
2. The duration of the short-term trend may be short and the profit potential is limited.
3. The ability to grasp long-term trends is weak and may miss the profits brought by big trends.
4. Improper parameter settings may cause signal failure or an increase in false signals.
#### Strategy optimization direction
1. Introduce other technical indicators or price action patterns, such as MACD, Bollinger Bands, etc., to improve the reliability and filtering effect of signals.
2. Optimize parameter selection, such as adjusting the period of the moving average and the overbought and oversold levels of RSI according to different market characteristics and trading varieties.
3. Add stop-loss and take-profit mechanisms to control the risk exposure and profit expectations of a single transaction.
4. Combined with multi-time frame analysis, such as determining the general trend at the daily level and conducting actual transactions at the hour or minute level to improve the accuracy of trend grasp.
5. Consider adding position management and money management strategies, such as dynamically adjusting the position size of each transaction based on market volatility and personal risk preferences.
#### Summary
This strategy captures price trends in the short term by combining double moving averages and RSI indicators, and is suitable for short-term trading in volatile markets. The strategy logic is clear, the parameters are flexible, and it is easy to implement and optimize. However, in a volatile market, too many trading signals may be generated, and the ability to grasp long-term trends is weak. Therefore, in practical applications, methods such as introducing other indicators, optimizing parameter selection, and adding risk management measures can be considered to improve the robustness and profitability of the strategy.
|| 

#### Overview
This strategy uses two moving averages (a fast moving average and a slow moving average) and the Relative Strength Index (RSI) to identify short-term market trends and overbought/oversold conditions. When the fast moving average crosses above the slow moving average and the RSI is below the oversold level, the strategy enters a long position. When the fast moving average crosses below the slow moving average and the RSI is above the overbought level, the strategy enters a short position. The strategy determines entry and exit points based on the crossover of the moving averages and RSI levels to capture short-term price trends.

#### Strategy Principles
1. Calculate the fast moving average (default period of 5) and the slow moving average (default period of 10).
2. Calculate the Relative Strength Index (RSI) with a default period of 7 and set the overbought and oversold levels (default values of 80 and 20, respectively).
3. Enter a long position when the fast moving average crosses above the slow moving average and the RSI is below the oversold level.
4. Enter a short position when the fast moving average crosses below the slow moving average and the RSI is above the overbought level.
5. Close the position when the fast moving average crosses the slow moving average again or when the RSI exceeds the opposite overbought/oversold level.

#### Strategy Advantages
1. Combines two indicators, moving averages and RSI, to improve signal reliability and accuracy.
2. Suitable for short-term trading in volatile markets by capturing short-term trends.
3. Adjustable parameters provide flexibility and adaptability to different market conditions and trading styles.
4. Clear and easy-to-understand logic, making it simple to implement.

#### Strategy Risks
1. In choppy markets, frequent crossover signals may lead to excessive trading and commission costs.
2. The duration of short-term trends may be limited, resulting in limited profit potential.
3. Weak ability to capture long-term trends, potentially missing out on profits from major trends.
4. Improper parameter settings may lead to ineffective or false signals.

#### Strategy Optimization Directions
1. Incorporate additional technical indicators or price action patterns, such as MACD or Bollinger Bands, to improve signal reliability and filtering.
2. Optimize parameter selection based on different market characteristics and trading instruments, adjusting the periods of moving averages and RSI overbought/oversold levels accordingly.
3. Implement stop-loss and take-profit mechanisms to control risk exposure and profit expectations for each trade.
4. Combine multiple timeframe analysis, such as identifying the major trend on the daily timeframe and executing actual trades on hourly or minute timeframes, to improve trend-capturing accuracy.
5. Consider incorporating position sizing and money management strategies, such as dynamically adjusting the position size for each trade based on market volatility and personal risk preferences.

#### Summary
This strategy combines dual moving averages and the RSI indicator to capture short-term price trends, making it suitable for short-term trading in volatile markets. The strategy logic is clear, parameters are flexible, and it is easy to implement and optimize. However, it may generate excessive trading signals in choppy markets and has a weak ability to capture long-term trends. Therefore, in practical applications, consider introducing additional indicators, optimizing parameter selection, implementing risk management measures, and other approaches to improve the strategy's robustness and profitability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|5|Fast MA Length|
|v_input_2|10|Slow MA Length|
|v_input_3|7|RSI Length|
|v_input_4|20|RSI Oversold Level|
|v_input_5|80|RSI Overbought Level|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-03-24 00:00:00
end: 2024-03-25 05:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Short-Term Scalp Trading Strategy", overlay=true)

// Define strategy parameters
fastMA_length = input(5, title="Fast MA Length")
slowMA_length = input(10, title="Slow MA Length")
rsi_length = input(7, title="RSI Length")
rsi_oversold = input(20, title="RSI Oversold Level")
rsi_overbought = input(80, title="RSI Overbought Level")

// Calculate Moving Averages
fastMA = ta.sma(close, fastMA_length)
slowMA = ta.sma(close, slowMA_length)

// Calculate RSI
rsi = ta.rsi(close, rsi_length)

// Define entry conditions
longCondition = ta.crossunder(fastMA, slowMA) and rsi < rsi_oversold
shortCondition = ta.crossover(fastMA, slowMA) and rsi > rsi_overbought

// Enter long position
strategy.entry("Long", strategy.long, when=longCondition)

// Enter short position
strategy.entry("Short", strategy.short, when=shortCondition)

// Define exit conditions
longExitCondition = ta.crossunder(fastMA, slowMA) or ta.crossover(rsi, rsi_overbought)
shortExitCondition = ta.crossover(fastMA, slowMA) or ta.crossunder(rsi, rsi_oversold)

// Exit long position
if (longExitCondition)
    strategy.close("Exit Long", "Long")

// Exit short position
if (shortExitCondition)
    strategy.close("Exit Short", "Short")

// Plot buy and sell signals
plotshape(series=longCondition, title="Buy Signal", location=location.belowbar, color=color.green, style=shape.triangleup, size=size.small)
plotshape(series=shortCondition, title="Sell Signal", location=location.abovebar, color=color.red, style=shape.triangledown, size=size.small)

```

> Detail

https://www.fmz.com/strategy/446756

> Last Modified

2024-04-01 10:58:30
