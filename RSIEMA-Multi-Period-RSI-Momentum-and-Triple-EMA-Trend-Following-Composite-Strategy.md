
> Name

Multi-Period-RSI-Momentum-and-Triple-EMA-Trend-Following-Composite-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1609e3215807bea0a9a.png)

[trans]
#### Overview
This strategy is a composite trading system that combines the momentum indicator RSI and the trend indicator EMA. It operates on two time periods of 1 minute and 5 minutes, and makes trading decisions through the overbought and oversold signals of RSI and the trend judgment of triple EMA. The strategy includes both trend tracking and mean reversion characteristics, and can capture trading opportunities in different market environments.
#### Strategy Principle
The strategy uses the 21/50/200-day triple EMA as the benchmark for trend judgment, and combines it with an improved version of the RSI indicator (calculated using the Chebyshev method) to identify overbought and oversold conditions in the market. On the 1-minute period, short selling is initiated when the RSI exceeds 94, closed when the RSI falls below 4, and a breakeven stop is set when the RSI returns to 50. On the 5-minute time frame, open long positions when the price falls below the 200-day EMA and rebounds, and close the position when the RSI is overbought or falls below the median. The strategy uses the position management variables inPositionLong and inPositionShort to avoid repeated entries.
#### Strategic Advantages
1. Multiple time period analysis improves signal reliability
2. Combine trend and momentum indicators to complement each other’s strengths
3. Equipped with a capital guarantee and stop-loss mechanism to control risks
4. Using an improved version of RSI calculation method, the signal is more accurate
5. Avoid duplicate transactions through position management
6. Can adapt to different market environments
#### Strategy Risk
1. Frequent transactions may result in higher handling fees
2. Stop loss may be triggered frequently in highly volatile markets
3. The RSI indicator may produce false signals under certain market conditions.
4. Multi-period strategies may have a lag in signal confirmation
5. EMA crossover signals can be misleading in volatile markets
#### Strategy optimization direction
1. Introduce volatility filter to adjust parameters during periods of high volatility
2. Add transaction volume confirmation mechanism
3. Optimize the RSI threshold and consider dynamic adjustment
4. Add more technical indicators for cross-validation
5. Introduce adaptive parameter mechanism
6. Develop a more sophisticated stop-loss mechanism
#### Summary
This strategy improves the stability and reliability of trading by combining multiple technical indicators and multi-time period analysis. Although there are certain risks, effective risk control can be achieved through reasonable position management and stop-loss mechanisms. The optimization space of the strategy is large, and the performance of the strategy can be further improved by introducing more technical indicators and optimization parameters.
||

#### Overview
This strategy is a composite trading system that combines the momentum indicator RSI with the trend indicator EMA. Operating on both 1-minute and 5-minute timeframes, it makes trading decisions based on RSI overbought/oversold signals and triple EMA trend determination. The strategy incorporates both trend following and mean reversion characteristics, enabling it to capture trading opportunities in different market environments.

#### Strategy Principles
The strategy uses 21/50/200-day triple EMA as trend judgment benchmark, combined with a modified RSI indicator (calculated using Chebyshev method) to identify market overbought/oversold conditions. On the 1-minute timeframe, it initiates short positions when RSI breaks above 94 and closes when it falls below 4, with breakeven stops set when RSI returns to 50. On the 5-minute timeframe, it initiates long positions when price rebounds after falling below the 200-day EMA, closing positions when RSI is overbought or breaks below the median. Position management variables inPositionLong and inPositionShort prevent repeated entries.

#### Strategy Advantages
1. Multi-timeframe analysis enhances signal reliability
2. Combines trend and momentum indicators for complementary benefits
3. Implements breakeven stop-loss mechanism for risk control
4. Uses improved RSI calculation method for more accurate signals
5. Prevents duplicate trades through position management
6. Adaptable to different market environments

#### Strategy Risks
1. Frequent trading may incur high transaction costs
2. May trigger frequent stops in volatile markets
3. RSI indicator may generate false signals under certain market conditions
4. Multi-period strategy may have lag in signal confirmation
5. EMA crossover signals may be misleading in ranging markets

#### Optimization Directions
1. Introduce volatility filters to adjust parameters during high volatility periods
2. Add volume confirmation mechanism
3. Optimize RSI thresholds with potential dynamic adjustment
4. Include additional technical indicators for cross-validation
5. Implement adaptive parameter mechanisms
6. Develop more sophisticated stop-loss mechanisms

#### Summary
The strategy enhances trading stability and reliability through the combination of multiple technical indicators and multi-timeframe analysis. While certain risks exist, they can be effectively controlled through proper position management and stop-loss mechanisms. The strategy has significant optimization potential, and its performance can be further improved by introducing additional technical indicators and optimizing parameters.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-12 00:00:00
end: 2024-07-10 00:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Combined RSI Primed and 3 EMA Strategy", overlay=true)

// Input for EMA lengths
emaLength1 = input(21, title="EMA Length 1")
emaLength2 = input(50, title="EMA Length 2")
emaLength3 = input(200, title="EMA Length 3")

// Input for RSI settings
rsiLength = input(14, title="RSI Length")
rsiOverbought = input(94, title="RSI Overbought Level")
rsiNeutral = input(50, title="RSI Neutral Level")
rsiOversold = input(4, title="RSI Oversold Level")

// Calculate EMAs
ema1 = ta.ema(close, emaLength1)
ema2 = ta.ema(close, emaLength2)
ema3 = ta.ema(close, emaLength3)

// Calculate RSI using Chebyshev method from RSI Primed
rsi(source) =>
    up = math.max(ta.change(source), 0)
    down = -math.min(ta.change(source), 0)
    rs = up / down
    rsiValue = down == 0 ? 100 : 100 - (100 / (1 + rs))
    rsiValue

rsiValue = rsi(close)

// Plot EMAs
plot(ema1, color=color.red, title="EMA 21")
plot(ema2, color=color.white, title="EMA 50")
plot(ema3, color=color.blue, title="EMA 200")

// Plot RSI for visual reference
hline(rsiOverbought, "Overbought", color=color.red)
hline(rsiNeutral, "Neutral", color=color.gray)
hline(rsiOversold, "Oversold", color=color.green)
plot(rsiValue, color=color.blue, title="RSI")

// Trading logic with position management
var bool inPositionShort = false
var bool inPositionLong = false

// Trading logic for 1-minute timeframe
if (rsiValue > rsiOverbought and not inPositionShort)
    strategy.entry("Sell", strategy.short)
    inPositionShort := true

if (rsiValue < rsiOversold and inPositionShort)
    strategy.close("Sell")
    inPositionShort := false

if (ta.crossover(rsiValue, rsiNeutral) and inPositionShort)
    strategy.exit("Break Even", "Sell", stop=close)

// Trading logic for 5-minute timeframe
var float lastBearishClose = na

if (close < ema3 and close[1] >= ema3) // Check if the current close is below EMA200
    lastBearishClose := close

if (not na(lastBearishClose) and close > lastBearishClose and not inPositionLong)
    strategy.entry("Buy", strategy.long)
    inPositionLong := true

if (rsiValue > rsiOverbought and inPositionLong)
    strategy.close("Buy")
    inPositionLong := false

if (ta.crossunder(rsiValue, rsiNeutral) and inPositionLong)
    strategy.exit("Break Even", "Buy", stop=close)

lastBearishClose := na // Reset after trade execution
```

> Detail

https://www.fmz.com/strategy/471694

> Last Modified

2024-11-12 15:07:54
