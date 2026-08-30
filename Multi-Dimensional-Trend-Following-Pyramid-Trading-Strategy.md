
> Name

Multi-Dimensional-Trend-Following-Pyramid-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/12f3361a0954c1e75d4.png)

[trans]
#### Overview
This is a quantitative trading strategy based on the Markttechnik (MT) analysis method widely used by German financial institutions. This strategy combines multiple dimensions such as moving average (SMA) trend tracking, identification of support and resistance levels, reversal K-line pattern analysis, and pyramidal positioning to achieve robust trading through strict risk control. The core of the strategy is to determine the direction of the market trend through comprehensive judgment of multi-dimensional signals, and to expand profits by adding positions in a pyramid style when the trend is formed.
#### Strategy Principle
The strategy uses the following key components to build a trading system:
1. Trend judgment: Use the 10-period simple moving average (SMA) as the main trend judgment indicator. Prices above the SMA are considered an upward trend, and vice versa.
2. Support and resistance: Determine the short-term support and resistance areas through the highest price and lowest price of three periods.
3. Reversal pattern: Analyze two important reversal K-line patterns, hammer line and shooting star line.
4. Trading signals: On the basis of confirming the trend direction, trading signals are triggered by combining support and resistance levels and reversal K-line patterns.
5. Position management: Adopt a pyramid-type position accumulation strategy, allowing up to 2 times of position accumulation.
6. Risk control: Set a maximum drawdown limit of 5%, and use a risk-return ratio of 2.0 to set stop loss and take profit.
#### Strategic Advantages
1. Multi-dimensional signal confirmation: Improve the accuracy of transactions through comprehensive analysis of signals from multiple dimensions such as trends, support and resistance, K-line patterns, etc.
2. Pyramid-style position addition: When the trend continues, you can expand your profit margin by adding positions.
3. Strict risk control: Control risks through maximum drawdown limits and fixed risk-return ratios.
4. Visual support: The strategy provides a complete graphical display, including support and resistance areas, trend lines and signal backgrounds.
5. Flexible parameter settings: Key parameters can be adjusted according to different market conditions.
#### Strategy Risk
1. Trend reversal risk: Continuous losses may occur when a strong trend suddenly reverses.
2. False breakthrough risk: The market may have false support and resistance breakthrough signals.
3. Parameter sensitivity: Strategy performance is more sensitive to parameter settings, and different market environments may require different parameter combinations.
4. Impact of slippage: When the market fluctuates greatly, the actual transaction price may deviate greatly from the signal price.
5. Risk of adding positions: Pyramid adding positions may amplify losses when the market fluctuates violently.
#### Strategy optimization direction
1. Dynamic parameter optimization: An adaptive parameter adjustment mechanism can be introduced to dynamically adjust various parameters according to market fluctuations.
2. Market environment classification: Add a market environment identification module and use different parameter combinations in different market environments.
3. Stop loss optimization: A moving stop loss mechanism can be introduced to better protect existing profits.
4. Refining the conditions for adding positions: The conditions for adding positions can be optimized based on factors such as volatility and trading volume.
5. Signal filtering: Increase filtering conditions such as trading volume and volatility to improve signal quality.
#### Summary
This strategy builds a complete trading system through multi-dimensional signal analysis and strict risk control. The core advantage of the strategy lies in the reliability of signals and the controllability of risks, but parameters still need to be optimized for different market environments. Through the suggested optimization direction, the stability and profitability of the strategy are expected to be further improved. The strategy is suitable for use in markets with obvious trends, and is an option worth considering for traders seeking steady returns. ||
#### Overview
This is a quantitative trading strategy based on the Markttechnik (MT) analysis method widely used by German financial institutions. The strategy combines multiple dimensions including SMA trend following, support and resistance identification, reversal candlestick pattern analysis, and pyramid position sizing, achieving stable trading through strict risk control. The core of the strategy lies in determining market trend direction through multi-dimensional signal synthesis and expanding profits through pyramid position sizing when trends form.

#### Strategy Principles
The strategy employs the following key components to build the trading system:
1. Trend Determination: Uses 10-period Simple Moving Average (SMA) as the main trend indicator, with prices above SMA indicating uptrend and vice versa.
2. Support and Resistance: Determines short-term support and resistance zones using 3-period high and low prices.
3. Reversal Patterns: Analyzes hammer and shooting star candlestick patterns as important reversal indicators.
4. Trading Signals: Triggers trading signals based on trend direction confirmation combined with support/resistance levels and reversal patterns.
5. Position Management: Employs pyramid position sizing strategy allowing up to 2x position accumulation.
6. Risk Control: Sets 5% maximum drawdown limit and uses 2.0 risk-reward ratio for stop loss and take profit levels.

#### Strategy Advantages
1. Multi-dimensional Signal Confirmation: Improves trading accuracy through comprehensive analysis of signals from trend, support/resistance, and candlestick patterns.
2. Pyramid Position Sizing: Allows profit expansion through position accumulation during trend continuation.
3. Strict Risk Control: Controls risk through maximum drawdown limits and fixed risk-reward ratio.
4. Visualization Support: Provides complete graphical display including support/resistance zones, trend lines, and signal backgrounds.
5. Flexible Parameter Settings: Key parameters can be adjusted according to different market conditions.

#### Strategy Risks
1. Trend Reversal Risk: Consecutive losses may occur during sudden trend reversals.
2. False Breakout Risk: Market may generate false support/resistance breakout signals.
3. Parameter Sensitivity: Strategy performance is sensitive to parameter settings, requiring different combinations for different market environments.
4. Slippage Impact: Actual execution prices may significantly deviate from signal prices during high market volatility.
5. Position Sizing Risk: Pyramid position sizing may amplify losses during extreme market volatility.

#### Strategy Optimization Directions
1. Dynamic Parameter Optimization: Introduce adaptive parameter adjustment mechanism based on market volatility conditions.
2. Market Environment Classification: Add market environment recognition module to apply different parameter combinations under different market conditions.
3. Stop Loss Optimization: Introduce trailing stop mechanism to better protect existing profits.
4. Position Sizing Condition Refinement: Optimize position sizing conditions based on volatility, volume, and other factors.
5. Signal Filtering: Add volume, volatility, and other filtering conditions to improve signal quality.

#### Summary
This strategy constructs a complete trading system through multi-dimensional signal analysis and strict risk control. The core advantages lie in signal reliability and risk controllability, though parameter optimization is still needed for different market environments. Through the suggested optimization directions, strategy stability and profitability can be further improved. The strategy is suitable for markets with clear trends and is a worthwhile consideration for traders seeking stable returns.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-01-02 00:00:00
end: 2025-01-09 00:00:00
period: 30m
basePeriod: 30m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT","balance":49999}]
*/

//@version=6
strategy("Markttechnik Strategie mit Pyramiding und Drawdown-Limit", overlay=true, pyramiding=2)

// Eingabewerte
lengthSupport = input.int(3, title="Unterstützungs-/Widerstandsfenster", minval=1)
lengthSMA = input.int(10, title="SMA Länge für Trends", minval=1)
riskRewardRatio = input.float(2.0, title="Risk-Reward-Ratio", minval=0.1, step=0.1)
maxDrawdown = input.float(5.0, title="Maximaler Drawdown (%)", minval=0.1, step=0.1)

// Unterstützungs- und Widerstandszonen berechnen
support = ta.lowest(low, lengthSupport)
resistance = ta.highest(high, lengthSupport)

// Trendindikator (SMA-basierter Trend)
sma = ta.sma(close, lengthSMA)
trendUp = close > sma
trendDown = close < sma

// Umkehrstäbe erkennen
isHammer = close > open and (low < open) and ((open - low) > 2 * (close - open))
isShootingStar = open > close and (high > open) and ((high - open) > 2 * (open - close))

// Kauf- und Verkaufssignale
buySignal = isHammer and close > support and trendUp
sellSignal = isShootingStar and close < resistance and trendDown

// Strategiefunktionen: Pyramiding und Drawdown
equityPeak = na(strategy.equity[1]) or strategy.equity > strategy.equity[1] ? strategy.equity : strategy.equity[1]  // Höchster Kontostand
drawdown = equityPeak > 0 ? (strategy.equity - equityPeak) / equityPeak * 100 : 0  // Drawdown in Prozent

if buySignal and drawdown > -maxDrawdown
    strategy.entry("Buy", strategy.long)
    strategy.exit("Sell", "Buy", stop=low - (high - low) * riskRewardRatio, limit=close + (close - low) * riskRewardRatio)

if sellSignal and drawdown > -maxDrawdown
    strategy.entry("Sell", strategy.short)
    strategy.exit("Cover", "Sell", stop=high + (high - low) * riskRewardRatio, limit=close - (high - close) * riskRewardRatio)

// Unterstützungs- und Widerstandslinien zeichnen
plot(support, color=color.new(color.green, 80), linewidth=1, title="Unterstützungszone")
plot(resistance, color=color.new(color.red, 80), linewidth=1, title="Widerstandszone")

// Trendlinie (SMA)
plot(sma, color=color.blue, linewidth=2, title="SMA-Trend")

// Umkehrstäbe hervorheben
bgcolor(buySignal ? color.new(color.green, 90) : na, title="Kaufsignal Hintergrund")
bgcolor(sellSignal ? color.new(color.red, 90) : na, title="Verkaufssignal Hintergrund")

// Debugging: Drawdown anzeigen
plot(drawdown, title="Drawdown (%)", color=color.purple, linewidth=2, style=plot.style_line)

```

> Detail

https://www.fmz.com/strategy/477970

> Last Modified

2025-01-10 16:17:03
