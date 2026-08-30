
> Name

Multi-Kernel-Regression-Dynamic-Reactor-Trend-Following-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](assets/images/d452e07723d5ae0dac26181c560b63957f85381df027f5eb84af9dc475069852.png)
![IMG](assets/images/00fc5a90a290057d3afffdb739e23caccd8096c2f7e83c5f811c96140cff4081.png)



[trans]
#### Overview
This strategy is a trend following system that combines Dynamic Reactor and Multi-Kernel Regression. It captures market trends by integrating ATR channels, SMA moving averages, Gaussian kernel regression and Epanechnikov kernel regression, and uses the RSI indicator for signal filtering. The strategy also includes a complete position management system, including dynamic stop losses, multiple profit targets, and trailing stops.
#### Strategy Principle
The core of the strategy consists of two main parts. The first part is the Dynamic Reactor (DR), which builds an adaptive price channel based on ATR and SMA. The width of the channel is determined by the ATR multiplier, and the position of the channel adjusts with the movement of the SMA. When price breaks out of the channel, the system updates the trend direction. The second part is multi-kernel regression (MKR), which combines two different kernel functions: Gaussian kernel regression and Epanechnikov kernel regression. By setting different bandwidth parameters and weights, the system can better fit the price trend. Trading signals are generated from the intersection of the MKR line and the DR line and are filtered by the RSI indicator to avoid trading in overbought and oversold areas.
#### Strategic Advantages
1. Strong adaptability: Through the combination of dynamic reactor and multi-core regression, the strategy can automatically adapt to different market environments and fluctuation conditions.
2. Improved risk management: including multiple risk control mechanisms such as dynamic stop loss, batch profit and trailing stop loss.
3. High signal quality: Through RSI filtering and cross confirmation of two lines, false signals can be effectively reduced.
4. High computational efficiency: Although a complex kernel regression algorithm is used, the real-time performance of the strategy is ensured by optimizing the calculation method.
#### Strategy Risk
1. Parameter sensitivity: The effect of the strategy is highly dependent on the settings of parameters such as ATR multiplier and kernel function bandwidth. Improper parameters may lead to over-trading or missed opportunities.
2. Hysteresis: Due to the use of moving average and regression algorithms, there may be a certain lag in fast market conditions.
3. Market adaptability: The strategy performs better in trending markets, but may frequently generate false signals in range-bound markets.
4. Computational complexity: The calculation of the multi-core regression part is relatively complex, and performance optimization needs to be paid attention to in a high-frequency trading environment.
#### Strategy optimization direction
1. Parameter adaptation: An adaptive mechanism can be introduced to dynamically adjust the ATR multiplier and kernel function bandwidth according to market fluctuations.
2. Signal optimization: Consider adding auxiliary indicators such as trading volume and price patterns to improve the reliability of signals.
3. Risk control: The ratio of stop loss and profit targets can be dynamically adjusted according to market volatility.
4. Market filtering: Add a market environment identification module to use different trading strategies under different market conditions.
#### Summary
This is a complete trading system that combines modern statistical methods with traditional technical analysis. Through the innovative combination of dynamic reactor and multi-core regression, as well as a complete risk management mechanism, this strategy shows good adaptability and stability. Although there are some areas that need optimization, through continuous improvement and parameter optimization, this strategy is expected to maintain stable performance in different market environments. ||
#### Overview
This strategy is a trend following system that combines Dynamic Reactor (DR) and Multi-Kernel Regression (MKR). It captures market trends by integrating ATR channels, SMA, and a combination of Gaussian and Epanechnikov kernel regressions, with RSI-based signal filtering. The strategy includes a comprehensive position management system featuring dynamic stop-loss, multiple take-profit targets, and trailing stops.

#### Strategy Principles
The strategy consists of two main components. The first is the Dynamic Reactor (DR), which constructs an adaptive price channel based on ATR and SMA. The channel width is determined by the ATR multiplier, while its position adjusts with the SMA movement. Trend direction updates when price breaks through the channel. The second component is the Multi-Kernel Regression (MKR), combining Gaussian and Epanechnikov kernel regressions. Through different bandwidth parameters and weights, the system better fits price movements. Trading signals are generated at MKR and DR line crossovers, filtered by RSI to avoid overbought and oversold areas.

#### Strategy Advantages
1. High Adaptability: The combination of Dynamic Reactor and Multi-Kernel Regression allows the strategy to automatically adapt to different market environments and volatility conditions.
2. Comprehensive Risk Management: Includes multiple risk control mechanisms such as dynamic stop-loss, partial profit-taking, and trailing stops.
3. High Signal Quality: Effectively reduces false signals through RSI filtering and line crossover confirmation.
4. High Computational Efficiency: Despite using complex kernel regression algorithms, optimized calculation methods ensure real-time performance.

#### Strategy Risks
1. Parameter Sensitivity: Strategy effectiveness highly depends on proper setting of parameters like ATR multiplier and kernel bandwidth.
2. Latency: Due to moving averages and regression algorithms, some lag may exist in fast-moving markets.
3. Market Adaptability: Strategy performs well in trending markets but may generate false signals in ranging markets.
4. Computational Complexity: Multi-kernel regression calculations are complex, requiring performance optimization for high-frequency trading.

#### Optimization Directions
1. Parameter Adaptation: Introduce adaptive mechanisms to dynamically adjust ATR multiplier and kernel bandwidth based on market volatility.
2. Signal Enhancement: Consider adding volume, price patterns, and other auxiliary indicators to improve signal reliability.
3. Risk Control: Dynamically adjust stop-loss and take-profit ratios based on market volatility.
4. Market Filtering: Add market environment recognition module to apply different trading strategies under different market conditions.

#### Summary
This is a complete trading system integrating modern statistical methods with traditional technical analysis. Through the innovative combination of Dynamic Reactor and Multi-Kernel Regression, along with comprehensive risk management mechanisms, the strategy demonstrates good adaptability and stability. While there are areas for optimization, continuous improvement and parameter optimization should help maintain stable performance across different market environments.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-25 00:00:00
end: 2025-02-22 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Binance","currency":"SOL_USDT"}]
*/

//@version=5
strategy("DR+MKR Signals – Band SL, Multiple TP & Trailing Stop", overlay=true, pyramiding=0, default_qty_type=strategy.percent_of_equity, default_qty_value=10)

// =====================================================================
// PART 1: Optimized Dynamic Reactor
// =====================================================================
atrLength  = input.int(10, "ATR Length", minval=1)         // Lower value for increased sensitivity
smaLength  = input.int(10, "SMA Length", minval=1)         // Lower value for a faster response
multiplier = input.float(1.2, "ATR Multiplier", minval=0.1, step=0.1) // Adjusted for tighter bands

atrValue  = ta.atr(atrLength)
smaValue  = ta.sma(close, smaLength)

basicUpper = smaValue + atrValue * multiplier
basicLower = smaValue - atrValue * multiplier

var float finalUpper = basicUpper
var float finalLower = basicLower
if bar_index > 0
    finalUpper := close[1] > finalUpper[1] ? math.max(basicUpper, finalUpper[1]) : basicUpper
if bar_index > 0
    finalLower := close[1] < finalLower[1] ? math.min(basicLower, finalLower[1]) : basicLower

var int trend = 1
if bar_index > 0
    trend := close > finalUpper[1] ? 1 : close < finalLower[1] ? -1 : nz(trend[1], 1)

drLine = trend == 1 ? finalLower : finalUpper
p_dr   = plot(drLine, color = trend == 1 ? color.green : color.red, title="Dynamic Reactor", linewidth=2)

// =====================================================================
// PART 2: Optimized Multi Kernel Regression
// =====================================================================
regLength = input.int(30, "Regression Period", minval=1)  // Lower value for increased sensitivity
h1        = input.float(5.0, "Gaussian Band (h1)", minval=0.1) // Adjusted for a better fit
h2        = input.float(5.0, "Epanechnikov Band (h2)", minval=0.1)
alpha     = input.float(0.5, "Gaussian Kernel Weight", minval=0, maxval=1)

f_gaussian_regression(bw) =>
    num = 0.0
    den = 0.0
    for i = 0 to regLength - 1
        weight = math.exp(-0.5 * math.pow(i / bw, 2))
        num += close[i] * weight
        den += weight
    num / (den == 0 ? 1 : den)

f_epanechnikov_regression(bw) =>
    num = 0.0
    den = 0.0
    for i = 0 to regLength - 1
        ratio = i / bw
        weight = math.abs(ratio) <= 1 ? (1 - math.pow(ratio, 2)) : 0
        num += close[i] * weight
        den += weight
    num / (den == 0 ? 1 : den)

regGauss = f_gaussian_regression(h1)
regEpan  = f_epanechnikov_regression(h2)
multiKernelRegression = alpha * regGauss + (1 - alpha) * regEpan
p_mkr = plot(multiKernelRegression, color = trend == 1 ? color.green : color.red, title="Multi Kernel Regression", linewidth=2)

fill(p_dr, p_mkr, color = trend == 1 ? color.new(color.green, 80) : color.new(color.red, 80), title="Trend Fill")

// =====================================================================
// PART 3: Buy and Sell Signals + RSI Filter
// =====================================================================
rsi = ta.rsi(close, 14)
buySignal  = ta.crossover(multiKernelRegression, drLine) and rsi < 70
sellSignal = ta.crossunder(multiKernelRegression, drLine) and rsi > 30

plotshape(buySignal, style=shape.triangleup, location=location.belowbar, color=color.green, size=size.tiny, title="Buy Signal")
plotshape(sellSignal, style=shape.triangledown, location=location.abovebar, color=color.red, size=size.tiny, title="Sell Signal")

alertcondition(buySignal, title="Buy Alert", message="Buy Signal generated")
alertcondition(sellSignal, title="Sell Alert", message="Sell Signal generated")

// =====================================================================
// PART 4: Trade Management – Dynamic Stop Loss & Adaptive Take Profit
// =====================================================================
var float riskValue = na
if strategy.position_size == 0
    riskValue := na

enterLong() =>
    strategy.entry("Long", strategy.long)
    close - finalLower

enterShort() =>
    strategy.entry("Short", strategy.short)
    finalUpper - close

if (buySignal)
    riskValue := enterLong()

if (sellSignal)
    riskValue := enterShort()

exitLongOrders() =>
    entryPrice = strategy.position_avg_price
    TP1 = entryPrice + riskValue
    strategy.exit("Long_TP1", from_entry="Long", limit=TP1, qty_percent=50, comment="TP 1:1")
    strategy.exit("Long_TS", from_entry="Long", trail_offset=riskValue * 0.8, trail_points=riskValue * 0.8, comment="Trailing Stop")

if (strategy.position_size > 0)
    exitLongOrders()

exitShortOrders() =>
    entryPrice = strategy.position_avg_price
    TP1 = entryPrice - riskValue
    strategy.exit("Short_TP1", from_entry="Short", limit=TP1, qty_percent=50, comment="TP 1:1")
    strategy.exit("Short_TS", from_entry="Short", trail_offset=riskValue * 0.8, trail_points=riskValue * 0.8, comment="Trailing Stop")

if (strategy.position_size < 0)
    exitShortOrders()


```

> Detail

https://www.fmz.com/strategy/483498

> Last Modified

2025-03-03 15:42:02
