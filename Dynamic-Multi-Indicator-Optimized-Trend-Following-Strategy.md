
> Name

Dynamic-Multi-Indicator-Optimized-Trend-Following-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d8064c13a4d6fc856d04.png)
![IMG](https://www.fmz.com/upload/asset/2d96bd27b8861486d86e3.png)

[trans]
#### Overview
This strategy is a multi-indicator trend-following trading system that combines the analysis of three dimensions: market trend, momentum and volatility. The core logic is to judge the market trend through the Ichimoku Cloud indicator, confirm the momentum through the MACD histogram, filter the market fluctuation state through the Bollinger Band Width, introduce a weekly level trend confirmation mechanism, and finally manage risks through dynamic stop loss based on ATR.
#### Strategy Principle
The strategy adopts a multi-layer signal filtering mechanism: first, use the leading span A and B of the cloud indicator to determine whether the price is above or below the cloud layer and determine the general market trend; secondly, use the MACD histogram to determine the momentum strength, which requires the histogram to be greater than -0.05 when long and less than 0 when short; thirdly, introduce the 50-period moving average of the weekly time period to confirm the larger-level trend direction; fourthly, use the Bollinger Band width indicator to filter low-volatility markets, and only open positions when the width is greater than 0.02. The stop loss setting is adaptive according to the market fluctuation state: when the volatility is low, the previous high and low points are used, and when the volatility is high, the ATR multiple is used.
#### Strategic Advantages
1. Multi-dimensional signal filtering: Effectively reduce false signals through a combination of indicators in the three dimensions of trend, momentum and volatility.
2. Multi-time cycle analysis: introduce weekly trend confirmation to improve the accuracy of trading direction.
3. Dynamic risk management: The adaptive stop-loss mechanism based on ATR and Bollinger Band width not only protects profits but also gives room for trend development.
4. The backtest results are excellent: net profit 10.80%, profit-loss ratio 2.593, winning rate 50.70%, and the maximum drawdown is only 1.47%.
#### Strategy Risk
1. Trend dependence: The strategy may produce frequent false signals in volatile markets.
2. Parameter sensitivity: Multiple indicator parameters need to be optimized for different market conditions.
3. Lagging risk: Multiple signal filtering may lead to late entry timing and missing part of the market.
4. Limitations of backtesting: historical performance does not represent future performance, and slippage and handling fees need to be considered in real trading.
#### Strategy optimization direction
1. Signal system optimization: Other momentum indicators such as RSI can be introduced to enhance signal reliability.
2. Position management optimization: position size can be dynamically adjusted based on volatility.
3. Optimization of the take-profit mechanism: Trailing stop loss or take-profit conditions based on technical indicators can be added.
4. Market adaptability optimization: dynamically adjust parameters according to different market conditions.
#### Summary
This strategy builds a complete trend tracking system through multi-dimensional indicator fusion and multi-time period analysis, and is equipped with a dynamic risk management mechanism. Although the backtest performance is excellent, you still need to pay attention to the risks caused by changes in the market environment. It is recommended to verify carefully and continue to optimize in the real market. ||
#### Overview
This strategy is a multi-indicator trend following trading system that combines analysis across three dimensions: market trend, momentum, and volatility. The core logic uses the Ichimoku Cloud to determine market trends, MACD histogram for momentum confirmation, Bollinger Band Width for market volatility filtering, while incorporating weekly timeframe trend confirmation, and managing risk through ATR-based dynamic stop-loss.

#### Strategy Principles
The strategy employs a multi-layer signal filtering mechanism: First, it determines the market trend by checking if price is above or below the Ichimoku Cloud's Leading Spans A and B; Second, it uses the MACD histogram to judge momentum strength, requiring the histogram to be greater than -0.05 for longs and less than 0 for shorts; Third, it incorporates a 50-period moving average on the weekly timeframe to confirm higher timeframe trend direction; Fourth, it uses Bollinger Band Width to filter low volatility conditions, only entering trades when the width exceeds 0.02. Stop-loss settings adapt to market volatility: using recent highs/lows in low volatility and ATR multipliers in high volatility conditions.

#### Strategy Advantages
1. Multi-dimensional signal filtering: Effectively reduces false signals through combination of trend, momentum, and volatility indicators.
2. Multi-timeframe analysis: Incorporates weekly trend confirmation to improve directional accuracy.
3. Dynamic risk management: Adaptive stop-loss mechanism based on ATR and Bollinger Band Width that both protects profits and gives trends room to develop.
4. Excellent backtesting results: Net profit 10.80%, profit factor 2.593, win rate 50.70%, maximum drawdown only 1.47%.

#### Strategy Risks
1. Trend dependency: Strategy may generate frequent false signals in ranging markets.
2. Parameter sensitivity: Multiple indicator parameters need optimization for different market conditions.
3. Lag risk: Multiple signal filters may lead to delayed entries, missing part of the move.
4. Backtesting limitations: Historical performance doesn't guarantee future results, live trading needs to consider slippage and fees.

#### Strategy Optimization Directions
1. Signal system optimization: Can introduce other momentum indicators like RSI to enhance signal reliability.
2. Position management optimization: Can dynamically adjust position size based on volatility.
3. Take-profit optimization: Can add trailing stops or technical indicator-based profit targets.
4. Market adaptability optimization: Dynamically adjust parameters for different market conditions.

#### Summary
The strategy builds a complete trend following system through multi-dimensional indicator fusion and multi-timeframe analysis, equipped with dynamic risk management mechanisms. While backtesting performance is excellent, attention must be paid to risks from changing market environments, and it's recommended to carefully validate and continuously optimize in live trading.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-11-01 00:00:00
end: 2025-02-19 08:00:00
period: 2d
basePeriod: 2d
exchanges: [{"eid":"Binance","currency":"ETH_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © FIWB
//@version=6
strategy("Momentum Edge Strategy - 1D BTC Optimized", overlay=true)

// --- Input Parameters ---
atrLength     = input.int(14, title="ATR Length")
atrMultiplier = input.float(1.5, title="ATR Multiplier")
bbWidthThreshold = input.float(0.02, title="Bollinger Band Width Threshold")

// --- Ichimoku Cloud ---
conversionLine = (ta.highest(high, 9) + ta.lowest(low, 9)) / 2
baseLine = (ta.highest(high, 26) + ta.lowest(low, 26)) / 2
leadingSpanA = (conversionLine + baseLine) / 2
leadingSpanB = (ta.highest(high, 52) + ta.lowest(low, 52)) / 2
priceAboveCloud = close > leadingSpanA and close > leadingSpanB
priceBelowCloud = close < leadingSpanA and close < leadingSpanB

// --- MACD Histogram ---
[_, _, macdHistogram] = ta.macd(close, 12, 26, 9)

// --- Multi-Timeframe Trend Confirmation ---
higherTFTrend = request.security(syminfo.tickerid, "W", close > ta.sma(close, 50))

// --- Bollinger Band Width ---
bbBasis = ta.sma(close, 20)
bbUpper = bbBasis + 2 * ta.stdev(close, 20)
bbLower = bbBasis - 2 * ta.stdev(close, 20)
bbWidth = (bbUpper - bbLower) / bbBasis

// --- ATR-based Stop Loss ---
atrValue     = ta.atr(atrLength)
highestHigh = ta.highest(high, atrLength)
lowestLow = ta.lowest(low, atrLength)
longStopLoss = bbWidth < bbWidthThreshold ? lowestLow : close - atrValue * atrMultiplier
shortStopLoss= bbWidth < bbWidthThreshold ? highestHigh : close + atrValue * atrMultiplier

// --- Entry Conditions ---
longCondition = priceAboveCloud and macdHistogram > -0.05 and higherTFTrend and bbWidth > bbWidthThreshold
shortCondition = priceBelowCloud and macdHistogram < 0 and not higherTFTrend and bbWidth > bbWidthThreshold

// --- Strategy Execution ---
if longCondition
    strategy.entry("Long", strategy.long)
    strategy.exit("Exit Long", from_entry="Long", stop=longStopLoss)

if shortCondition
    strategy.entry("Short", strategy.short)
    strategy.exit("Exit Short", from_entry="Short", stop=shortStopLoss)

// --- Plotting ---
plot(leadingSpanA, color=color.new(color.green, 80), title="Leading Span A")
plot(leadingSpanB, color=color.new(color.red, 80), title="Leading Span B")
plotshape(series=longCondition ? close : na, title="Long Signal", location=location.belowbar, color=color.green)
plotshape(series=shortCondition ? close : na, title="Short Signal", location=location.abovebar, color=color.red)

```

> Detail

https://www.fmz.com/strategy/483044

> Last Modified

2025-02-21 10:46:28
