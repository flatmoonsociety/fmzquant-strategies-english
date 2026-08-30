
> Name

Heikin-Ashi Non-Repainting Trend Confirmation Strategy-Heikin-Ashi-Non-Repainting-Trend-Confirmation-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](assets/images/4e3befe75f94ea97f026f13ac5a022a23b9dbabcd45166c116cb0a964898ccc0.png)
![IMG](assets/images/9da8bd3d59acd0dcd7350a92ea81f0de94bfbd68a4dd0024eced38d4ab87bcd6.png)





[trans]
#### Overview
This is an innovative Heikin-Ashi non-repaint trend confirmation strategy designed to solve the repaint problem of the Heikin-Ashi strategy in traditional TradingView. With manual calculation of Haikan Assi candles and multiple trend confirmation mechanisms, this strategy provides a more reliable and transparent trading method.
#### Strategy Principle
The core principles of the strategy include three key steps:
1. Manual non-repaint Haikan Assi candle calculation:
   - Use unique formulas to calculate closing, opening, high and low prices
   - Ensure that historical price data remains stable during subsequent K-line updates
   - Avoid common repaint issues in traditional Haikanasi strategy
2. Multiple trend confirmation:
   - Requires multiple consecutive candles to confirm trend direction
   - Long entry signal: requires X consecutive bullish candles
   - Short entry signal: X consecutive bearish candles are required
   - Filter out false signals through multiple confirmations to improve strategy reliability
3. Flexible trading model:
   -Support traditional trend following mode
   - Provides trend reversal trading options
   - Customizable trading modes (all, long only, short only)
#### Strategic Advantages
1. Eliminate redrawing problems: historical data remains stable, and backtest results are highly consistent with real execution.
2. Multiple trend confirmation: filter out false signals through continuous candles and reduce unnecessary transactions
3. Highly customizable:
   - Flexible entry and exit threshold settings
   - Supports trend following and reversal trading
   - Standard K lines can be hidden to provide clear visualization
4. Suitable for medium and long-term trading: especially suitable for swing trading and trend following
#### Strategy Risk
1. Performance limitations:
   - Not suitable for high-frequency scalping transactions
   - Performance may be poor in volatile markets where the trend is not obvious
   - Need to adjust parameters for different time frames
2. Potential risk control:
   - It is recommended to set up an appropriate stop loss mechanism
   - Continuously optimize parameters under different market conditions
   - Combined with other technical indicators for cross-validation
#### Strategy optimization direction
1. Dynamic adjustment of parameters:
   - Develop adaptive entry and exit threshold algorithms
   - Adjust the number of consecutive candles in real time based on market volatility
   - Introduce machine learning algorithm to optimize parameter selection
2. Enhanced risk management:
   - Integrated dynamic position management
   - Add relevance filter
   - Develop smarter stop-loss mechanisms
3. Indicator combination:
   - Combined with other technical indicators (such as RSI, MACD)
   - Develop multi-index confirmation system
   - Improve signal accuracy and reliability
#### Summary
The Haikan Axi African Repaint Trend Confirmation Strategy provides traders with a more reliable and transparent trading tool through innovative candle calculations and multiple trend confirmation methods. This strategy demonstrates the potential for technological innovation in quantitative trading by eliminating repaint issues, filtering false signals, and providing flexible trading modes.
|| 
#### Overview
This is an innovative Heikin-Ashi Non-Repainting Trend Confirmation Strategy designed to address the repainting issues in traditional TradingView Heikin-Ashi strategies. By manually calculating Heikin-Ashi candles and implementing multi-stage trend confirmation mechanisms, the strategy offers a more reliable and transparent trading approach.

#### Strategy Principles
The strategy's core principles include three key steps:
1. Manual Non-Repainting Heikin-Ashi Candle Calculation:
   - Utilizing unique formulas to calculate close, open, high, and low prices
   - Ensuring historical price data remains stable during subsequent candle updates
   - Avoiding common repainting problems in traditional Heikin-Ashi strategies

2. Multi-Stage Trend Confirmation:
   - Requiring consecutive candles to confirm trend direction
   - Long entry signals: X consecutive bullish candles
   - Short entry signals: X consecutive bearish candles
   - Filtering false signals through multi-confirmation, enhancing strategy reliability

3. Flexible Trading Modes:
   - Supporting traditional trend-following modes
   - Offering trend reversal trading options
   - Customizable trading modes (all, long only, short only)

#### Strategy Advantages
1. Eliminates Repainting: Stable historical data with consistent backtest and live execution results
2. Multi-Trend Confirmation: Filtering false signals through consecutive candles, reducing unnecessary trades
3. High Customizability:
   - Flexible entry and exit threshold settings
   - Supports trend-following and reversal trading
   - Option to hide standard candles for clear visualization
4. Suitable for Medium to Long-Term Trading: Particularly effective for swing trading and trend following

#### Strategy Risks
1. Performance Limitations:
   - Not suitable for high-frequency scalping
   - Potential underperformance in range-bound markets with unclear trends
   - Requires parameter adjustments for different timeframes

2. Potential Risk Mitigation:
   - Recommend implementing appropriate stop-loss mechanisms
   - Continuous parameter optimization across market conditions
   - Cross-verification with additional technical indicators

#### Strategy Optimization Directions
1. Dynamic Parameter Adjustment:
   - Develop adaptive entry and exit threshold algorithms
   - Real-time adjustment of consecutive candle counts based on market volatility
   - Integrate machine learning algorithms for parameter optimization

2. Enhanced Risk Management:
   - Implement dynamic position sizing
   - Add correlation filters
   - Develop more intelligent stop-loss mechanisms

3. Indicator Combination:
   - Integrate with other technical indicators (e.g., RSI, MACD)
   - Develop multi-indicator confirmation systems
   - Improve signal accuracy and reliability

#### Conclusion
The Heikin-Ashi Non-Repainting Trend Confirmation Strategy provides traders with a more reliable and transparent trading tool through innovative candle calculation and multi-stage trend confirmation methods. By eliminating repainting issues, filtering false signals, and offering flexible trading modes, the strategy demonstrates the technical innovation potential in quantitative trading.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-03-15 00:00:00
end: 2025-03-27 00:00:00
period: 3h
basePeriod: 3h
exchanges: [{"eid":"Futures_Binance","currency":"ETH_USDT"}]
*/

//@version=5
//© PineIndicators

strategy("Heikin-Ashi Non-Repainting Strategy [PineIndicators]", overlay=true, initial_capital=100000, default_qty_type=strategy.percent_of_equity, default_qty_value=100, max_boxes_count=500, max_labels_count=500, max_lines_count=500, commission_value=0.01, process_orders_on_close=true, slippage= 2, behind_chart=false)

//====================================
// INPUTS
//====================================
// Number of consecutive candles required for entry and exit
openThreshold = input.int(title="Number of Candles for Entry", defval=2, minval=1)
exitThreshold = input.int(title="Number of Candles for Exit", defval=2, minval=1)
// Trade mode selection: "Long & Short", "Only Long", or "Only Short"
tradeMode = input.string(title="Trade Mode", defval="Only Long", options=["Long & Short", "Only Long", "Only Short"])
// Option to invert the trading logic (bullish signals become short signals, and vice versa)
invertTrades = input.bool(title="Invert Trading Logic (Long ↔ Short)", defval=false)
// Option to hide the standard candles (bodies only)
hideStandard = input.bool(title="Hide Standard Candles", defval=true)
// Heikin-Ashi transparency is fixed (0 = fully opaque)
heikinTransparency = 0

//====================================
// HIDE STANDARD CANDLES
//====================================
// Hide the body of the standard candles by setting them to 100% transparent.
// Note: The wicks of the standard candles cannot be hidden via code.
barcolor(hideStandard ? color.new(color.black, 100) : na)

//====================================
// HEIKIN-ASHI CALCULATION
//====================================
// Calculate Heikin-Ashi values manually
haClose = (open + high + low + close) / 4
var float haOpen = na
haOpen := na(haOpen[1]) ? (open + close) / 2 : (haOpen[1] + haClose[1]) / 2
haHigh = math.max(high, math.max(haOpen, haClose))
haLow  = math.min(low, math.min(haOpen, haClose))

// Define colors for Heikin-Ashi candles (using fixed transparency)
bullColor = color.new(#0097a7, heikinTransparency)
bearColor = color.new(#ff195f, heikinTransparency)

//====================================
// PLOT HEIKIN-ASHI CANDLES
//====================================
// Plot the manually calculated Heikin-Ashi candles over the chart.
// The candle body, wicks, and borders will be colored based on whether the candle is bullish or bearish.
plotcandle(haOpen, haHigh, haLow, haClose, title="Heikin-Ashi", 
     color       = haClose >= haOpen ? bullColor : bearColor,
     wickcolor   = haClose >= haOpen ? bullColor : bearColor,
     bordercolor = haClose >= haOpen ? bullColor : bearColor,
     force_overlay = true)

//====================================
// COUNT CONSECUTIVE TREND CANDLES
//====================================
// Count the number of consecutive bullish or bearish Heikin-Ashi candles.
var int bullishCount = 0
var int bearishCount = 0

if haClose > haOpen
    bullishCount := bullishCount + 1
    bearishCount := 0
else if haClose < haOpen
    bearishCount := bearishCount + 1
    bullishCount := 0
else
    bullishCount := 0
    bearishCount := 0

//====================================
// DEFINE ENTRY & EXIT SIGNALS
//====================================
// The signals are based on the number of consecutive trend candles.
// In normal logic: bullish candles trigger a long entry and bearish candles trigger a short entry.
// If invertTrades is enabled, the signals are swapped.
var bool longEntrySignal  = false
var bool shortEntrySignal = false
var bool exitLongSignal   = false
var bool exitShortSignal  = false

if not invertTrades
    longEntrySignal  := bullishCount >= openThreshold
    shortEntrySignal := bearishCount >= openThreshold
    exitLongSignal   := bearishCount >= exitThreshold
    exitShortSignal  := bullishCount >= exitThreshold
else
    // Inverted logic: bullish candles trigger short entries and bearish candles trigger long entries.
    longEntrySignal  := bearishCount >= openThreshold
    shortEntrySignal := bullishCount >= openThreshold
    exitLongSignal   := bullishCount >= exitThreshold
    exitShortSignal  := bearishCount >= exitThreshold

//====================================
// APPLY TRADE MODE RESTRICTIONS
//====================================
// If the user selects "Only Long", disable short signals (and vice versa).
if tradeMode == "Only Long"
    shortEntrySignal := false
    exitShortSignal  := false
else if tradeMode == "Only Short"
    longEntrySignal  := false
    exitLongSignal   := false

//====================================
// TRADING STRATEGY LOGIC
//====================================
// Execute trades based on the calculated signals.

// If a long position is open:
if strategy.position_size > 0
    if shortEntrySignal
        strategy.close("Long", comment="Reverse Long")
        strategy.entry("Short", strategy.short, comment="Enter Short")
    else if exitLongSignal
        strategy.close("Long", comment="Exit Long")

// If a short position is open:
if strategy.position_size < 0
    if longEntrySignal
        strategy.close("Short", comment="Reverse Short")
        strategy.entry("Long", strategy.long, comment="Enter Long")
    else if exitShortSignal
        strategy.close("Short", comment="Exit Short")

// If no position is open:
if strategy.position_size == 0
    if longEntrySignal
        strategy.entry("Long", strategy.long, comment="Enter Long")
    else if shortEntrySignal
        strategy.entry("Short", strategy.short, comment="Enter Short")

```

> Detail

https://www.fmz.com/strategy/488544

> Last Modified

2025-03-28 17:35:26
