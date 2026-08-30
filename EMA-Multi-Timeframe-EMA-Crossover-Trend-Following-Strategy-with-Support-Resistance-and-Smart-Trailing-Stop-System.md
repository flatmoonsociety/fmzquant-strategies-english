
> Name

Multi-Timeframe-EMA-Crossover-Trend-Following-Strategy-with-Support-Resistance-and-Smart-Trailing-Stop-System
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d873926329a2e55cdb2b.png)
![IMG](https://www.fmz.com/upload/asset/2d8b855463ddcb58badad.png)





[trans]

#### Overview
This strategy is a trend following trading system that combines multiple time frame analysis, mainly based on three exponential moving average (EMA) crossover signals of different periods, supplemented by high time frame support and resistance levels for filtering. The core of this strategy is to use the cross relationship between EMA5, EMA8 and EMA13 to generate buy and sell signals, while introducing a percentage-based intelligent trailing stop loss mechanism to protect earned profits and limit potential losses. The entire system design focuses on providing clear entry and exit rules and risk management framework while trading with the trend.
#### Strategy Principle
From a deep dive into the code, here's how the strategy works:
1. Signal generation:
   - Buy signal: Triggered when the short-term EMA5 crosses the mid-term EMA8 and the long-term EMA13 from below at the same time
   - Sell signal: Triggered when short-term EMA5 falls below mid-term EMA8 and long-term EMA13 from above at the same time
2. High time frame filtering:
   - The strategy introduces the highs and lows of the 1-hour chart as support and resistance levels
   - These levels are shown on the chart as red (resistance) and green (support) lines, helping traders identify potential price reversal areas
3. Risk management:
   - Implemented percentage trailing stop loss based on user-defined parameters (default 0.10%)
   - When holding a long position, the stop loss point is set as a trailOffset percentage below the highest price.
   - When holding a short position, the stop loss point is set as a percentage of trailOffset above the lowest price.
   - The stop loss level will be continuously adjusted as the price moves in a favorable direction to lock in profits
4. Graphical feedback:
   - Trade exit points are highlighted with cross marks on the chart
   - The trailing stop loss level is marked with a circle to visually display the risk control level
#### Strategic Advantages
This strategy has the following outstanding advantages:
1. Multiple signal confirmation: EMA5 is required to cross EMA8 and EMA13 at the same time, which reduces the possibility of false breakthroughs and improves signal reliability.
2. Multi-time frame analysis: Integrate the support and resistance levels of higher time frames (1 hour) to help traders consider trading decisions from a more macro market structure perspective.
3. Intelligent dynamic stop loss: Unlike fixed stop loss, the trailing stop loss mechanism can protect funds while allowing profits to continue to grow and improve the risk-reward ratio.
4. Clear visual feedback: By drawing key indicators, signals and exit points on the chart, traders can intuitively understand the market status and strategy logic.
5. Two-way trading capabilities: The strategy supports both long and short transactions, allowing you to find opportunities in various market environments and maximize profit potential.
6. Parametric risk control: The trailing stop loss offset can be adjusted by the user (0.01% to 1%), allowing the risk parameters to be flexibly set according to personal risk preferences and market conditions.
#### Strategy Risk
Although this strategy has several advantages, it also has the following potential risks:
1. Risk of volatile market: In a sideways market without a clear trend, EMA crossovers may produce frequent false signals, leading to continuous losses. The solution is to add a market structure or volatility filter and only trade when the trend is clear.
2. Trailing stop loss gap risk: In the case of rapid fluctuations or overnight gaps, the price may skip the trailing stop loss level, causing the actual stop loss price to be much lower than expected. It is recommended to consider adding a fixed maximum loss limit as additional protection.
3. Parameter sensitivity: Strategy performance is highly dependent on the selected EMA period and trailing stop loss percentage. Different markets and time frames may require different parameter settings. Parameter validity should be verified through comprehensive backtesting before live trading.
4. Lack of volatility adaptation: The current version of the trailing stop is based on a fixed percentage, which may be too tight in high volatility markets and too loose in low volatility markets. Consider adjusting the trailing stop distance based on ATR.
5. Signal conflict: Under certain market conditions, EMA crossover signals may conflict with support/resistance levels on the 1-hour chart, causing difficulty in trading decisions. In this case, clear priority rules should be established or wait for consistent signals.
#### Strategy optimization direction
Based on code analysis, the following are potential directions for improvement strategies:
1. Introduce ATR dynamic stop loss: replace the fixed percentage trailing stop loss and use a dynamic stop loss based on the average true fluctuation range (ATR) to better adapt to the fluctuation characteristics of different markets. This provides a looser stop-loss space during periods of high volatility and closer to price during periods of low volatility.
2. Add trend strength filtering: Integrate ADX (average directional index) or similar trend strength indicators to only execute transactions when a strong trend is confirmed to avoid frequent false signals in sideways markets.
3. Add trading volume confirmation: Require trading signals to be accompanied by higher-than-average trading volume to increase the credibility of breakthroughs and reduce the erosion of false signals on accounts.
4. Realize dynamic risk management: automatically adjust position size based on account size, historical volatility and winning rate, optimizing capital growth potential while keeping risks controllable.
5. Optimize the high time frame filter: The current strategy uses the high and low points of the previous K line on the 1-hour chart as support and resistance. Consider introducing more complex support and resistance identification algorithms, such as key structural areas or multiple time frame support and resistance combinations.
6. Add market status classification: Develop a market environment classification system (trend, range, high volatility, etc.), and adjust strategy parameters or trading logic according to different market status to improve adaptability.
#### Summary
The multi-time frame EMA cross trend following strategy combines classic technical analysis elements with modern risk management techniques to provide traders with a trading system with clear structure and clear rules. Its core advantage is that the signal generation logic is simple and intuitive, and at the same time, it effectively controls risks and protects the safety of funds through the tracking stop loss mechanism.
The strategy combines the precise entry signals provided by short-term EMA crossovers with the market structure perspective provided by higher timeframe support and resistance levels, helping traders to capture high-probability trading opportunities when the trend direction is clear. Although it may face challenges in volatile markets, the stability and performance of the strategy in different market environments can be significantly improved through the recommended optimization directions, especially increasing trend strength filtering and ATR-based dynamic stop loss.
For investors looking to build a systematic trading approach, this strategy provides a solid foundational framework that can be further customized and optimized based on personal risk appetite and trading objectives. By strictly following the rules of the strategy and maintaining trading discipline, traders can expect to achieve consistent returns in a market with clear trends. ||
#### Overview
This strategy is a trend-following trading system that incorporates multi-timeframe analysis, primarily based on crossover signals from three different exponential moving averages (EMAs), supplemented with higher timeframe support and resistance levels. The core of the strategy lies in utilizing the crossing relationships between EMA5, EMA8, and EMA13 to generate buy and sell signals, while implementing a percentage-based smart trailing stop mechanism to protect profits and limit potential losses. The entire system is designed to focus on trading with the trend while providing clear entry and exit rules and a risk management framework.

#### Strategy Principles
Through in-depth code analysis, the operational principles of this strategy are as follows:

1. Signal Generation:
   - Buy Signal: Triggered when the short-term EMA5 simultaneously crosses above the medium-term EMA8 and long-term EMA13
   - Sell Signal: Triggered when the short-term EMA5 simultaneously crosses below the medium-term EMA8 and long-term EMA13

2. Higher Timeframe Filtering:
   - The strategy incorporates high and low points from the 1-hour chart as support and resistance levels
   - These levels are displayed on the chart as red (resistance) and green (support) lines, helping traders identify potential price reversal zones

3. Risk Management:
   - Implements a percentage-based trailing stop based on user-defined parameters (default 0.10%)
   - For long positions, the stop loss is set at trailOffset percentage below the highest price
   - For short positions, the stop loss is set at trailOffset percentage above the lowest price
   - The stop loss level continuously adjusts as the price moves in a favorable direction, locking in profits

4. Graphical Feedback:
   - Trade exit points are highlighted on the chart with cross markers
   - Trailing stop levels are marked with circles, providing intuitive visualization of risk control levels

#### Strategy Advantages
This strategy offers several notable advantages:

1. Multiple Signal Confirmation: Requiring EMA5 to simultaneously cross both EMA8 and EMA13 reduces the possibility of false breakouts and increases signal reliability.

2. Multi-Timeframe Analysis: Integration of higher timeframe (1-hour) support and resistance levels helps traders consider trading decisions from a more macroscopic market structure perspective.

3. Smart Dynamic Stop Loss: Unlike fixed stop losses, the trailing stop mechanism allows profits to continue growing while protecting capital, improving the risk-reward ratio.

4. Clear Visual Feedback: By plotting key indicators, signals, and exit points on the chart, traders can intuitively understand market conditions and strategy logic.

5. Bidirectional Trading Capability: The strategy supports both long and short trading, seeking opportunities in various market environments to maximize profit potential.

6. Parameterized Risk Control: The trailing stop offset can be adjusted by users (0.01% to 1%), allowing flexible risk parameter settings based on personal risk preferences and market conditions.

#### Strategy Risks
Despite its many advantages, the strategy also presents the following potential risks:

1. Choppy Market Risk: In sideways markets without clear trends, EMA crossovers may produce frequent false signals, leading to consecutive losses. The solution is to add market structure or volatility filters and only trade when trends are clearly defined.

2. Trailing Stop Gap Risk: In cases of rapid fluctuations or overnight gaps, prices may jump past trailing stop levels, causing actual stop-loss prices to be far lower than expected. Consider adding fixed maximum loss limits as additional protection.

3. Parameter Sensitivity: Strategy performance highly depends on the chosen EMA periods and trailing stop percentage; different markets and timeframes may require different parameter settings. Parameters should be validated through comprehensive backtesting before live trading.

4. Lack of Volatility Adaptation: The current version of trailing stop is based on a fixed percentage, which may be too tight in high-volatility markets and too loose in low-volatility markets. Consider adjusting trailing stop distances based on ATR.

5. Signal Conflicts: Under certain market conditions, EMA crossover signals may contradict support/resistance levels from the 1-hour chart, making trading decisions difficult. In such cases, clear priority rules should be established or wait for signal alignment.

#### Strategy Optimization Directions
Based on code analysis, here are potential directions for improving the strategy:

1. Introduce ATR Dynamic Stop Loss: Replace fixed percentage trailing stops with dynamic stops based on Average True Range (ATR) to better adapt to different market volatility characteristics. This would provide wider stop space during high-volatility periods and tighter stops during low-volatility periods.

2. Add Trend Strength Filtering: Integrate the ADX (Average Directional Index) or similar trend strength indicators, executing trades only when strong trends are confirmed, avoiding frequent false signals in sideways markets.

3. Incorporate Volume Confirmation: Require trading signals to be accompanied by above-average volume, increasing the credibility of breakouts and reducing account erosion from false signals.

4. Implement Dynamic Risk Management: Automatically adjust position size based on account size, historical volatility, and win rate, optimizing capital growth potential while keeping risk controllable.

5. Optimize Higher Timeframe Filters: The current strategy uses the previous candlestick's high and low points from the 1-hour chart as support and resistance; consider introducing more complex support and resistance identification algorithms, such as key structural zones or multiple timeframe support and resistance combinations.

6. Add Market State Classification: Develop a market environment classification system (trend, range, high volatility, etc.) and adjust strategy parameters or trading logic for different market states to improve adaptability.

#### Conclusion
The Multi-Timeframe EMA Crossover Trend Following Strategy combines classic technical analysis elements with modern risk management techniques, providing traders with a structurally clear and rule-based trading system. Its core strengths lie in simple and intuitive signal generation logic while effectively controlling risk through the trailing stop mechanism to protect capital safety.

The strategy combines precise entry signals provided by short-term EMA crossovers with market structure perspective from higher timeframe support and resistance levels, helping traders capture high-probability trading opportunities when trend direction is clear. Although it may face challenges in oscillating markets, through the suggested optimization directions, especially adding trend strength filtering and ATR-based dynamic stops, the strategy's stability and performance across different market environments can be significantly enhanced.

For investors looking to build a systematic trading approach, this strategy provides a solid foundation framework that can be further customized and optimized according to personal risk preferences and trading goals. By strictly following strategy rules and maintaining trading discipline, traders can expect to achieve consistent returns in clearly trending markets.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-02-25 14:00:00
end: 2025-03-02 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"ETH_USDT"}]
*/

//@version=6
strategy("EMA Crossover Strategy with S/R and Cross Exits v6", overlay=true, margin_long=100, margin_short=100)

// Eingabeparameter
trailOffset = input.float(0.10, "Trailing Stop Offset (%)", minval=0.01, maxval=1, step=0.01)

// EMA Berechnungen
ema5 = ta.ema(close, 5)
ema8 = ta.ema(close, 8)
ema13 = ta.ema(close, 13)

// Plot der EMAs
plot(ema5, "EMA 5", color.rgb(7, 7, 7), 2)
plot(ema8, "EMA 8", color.new(color.blue, 0), 2)
plot(ema13, "EMA 13", color.new(color.red, 0), 2)

// Unterstützungs- und Widerstandsniveaus aus dem 1-Stunden-Chart
hourlyHigh = request.security(syminfo.tickerid, "60", high[1], gaps=barmerge.gaps_off, lookahead=barmerge.lookahead_on)
hourlyLow = request.security(syminfo.tickerid, "60", low[1], gaps=barmerge.gaps_off, lookahead=barmerge.lookahead_on)

// Plot der Unterstützungs- und Widerstandsniveaus
plot(hourlyHigh, "Hourly Resistance", color.new(color.red, 0), linewidth=2)
plot(hourlyLow, "Hourly Support", color.new(color.green, 0), linewidth=2)

// Signalerkennung
buySignal = ta.crossover(ema5, ema8) and ta.crossover(ema5, ema13)
sellSignal = ta.crossunder(ema5, ema8) and ta.crossunder(ema5, ema13)

// Trailing Stop Berechnungen
var float longStop = na
var float shortStop = na
var float maxHigh = na
var float minLow = na

if strategy.position_size > 0
    if strategy.position_size[1] <= 0
        maxHigh := high
        longStop := high * (1 - trailOffset)
    else
        maxHigh := math.max(maxHigh, high)
        longStop := math.max(longStop, maxHigh * (1 - trailOffset))
else
    maxHigh := na
    longStop := na

if strategy.position_size < 0
    if strategy.position_size[1] >= 0
        minLow := low
        shortStop := low * (1 + trailOffset)
    else
        minLow := math.min(minLow, low)
        shortStop := math.min(shortStop, minLow * (1 + trailOffset))
else
    minLow := na
    shortStop := na

// Ausführung der Orders
if (buySignal)
    strategy.entry("Long", strategy.long)
if (sellSignal)
    strategy.entry("Short", strategy.short)

// Schließen bei gegenteiligem Signal
if (buySignal)
    strategy.close("Short")
if (sellSignal)
    strategy.close("Long")

// Trailing Stop Anwendung
strategy.exit("Long Exit", "Long", stop = longStop)
strategy.exit("Short Exit", "Short", stop = shortStop)

// Exit-Punkte im Chart mit Kreuzen markieren
plotshape(series=strategy.position_size[1] > 0 and strategy.position_size == 0, title="Long Exit", location=location.belowbar, color=color.red, style=shape.cross, text="Exit Long", textcolor=color.rgb(5, 5, 5), size=size.small)
plotshape(series=strategy.position_size[1] < 0 and strategy.position_size == 0, title="Short Exit", location=location.abovebar, color=color.green, style=shape.cross, text="Exit Short", textcolor=color.rgb(7, 7, 7), size=size.small)

// Plot der Trailing Stops
plot(strategy.position_size > 0 ? longStop : na, "Long Stop", color.green, style=plot.style_circles)
plot(strategy.position_size < 0 ? shortStop : na, "Short Stop", color.red, style=plot.style_circles)
```

> Detail

https://www.fmz.com/strategy/484571

> Last Modified

2025-03-03 09:25:58
