
> Name

Adaptive-Dual-Indicator-Cross-Smart-Timing-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/106d9822f479a117d05.png)

[trans]
#### Overview
This is an adaptive trading strategy based on dual technical indicators RSI and CCI. The strategy builds a complete trading system by monitoring the cross status of RSI and CCI indicators in different time periods, combined with the EMA moving average trend. This strategy has the characteristics of strong adaptability and stable signals, and can effectively capture overbought and oversold market opportunities.
#### Strategy Principle
The core logic of the strategy includes the following aspects:
1. Time period adaptation: Dynamically adjust the parameter settings of RSI and CCI according to different time periods (1 minute to 4 hours).
2. Dual indicator confirmation: Use a combination of RSI (relative strength indicator) and CCI (concomitant indicator) to filter trading signals. Trading signals are generated when RSI and CCI meet specific conditions at the same time.
3. Signal continuity verification: Ensure signal stability by setting the minimum duration (stayTimeFrames).
4. Dynamic take-profit and stop-loss: Set dynamic take-profit and stop-loss points based on the RSI and CCI levels at the time of entry.
5. Trend confirmation: Use the 200-period EMA as a trend reference.
#### Strategic Advantages
1. Strong adaptability: The strategy can automatically adjust parameters according to different time periods, making it more adaptable.
2. High signal reliability: Through the cross-confirmation of dual technical indicators, the reliability of the signal is significantly improved.
3. Improved risk control: The use of dynamic stop-profit and stop-loss mechanisms can effectively control risks.
4. The operating rules are clear: the entry and exit conditions are clear and easy to operate.
5. Good scalability: The policy framework is flexible and new filtering conditions can be added as needed.
#### Strategy Risk
1. Parameter sensitivity: There may be differences in optimal parameters under different market environments.
2. Sideways shock risk: False signals may be generated during market shocks.
3. Impact of slippage: High-frequency trading may face the impact of slippage.
4. Signal delay: The multiple confirmation mechanism may cause a slight delay in entry timing.
5. Market environment dependence: Performance in strong trending markets may be better than volatile markets.
#### Strategy optimization direction
1. Parameter adaptation: An adaptive parameter optimization mechanism can be introduced to dynamically adjust parameters according to market conditions.
2. Market environment identification: Add a market environment identification module to adopt different trading strategies under different market conditions.
3. Volatility adaptation: introduce volatility indicators and adjust stop-profit and stop-loss parameters according to the volatility.
4. Signal filtering: Add more technical indicators and pattern recognition to filter out false signals.
5. Risk management: Improve fund management plans, increase holding time and position control.
#### Summary
This strategy builds a robust trading system by combining the advantages of RSI and CCI indicators. The adaptive nature of the strategy and the complete risk control mechanism make it highly practical. Through continuous optimization and improvement, this strategy is expected to achieve better performance in actual transactions. It is recommended that traders conduct sufficient backtesting and parameter optimization before using it in real trading. ||
#### Overview
This is an adaptive trading strategy based on dual technical indicators RSI and CCI. The strategy monitors the cross-state of RSI and CCI indicators under different time periods, combined with EMA trend, to build a complete trading system. The strategy features strong adaptability and stable signals, effectively capturing market overbought and oversold opportunities.

#### Strategy Principle
The core logic includes:
1. Time period adaptation: Dynamically adjusts RSI and CCI parameters based on different time periods (1 minute to 4 hours).
2. Dual indicator confirmation: Uses combination of RSI (Relative Strength Index) and CCI (Commodity Channel Index) to filter trading signals. Trading signals are generated only when both RSI and CCI meet specific conditions.
3. Signal persistence verification: Ensures signal stability through minimum duration settings (stayTimeFrames).
4. Dynamic profit/loss limits: Sets dynamic take-profit and stop-loss levels based on entry RSI and CCI levels.
5. Trend confirmation: Uses 200-period EMA as trend reference.

#### Strategy Advantages
1. Strong adaptability: Strategy automatically adjusts parameters for different time periods.
2. High signal reliability: Cross-confirmation through dual technical indicators significantly improves signal reliability.
3. Comprehensive risk control: Dynamic profit/loss mechanism effectively controls risk.
4. Clear operation rules: Entry and exit conditions are clear for practical operation.
5. Good extensibility: Flexible strategy framework allows addition of new filtering conditions.

#### Strategy Risks
1. Parameter sensitivity: Optimal parameters may vary in different market environments.
2. Range-bound market risk: False signals may occur during market consolidation.
3. Slippage impact: High-frequency trading may face slippage effects.
4. Signal delay: Multiple confirmation mechanisms may cause slight delays in entry timing.
5. Market environment dependence: May perform better in trending markets than ranging markets.

#### Strategy Optimization
1. Parameter adaptation: Introduce adaptive parameter optimization mechanism for dynamic adjustment based on market conditions.
2. Market environment recognition: Add market state identification module for different trading strategies in various market conditions.
3. Volatility adaptation: Introduce volatility indicators to adjust profit/loss parameters based on volatility levels.
4. Signal filtering: Add more technical indicators and pattern recognition to filter false signals.
5. Risk management: Improve money management plan, enhance position time and size control.

#### Summary
The strategy builds a robust trading system by combining the advantages of RSI and CCI indicators. Its adaptive features and comprehensive risk control mechanisms provide good practicality. Through continuous optimization and improvement, the strategy shows promise for better performance in actual trading. Traders are advised to conduct thorough backtesting and parameter optimization before live implementation.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-01-19 00:00:00
end: 2025-02-18 00:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=6
strategy("RSI & CCI Strategy with Alerts", overlay=true)

// Detect current chart timeframe
tf = timeframe.period

// Define settings for different timeframes
rsiLength = tf == "1" ? 30 : tf == "5" ? 30 : tf == "15" ? 30 : tf == "30" ? 30 : 30  // Default
cciLength = tf == "1" ? 15 : tf == "5" ? 20 : tf == "15" ? 20 : tf == "30" ? 20 : 20  // Default
cciBuyThreshold = tf == "1" ? -100 : tf == "5" ? -100 : tf == "15" ? -100 : tf == "30" ? -100 : -100
cciSellThreshold = tf == "1" ? 100 : tf == "5" ? 100 : tf == "15" ? 100 : tf == "30" ? 100 : 100  // Default
stayTimeFrames = tf == "1" ? 1 : tf == "5" ? 1 : tf == "15" ? 1 : tf == "30" ? 1 : tf == "240" ? 1 : 2  // Default
stayTimeFramesOver =tf == "1" ? 1 : tf == "5" ? 2 : tf == "15" ? 2 : tf == "30" ? 3 : 2 // Default

// Calculate RSI & CCI
rsi = ta.rsi(close, rsiLength)
rsiOver = ta.rsi(close, 14)
cci = ta.cci(close, cciLength)

// EMA 50
ema200 = ta.ema(close, 200)
plot(ema200, color=color.rgb(255, 255, 255), linewidth=2, title="EMA 200")

// CCI candle threshold tracking
var int cciEntryTimeLong = na
var int cciEntryTimeShort = na

// Store entry time when CCI enters the zone
if (cci < cciBuyThreshold)
    if na(cciEntryTimeLong)
        cciEntryTimeLong := bar_index
else
    cciEntryTimeLong := na

if (cci > cciSellThreshold)
    if na(cciEntryTimeShort)
        cciEntryTimeShort := bar_index
else
    cciEntryTimeShort := na

// Confirming CCI has stayed in the threshold for required bars
cciStayedBelowNeg100 = not na(cciEntryTimeLong) and (bar_index - cciEntryTimeLong >= stayTimeFrames) and rsi >= 53
cciStayedAbove100 = not na(cciEntryTimeShort) and (bar_index - cciEntryTimeShort >= stayTimeFrames) and rsi <= 47


// CCI & RSI candle threshold tracking for Buy Over and Sell Over signals
var int buyOverEntryTime = na
var int sellOverEntryTime = na

// Track entry time when RSI and CCI conditions are met
if (rsiOver <= 31 and cci <= -120)
    if na(buyOverEntryTime)
        buyOverEntryTime := bar_index
else
    buyOverEntryTime := na

if (rsiOver >= 69 and cci >= 120)
    if na(sellOverEntryTime)
        sellOverEntryTime := bar_index
else
    sellOverEntryTime := na

// Confirm that conditions are met for the required stayTimeFrames
buyOverCondition = not na(buyOverEntryTime) and (bar_index - buyOverEntryTime >= stayTimeFramesOver)
sellOverCondition = not na(sellOverEntryTime) and (bar_index - sellOverEntryTime <= stayTimeFramesOver)

//Buy and sell for over bought or sell 
conditionOverBuy = buyOverCondition
conditionOverSell = sellOverCondition

// Buy and sell conditions
buyCondition = cciStayedBelowNeg100
sellCondition = cciStayedAbove100

// // Track open positions
var bool isLongOpen = false
var bool isShortOpen = false

// // Strategy logic for backtesting
// if (buyCondition and not isLongOpen)
//     strategy.entry("Long", strategy.long)
//     isLongOpen := true
//     isShortOpen := false

// if (sellCondition and not isShortOpen)
//     strategy.entry("Short", strategy.short)
//     isShortOpen := true
//     isLongOpen := false

// // Close positions based on EMA 50
// if (isLongOpen and exitLongCondition)
//     strategy.close("Long")
//     isLongOpen := false

// if (isShortOpen and exitShortCondition)
//     strategy.close("Short")
//     isShortOpen := false



// Track RSI at position entry
var float entryRSILong = na
var float entryRSIShort = na

// Track CCI at position entry
var float entryCCILong = na
var float entryCCIShort = na

if (buyOverCondition and not isLongOpen)
    strategy.entry("Long", strategy.long)
    entryRSILong := rsi  // Store RSI at entry
    entryCCILong := cci
    isLongOpen := true
    isShortOpen := false

if (sellOverCondition and not isShortOpen)
    strategy.entry("Short", strategy.short)
    entryRSIShort := rsi  // Store RSI at entry
    entryCCIShort := cci  // Stpre CCI at entry
    isShortOpen := true
    isLongOpen := false

exitLongRSICondition = isLongOpen and not na(entryRSILong) and rsi >= (entryRSILong + 12)  or rsi <= (entryRSILong -8)
exitShortRSICondition = isShortOpen and not na(entryRSIShort) and rsi <= (entryRSIShort - 12)  or rsi >= (entryRSIShort +8)

exitLongCCICondition = isLongOpen and not na(entryCCILong) and cci <= (entryCCILong -100)
exitShortCCICondition = isShortOpen and not na(entryCCIShort) and cci >= (entryCCIShort +100)

// Close positions based on EMA 50 or RSI change
if (isLongOpen and (exitLongRSICondition) or (exitLongCCICondition))
    strategy.close("Long")
    isLongOpen := false
    entryRSILong := na
    entryCCILong := na
    isLongOpen := false

if (isShortOpen and (exitShortRSICondition) or (exitShortCCICondition))
    strategy.close("Short")
    isShortOpen := false
    entryRSIShort := na
    entryCCIShort := na
    isShortOpen := false



// Plot buy and sell signals
plotshape(buyCondition, style=shape.labelup, location=location.belowbar, color=color.green, size=size.large, title="Buy Signal", text="BUY")
plotshape(sellCondition, style=shape.labeldown, location=location.abovebar, color=color.red, size=size.large, title="Sell Signal", text="SELL")

//Plot buy and sell OverBought
plotshape(conditionOverBuy, style=shape.labelup, location=location.belowbar, color=color.rgb(255, 238, 0), size=size.large, title="OverBuy Signal", text="Over Sell")
plotshape(conditionOverSell, style=shape.labeldown, location=location.abovebar, color=color.rgb(186, 40, 223), size=size.large, title="OverSell Signal", text="Over Buy")

// Alerts
alertcondition(buyCondition, title="Buy Alert", message="Buy Signal Triggered")
alertcondition(sellCondition, title="Sell Alert", message="Sell Signal Triggered")

```

> Detail

https://www.fmz.com/strategy/482591

> Last Modified

2025-02-19 10:56:59
