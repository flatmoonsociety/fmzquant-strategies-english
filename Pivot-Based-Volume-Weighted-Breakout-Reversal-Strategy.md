
> Name

Pivot-Based-Volume-Weighted-Breakout-Reversal-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d87e45522d5ef9112c83.png)
![IMG](https://www.fmz.com/upload/asset/2d80d09add8daa10daa4e.png)




[trans]
#### Overview
This strategy combines support/resistance (S/R) breakouts/reversals, volume filtering, and an alert system to capture key turning points in the market. The strategy improves the reliability of trading signals by identifying price breakout or reversal signals and combining them with abnormal volume confirmations. The strategy uses a fixed stop loss of 2% and an adjustable take profit ratio (default 3%) to manage risk.
#### Strategy Principles
1. **Support/Resistance Identification**: Use the `ta.pivothigh()` and `ta.pivotlow()` functions to identify key price levels within a specified period (pivotLen). The signal is triggered when the price breaks through a resistance level (a break of 1%) or rebounds from a support level (a dip below and then back out).  
2. **Trading volume filter**: Calculate the SMA (volSmaLength period) of the trading volume. When the current trading volume exceeds the volMultiplier times of the SMA (default 1.5 times), it is considered a valid confirmation.  
3. **Long and short logic**:
   - **Bull condition**: The price breaks through the resistance zone (close > resZone*1.01) and is accompanied by high trading volume, or the price is close to the support zone (within ±1% range) and a "false break" occurs (low ≤ supZone but is recovered at the close) and the trading volume is enlarged.  
   - **Short conditions**: The price falls below the support zone (close < supZone*0.99) and is accompanied by high trading volume, or the price is close to the resistance zone (within ±1% range) and a "false breakthrough" occurs (high ≥ resZone but the closing price falls) and the trading volume is enlarged.  
4. **Risk Management**: Fixed 2% stop loss and adjustable take profit (default 3%) are implemented through `strategy.exit()`.
#### Advantage Analysis
1. **Multi-factor verification**: Combined with price structure (S/R), trading volume and market behavior (false breakthrough/false break), it significantly reduces the probability of false signals.  
2. **Dynamic Adaptation**: Automatically update support/resistance levels to adapt to market changes.  
3. **Strict risk control**: Fixed stop loss prevents excessive losses in a single transaction, and the take-profit ratio is adjustable to adapt to different volatile markets.  
4. **Strong visualization**: Support/resistance lines are drawn in real time, and trading signals are clearly marked.  
5. **Alert integration**: Can be connected to automated trading systems, suitable for different trading scenarios.
#### Risk Analysis
1. **Concussive market risk**: False breakthroughs are frequently triggered in a trendless market, resulting in multiple stop losses. Solution: Add trend filter indicators such as ADX or EMA.  
2. **Sensitive parameters**: pivotLen and volMultiplier need to be adjusted according to the market. Solution: Perform parameter optimization and Walk-Forward testing.  
3. **Volume Lag**: Abnormal volume may appear after a price move. Solution: Combine handicap data or shorten volSmaLength.  
4. **Gap risk**: A short opening may skip the stop loss level. Solution: Use limit orders or avoid periods of high volatility.
#### Optimization direction
1. **Trend filter**: Add ADX>25 condition or 200EMA direction filter to avoid counter-trend trading.  
2. **Dynamic Parameters**: Automatically adjust pivotLen and volMultiplier according to market volatility (such as ATR).  
3. **Graded take-profit**: Set two levels of take-profit (such as 2% to close half of the position and the remaining trailing stop-loss) to increase the profit-loss ratio.  
4. **Machine Learning Optimization**: Use historical data to train the model to optimize the volMultiplier and tpPerc parameters.  
5. **Cross-cycle verification**: Introduce S/R confirmation of a higher time frame to enhance signal quality.
#### Summary
This strategy designs a high-probability trading framework through triple verification (price position, trading volume, price action), which is especially suitable for capturing the early stage of trends. The core advantages lie in transparent logic and controllable risks, but attention should be paid to its limitations in a volatile market. Future optimization can focus on parameter adaptation and trend filtering to further improve stability.
||  

#### Overview  
This strategy combines support/resistance (S/R) breakout/reversal, volume filtering, and alert systems to capture key market turning points. It identifies price breakout/reversal signals validated by abnormal volume activity to improve reliability. The strategy employs a fixed 2% stop loss and adjustable take profit (default 3%) for risk management.  

#### Strategy Logic  
1. **S/R Identification**: Uses `ta.pivothigh()` and `ta.pivotlow()` to detect key price levels within a specified period (pivotLen). Signals trigger when price breaks resistance (upward >1%) or bounces from support (false breakdown recovery).  
2. **Volume Filter**: Calculates volume SMA (volSmaLength periods). A valid signal requires current volume exceeding SMA by volMultiplier (default 1.5x).  
3. **Long/Short Logic**:  
   - **Long Condition**: Price breaks resistance (close > resZone*1.01) with high volume, or shows false breakdown near support (±1% range) with volume confirmation.  
   - **Short Condition**: Price breaks support (close < supZone*0.99) with high volume, or shows false breakout near resistance (±1% range) with volume confirmation.  
4. **Risk Management**: Fixed 2% stop loss and adjustable take profit (default 3%) via `strategy.exit()`.  

#### Advantages  
1. **Multi-Factor Validation**: Combines price structure (S/R), volume, and market behavior (false breaks), significantly reducing false signals.  
2. **Dynamic Adaptation**: Auto-updates S/R levels to adapt to market changes.  
3. **Strict Risk Control**: Fixed stop loss prevents excessive losses; adjustable take profit suits varying market conditions.  
4. **High Visibility**: Real-time S/R plotting and clear signal labels.  
5. **Alert Integration**: Compatible with automated trading systems.  

#### Risks  
1. **Range-Bound Risk**: Frequent false breakouts in choppy markets. Solution: Add trend filters like ADX or EMA.  
2. **Parameter Sensitivity**: pivotLen and volMultiplier require market-specific tuning. Solution: Parameter optimization and Walk-Forward testing.  
3. **Volume Lag**: Abnormal volume may follow price moves. Solution: Incorporate order book data or reduce volSmaLength.  
4. **Gap Risk**: Opening gaps may skip stop levels. Solution: Use limit orders or avoid high-volatility sessions.  

#### Optimization Directions  
1. **Trend Filtering**: Add ADX>25 or 200EMA direction filters to avoid counter-trend trades.  
2. **Dynamic Parameters**: Auto-adjust pivotLen and volMultiplier based on volatility (e.g., ATR).  
3. **Scaled Take Profit**: Implement two-tier exits (e.g., close 50% at 2%, trail remainder).  
4. **Machine Learning**: Train models to optimize volMultiplier and tpPerc historically.  
5. **Multi-Timeframe Confirmation**: Validate signals with higher timeframe S/R levels.  

#### Conclusion  
This strategy establishes a high-probability framework through triple validation (price position, volume, price action), ideal for capturing early trend phases. Its transparency and controlled risk are key strengths, though range-bound performance requires caution. Future enhancements should focus on parameter self-adaptation and trend filtering for greater robustness.  
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-04-24 00:00:00
end: 2024-12-31 00:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"DOGE_USDT"}]
*/

//@version=5
strategy("S/R Breakout/Reversal + Volume + Alerts", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=100)

// === INPUTS ===
pivotLen       = input.int(10, "Pivot Lookback for S/R")
volSmaLength   = input.int(20, "Volume SMA Length")
volMultiplier  = input.float(1.5, "Volume Multiplier")
tpPerc         = input.float(3.0, "Take Profit %", step=0.1)
slPerc         = 2.0  // Stop Loss fixed at 2%

// === S/R ZONES ===
pivotHigh = ta.pivothigh(high, pivotLen, pivotLen)
pivotLow  = ta.pivotlow(low, pivotLen, pivotLen)

var float resZone = na
var float supZone = na
if not na(pivotHigh)
    resZone := pivotHigh
if not na(pivotLow)
    supZone := pivotLow

plot(supZone, title="Support", color=color.green, linewidth=2, style=plot.style_linebr)
plot(resZone, title="Resistance", color=color.red,   linewidth=2, style=plot.style_linebr)

// === VOLUME FILTER ===
volSma     = ta.sma(volume, volSmaLength)
highVolume = volume > volSma * volMultiplier

// === LONG LOGIC ===
priceAboveRes     = close > resZone * 1.01
nearSupport       = close >= supZone * 0.99 and close <= supZone * 1.01
rejectSupport     = low <= supZone and close > supZone
longBreakoutCond  = priceAboveRes and highVolume
longReversalCond  = nearSupport and rejectSupport and highVolume
longCondition     = longBreakoutCond or longReversalCond

// === SHORT LOGIC ===
priceBelowSup     = close < supZone * 0.99
nearResistance    = close >= resZone * 0.99 and close <= resZone * 1.01
rejectResistance  = high >= resZone and close < resZone
shortBreakoutCond = priceBelowSup and highVolume
shortReversalCond = nearResistance and rejectResistance and highVolume
shortCondition    = shortBreakoutCond or shortReversalCond

// === ENTRIES WITH LABELS ===
if (longCondition)
    strategy.entry("Long", strategy.long)
    label.new(bar_index, low * 0.995, "BUY", style=label.style_label_up, color=color.green, textcolor=color.white)

if (shortCondition)
    strategy.entry("Short", strategy.short)
    label.new(bar_index, high * 1.005, "SELL", style=label.style_label_down, color=color.red, textcolor=color.white)

// === TP/SL ===
longTP  = close * (1 + tpPerc / 100)
longSL  = close * (1 - slPerc / 100)
shortTP = close * (1 - tpPerc / 100)
shortSL = close * (1 + slPerc / 100)

strategy.exit("Long TP/SL",  from_entry="Long",  limit=longTP,  stop=longSL)
strategy.exit("Short TP/SL", from_entry="Short", limit=shortTP, stop=shortSL)

// === ALERT CONDITIONS ===
alertcondition(longCondition,  title="Buy Alert",  message="? BUY signal: S/R + Volume breakout/reversal")
alertcondition(shortCondition, title="Sell Alert", message="? SELL signal: S/R + Volume breakout/reversal")

```

> Detail

https://www.fmz.com/strategy/491895

> Last Modified

2025-04-24 17:08:39
