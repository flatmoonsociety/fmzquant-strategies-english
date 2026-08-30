
> Name

Trend-enhanced RSI-ADX Linear Regression Prediction Trading Strategy-Enhanced-Trend-RSI-ADX-Linear-Regression-Prediction-Trading-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d87172fc006e0c5fdd49.png)
![IMG](https://www.fmz.com/upload/asset/2d8c51cead5aa2583aff3.png)




[trans]
#### Overview
This strategy is a trend following system that combines technical indicators and machine learning methods. The strategy integrates the Relative Strength Index (RSI), the Average Trend Index (ADX) and the linear regression prediction model to determine market trends and trading opportunities through multi-dimensional analysis. This strategy operates on a 5-minute time period and implements a complete trading decision-making system by combining RSI overbought and oversold signals, ADX trend confirmation and linear regression prediction.
#### Strategy Principle
The strategy uses a three-layer filtering mechanism to determine trading signals:
1. The RSI indicator is used to identify overbought and oversold conditions. When the RSI exceeds 30 (oversold), it generates a long signal, and when it exceeds 70 (overbought), it generates a short signal.
2. The ADX indicator is used to confirm the strength of the trend. Trading is only allowed when ADX is greater than 25 to ensure operations in a strong trend environment.
3. The linear regression prediction module analyzes the data of the past 20 price cycles, calculates the slope and intercept of the price trend, and predicts the next price level.
Only when these three conditions are met at the same time (the direction is consistent), the strategy will issue a trading signal.
#### Strategic Advantages
1. Multi-dimensional verification: Combining technical indicators and statistical prediction methods to provide more reliable trading signals
2. Trend confirmation: Use ADX filtering to ensure that you only trade in strong trending markets and avoid false signals that shake the market.
3. Forecasting ability: Introducing a linear regression forecast model to enable forward-looking analysis of price trends
4. High flexibility: the main parameters can be adjusted according to different market conditions
5. Clear execution: Clear trading rules and strict signal generation conditions reduce the impact of subjective judgments
#### Strategy Risk
1. Parameter sensitivity: The strategy effect strongly depends on the parameter settings of RSI, ADX and return period.
2. Lagging risk: Technical indicators themselves have a certain lag, which may lead to a slight delay in entry timing.
3. Trend reversal risk: When the trend suddenly reverses, losses may occur due to the system not responding in time.
4. Overfitting risk: Linear regression prediction may overfit historical data, affecting prediction accuracy.
5. Dependence on market conditions: Strategies may perform poorly in volatile markets
#### Strategy optimization direction
1. Dynamic parameter adjustment: Introduce an adaptive parameter mechanism to automatically adjust the parameters of RSI and ADX according to market volatility
2. Add market environment filtering: add volatility indicators, adjust strategy parameters or suspend trading under different market environments
3. Optimize prediction models: Consider using more complex machine learning models, such as LSTM or random forests, to improve prediction accuracy
4. Improve risk management: add a dynamic stop-loss mechanism and adjust the stop-loss position according to market fluctuations
5. Add trading time filtering: avoid low liquidity periods and important news release periods
#### Summary
This strategy builds a relatively complete trading system by combining traditional technical analysis and modern forecasting methods. The core advantage of the strategy lies in the multi-dimensional signal confirmation mechanism, which can effectively reduce the impact of false signals. By improving the prediction model, optimizing the parameter adjustment mechanism and enhancing risk management, the strategy still has a lot of room for optimization. In practical applications, it is recommended that investors make appropriate adjustments to the strategy parameters based on specific market characteristics and their own risk tolerance. ||
#### Overview
This strategy is a trend-following system that combines technical indicators with machine learning methods. The strategy integrates the Relative Strength Index (RSI), Average Directional Index (ADX), and linear regression prediction model to analyze market trends and trading opportunities from multiple dimensions. Operating on a 5-minute timeframe, it creates a complete trading decision system by combining RSI overbought/oversold signals, ADX trend confirmation, and linear regression predictions.

#### Strategy Principles
The strategy employs a three-layer filtering mechanism to determine trading signals:
1. RSI indicator identifies overbought/oversold conditions, generating long signals at RSI 30 (oversold) and short signals at RSI 70 (overbought)
2. ADX indicator confirms trend strength, allowing trades only when ADX is above 25 to ensure operations in strong trend environments
3. Linear regression prediction module analyzes data from the past 20 price periods to calculate price trend slope and intercept, predicting the next price level
Trading signals are only generated when all three conditions align in direction.

#### Strategy Advantages
1. Multi-dimensional verification: Combines technical indicators and statistical prediction methods for more reliable trading signals
2. Trend confirmation: Uses ADX filtering to ensure trading only in strong trend markets, avoiding false signals in ranging markets
3. Predictive capability: Incorporates linear regression prediction model for forward-looking price analysis
4. High flexibility: Key parameters can be adjusted according to different market conditions
5. Clear execution: Trading rules are clear and signal generation conditions are strict, reducing subjective judgment impact

#### Strategy Risks
1. Parameter sensitivity: Strategy effectiveness heavily depends on RSI, ADX, and regression period parameter settings
2. Lag risk: Technical indicators have inherent lag, potentially causing delayed entry timing
3. Trend reversal risk: Sudden trend reversals may cause losses due to system response delay
4. Overfitting risk: Linear regression predictions may overfit historical data, affecting prediction accuracy
5. Market condition dependency: Strategy may underperform in ranging markets

#### Strategy Optimization Directions
1. Dynamic parameter adjustment: Introduce adaptive parameter mechanisms to automatically adjust RSI and ADX parameters based on market volatility
2. Enhanced market environment filtering: Add volatility indicators to adjust strategy parameters or pause trading in different market conditions
3. Improved prediction model: Consider using more sophisticated machine learning models like LSTM or Random Forests for better prediction accuracy
4. Enhanced risk management: Add dynamic stop-loss mechanisms that adjust based on market volatility
5. Trading time filters: Avoid low liquidity periods and major news release times

#### Summary
This strategy builds a relatively complete trading system by combining traditional technical analysis with modern prediction methods. Its core advantage lies in the multi-dimensional signal confirmation mechanism, effectively reducing the impact of false signals. There is significant optimization potential through improving the prediction model, optimizing parameter adjustment mechanisms, and enhancing risk management. In practical application, investors should adjust strategy parameters according to specific market characteristics and their risk tolerance.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-01-20 00:00:00
end: 2025-02-19 08:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Binance","currency":"SOL_USDT"}]
*/

//@version=5
strategy("RSI + ADX + ML-like Strategy (5min)", overlay=true)

// ———— 1. Inputs ————
rsiLength = input(14, "RSI Length")
adxLength = input(14, "ADX Length")
mlLookback = input(20, "ML Lookback (Bars)")

// ———— 2. Calculate Indicators ————
// RSI
rsi = ta.rsi(close, rsiLength)

// ADX
[diPlus, diMinus, adx] = ta.dmi(adxLength, adxLength)

// ———— 3. Simplified ML-like Component (Linear Regression) ————
var float predictedClose = na
sumX = math.sum(bar_index, mlLookback)          // FIXED: Using math.sum()
sumY = math.sum(close, mlLookback)              // FIXED: Using math.sum()
sumXY = math.sum(bar_index * close, mlLookback) // FIXED: Using math.sum()
sumX2 = math.sum(bar_index * bar_index, mlLookback)

slope = (mlLookback * sumXY - sumX * sumY) / (mlLookback * sumX2 - sumX * sumX)
intercept = (sumY - slope * sumX) / mlLookback
predictedClose := slope * bar_index + intercept

// ———— 4. Strategy Logic ————
mlBullish = predictedClose > close
mlBearish = predictedClose < close

enterLong = ta.crossover(rsi, 30) and adx > 25 and mlBullish
enterShort = ta.crossunder(rsi, 70) and adx > 25 and mlBearish

// ———— 5. Execute Orders ————
strategy.entry("Long", strategy.long, when=enterLong)
strategy.entry("Short", strategy.short, when=enterShort)

// ———— 6. Plotting ————
plot(predictedClose, "Predicted Close", color=color.purple)
plotshape(enterLong, "Buy", shape.triangleup, location.belowbar, color=color.green)
plotshape(enterShort, "Sell", shape.triangledown, location.abovebar, color=color.red)
```

> Detail

https://www.fmz.com/strategy/483106

> Last Modified

2025-02-21 13:46:54
