
> Name

Trend following and momentum strategy based on multiple technical indicators-Multi-Technical-Indicator-Based-Trend-Following-and-Momentum-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/d7637478472b8f114c.png)

[trans]
#### Overview
This strategy is a comprehensive trading system that combines moving averages, momentum and oscillators. The strategy uses the synergy of the Moving Average Convergence Divergence Index (MACD), the Exponential Moving Average (EMA) and the Relative Strength Index (RSI) to trade when the market trend is clear and the momentum is sufficient. This strategy mainly focuses on the upward trend and ensures the reliability of trading signals through cross-validation of multiple technical indicators.
#### Strategy Principle
The strategy uses a triple filtering mechanism to determine trade timing:
1. Trend confirmation: Use the 200-day exponential moving average (EMA200) as a trend filter and only consider going long when the price is above EMA200.
2. Momentum confirmation: Determine the market momentum through the MACD indicator (parameters are fast line 12, slow line 26, signal line 9), which requires the MACD line to be above the signal line.
3. Fluctuation confirmation: Use the RSI indicator (parameter is 14) to determine overbought and oversold, and the RSI is required to be within the 50-70 range.
The setting of closing conditions is relatively flexible, and it will be triggered when any of the following conditions is met:
- MACD line falls below the signal line
- Price falls below EMA200
- RSI exceeds 70 and enters overbought territory
#### Strategic Advantages
1. The multiple confirmation mechanism greatly reduces the impact of false signals and improves the reliability of transactions.
2. Combine trend and momentum indicators to grasp the general trend without missing short-term opportunities.
3. Use RSI for auxiliary filtering to effectively avoid the risk of chasing highs.
4. The strategy logic is clear and the parameters are highly adjustable, making it suitable for different market environments.
5. The use of percentage position management is conducive to the long-term growth of funds.
#### Strategy Risk
1. Too many filter conditions may lead to missing some profit opportunities.
2. In a volatile market, frequent false breakthroughs may lead to continuous stop losses.
3. As a trend indicator, EMA200 may respond slowly, resulting in greater losses when the market turns sharply.
4. Without setting stop loss conditions, you may face a large retracement in extreme market conditions.
#### Strategy optimization direction
1. Introduce adaptive parameters:
   - Dynamically adjust MACD parameters based on market volatility
   - Optimize your stop loss settings using the ATR indicator
2. Improve risk control:
   - Add trailing stop function
   - Set maximum drawdown limit
3. Optimize entry timing:
   - Added transaction volume confirmation mechanism
   - Consider introducing price pattern analysis
4. Improve position management:
   - Dynamically adjust position ratio based on volatility
   - Implement the mechanism of opening and reducing positions in batches
#### Summary
This strategy builds a relatively robust trading system by comprehensively using multiple technical indicators. The core advantage of the strategy lies in the multiple confirmation mechanism, which can effectively reduce the impact of false signals. Through reasonable optimization and improvement of risk control, this strategy is expected to maintain stable performance in different market environments. Although there is a certain degree of lag and the risk of missing opportunities, overall it is a trading strategy with practical value. ||
#### Overview
This strategy is a comprehensive trading system that combines moving averages, momentum, and oscillator indicators. The strategy utilizes the Moving Average Convergence Divergence (MACD), Exponential Moving Average (EMA), and Relative Strength Index (RSI) to execute trades when market trends are clear and momentum is sufficient. The strategy primarily focuses on upward trends, using multiple technical indicators for cross-validation to ensure signal reliability.

#### Strategy Principles
The strategy employs a triple-filtering mechanism to determine trading opportunities:
1. Trend Confirmation: Uses the 200-day Exponential Moving Average (EMA200) as a trend filter, considering long positions only when price is above EMA200.
2. Momentum Confirmation: Uses MACD indicator (parameters: fast 12, slow 26, signal 9) to assess market momentum, requiring MACD line above signal line.
3. Oscillation Confirmation: Employs RSI indicator (parameter 14) for overbought/oversold conditions, requiring RSI between 50-70.

Position closing conditions are flexible, triggered by any of the following:
- MACD line crosses below signal line
- Price falls below EMA200
- RSI exceeds 70 entering overbought territory

#### Strategy Advantages
1. Multiple confirmation mechanisms significantly reduce the impact of false signals, improving trading reliability.
2. Combination of trend and momentum indicators captures both major trends and short-term opportunities.
3. RSI filtering effectively prevents chasing high prices.
4. Clear strategy logic with adjustable parameters, suitable for different market conditions.
5. Percentage-based position management promotes long-term capital growth.

#### Strategy Risks
1. Multiple filtering conditions may result in missing profitable opportunities.
2. Frequent false breakouts in ranging markets may lead to consecutive stops.
3. EMA200 as a trend indicator may react slowly, leading to larger losses during sharp market reversals.
4. Absence of stop-loss conditions may result in significant drawdowns in extreme market conditions.

#### Strategy Optimization Directions
1. Introduce Adaptive Parameters:
   - Dynamically adjust MACD parameters based on market volatility
   - Optimize stop-loss settings using ATR indicator
2. Improve Risk Control:
   - Add trailing stop functionality
   - Set maximum drawdown limits
3. Optimize Entry Timing:
   - Add volume confirmation mechanism
   - Consider incorporating price pattern analysis
4. Enhance Position Management:
   - Dynamically adjust position size based on volatility
   - Implement scaled entry and exit mechanisms

#### Summary
The strategy constructs a relatively robust trading system through the comprehensive use of multiple technical indicators. Its core advantage lies in the multiple confirmation mechanisms, effectively reducing the impact of false signals. Through reasonable optimization and improved risk control, the strategy has the potential to maintain stable performance across different market conditions. While there are risks of lagging and missed opportunities, it is overall a practical trading strategy with real-world value.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-12-10 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Simplified SOL/USDT Strategy", overlay=true, initial_capital=10000, default_qty_type=strategy.percent_of_equity, default_qty_value=100)

// Input parameters
fast_length = input(12, "MACD Fast Length")
slow_length = input(26, "MACD Slow Length")
signal_length = input(9, "MACD Signal Length")
ema_length = input(200, "EMA Length")
rsi_length = input(14, "RSI Length")

// Calculate indicators
[macd, signal, hist] = ta.macd(close, fast_length, slow_length, signal_length)
ema200 = ta.ema(close, ema_length)
rsi = ta.rsi(close, rsi_length)

// Entry conditions
long_entry = close > ema200 and
             macd > signal and
             rsi > 50 and rsi < 70

// Exit conditions
long_exit = macd < signal or close < ema200 or rsi > 70

// Strategy execution
if (long_entry)
    strategy.entry("Long", strategy.long)

if (long_exit)
    strategy.close("Long")

// Plot indicators
plot(ema200, color=color.blue, title="EMA 200")
plot(macd, color=color.blue, title="MACD")
plot(signal, color=color.orange, title="Signal")

// Plot entry and exit points
plotshape(long_entry, title="Long Entry", location=location.belowbar, color=color.green, style=shape.triangleup, size=size.small)
plotshape(long_exit, title="Long Exit", location=location.abovebar, color=color.red, style=shape.triangledown, size=size.small)

```

> Detail

https://www.fmz.com/strategy/474846

> Last Modified

2024-12-12 15:01:09
