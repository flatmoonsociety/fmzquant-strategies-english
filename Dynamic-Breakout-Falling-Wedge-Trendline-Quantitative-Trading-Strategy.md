
> Name

Dynamic Breakout Falling Wedge Trendline Quantitative Trading Strategy-Dynamic-Breakout-Falling-Wedge-Trendline-Quantitative-Trading-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d8f163ef48d4bc36d9d8.png)
![IMG](https://www.fmz.com/upload/asset/2d971ceefeb34a5aa00ed.png)



[trans]
#### Overview
This strategy is a trend breakout trading system based on the falling wedge pattern in technical analysis. It dynamically identifies highs and lows in price, constructs upper and lower trend lines, and enters long positions when price breaks above the upper trend line. The strategy uses a dynamic stop-profit and stop-loss mechanism to control risks and lock in profits. This is a programmed implementation of a classic technical analysis trading method, especially suitable for capturing reversal opportunities when a downward trend is about to end.
#### Strategy Principle
The core logic of the strategy includes the following key steps:
1. Use the Pivot method to dynamically identify highs and lows in price trends
2. Record and save the two most recent high points and low points and their corresponding time indexes
3. Calculate the slope of the upper and lower trend lines based on these points
4. Determine whether a falling wedge is formed: two high points are required to decrease, two low points are required to decrease, and the slope of the upper trend line is smaller than the slope of the lower trend line.
5. When the price breaks through the upper trend line, a buy signal is triggered
6. Set take-profit and stop-loss conditions based on the percentage of the entry price
#### Strategic Advantages
1. Dynamically identify market structure: The strategy can automatically identify key points in the price structure without manual intervention.
2. Trend reversal capture: Focus on capturing potential reversal opportunities in downward trends, which are usually trading opportunities with higher risk-return ratios.
3. Accurate signal generation: Precisely calculate trend line positions and breakthrough points through mathematical methods
4. Perfect risk management: including a preset stop-profit and stop-loss mechanism, which can effectively control the risk of each transaction
5. Systematic operation: The strategy logic is completely systematic and avoids interference from human emotions.
#### Strategy Risk
1. Risk of false breakthrough: The market may have a false breakthrough, resulting in false signals
2. Parameter sensitivity: The strategy effect is more sensitive to parameter settings. Different market environments may require adjusting parameters.
3. Dependence on market conditions: The strategy may produce too many false signals in volatile markets
4. Stop loss risk: Rapid market conditions may cause the actual stop loss price to slip.
5. Transaction cost impact: Frequent transactions may bring higher transaction costs
#### Strategy optimization direction
1. Signal confirmation mechanism: You can add trading volume, momentum and other indicators as breakthrough confirmation
2. Dynamic parameter optimization: introduce an adaptive mechanism to adjust parameters according to market volatility
3. Multi-time period verification: Add a multi-time period confirmation mechanism to improve signal reliability
4. Improved take profit and stop loss: you can use dynamic take profit and stop loss, such as trailing take profit
5. Market environment filtering: Add trend filters to trade in suitable market environments
#### Summary
This is a well-designed trend trading strategy that implements traditional technical analysis methods in a programmed way. The advantage of the strategy is its ability to automatically identify market structures and capture potential trend reversal opportunities. But at the same time, we also need to pay attention to issues such as false breakthroughs and parameter optimization. Through further optimization and improvement, this strategy is expected to achieve better results in actual transactions.
||

#### Overview
This strategy is a trend breakout trading system based on the falling wedge pattern in technical analysis. It dynamically identifies highs and lows in price action to construct upper and lower trendlines, entering long positions when price breaks above the upper trendline. The strategy employs dynamic take-profit and stop-loss mechanisms to control risk and lock in profits. This is a programmatic implementation of a classic technical analysis trading method, particularly suitable for capturing reversal opportunities when downtrends are potentially ending.

#### Strategy Principles
The core logic includes several key steps:
1. Using Pivot method to dynamically identify highs and lows in price movement
2. Recording and storing the last two highs and lows with their corresponding time indices
3. Calculating slopes of upper and lower trendlines based on these points
4. Identifying falling wedge formation: requiring descending highs and lows, with upper trendline slope less than lower trendline slope
5. Triggering buy signals when price breaks above the upper trendline
6. Setting percentage-based take-profit and stop-loss conditions relative to entry price

#### Strategy Advantages
1. Dynamic Market Structure Recognition: Automatically identifies key price points without manual intervention
2. Trend Reversal Capture: Focuses on capturing potential reversals of downtrends, typically high-reward opportunities
3. Precise Signal Generation: Accurately calculates trendline positions and breakout points using mathematical methods
4. Comprehensive Risk Management: Includes preset take-profit and stop-loss mechanisms for effective risk control
5. Systematic Operation: Fully systematized strategy logic, avoiding emotional interference

#### Strategy Risks
1. False Breakout Risk: Market may produce false breakouts leading to incorrect signals
2. Parameter Sensitivity: Strategy effectiveness is sensitive to parameter settings, requiring adjustment in different market conditions
3. Market Condition Dependency: May generate excessive false signals in ranging markets
4. Stop Loss Risk: Fast market movements may cause slippage in actual stop loss execution
5. Transaction Cost Impact: Frequent trading may incur high transaction costs

#### Strategy Optimization Directions
1. Signal Confirmation Mechanism: Add volume, momentum indicators for breakout confirmation
2. Dynamic Parameter Optimization: Introduce adaptive mechanisms to adjust parameters based on market volatility
3. Multiple Timeframe Verification: Add multi-timeframe confirmation to improve signal reliability
4. Improved Stop Loss/Take Profit: Implement dynamic mechanisms like trailing stops
5. Market Environment Filtering: Add trend filters to trade only in suitable market conditions

#### Summary
This is a well-designed trend trading strategy that implements traditional technical analysis methods programmatically. Its strength lies in automated market structure identification and potential trend reversal capture. However, attention must be paid to false breakouts and parameter optimization. With further enhancement and refinement, this strategy has potential for improved performance in actual trading.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-22 00:00:00
end: 2025-02-19 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Binance","currency":"ETH_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/

//@version=6
strategy("Falling Wedge Strategy by Nitin", overlay=true, margin_long=100, margin_short=100)

// Input parameters
leftBars = input.int(5, "Left Bars for Pivot", minval=1, maxval=20)
rightBars = input.int(5, "Right Bars for Pivot", minval=1, maxval=20)
takeProfitPercent = input.float(20, "Take Profit %", minval=0.1, maxval=100)/100
stopLossPercent = input.float(2, "Stop Loss %", minval=0.1, maxval=100)/100

// Global variables
var float buyPrice = na
var line upperLine = na
var line lowerLine = na

// Detect pivot highs and lows
ph = ta.pivothigh(leftBars, rightBars)
pl = ta.pivotlow(leftBars, rightBars)

// Track last two pivot highs
var float[] highs = array.new_float()
var int[] highIndices = array.new_int()
if not na(ph)
    array.unshift(highs, ph)
    array.unshift(highIndices, bar_index[rightBars])
    if array.size(highs) > 2
        array.pop(highs)
        array.pop(highIndices)

// Track last two pivot lows
var float[] lows = array.new_float()
var int[] lowIndices = array.new_int()
if not na(pl)
    array.unshift(lows, pl)
    array.unshift(lowIndices, bar_index[rightBars])
    if array.size(lows) > 2
        array.pop(lows)
        array.pop(lowIndices)

// Calculate trendlines and signals
if array.size(highs) >= 2 and array.size(lows) >= 2
    h1 = array.get(highs, 0)
    h2 = array.get(highs, 1)
    i1 = array.get(highIndices, 0)
    i2 = array.get(highIndices, 1)
    
    l1 = array.get(lows, 0)
    l2 = array.get(lows, 1)
    j1 = array.get(lowIndices, 0)
    j2 = array.get(lowIndices, 1)
    
    m_upper = (h1 - h2) / (i1 - i2)
    m_lower = (l1 - l2) / (j1 - j2)
    
    currentUpper = h2 + m_upper * (bar_index - i2)
    currentLower = l2 + m_lower * (bar_index - j2)
    
    if h1 < h2 and l1 < l2 and m_upper < m_lower and m_upper < 0 and m_lower < 0
        
        // Buy signal on breakout
        if ta.crossover(close, currentUpper)
            strategy.entry("Buy", strategy.long)
            buyPrice := close
            strategy.exit("Take Profit/Stop Loss", "Buy", stop=buyPrice * (1 - stopLossPercent), limit=buyPrice * (1 + takeProfitPercent))

// Plotting
plotshape(strategy.position_size > 0 ? buyPrice : na, "Buy Price", style=shape.labelup, location=location.belowbar, color=color.green, textcolor=color.white, text="BUY")
plot(strategy.position_size > 0 ? buyPrice * (1 - stopLossPercent) : na, "Stop Loss", color=color.red, linewidth=2)
plot(strategy.position_size > 0 ? buyPrice * (1 + takeProfitPercent) : na, "Take Profit", color=color.green, linewidth=2)
```

> Detail

https://www.fmz.com/strategy/483089

> Last Modified

2025-02-27 17:02:08
