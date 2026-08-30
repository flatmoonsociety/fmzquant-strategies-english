
> Name

Dual-Moving-Average-Crossover-with-Stochastic-RSI-Overbought-Oversold-Enhanced-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/fd1fb97a1afe2c3fb6.png)

[trans]
#### Overview
This strategy is a trend following trading system that combines dual moving averages and the Stochastic RSI indicator. Use the 21-period and 55-period simple moving averages to determine market trends, and use the overbought and oversold ranges of stochastic RSI to find the optimal entry and exit points to optimize trend trading. On the basis of confirming the upward trend, the strategy looks for buying opportunities in oversold areas and selling opportunities in overbought areas.
#### Strategy Principle
The strategy adopts the following core logic:
1. Trend confirmation: Using the 21-period SMA and the 55-period SMA, when the short-term moving average is above the long-term moving average, the upward trend is confirmed.
2. Entry signal: After confirming the trend, wait for the K line of the stochastic RSI to form a golden cross with the D line in the oversold area below 20.
3. Exit signal: When the K line of the stochastic RSI forms a death cross with the D line in the overbought area above 80, close the position and exit.
4. Signal filtering: Effectively reduce false signals by combining trend and momentum indicators.
#### Strategic Advantages
1. Multiple confirmation mechanism: Improve the reliability of transactions through dual confirmation of trend and momentum.
2. Risk control optimization: Use the overbought and oversold range to choose a better entry point in the direction of the trend.
3. Strong adaptability: strategy parameters can be adjusted according to different market characteristics.
4. Clear signals: The entry and exit conditions are clear and easy to execute.
5. High degree of systematization: The strategy logic is completely systematized, reducing subjective judgment.
#### Strategy Risk
1. Risk of volatile market: Frequent transactions may occur in a volatile market.
2. Lagging risk: The moving average has a certain lag and may miss the best entry opportunity.
3. False breakthrough risk: Stochastic RSI may produce false signals in volatile markets.
4. Parameter sensitivity: Different parameter combinations may lead to large differences in strategy performance.
#### Strategy optimization direction
1. Add volatility filtering: Introduce the ATR indicator to reduce trading frequency during periods of low volatility.
2. Optimize the exit mechanism: consider adding a trailing stop loss or profit target.
3. Market environment classification: dynamically adjust parameters according to different market environments.
4. Increase trading volume confirmation: Add trading volume indicators to verify the validity of the signal.
5. Introduce trend strength indicators: such as ADX, to filter weak trend environments.
#### Summary
This strategy builds a complete trend following trading system by combining classic technical indicators. The strategy improves reliability through multiple signal confirmations while remaining simple and intuitive. Through reasonable parameter optimization and risk management, this strategy has good practical value. It is recommended that traders conduct sufficient backtesting before using it in real trading, and adjust parameters according to specific market characteristics. ||
#### Overview
This strategy is a trend-following trading system that combines dual moving averages with the Stochastic RSI indicator. It uses 21-period and 55-period Simple Moving Averages to determine market trends, while utilizing Stochastic RSI's overbought/oversold zones to optimize entry and exit points, enhancing trend trading effectiveness.

#### Strategy Principles
The strategy employs the following core logic:
1. Trend Confirmation: Uses 21-period SMA and 55-period SMA, confirming an uptrend when the shorter MA is above the longer MA.
2. Entry Signal: After trend confirmation, waits for the Stochastic RSI K-line to form a golden cross with the D-line in the oversold zone below 20.
3. Exit Signal: Closes positions when the Stochastic RSI K-line forms a death cross with the D-line in the overbought zone above 80.
4. Signal Filtering: Effectively reduces false signals by combining trend and momentum indicators.

#### Strategy Advantages
1. Multiple Confirmation Mechanism: Enhances trading reliability through dual confirmation of trend and momentum.
2. Optimized Risk Control: Uses overbought/oversold zones to select optimal entry points in trend direction.
3. Strong Adaptability: Strategy parameters can be adjusted for different market characteristics.
4. Clear Signals: Entry and exit conditions are well-defined and easy to execute.
5. High Systematization: Strategy logic is fully systematic, reducing subjective judgment.

#### Strategy Risks
1. Choppy Market Risk: May generate frequent trades in sideways markets.
2. Lag Risk: Moving averages have inherent lag, potentially missing optimal entry points.
3. False Breakout Risk: Stochastic RSI may generate false signals in ranging markets.
4. Parameter Sensitivity: Different parameter combinations may lead to significant performance variations.

#### Strategy Optimization Directions
1. Add Volatility Filter: Incorporate ATR indicator to reduce trading frequency during low volatility periods.
2. Optimize Exit Mechanism: Consider adding trailing stops or profit targets.
3. Market Environment Classification: Dynamically adjust parameters based on different market conditions.
4. Add Volume Confirmation: Include volume indicators to verify signal validity.
5. Introduce Trend Strength Indicator: Such as ADX, to filter weak trend environments.

#### Summary
This strategy constructs a complete trend-following trading system by combining classic technical indicators. While maintaining simplicity and intuitiveness, it enhances reliability through multiple signal confirmations. With proper parameter optimization and risk management, the strategy demonstrates good practical value. Traders are advised to conduct thorough backtesting before live implementation and adjust parameters according to specific market characteristics.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2022-02-11 00:00:00
end: 2025-02-08 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=6
strategy("SMA & Stoch RSI Buy Strategy with K > 80 Exit", overlay=true)

// Input parameters for the SMAs
sma21Length = input(21, title="21 SMA Length")
sma55Length = input(55, title="55 SMA Length")

// Input parameters for the Stochastic RSI
stochRsiLength = input(14, title="Stoch RSI Length")
stochRsiK = input(3, title="Stoch RSI %K Smoothing")
stochRsiD = input(3, title="Stoch RSI %D Smoothing")

// Calculate the SMAs
sma21 = ta.sma(close, sma21Length)
sma55 = ta.sma(close, sma55Length)

// Calculate the Stochastic RSI
rsiValue = ta.rsi(close, stochRsiLength)
stochRsi = ta.stoch(rsiValue, rsiValue, rsiValue, stochRsiLength)
stochRsiKLine = ta.sma(stochRsi, stochRsiK)
stochRsiDLine = ta.sma(stochRsiKLine, stochRsiD)

// Buy signal conditions
smaCondition = sma21 > sma55
stochRsiCondition = ta.crossover(stochRsiKLine, stochRsiDLine) and stochRsiKLine < 20

// Entry condition
buySignal = smaCondition and stochRsiCondition

// Exit condition: Stochastic RSI K > 80 and K crosses below D
exitCondition = ta.crossunder(stochRsiKLine, stochRsiDLine) and stochRsiKLine > 80

// Execute buy order on signal
if (buySignal)
    strategy.entry("Buy", strategy.long)

// Exit the trade on the modified exit condition
if (exitCondition)
    strategy.close("Buy")

// Plot the SMAs
plot(sma21, color=color.blue, title="21 SMA")
plot(sma55, color=color.red, title="55 SMA")

// Plot Stochastic RSI for reference (not overlayed)
hline(20, "Stoch RSI 20", color=color.gray, linestyle=hline.style_dotted)
hline(80, "Stoch RSI 80", color=color.gray, linestyle=hline.style_dotted)
plot(stochRsiKLine, title="%K Line", color=color.green)
plot(stochRsiDLine, title="%D Line", color=color.red)
```

> Detail

https://www.fmz.com/strategy/481352

> Last Modified

2025-02-10 14:40:04
