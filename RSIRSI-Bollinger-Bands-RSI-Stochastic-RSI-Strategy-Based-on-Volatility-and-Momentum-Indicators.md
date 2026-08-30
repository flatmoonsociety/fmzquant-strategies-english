
> Name

Bollinger-Bands-RSI-Stochastic-RSI-Strategy-Based-on-Volatility-and-Momentum-Indicators
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/128b2d548f033319b4e.png)
[trans]
#### Overview
This strategy combines three technical indicators: Bollinger Bands, Relative Strength Index (RSI) and Stochastic RSI. By analyzing price volatility and momentum, it looks for overbought and oversold conditions in the market to determine the best buying and selling opportunities. The strategy uses 20 times leverage to simulate options trading, sets a 0.60% take-profit level and a 0.25% stop-loss level, and limits only one transaction per day to control risks.
#### Strategy Principle
The core of this strategy is to use three indicators, Bollinger Bands, RSI and Stochastic RSI, to evaluate the state of the market. The Bolinger Bands consist of the middle band (20-period simple moving average), the upper band (3 standard deviations above the middle band), and the lower band (3 standard deviations below the middle band) and are used to measure price volatility. RSI is a momentum oscillator used to identify overbought and oversold conditions. This strategy uses the 14-period RSI. Stochastic RSI applies the stochastic oscillator formula to the RSI value, also using a 14 period length.
When the RSI is below 34, the Stochastic RSI is below 20, and the closing price is near or below the lower rail, a buy signal is triggered. When the RSI is above 66, the Stochastic RSI is above 80, and the closing price is near or above the upper rail, a sell signal is triggered. The strategy uses 20 times leverage to simulate options trading, with the take-profit level set to 0.60% and the stop-loss level set to 0.25%. Additionally, this strategy only conducts one trade per day to control risk.
#### Strategic Advantages
1. Combining multiple technical indicators: This strategy takes into account both price volatility (Bollinger Bands) and momentum (RSI and Stochastic RSI) to provide a more comprehensive market analysis.
2. Risk control: The strategy sets clear take-profit and stop-loss levels, and limits only one transaction per day, effectively controlling risk exposure.
3. Strong adaptability: By adjusting parameters, such as the standard deviation multiple of Bolinger Bands, the threshold of RSI and stochastic RSI, etc., this strategy can adapt to different market conditions.
#### Strategy Risk
1. Market risk: The performance of the strategy depends on market conditions. When the trend is unclear or the volatility is extremely high, the strategy may perform poorly.
2. Parameter sensitivity: The effect of the strategy depends on the quality of the selected parameters. Improper parameter settings may lead to poor performance of the strategy.
3. Leverage risk: The strategy uses 20 times leverage, which can magnify gains but also magnify losses. Under extreme market conditions, high leverage can result in significant losses.
#### Strategy optimization direction
1. Dynamically adjust parameters: According to changes in market conditions, parameters such as the standard deviation multiple of the Bolinger Band, the threshold of RSI and stochastic RSI are dynamically adjusted to adapt to different market environments.
2. Add other indicators: Consider adding other technical indicators, such as MACD, ADX, etc., to improve the reliability and stability of the strategy.
3. Optimize take profit and stop loss: Through backtesting and optimization, find the best take profit and stop loss ratio to maximize returns while controlling risks.
4. Improve money management: Explore more advanced money management techniques, such as the Kelly Criterion, to optimize the long-term performance of your strategy.
#### Summary
This strategy combines three technical indicators, Bollinger Bands, RSI and Stochastic RSI, and uses price volatility and momentum information to find the best buying and selling opportunities. The strategy sets clear take-profit and stop-loss levels and controls the number of transactions per day to manage risk. Although this strategy has its advantages, it still faces challenges such as market risk, parameter sensitivity and leverage risk. The performance of this strategy can be further optimized by dynamically adjusting parameters, incorporating other indicators, optimizing take-profit and stop-loss, and improving fund management.
|| 

#### Overview
This strategy combines three technical indicators: Bollinger Bands, Relative Strength Index (RSI), and Stochastic RSI. By analyzing price volatility and momentum, it aims to identify overbought and oversold market conditions to determine optimal entry and exit points. The strategy simulates options trading with 20x leverage, sets a 0.60% take-profit and a 0.25% stop-loss, and limits trading to once per day to manage risk.

#### Strategy Principle
The core of this strategy lies in using Bollinger Bands, RSI, and Stochastic RSI to assess market conditions. Bollinger Bands consist of a middle band (20-period simple moving average), an upper band (3 standard deviations above the middle band), and a lower band (3 standard deviations below the middle band), measuring price volatility. RSI is a momentum oscillator used to identify overbought and oversold conditions, with a 14-period length in this strategy. Stochastic RSI applies the Stochastic Oscillator formula to RSI values, also using a 14-period length.

A long signal is triggered when the RSI is below 34, the Stochastic RSI is below 20, and the close price is at or below the lower Bollinger Band. A short signal is triggered when the RSI is above 66, the Stochastic RSI is above 80, and the close price is at or above the upper Bollinger Band. The strategy uses 20x leverage to simulate options trading, with a 0.60% take-profit and a 0.25% stop-loss. Furthermore, it limits trading to once per day to control risk.

#### Strategy Advantages
1. Multi-indicator approach: The strategy considers both price volatility (Bollinger Bands) and momentum (RSI and Stochastic RSI), providing a more comprehensive market analysis.
2. Risk management: The strategy sets clear take-profit and stop-loss levels and limits trading to once per day, effectively managing risk exposure.
3. Adaptability: By adjusting parameters such as the standard deviation multiplier for Bollinger Bands and the thresholds for RSI and Stochastic RSI, the strategy can adapt to various market conditions.

#### Strategy Risks
1. Market risk: The strategy's performance depends on market conditions and may underperform during unclear trends or extremely high volatility.
2. Parameter sensitivity: The strategy's effectiveness relies on the quality of chosen parameters, and improper settings may lead to suboptimal performance.
3. Leverage risk: The strategy employs 20x leverage, which can amplify gains but also magnify losses. In extreme market conditions, high leverage may result in significant losses.

#### Strategy Optimization Directions
1. Dynamic parameter adjustment: Dynamically adjust parameters such as the standard deviation multiplier for Bollinger Bands and the thresholds for RSI and Stochastic RSI based on changing market conditions to adapt to different environments.
2. Additional indicators: Consider incorporating other technical indicators like MACD or ADX to enhance the strategy's reliability and stability.
3. Optimize take-profit and stop-loss: Through backtesting and optimization, find the optimal take-profit and stop-loss ratios to maximize returns while managing risk.
4. Improve money management: Explore more advanced money management techniques, such as the Kelly Criterion, to optimize the strategy's long-term performance.

#### Summary
This strategy combines Bollinger Bands, RSI, and Stochastic RSI to identify optimal entry and exit points by leveraging price volatility and momentum information. It sets clear take-profit and stop-loss levels and controls the number of daily trades to manage risk. Despite its advantages, the strategy faces challenges such as market risk, parameter sensitivity, and leverage risk. Further optimization can be achieved through dynamic parameter adjustment, incorporating additional indicators, optimizing take-profit and stop-loss, and improving money management techniques.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-05-01 00:00:00
end: 2024-05-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Bollinger Bands + RSI + Stochastic RSI Strategy with OTM Options", overlay=true)
// Define leverage factor (e.g., 20x leverage for OTM options)
leverage = 1         
// Bollinger Bands
length = 20
deviation = 3
basis = ta.sma(close, length)
dev = ta.stdev(close, length)
upper = basis + deviation * dev
lower = basis - deviation * dev
// RSI
rsi_length = 14
rsi = ta.rsi(close, rsi_length)
// Stochastic RSI
stoch_length = 14
stoch_k = ta.stoch(close, close, close, stoch_length)
// Entry condition with Bollinger Bands
longCondition = rsi < 34 and stoch_k < 20 and close <= lower
shortCondition = rsi > 66 and stoch_k > 80 and close >= upper
// Plot Bollinger Bands
plot(basis, color=color.blue, title="Basis")
plot(upper, color=color.red, title="Upper Bollinger Band")
plot(lower, color=color.green, title="Lower Bollinger Band")
// Track if a trade has been made today
var int lastTradeDay = na
// Options Simulation: Take-Profit and Stop-Loss Conditions
profitPercent = 0.01    // 1% take profit
lossPercent = 0.002  // 0.2% stop loss
// Entry Signals
if (dayofmonth(timenow) != dayofmonth(lastTradeDay)) 
    if (longCondition)
        longTakeProfitPrice = close * (1 + profitPercent)
        longStopLossPrice = close * (1 - lossPercent)
        strategy.entry("Long", strategy.long, qty=leverage * strategy.equity / close)
        strategy.exit("Take Profit Long", from_entry="Long", limit=longTakeProfitPrice, stop=longStopLossPrice)
        lastTradeDay := dayofmonth(timenow)
    if (shortCondition)
        shortTakeProfitPrice = close * (1 - profitPercent)
        shortStopLossPrice = close * (1 + lossPercent)
        strategy.entry("Short", strategy.short, qty=leverage * strategy.equity / close)
        strategy.exit("Take Profit Short", from_entry="Short", limit=shortTakeProfitPrice, stop=shortStopLossPrice)
        lastTradeDay := dayofmonth(timenow)
```

> Detail

https://www.fmz.com/strategy/453230

> Last Modified

2024-06-03 10:51:36
