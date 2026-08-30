
> Name

Moving-Average-Crossover-with-Trailing-Stop-Loss-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/f6222f31dd29f50aac.png)

[trans]
#### Overview
This strategy uses two simple moving averages (SMA) with different periods to capture price trends, and utilizes the relative strength index (RSI) and average true range (ATR) indicators to optimize trading signals and risk management. When the short-term SMA crosses above the long-term SMA, a buy signal is generated, and vice versa, a sell signal is generated. At the same time, this strategy uses a moving take-profit and stop-loss method to dynamically adjust the take-profit and stop-loss positions according to price trends to better protect profits and control risks.
#### Strategy Principle
1. Calculate two SMAs with different periods. The default periods are 10 and 30.
2. When the short-term SMA crosses above the long-term SMA, a buy signal is generated; when the short-term SMA crosses below the long-term SMA, a sell signal is generated.
3. When buying, set the stop loss and take profit levels based on the current closing price. The default stop loss level is 2 units below the closing price, and the take profit level is 6 units above the closing price.
4. During the position holding process, the take-profit level is dynamically adjusted according to the price trend to better protect profits.
5. Use the 14-period RSI indicator and ATR indicator to assist in judging market trends and volatility and optimize trading signals.
#### Strategic Advantages
1. Simple and easy to understand: This strategy is based on the classic moving average crossover principle, with clear logic and easy to understand and implement.
2. Trend following: Through two SMAs of different periods, we can effectively capture the mid- to long-term trends of the market and adapt to different market environments.
3. Dynamic stop-profit and stop-loss: Using the moving stop-profit and stop-loss method, the stop-profit and stop-loss positions are adjusted in real time according to the price trend, which can not only protect profits but also control risks.
4. Multi-indicator collaboration: Combine RSI and ATR indicators to more comprehensively assess market trends and volatility and improve the reliability of trading signals.
#### Strategy Risk
1. Parameter optimization risk: Parameters such as SMA cycle and stop-profit and stop-loss positions need to be optimized according to different markets and varieties. Improper parameter settings may lead to poor strategy performance.
2. Volatile market risk: In a volatile market environment, frequent trading signals may lead to excessive trading and rapid loss of funds.
3. Trend turning risk: When the market trend turns, this strategy may suffer continuous losses.
#### Strategy optimization direction
1. Dynamic parameter optimization: According to market changes, key parameters such as SMA cycle and stop-profit and stop-loss positions are adjusted in real time to improve the adaptability of the strategy.
2. Signal filtering: Introduce other technical indicators or market sentiment indicators to conduct secondary confirmation of trading signals to reduce misjudgments and over-trading.
3. Position management: Dynamically adjust the position size based on market volatility and account risk tolerance to control single transaction risks.
4. Multi-variety synergy: Apply this strategy to multiple related varieties, and reduce the overall portfolio risk through correlation hedging between varieties.
#### Summary
The moving average crossover moving stop-profit and stop-loss strategy is a quantitative trading strategy based on the principles of classic technical analysis. It captures market trends through two SMAs of different periods and uses the moving stop-profit and stop-loss method to dynamically control risks. At the same time, this strategy also combines the RSI and ATR indicators to more comprehensively assess the state of the market. Although the logic of this strategy is clear and easy to implement, issues such as parameter optimization, market shock risks, and trend turning risks still need to be paid attention to in practical applications. In the future, the strategy can be optimized from aspects such as dynamic parameter optimization, signal filtering, position management and multi-variety collaboration to improve its stability and profitability.
||

#### Overview
This strategy uses two Simple Moving Averages (SMAs) with different periods to capture price trends and incorporates the Relative Strength Index (RSI) and Average True Range (ATR) indicators to optimize trade signals and risk management. A buy signal is generated when the short-term SMA crosses above the long-term SMA, and a sell signal is generated when the opposite occurs. The strategy employs a trailing stop loss method, dynamically adjusting the take profit and stop loss levels based on price movements to better protect profits and control risks.

#### Strategy Principle
1. Calculate two SMAs with different periods, defaulting to 10 and 30.
2. Generate a buy signal when the short-term SMA crosses above the long-term SMA, and a sell signal when the short-term SMA crosses below the long-term SMA.
3. Upon buying, set the stop loss and take profit levels based on the current closing price, defaulting to 2 units below and 6 units above the closing price, respectively.
4. Dynamically adjust the take profit level during the holding period to better protect profits based on price movements.
5. Use the 14-period RSI and ATR indicators to assist in assessing market trends and volatility, optimizing trade signals.

#### Strategy Advantages
1. Simplicity: The strategy is based on the classic moving average crossover principle, with clear logic and easy to understand and implement.
2. Trend following: By using two SMAs with different periods, the strategy effectively captures medium to long-term market trends and adapts to various market environments.
3. Dynamic stop loss and take profit: The trailing stop loss method dynamically adjusts the take profit and stop loss levels based on price movements, protecting profits while controlling risks.
4. Multi-indicator synergy: Combining RSI and ATR indicators provides a more comprehensive assessment of market trends and volatility, improving the reliability of trade signals.

#### Strategy Risks
1. Parameter optimization risk: SMA periods, take profit and stop loss levels, and other parameters need to be optimized for different markets and instruments. Improper parameter settings may lead to poor strategy performance.
2. Choppy market risk: In choppy market conditions, frequent trade signals may result in overtrading and rapid capital depletion.
3. Trend reversal risk: When market trends reverse, the strategy may experience consecutive losses.

#### Strategy Optimization Directions
1. Dynamic parameter optimization: Dynamically adjust key parameters such as SMA periods and take profit/stop loss levels based on market changes to improve the strategy's adaptability.
2. Signal filtering: Introduce additional technical indicators or market sentiment indicators for secondary confirmation of trade signals, reducing misjudgments and overtrading.
3. Position sizing: Dynamically adjust position sizes based on market volatility and account risk tolerance to control single trade risk.
4. Multi-instrument synergy: Apply the strategy to multiple related instruments and use inter-instrument correlations for hedging to reduce overall portfolio risk.

#### Summary
The Moving Average Crossover with Trailing Stop Loss Strategy is a quantitative trading strategy based on classic technical analysis principles. It captures market trends using two SMAs with different periods and dynamically controls risk using a trailing stop loss method. The strategy also incorporates RSI and ATR indicators for a more comprehensive assessment of market conditions. Although the strategy has clear logic and is easy to implement, it is essential to consider issues such as parameter optimization, choppy market risk, and trend reversal risk in practical applications. Future optimizations can focus on dynamic parameter optimization, signal filtering, position sizing, and multi-instrument synergy to improve the strategy's stability and profitability.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-05-23 00:00:00
end: 2024-05-28 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
// suitable for : AMZN - 30 minutes, MSFT - 30 minutes, NVDA -15 minutes

strategy("AAPL-SIMPLE_SMA", overlay=true)

// Create Indicator's

// Create Indicator's
shortSMA = ta.sma(close, 10)
longSMA = ta.sma(close, 30)
rsi = ta.rsi(close, 14)
atr = ta.atr(14)
qty = 1

// Specify crossover conditions
longCondition = ta.crossover(shortSMA, longSMA)
shortCondition = ta.crossunder(shortSMA, longSMA)

// // Execute trade if condition is True
if (longCondition)
    stopLoss = close -2
    // stopLoss=1
    takeProfit = close +6

    action = "buy"
    strategy.entry("long", strategy.long, qty=qty)
    // strategy.exit("exit", "long", stop=stopLoss, limit=takeProfit)
    strategy.exit("exit", "long",  limit=takeProfit)
    alert('{"TICKER":"'+syminfo.ticker+'","ACTION":"'+action+'","PRICE":"'+str.tostring(close)+'","STOPLOSS":"'+str.tostring(stopLoss)+'","TAKEPROFIT":"'+str.tostring(takeProfit)+'","QTY":"'+str.tostring(qty)+'"}')




plot(shortSMA)
plot(longSMA, color=color.purple)
```

> Detail

https://www.fmz.com/strategy/452821

> Last Modified

2024-05-29 17:02:19
