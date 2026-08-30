
> Name

Dynamic-ATR-Optimized-Intraday-High-Low-Breakout-Trading-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d905c84cf95c4762e587.png)
![IMG](https://www.fmz.com/upload/asset/2d8a820e9fe684e2b08d2.png)



[trans]
#### Overview
This is a trading strategy based on intraday price high and low breakthroughs, combined with the ATR indicator to dynamically adjust stop loss and profit targets. This strategy works by monitoring the high and low prices of the previous trading day and the current trading day, and trades when the price breaks through these key levels. The strategy also introduces the buffer concept to reduce false signals and uses ATR multiples to set dynamic risk management parameters.
#### Strategy Principle
The core logic of the strategy is based on trading above previous highs and lows. Specifically:
1. At the beginning of each trading day, record the highest and lowest prices of the previous day.
2. Track the highest and lowest prices of the day in real time
3. Compare the extreme values of the previous day and the current day, and select the highest value and the lowest value as the breakthrough reference point
4. Trading signals are triggered when the price breaks through these reference points (taking buffers into account)
5. Use 1.5 times ATR as stop loss distance and 2 times as profit target.
6. The system automatically draws the breakthrough position on the chart and provides a trading reminder function
#### Strategic Advantages
1. Strong dynamic adaptability - dynamically adjust stop loss and profit targets through ATR, allowing the strategy to adapt to different market fluctuation environments
2. Improved risk control - Stop loss and profit targets based on ATR are set to ensure that the risk of each transaction is controllable.
3. Signal filtering mechanism - use buffers to reduce false breakout signals
4. Visual support - clearly mark the breakthrough position on the chart to facilitate real-time monitoring by traders
5. High degree of automation - includes complete entry and exit logic, enabling fully automated trading
#### Strategy Risk
1. Sideways market risk - Frequent false signals may occur when market volatility is low
2. Gap risk - Gap at night may cause stop loss to be invalid
3. Trend continuation risk - fixed ATR multiples may close positions prematurely in strong trending markets
4. Parameter sensitivity - the settings of buffer and ATR multiples have a greater impact on strategy performance
5. Market environment dependence - strategies perform better in high-volatility markets, but may perform poorly in low-volatility periods
#### Strategy optimization direction
1. Introduce trend filter - you can add trend indicators such as moving averages and only trade in the direction of the trend
2. Dynamic buffer - automatically adjusts buffer size based on market volatility
3. Improve the take-profit mechanism - consider using trailing stop-loss to avoid exiting the market prematurely in a strong trend
4. Time filtering - add trading time period filtering to avoid periods with less volatility
5. Volume confirmation - Add a volume confirmation mechanism to improve the reliability of breakthroughs
#### Summary
This is a well-designed and logically designed breakout trading strategy. By combining the ATR indicator and buffer zone concepts, trading opportunities and risk control are effectively balanced. The strategy has a high degree of visualization and automation, making it suitable for day traders. However, users need to pay attention to the adaptability of the market environment and adjust parameter settings according to actual trading results. There is room for further improvement of the strategy through the suggested optimization directions. ||
#### Overview
This is a trading strategy based on intraday price high-low breakouts, incorporating the ATR indicator for dynamic adjustment of stop-loss and profit targets. The strategy monitors the previous and current day's highest and lowest prices, executing trades when prices break through these key levels. It introduces a buffer concept to reduce false signals and uses ATR multipliers for dynamic risk management parameters.

#### Strategy Principle
The core logic is based on trading price breakouts of previous high-low points. Specifically:
1. Records previous day's high and low at the start of each trading day
2. Tracks current day's high and low in real-time
3. Compares extremes from previous and current day to select reference points
4. Triggers trading signals when price breaks these reference points (considering buffer)
5. Uses 1.5x ATR for stop-loss distance and 2x for profit target
6. Automatically plots breakout positions and provides trading alerts

#### Strategy Advantages
1. Strong Dynamic Adaptability - Dynamically adjusts stop-loss and profit targets through ATR
2. Comprehensive Risk Control - Sets ATR-based stop-loss and profit targets for controlled risk
3. Signal Filtering Mechanism - Uses buffer to reduce false breakout signals
4. Visualization Support - Clearly marks breakout positions on charts for real-time monitoring
5. High Automation Level - Includes complete entry and exit logic for automated trading

#### Strategy Risks
1. Sideways Market Risk - May generate frequent false signals in low volatility markets
2. Gap Risk - Overnight gaps may render stop-losses ineffective
3. Trend Continuation Risk - Fixed ATR multipliers may exit too early in strong trends
4. Parameter Sensitivity - Buffer and ATR multiplier settings significantly impact performance
5. Market Environment Dependency - Strategy performs better in high volatility markets

#### Strategy Optimization Directions
1. Introduce Trend Filters - Add trend indicators like moving averages for directional trading
2. Dynamic Buffer - Automatically adjust buffer size based on market volatility
3. Improve Profit Taking - Consider trailing stops to avoid early exits in strong trends
4. Time Filtering - Add trading time filters to avoid low volatility periods
5. Volume Confirmation - Add volume confirmation mechanism for more reliable breakouts

#### Summary
This is a well-designed strategy with clear logic. By combining ATR indicators and buffer concepts, it effectively balances trading opportunities and risk control. The strategy's visualization and automation levels are high, suitable for intraday traders. However, users need to pay attention to market environment adaptability and adjust parameters based on actual trading results. Through the suggested optimization directions, there is room for further strategy improvement.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-02-13 00:00:00
end: 2025-02-14 01:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Binance","currency":"BTC_USDT"}]
*/

//@version=6
strategy("Previous/Current Day High-Low Breakout Strategy", overlay=true)

// === INPUTS ===
buffer = input(10, title="Buffer Points Above/Below Day High/Low")  // 0-10 point buffer
atrMultiplier = input.float(1.5, title="ATR Multiplier for SL/TP")  // ATR-based SL & TP

// === DETECT A NEW DAY CORRECTLY ===
dayChange = ta.change(time("D")) != 0  // Returns true when a new day starts

// === FETCH PREVIOUS DAY HIGH & LOW CORRECTLY ===
var float prevDayHigh = na
var float prevDayLow = na

if dayChange
    prevDayHigh := high[1]  // Store previous day's high
    prevDayLow := low[1]  // Store previous day's low

// === TRACK CURRENT DAY HIGH & LOW ===
todayHigh = ta.highest(high, ta.barssince(dayChange))  // Highest price so far today
todayLow = ta.lowest(low, ta.barssince(dayChange))  // Lowest price so far today

// === FINAL HIGH/LOW SELECTION (Whichever Happens First) ===
finalHigh = math.max(prevDayHigh, todayHigh)  // Use the highest value
finalLow = math.min(prevDayLow, todayLow)  // Use the lowest value

// === ENTRY CONDITIONS ===
// ? BUY (LONG) Condition: Closes below final low - buffer
longCondition = close <= (finalLow - buffer)

// ? SELL (SHORT) Condition: Closes above final high + buffer
shortCondition = close >= (finalHigh + buffer)

// === ATR STOP-LOSS & TAKE-PROFIT ===
atr = ta.atr(14)
longSL = close - (atr * atrMultiplier)  // Stop-Loss for Long
longTP = close + (atr * atrMultiplier * 2)  // Take-Profit for Long
shortSL = close + (atr * atrMultiplier)  // Stop-Loss for Short
shortTP = close - (atr * atrMultiplier * 2)  // Take-Profit for Short

// === EXECUTE LONG (BUY) TRADE ===
if longCondition
    strategy.entry("BUY", strategy.long, comment="? BUY Signal")
    strategy.exit("SELL TP", from_entry="BUY", stop=longSL, limit=longTP)

// === EXECUTE SHORT (SELL) TRADE ===
if shortCondition
    strategy.entry("SELL", strategy.short, comment="? SELL Signal")
    strategy.exit("BUY TP", from_entry="SELL", stop=shortSL, limit=shortTP)

// === PLOT LINES FOR VISUALIZATION ===
plot(finalHigh, title="Breakout High (Prev/Today)", color=color.new(color.blue, 60), linewidth=2, style=plot.style_stepline)
plot(finalLow, title="Breakout Low (Prev/Today)", color=color.new(color.red, 60), linewidth=2, style=plot.style_stepline)

// === ALERT CONDITIONS ===
alertcondition(longCondition, title="? Buy Signal", message="BUY triggered ?")
alertcondition(shortCondition, title="? Sell Signal", message="SELL triggered ?")

```

> Detail

https://www.fmz.com/strategy/483125

> Last Modified

2025-02-27 16:53:19
