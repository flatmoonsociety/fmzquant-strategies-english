
> Name

Dual-Timeframe Trend Reversal K-line Pattern Quantitative Trading Strategy-Dual-Timeframe-Trend-Reversal-Candlestick-Pattern-Quantitative-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/5206cc64e907b64324.png)

[trans]
#### Overview
This strategy is a quantitative trading system based on two classic K-line forms: hammer and hanging man. Strategies predict potential turning points in price action by identifying these reversal patterns in the market. The system combines multiple technical indicators to confirm the validity of the signal, including the proportional relationship between the K-line entity and the shadow line, the trend direction and other factors, to achieve accurate capture of the market reversal point.
#### Strategy Principle
The core logic of the strategy is to identify two key K-line patterns through a programmatic approach:
1. Hammer: Appears in a downward trend, suggesting a possible reversal and rise. It is characterized by a small real body, a long lower shadow (at least twice the length of the real body), and a very short or no upper shadow.
2. Hanging man: appears in an upward trend, suggesting a possible reversal and decline. The morphological characteristics are similar to the hammer line, but the location and meaning are opposite.
Strategies quantify these patterns by setting strict parameters, including:
- Minimum K-line real body length multiplier
- The ratio of the lower shadow line to the height of the K line
- Position holding period
#### Strategic Advantages
1. Systematic identification: Accurately identify market reversal signals through programmed methods, avoiding the subjectivity of human judgment.
2. Risk controllable: A clear position holding cycle is set to avoid risks caused by excessive position holdings.
3. Signal visualization: Visually display trading signals on the chart to facilitate analysis and optimization.
4. Flexible parameters: parameters can be adjusted according to different market conditions to improve strategy adaptability.
#### Strategy Risk
1. Risk of false breakthrough: False signals may occur in reversal patterns, which need to be confirmed in combination with other technical indicators.
2. Timeliness risk: A fixed holding period may not be able to fully capture the full potential of price movements.
3. Market environment dependence: Too many false signals may be generated in volatile markets.
#### Strategy optimization direction
1. Introducing trend filters: indicators such as moving averages can be added to filter trends and improve signal quality.
2. Dynamic holding period: dynamically adjust the holding time according to market volatility.
3. Multi-period confirmation: Introducing a trend confirmation mechanism with a higher time frame.
4. Stop loss optimization: Add a dynamic stop loss mechanism to improve risk control capabilities.
#### Summary
This strategy realizes the systematic application of classic technical analysis theory through quantitative methods, and has strong practical value. Through parameter optimization and improvement of risk control mechanisms, strategies can maintain stable performance in different market environments. The modular design of the strategy also provides a good foundation for subsequent optimization. ||
#### Overview
This strategy is a quantitative trading system based on two classic candlestick patterns: Hammer and Hanging Man. It predicts potential market turning points by identifying these reversal patterns. The system combines multiple technical indicators to confirm signal validity, including the relationship between candlestick body and shadows, trend direction, and other elements, achieving precise capture of market reversal points.

#### Strategy Principle
The core logic of the strategy is to identify two key candlestick patterns programmatically:
1. Hammer: Appears in downtrends, suggesting potential upward reversal. Characterized by a small body, long lower shadow (at least twice the body length), and minimal or no upper shadow.
2. Hanging Man: Appears in uptrends, suggesting potential downward reversal. Similar characteristics to Hammer but appears in different locations with opposite implications.

The strategy quantifies these patterns through strict parameters, including:
- Minimum candle body length multiplier
- Lower shadow to candle height ratio
- Holding periods

#### Strategy Advantages
1. Systematic Identification: Precisely identifies market reversal signals programmatically, avoiding subjective human judgment.
2. Controlled Risk: Sets clear holding periods, avoiding risks from excessive position holding.
3. Signal Visualization: Displays trading signals intuitively on charts for analysis and optimization.
4. Flexible Parameters: Can adjust parameters based on different market conditions, improving strategy adaptability.

#### Strategy Risks
1. False Breakout Risk: Reversal patterns may generate false signals, requiring confirmation from other technical indicators.
2. Timing Risk: Fixed holding periods may not fully capture price movement potential.
3. Market Environment Dependency: May generate excessive false signals in ranging markets.

#### Strategy Optimization Directions
1. Introduce Trend Filters: Add indicators like moving averages to filter trends and improve signal quality.
2. Dynamic Holding Periods: Adjust holding time based on market volatility.
3. Multi-timeframe Confirmation: Implement higher timeframe trend confirmation mechanisms.
4. Stop Loss Optimization: Add dynamic stop loss mechanisms to improve risk control.

#### Summary
This strategy implements classical technical analysis theory systematically through quantification, demonstrating strong practical value. Through parameter optimization and risk control mechanism refinement, the strategy can maintain stable performance in different market environments. The modular design also provides a solid foundation for subsequent optimization.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-12-10 00:00:00
end: 2025-01-08 08:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT","balance":49999}]
*/

//@version=6
strategy("Hammer and Hanging Man Strategy", overlay=true)

// Input parameters
length = input.int(5, title="Minimum Candle Body Length (Multiplier)", minval=1)
shadowRatio = input.float(1, title="Lower Shadow to Candle Height Ratio", minval=1.0)
holdPeriods = input.int(26, title="Hold Periods (Bars)", minval=1)  // Holding period in bars

// Function to calculate the absolute value
absValue(x) =>
    x >= 0 ? x : -x

// Function to check if it is a Hammer
isHammer() =>
    bodyLength = absValue(close - open)
    candleHeight = high - low
    lowerShadow = math.min(open, close) - low
    upperShadow = high - math.max(open, close)
    smallBody = bodyLength <= candleHeight / length
    longLowerShadow = lowerShadow >= bodyLength * shadowRatio
    shortUpperShadow = upperShadow <= bodyLength
    smallBody and longLowerShadow and shortUpperShadow and close > open

// Function to check if it is a Hanging Man
isHangingMan() =>
    bodyLength = absValue(close - open)
    candleHeight = high - low
    lowerShadow = math.min(open, close) - low
    upperShadow = high - math.max(open, close)
    smallBody = bodyLength <= candleHeight / length
    longLowerShadow = lowerShadow >= bodyLength * shadowRatio
    shortUpperShadow = upperShadow <= bodyLength
    smallBody and longLowerShadow and shortUpperShadow and close < open

// Detect the candles
hammer = isHammer()
hangingMan = isHangingMan()

// Trading logic: Long on Hammer, Short on Hanging Man
if hammer
    strategy.entry("Long", strategy.long)  // Long entry on Hammer

if hangingMan
    strategy.entry("Short", strategy.short)  // Short entry on Hanging Man

// Exit after X bars
if strategy.position_size > 0 and bar_index - strategy.opentrades.entry_bar_index(0) >= holdPeriods
    strategy.close("Long")

if strategy.position_size < 0 and bar_index - strategy.opentrades.entry_bar_index(0) >= holdPeriods
    strategy.close("Short")

// Visualization of signals
plotshape(hammer, title="Hammer", location=location.belowbar, color=color.green, style=shape.labelup, text="Hammer")
plotshape(hangingMan, title="Hanging Man", location=location.abovebar, color=color.red, style=shape.labeldown, text="Hanging Man")
```

> Detail

https://www.fmz.com/strategy/477960

> Last Modified

2025-01-10 15:47:53
