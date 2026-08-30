
> Name

Double-Seven-Strategy-Trend-Following-and-Mean-Reversion-Dual-Optimization-Trading-SystemDouble-Seven-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/17bacb16f999e2937a7.png)

[trans]
#### Overview
This strategy is a quantitative trading system that combines trend following and mean reversion. It determines the direction of the general trend through the 200-day moving average (MA200), and uses 7-day price fluctuations to identify short-term oversold opportunities to seize the best buying opportunities in the upward trend. This method not only ensures the correctness of the trading direction, but also can intervene in time when the price is adjusted, giving full play to the guiding role of technical analysis in trading.
#### Strategy Principle
The core logic of the strategy includes two dimensions: first, judge the long-term trend through MA200, and only consider opening a position when the price is above MA200; second, observe the price performance of the last 7 trading days, open a long position when a new 7-day low appears and is still above MA200, and close the position when the price reaches a new 7-day high. This design not only ensures following the trend, but also can build low positions during adjustments. It is a systematic strategy that integrates the ideas of trend tracking and mean reversion.
#### Strategic Advantages
1. Reliability of trend confirmation: Using MA200 as a trend filter can effectively avoid opening a position in a downward trend.
2. Accuracy of entry timing: identify oversold correction opportunities through the 7-day low to improve the cost-effectiveness of opening a position.
3. High degree of systematization: the strategy rules are clear, there are no subjective judgment factors, and it is easy to implement programmatically.
4. Improved risk control: Reduce the probability of false signals through the dual mechanisms of trend filtering and oversold judgment.
5. Wide applicability: The strategy logic is simple and universal, and can be applied to multiple markets and varieties.
#### Strategy Risk
1. Lag trend judgment: MA200, as a long-term moving average, is lagging and may cause errors in judgment at trend turning points.
2. Risk of false breakthrough: A false breakthrough may occur after the price breaks through the 7-day high, leading to premature closing of positions.
3. Not applicable in volatile markets: In sideways volatile markets, frequent short-term highs and lows may generate too many trading signals.
4. Dependence on market environment: The effect of strategy is greatly affected by market trend characteristics, and the performance of different market environments varies significantly.
#### Strategy optimization direction
1. Dynamic cycle optimization: The MA cycle and short-term observation cycle can be dynamically adjusted according to different market characteristics.
2. Multiple confirmation mechanism: Increase auxiliary indicators such as trading volume and volatility to improve signal reliability.
3. Position management optimization: Introduce a dynamic position management mechanism and adjust the position ratio according to market volatility.
4. Improved stop loss mechanism: Design a more flexible stop loss plan, such as trailing stop loss or volatility stop loss.
5. Type optimization: Design differentiated parameter combinations for different market environments.
#### Summary
Double Seven Strategy is a quantitative trading system that organically combines trend following with mean reversion. Through the combined use of MA200 and 7-day price fluctuations, it not only ensures the correctness of the trading direction, but also grasps the better entry opportunity. Although there are certain limitations, through reasonable optimization and risk control, this strategy has good practical value and room for expansion. It is recommended that traders conduct targeted optimization based on market characteristics and their own needs in practical applications to improve the stability and profitability of the strategy. ||
#### Overview
This strategy is a quantitative trading system that combines trend following and mean reversion. It uses the 200-day moving average (MA200) to determine the major trend direction while utilizing 7-day price fluctuations to identify short-term oversold opportunities, achieving optimal entry timing in uptrends. This method ensures both directional accuracy and timely intervention during price adjustments, fully leveraging technical analysis in trading.

#### Strategy Principles
The core logic includes two dimensions: First, using MA200 to judge long-term trends, only considering positions when price is above MA200; Second, observing price performance over the last 7 trading days, entering long positions when a 7-day low occurs while still above MA200, and closing positions when price reaches a 7-day high. This design ensures both trend following and low-point entry, creating a systematic strategy that combines trend following and mean reversion concepts.

#### Strategy Advantages
1. Trend Confirmation Reliability: Using MA200 as a trend filter effectively avoids opening positions in downtrends.
2. Entry Timing Precision: Identifies oversold correction opportunities through 7-day lows, improving entry value.
3. High Systematization: Clear strategy rules without subjective judgment factors, easy to implement programmatically.
4. Comprehensive Risk Control: Reduces false signal probability through dual mechanisms of trend filtering and oversold judgment.
5. Wide Applicability: Simple and universal strategy logic applicable across multiple markets and instruments.

#### Strategy Risks
1. Trend Judgment Lag: MA200 as a long-term moving average has inherent lag, potentially causing misjudgments at trend turning points.
2. False Breakout Risk: Price breaking above 7-day highs may result in false breakouts, leading to premature exits.
3. Unsuitable for Ranging Markets: Frequent short-term highs and lows in sideways markets may generate excessive trading signals.
4. Market Environment Dependency: Strategy effectiveness heavily influenced by market trend characteristics, showing significant performance differences across market environments.

#### Strategy Optimization Directions
1. Dynamic Period Optimization: Adjust MA period and short-term observation period based on different market characteristics.
2. Multiple Confirmation Mechanisms: Add auxiliary indicators like volume and volatility to improve signal reliability.
3. Position Management Optimization: Introduce dynamic position management mechanisms to adjust holding ratios based on market volatility.
4. Stop Loss Enhancement: Design more flexible stop loss solutions, such as trailing stops or volatility-based stops.
5. Pattern Optimization: Design differentiated parameter combinations for different market environments.

#### Summary
The Double Seven Strategy is a quantitative trading system that organically combines trend following with mean reversion. Through the coordinated use of MA200 and 7-day price fluctuations, it ensures both directional accuracy and optimal entry timing. While certain limitations exist, the strategy holds practical value and expansion potential through reasonable optimization and risk control. Traders are advised to optimize the strategy based on market characteristics and personal needs in practical applications to enhance stability and profitability.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-11-27 00:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © EdgeTools

//@version=5
strategy("Larry Connors' Double Seven Strategy", overlay=true)

// 200-day moving average
ma200 = ta.sma(close, 200)

// Conditions for Double Seven Strategy
priceAboveMa200 = close > ma200

// Find the lowest close over the last 7 days
lowestClose7Days = ta.lowest(close, 7)

// Find the highest close over the last 7 days
highestClose7Days = ta.highest(close, 7)

// Entry and exit rules
longCondition = priceAboveMa200 and close <= lowestClose7Days
exitCondition = close >= highestClose7Days

// Enter long position
if (longCondition)
    strategy.entry("Long", strategy.long)

// Exit long position
if (exitCondition)
    strategy.close("Long")
    
// Plot moving averages
plot(ma200, "200-day MA", color=color.blue)

```

> Detail

https://www.fmz.com/strategy/473246

> Last Modified

2024-11-28 15:41:34
