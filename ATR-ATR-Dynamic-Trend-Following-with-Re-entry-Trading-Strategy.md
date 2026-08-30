
> Name

ATR dynamic trend following and re-entry trading strategy-ATR-Dynamic-Trend-Following-with-Re-entry-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1130fe9232956b0e1dc.png)

[trans]
#### Overview
This is a trend following strategy based on dynamic adjustment of ATR, which combines moving averages and ATR indicators to determine entry and exit points. The core feature of this strategy is to dynamically adjust the upper and lower tracks of the moving average through ATR, enter the market when the price breaks through the upper track, and set stop-loss and take-profit points based on the ATR multiple. At the same time, the strategy also includes an innovative re-entry mechanism, which allows re-opening of positions when the price pulls back to the entry point.
#### Strategy Principle
The strategy operates based on the following key elements:
1. Use the ATR-adjusted moving average as the basis for trend judgment to form a dynamic upper and lower track.
2. When the price breaks through the upper track, a long signal is generated, and the entry price is the current closing price.
3. The stop loss level is set to 2 times the ATR distance below the entry price.
4. The take-profit level is set to be above the entry price (5 + custom multiple) × ATR distance
5. After stop loss or take profit is triggered, if the price falls back to the original entry price, the strategy will automatically re-enter the market.
6. Use the display limit of a maximum of 30 K lines to optimize chart display
#### Strategic Advantages
1. Strong dynamic adaptability: the moving average adjusted by ATR can adapt to changes in market volatility
2. Scientific risk management: stop loss and take profit points are dynamically set based on ATR, in line with market fluctuation characteristics
3. Innovation in the re-entry mechanism: allowing re-entry when the price pulls back to a favorable position, increasing profit opportunities
4. Excellent visualization effect: The strategy provides clear entry, stop loss, and take profit line display, which facilitates transaction monitoring.
5. Flexible and adjustable parameters: the trend judgment period and take-profit multiple can be adjusted by inputting parameters
#### Strategy Risk
1. Trend reversal risk: Stop loss may be triggered frequently in volatile markets
2. Risk of re-entry: If the price pulls back to the entry point and re-opens a position, you may face continuous stop loss.
3. Slippage risk: During periods of severe volatility, the actual transaction price may deviate from the signal price.
4. Parameter sensitivity: The optimal parameters may vary greatly under different market conditions.
5. Computational load: multiple technical indicators need to be calculated in real time, which may increase the system load
#### Strategy optimization direction
1. Introduce market environment filtering: you can add a volatility filter to adjust strategy parameters or suspend trading during periods of high volatility.
2. Optimize re-entry logic: Consider adopting stricter conditions when re-entering, such as trend confirmation indicators.
3. Improve the stop-profit mechanism: the moving stop-loss function can be implemented to protect more profits when the trend continues.
4. Add time filtering: you can add trading time period restrictions to avoid low liquidity periods
5. Optimize calculation efficiency: improve strategy operation efficiency by reducing unnecessary calculations and drawings
#### Summary
This is a trend following strategy with reasonable design and clear logic, which provides good market adaptability through dynamic adjustment of ATR. The strategy's re-entry mechanism is an innovative point that can provide additional profit opportunities under good market conditions. Although there are some risk points that need attention, the stability and profitability of the strategy can be further improved through the suggested optimization directions. For investors looking for a systematic approach to trading, this is a basic strategy framework worth considering. ||
#### Overview
This is a trend-following strategy that dynamically adjusts using ATR, combining moving averages and ATR indicators to determine entry and exit points. The strategy's core feature is using ATR to dynamically adjust moving average bands, entering long positions when price breaks above the upper band, and setting stop-loss and take-profit levels based on ATR multiples. Additionally, the strategy includes an innovative re-entry mechanism allowing new positions when price retraces to the entry point.

#### Strategy Principles
The strategy operates based on the following key elements:
1. Uses ATR-adjusted moving averages as trend indicators, forming dynamic upper and lower bands
2. Generates long entry signals when price breaks above the upper band, with entry price at current close
3. Sets stop-loss at 2×ATR below entry price
4. Sets take-profit at (5+custom multiplier)×ATR above entry price
5. Automatically re-enters positions if price retraces to original entry level after stop-loss or take-profit
6. Implements 30-bar maximum display limit for optimized chart visualization

#### Strategy Advantages
1. Strong Dynamic Adaptability: ATR-adjusted moving averages self-adapt to market volatility changes
2. Scientific Risk Management: Stop-loss and take-profit levels dynamically set based on ATR, matching market volatility characteristics
3. Innovative Re-entry Mechanism: Allows re-entry at favorable price levels, increasing profit opportunities
4. Excellent Visualization: Provides clear entry, stop-loss, and take-profit line displays for trade monitoring
5. Flexible Parameters: Adjustable trend period and take-profit multiplier through input parameters

#### Strategy Risks
1. Trend Reversal Risk: Frequent stop-losses possible in ranging markets
2. Re-entry Risk: Consecutive stop-losses possible when re-entering at previous entry points
3. Slippage Risk: Actual execution prices may deviate from signal prices during high volatility
4. Parameter Sensitivity: Optimal parameters may vary significantly across different market conditions
5. Computational Load: Real-time calculation of multiple technical indicators may increase system load

#### Strategy Optimization Directions
1. Implement Market Environment Filters: Add volatility filters to adjust parameters or pause trading during high volatility
2. Optimize Re-entry Logic: Consider stricter conditions for re-entry, such as trend confirmation indicators
3. Enhance Profit Taking: Implement trailing stops to protect more profits in trending markets
4. Add Time Filters: Implement trading time restrictions to avoid low liquidity periods
5. Improve Calculation Efficiency: Reduce unnecessary calculations and plotting to enhance strategy performance

#### Summary
This is a well-designed, logically clear trend-following strategy with good market adaptability through ATR dynamic adjustment. The re-entry mechanism is an innovative feature that can provide additional profit opportunities under favorable market conditions. While there are some risk factors to consider, the suggested optimization directions can further enhance the strategy's stability and profitability. For investors seeking systematic trading methods, this represents a worthwhile basic strategy framework.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-19 00:00:00
end: 2025-02-16 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=6
strategy("KON SET By Sai", overlay=true, max_lines_count=40)

// INPUTS
length = input.int(10, "Trend Length")
target_multiplier = input.int(0, "Set Targets") // Target adjustment
max_bars = 30  // Number of bars to display the lines after signal

// VARIABLES
var bool inTrade = false
var float entryPrice = na
var float stopLoss = na
var float targetPrice = na
var int barCount = na  // Counter to track how many bars have passed since signal

// ATR for stop-loss and target calculation
atr_value = ta.sma(ta.atr(200), 200) * 0.8

// Moving averages for trend detection
sma_high = ta.sma(high, length) + atr_value
sma_low = ta.sma(low, length) - atr_value

// Signal conditions for trend changes
signal_up = ta.crossover(close, sma_high)
signal_down = ta.crossunder(close, sma_low)

// Entry conditions
if not inTrade and signal_up
    entryPrice := close
    stopLoss := close - atr_value * 2
    targetPrice := close + atr_value * (5 + target_multiplier)
    strategy.entry("Long", strategy.long)
    strategy.exit("Exit Long", "Long", stop=stopLoss, limit=targetPrice)
    inTrade := true
    barCount := 0  // Reset bar count when signal occurs

// Exit conditions
if inTrade and (close <= stopLoss or close >= targetPrice)
    inTrade := false
    entryPrice := na
    stopLoss := na
    targetPrice := na
    barCount := na  // Reset bar count on exit

// Re-entry logic
if not inTrade and close == entryPrice
    entryPrice := close
    stopLoss := close - atr_value * 2
    targetPrice := close + atr_value * (5 + target_multiplier)
    strategy.entry("Re-Long", strategy.long)
    strategy.exit("Re-Exit Long", "Re-Long", stop=stopLoss, limit=targetPrice)
    inTrade := true
    barCount := 0  // Reset bar count when re-entry happens

// Count bars since the signal appeared (max 30 bars)
if inTrade and barCount < max_bars
    barCount := barCount + 1

// Plotting lines for entry, stop-loss, and targets (Only during active trade and within max_bars)
entry_line = plot(inTrade and barCount <= max_bars ? entryPrice : na, title="Entry Price", color=color.new(color.green, 0), linewidth=1, style=plot.style_cross)
sl_line = plot(inTrade and barCount <= max_bars ? stopLoss : na, title="Stop Loss", color=color.new(color.red, 0), linewidth=1, style=plot.style_cross)
target_line = plot(inTrade and barCount <= max_bars ? targetPrice : na, title="Target Price", color=color.new(color.blue, 0), linewidth=1, style=plot.style_cross)

// Background color between entry and target/stop-loss (Only when inTrade and within max_bars)
fill(entry_line, target_line, color=color.new(color.green, 90), title="Target Zone")
fill(entry_line, sl_line, color=color.new(color.red, 90), title="Stop-Loss Zone")

// Label updates (reduce overlap and clutter)
if bar_index % 50 == 0 and inTrade and barCount <= max_bars  // Adjust label frequency for performance
    label.new(bar_index + 1, entryPrice, text="Entry: " + str.tostring(entryPrice, "#.##"), style=label.style_label_left, color=color.green, textcolor=color.white, size=size.small)
    label.new(bar_index + 1, stopLoss, text="Stop Loss: " + str.tostring(stopLoss, "#.##"), style=label.style_label_left, color=color.red, textcolor=color.white, size=size.small)
    label.new(bar_index + 1, targetPrice, text="Target: " + str.tostring(targetPrice, "#.##"), style=label.style_label_left, color=color.blue, textcolor=color.white, size=size.small)

```

> Detail

https://www.fmz.com/strategy/482457

> Last Modified

2025-02-18 15:11:28
