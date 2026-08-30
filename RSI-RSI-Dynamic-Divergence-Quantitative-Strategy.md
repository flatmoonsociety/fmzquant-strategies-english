
> Name

RSI dynamic divergence quantification strategy-RSI-Dynamic-Divergence-Quantitative-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d8efd98d034d6cdac860.png)
![IMG](https://www.fmz.com/upload/asset/2d7f2223dabae5f1bed1a.png)


[trans]
#### Overview
The RSI Double Pivot Divergence Quantitative Strategy is an advanced trading strategy that identifies potential reversal opportunities by detecting regular bullish and bearish divergences between price action and the Relative Strength Index (RSI). The strategy uses an automated pivot point detection algorithm combined with two different stop-loss/take-profit management methods to automatically open positions when divergence signals are confirmed. The core of the strategy lies in verifying the divergence between price and RSI indicators through precise mathematical calculations, and using a dynamic risk management mechanism to ensure that each transaction follows the preset risk-reward ratio.
#### Strategy Principles
1. RSI calculation module: Use the Wilder smoothing method to calculate the 14-period (adjustable) RSI value, using the closing price as the default input source (configurable).  
2. Pivot point detection:
   - Use a sliding window of 5 periods (adjustable) on the left and right to detect the local highs and lows of the RSI indicator
   - Use the ta.barssince function to ensure that the pivot points are separated by 5-60 K lines (adjustable range)
3. Departure from confirmation logic:
   - Bullish Divergence: Price makes new lows while RSI forms higher lows
   - Bearish divergence: Price makes new highs while RSI forms lower highs
4. Transaction execution system:
   - Adopt a dual-mode stop loss mechanism: based on the last 20 periods (adjustable) swing point or ATR fluctuation range
   - Dynamic take-profit calculation: multiply the risk amount by the preset reward-risk ratio (default 2:1)
5. Visualization system: Mark all valid divergence signals on the chart, and display the stop loss (red) and take profit (green) horizontal lines of the current position in real time.
#### Advantage Analysis
1. Multi-dimensional verification mechanism: It requires that price and RSI must meet specific forms at the same time, and the time interval must be within a preset range, greatly reducing the probability of false signals.  
2. Adaptive risk management:
   - The swing point model is suitable for trending markets and can effectively capture the swing market
   - ATR mode is suitable for volatile markets and automatically adjusts the stop loss range according to volatility
3. Parameters are highly configurable: all key parameters (RSI period, pivot detection range, risk-reward ratio, etc.) can be adjusted according to market characteristics.  
4. Scientific fund management: The default position ratio is 10% to prevent excessive risk exposure in a single transaction.  
5. Real-time visual feedback: Provide intuitive trading decision support through chart markers and dynamic stop loss/take profit lines.
#### Risk Analysis
1. Lagging risk: As a lagging indicator, RSI may produce delayed signals in violent unilateral market conditions. Mitigation options: Incorporate a trend filter or shorten the RSI period.  
2. Risk of volatile market: Continuous false signals may occur when there is no clear trend. Mitigation solution: Enable ATR mode and increase the multiplier, or attach a volatility filter.  
3. Risk of parameter overfitting: A specific parameter combination may perform well in historical data but fail in real terms. Mitigation plan: Conduct multi-cycle and multi-variety stress testing.  
4. Extreme market risk: Gap may cause stop loss to be invalid. Mitigation options: Avoid trading around major economic events, or use options to hedge.  
5. Time frame dependence: The performance of different time periods varies greatly. Mitigation plan: Perform adequate backtest optimization in the target time frame.
#### Optimization direction
1. Composite indicator verification: Add MACD or trading volume indicators as secondary confirmation to improve signal quality.  
2. Dynamic parameter adjustment: Automatically adjust the RSI cycle and ATR multiplier according to market volatility.  
3. Machine learning optimization: Use genetic algorithm to optimize key parameter combinations.  
4. Multi-time frame analysis: Introduce trend direction filtering of higher time frames.  
5. Dynamic position management: adjust position size according to volatility to achieve risk balance.  
6. Event filter: Integrate economic calendar data to avoid transactions before and after the release of important data.
#### Summary
The RSI Double Pivot Divergence Quantitative Strategy provides a structured reversal trading method through systematic divergence identification and strict risk management. Its core value lies in transforming traditional technical analysis concepts into quantifiable trading rules and adapting to different market environments through dual-mode stop-loss mechanisms. Three key elements are required for a strategy to perform well: proper parameter optimization, tight risk control, and consistent execution discipline. This strategy is particularly suitable for market environments with a certain degree of volatility but not extreme trends. It is an excellent template for intermediate traders to transition to quantitative trading.
||  

#### Overview  
The RSI Dual-Pivot Divergence Quantification Strategy is an advanced trading methodology that identifies potential reversal opportunities by detecting regular bullish and bearish divergences between price action and the Relative Strength Index (RSI). This strategy employs an automated pivot detection algorithm combined with two distinct stop-loss/take-profit management approaches to automatically establish positions when divergence signals are confirmed. The core innovation lies in its precise mathematical validation of price-RSI divergence phenomena and dynamic risk management mechanisms that ensure each trade adheres to predetermined risk-reward ratios.  

#### Strategy Logic  
1. RSI Calculation Module: Utilizes Wilder's smoothing method to compute 14-period (adjustable) RSI values with close price as default input (configurable).  
2. Pivot Detection:  
   - Employs sliding windows of 5 periods (adjustable) on both sides to identify local RSI highs and lows  
   - Uses ta.barssince function to ensure 5-60 bar intervals (adjustable range) between pivots  
3. Divergence Confirmation:  
   - Bullish divergence: Price makes lower low while RSI forms higher low  
   - Bearish divergence: Price makes higher high while RSI forms lower high  
4. Trade Execution System:  
   - Dual-mode stop-loss: Based on recent 20-period (adjustable) swing points or ATR volatility  
   - Dynamic take-profit: Calculated as risk amount multiplied by preset reward-risk ratio (default 2:1)  
5. Visualization System: Marks all valid divergence signals on chart and displays real-time stop-loss (red) and take-profit (green) levels for open positions.  

#### Advantages  
1. Multi-dimensional Validation: Requires both price and RSI to meet specific patterns within preset time ranges, significantly reducing false signals.  
2. Adaptive Risk Management:  
   - Swing mode suits trending markets for capturing wave movements  
   - ATR mode adapts to ranging markets with volatility-based stops  
3. High Customizability: All critical parameters (RSI period, pivot range, risk-reward ratio etc.) adjustable for market conditions.  
4. Scientific Position Sizing: Default 10% capital allocation prevents overexposure in single trades.  
5. Visual Feedback: Real-time chart markings and dynamic stop/take-profit lines provide intuitive decision support.  

#### Risks  
1. Lag Risk: RSI as lagging indicator may generate delayed signals during strong trends. Mitigation: Add trend filters or shorten RSI period.  
2. Whipsaw Risk: May produce consecutive false signals in choppy markets. Mitigation: Use ATR mode with higher multipliers or add volatility filters.  
3. Overfitting Risk: Parameter sets may perform well historically but fail live. Mitigation: Conduct multi-period multi-asset stress tests.  
4. Gap Risk: Price gaps may bypass stops. Mitigation: Avoid trading around major economic events or use options hedging.  
5. Timeframe Dependency: Performance varies across timeframes. Mitigation: Thorough backtesting on target timeframe.  

#### Optimization Directions  
1. Composite Verification: Add MACD or volume indicators for secondary confirmation.  
2. Dynamic Parameters: Auto-adjust RSI period and ATR multiplier based on market volatility.  
3. Machine Learning: Apply genetic algorithms to optimize parameter combinations.  
4. Multi-Timeframe Analysis: Incorporate higher timeframe trend filters.  
5. Dynamic Position Sizing: Adjust trade size based on volatility for risk parity.  
6. Event Filters: Integrate economic calendar to avoid trading around major news.  

#### Conclusion  
The RSI Dual-Pivot Divergence Quantification Strategy provides a structured approach to reversal trading through systematic divergence identification and rigorous risk management. Its core value lies in transforming traditional technical analysis concepts into quantifiable trading rules with dual-mode stop mechanisms adaptable to varying market conditions. Strategy excellence requires three key elements: appropriate parameter optimization, strict risk control, and consistent execution discipline. Particularly effective in moderately volatile, non-extreme trending environments, this strategy serves as an excellent template for intermediate traders transitioning to quantitative trading methodologies.  
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-04-25 00:00:00
end: 2025-04-23 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"DOGE_USDT"}]
*/

//@version=6
strategy("RSI Divergence Strategy - AliferCrypto", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=10)

// === RSI Settings ===
rsiLength      = input.int(14, minval=1, title="RSI Length", group="RSI Settings", tooltip="Number of periods for RSI calculation")
rsiSource      = input.source(close, title="RSI Source", group="RSI Settings", tooltip="Price source used for RSI calculation")

// === Divergence Settings ===
lookLeft       = input.int(5, minval=1, title="Pivot Lookback Left", group="Divergence Settings", tooltip="Bars to the left for pivot detection")
lookRight      = input.int(5, minval=1, title="Pivot Lookback Right", group="Divergence Settings", tooltip="Bars to the right for pivot detection")
rangeLower     = input.int(5, minval=1, title="Min Bars Between Pivots", group="Divergence Settings", tooltip="Minimum bars between pivots to validate divergence")
rangeUpper     = input.int(60, minval=1, title="Max Bars Between Pivots", group="Divergence Settings", tooltip="Maximum bars between pivots to validate divergence")

// === SL/TP Method ===
method         = input.string("Swing", title="SL/TP Method", options=["Swing", "ATR"], group="SL/TP Settings", tooltip="Choose between swing-based or ATR-based stop and target")

// === Swing Settings ===
swingLook      = input.int(20, minval=1, title="Swing Lookback (bars)", group="Swing Settings", tooltip="Bars to look back for swing high/low")
swingMarginPct = input.float(1.0, minval=0.0, title="Swing Margin (%)", group="Swing Settings", tooltip="Margin around swing levels as percentage of price")
rrSwing        = input.float(2.0, title="R/R Ratio (Swing)", group="Swing Settings", tooltip="Risk/reward ratio when using swing-based method")

// === ATR Settings ===
atrLen         = input.int(14, minval=1, title="ATR Length", group="ATR Settings", tooltip="Number of periods for ATR calculation")
atrMult        = input.float(1.5, minval=0.1, title="ATR SL Multiplier", group="ATR Settings", tooltip="Multiplier for ATR-based stop loss calculation")
rrAtr          = input.float(2.0, title="R/R Ratio (ATR)", group="ATR Settings", tooltip="Risk/reward ratio when using ATR-based method")

// === RSI Calculation ===
_d    = ta.change(rsiSource)
up    = ta.rma(math.max(_d, 0), rsiLength)
down  = ta.rma(-math.min(_d, 0), rsiLength)
rsi   = down == 0 ? 100 : up == 0 ? 0 : 100 - (100 / (1 + up / down))

// === Divergence Detection ===
defPl      = not na(ta.pivotlow(rsi, lookLeft, lookRight))
defPh      = not na(ta.pivothigh(rsi, lookLeft, lookRight))
rsiAtRR   = rsi[lookRight]
barsPl    = ta.barssince(defPl)
barsPl1   = barsPl[1]
inRangePL = barsPl1 >= rangeLower and barsPl1 <= rangeUpper
barsPh    = ta.barssince(defPh)
barsPh1   = barsPh[1]
inRangePH = barsPh1 >= rangeLower and barsPh1 <= rangeUpper
prevPlRsi   = ta.valuewhen(defPl, rsiAtRR, 1)
prevPhRsi   = ta.valuewhen(defPh, rsiAtRR, 1)
prevPlPrice = ta.valuewhen(defPl, low[lookRight], 1)
prevPhPrice = ta.valuewhen(defPh, high[lookRight], 1)
bullCond    = defPl and low[lookRight] < prevPlPrice and rsiAtRR > prevPlRsi and inRangePL
bearCond    = defPh and high[lookRight] > prevPhPrice and rsiAtRR < prevPhRsi and inRangePH

plotshape(bullCond, title="Bullish Divergence", style=shape.triangleup, location=location.belowbar, color=color.green, size=size.tiny)
plotshape(bearCond, title="Bearish Divergence", style=shape.triangledown, location=location.abovebar, color=color.red, size=size.tiny)

// === Entries ===
if bullCond
    strategy.entry("Long", strategy.long)
if bearCond
    strategy.entry("Short", strategy.short)

// === Pre-calculate SL/TP components ===
swingLow    = ta.lowest(low, swingLook)
swingHigh   = ta.highest(high, swingLook)
atrValue    = ta.atr(atrLen)

// === SL/TP Calculation & Exits ===
var float slPrice = na
var float tpPrice = na
var float rr      = na

// Long exits
if strategy.position_size > 0
    entryPrice = strategy.position_avg_price
    if method == "Swing"
        slPrice := swingLow * (1 - swingMarginPct / 100)
        rr      := rrSwing
    else
        slPrice := entryPrice - atrValue * atrMult
        rr      := rrAtr
    risk     = entryPrice - slPrice
    tpPrice  := entryPrice + risk * rr
    strategy.exit("Exit Long", from_entry="Long", stop=slPrice, limit=tpPrice)

// Short exits
if strategy.position_size < 0
    entryPrice = strategy.position_avg_price
    if method == "Swing"
        slPrice := swingHigh * (1 + swingMarginPct / 100)
        rr      := rrSwing
    else
        slPrice := entryPrice + atrValue * atrMult
        rr      := rrAtr
    risk     = slPrice - entryPrice
    tpPrice  := entryPrice - risk * rr
    strategy.exit("Exit Short", from_entry="Short", stop=slPrice, limit=tpPrice)

// === Plot SL/TP Levels ===
plot(strategy.position_size != 0 ? slPrice : na, title="Stop Loss", style=plot.style_linebr, color=color.red)
plot(strategy.position_size != 0 ? tpPrice : na, title="Take Profit", style=plot.style_linebr, color=color.green)

// === Alerts ===
alertcondition(bullCond, title="Bull RSI Divergence", message="Bullish RSI divergence detected")
alertcondition(bearCond, title="Bear RSI Divergence", message="Bearish RSI divergence detected")
```

> Detail

https://www.fmz.com/strategy/492007

> Last Modified

2025-04-25 14:57:31
