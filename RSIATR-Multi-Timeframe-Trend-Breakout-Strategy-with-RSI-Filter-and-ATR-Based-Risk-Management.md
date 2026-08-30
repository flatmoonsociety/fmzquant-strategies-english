
> Name

Multi-Timeframe Trend Breakout Strategy-with-RSI-Filter-and-ATR-Based-Risk-Management
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d89859b64130b84ace89.png)
![IMG](https://www.fmz.com/upload/asset/2d8effa4a29888266ca3f.png)



[trans]
#### Overview
This strategy is a multi-timeframe strategy that combines trend following and breakout trading, using EMA crossover as a trend filter, RSI as a momentum confirmation indicator, and ATR for dynamic risk management. The strategy enables precise entry and exit signal management through a separate alert system and uses a percentage-based money management approach to control risk.
#### Strategy Principles
1. **Trend Determination**: Use the cross relationship between fast EMA (9) and slow EMA (21) to determine the market trend direction. When EMA9 crosses EMA21, it is determined to be an upward trend, and vice versa, it is a downward trend.  
2. **Momentum Confirmation**: Confirm the trend strength through the RSI indicator (period 14). Long trading requires RSI>50, and short trading requires RSI<50.  
3. **Breakthrough signal**: After the trend direction is confirmed, a trading signal is generated when the price breaks through the high and low points of the previous K line.  
4. **Risk Management**: Use ATR (period 14) to calculate the dynamic stop loss level, and the fixed risk ratio is 2% of the account equity. The take profit is set to 3 times the stop loss distance, and the trailing stop is activated after reaching 50% profit.  
5. **Position Calculation**: Dynamically calculate the position size based on the stop loss distance and risk ratio to ensure that the risk of each transaction is consistent.
#### Advantage Analysis
1. **Multi-factor verification**: Combines the confirmation of the three dimensions of trend, momentum and price action to improve signal quality.  
2. **Dynamic Risk Management**: ATR-based stop loss can adapt to changes in market volatility, and trailing stop loss protects floating profits.  
3. **Scientific Fund Management**: Fixed percentage risk control to avoid excessive trading, and position calculation accurately matches risk preferences.  
4. **Clear visual signals**: Visually display trading signals through the plotshape function for easy monitoring.  
5. **Separate Alert System**: Independent opening/closing alerts facilitate automated transaction docking.
#### Risk Analysis
1. **Concussive market risk**: Continuous false breakthrough signals may occur in consolidation markets where the trend is not obvious. The solution is to add a trend strength filter such as ADX.  
2. **Parameter Sensitivity Risk**: Fixed parameters may fail under different varieties or market environments. It is recommended to carry out parameter optimization or adaptive parameter settings.  
3. **Gap risk**: A price gap may lead to an expansion of slippage, and the actual stop-loss execution price is inconsistent with expectations. The solution is to reduce positions or suspend trading before important data is released.  
4. **Overfitting Risk**: Parameters optimized based on historical data may fail in the future, and sufficient forward testing should be performed.
#### Optimization direction
1. **Adaptive parameters**: Change fixed parameters to adaptive parameters based on volatility or market status, such as using ATR percentage to set the EMA period.  
2. **Composite Trend Filter**: Add trend confirmation in a higher time frame, for example, trade only if both daily trend and hourly signals are met.  
3. **Dynamic Take Profit**: Change the fixed TP ratio to a dynamic take profit based on support and resistance levels or Fibonacci extension levels.  
4. **Machine Learning Optimization**: Use reinforcement learning to dynamically adjust the RSI threshold and TP/SL ratio.  
5. **Event filtering**: Integrate economic calendar data to automatically adjust risk parameters or suspend trading before and after important events.
#### Summary
This is a rigorously structured trend following strategy that improves signal reliability through multiple technical indicator verifications and a scientific fund management system that effectively controls downside risks. The strategy is particularly suitable for market environments with clear trends and performs best on varieties with moderate volatility. By further optimizing the parameter adaptation mechanism and adding a market state recognition module, the robustness and adaptability of the strategy can be significantly improved.
||  

#### Overview  
This strategy combines trend-following and breakout trading across multiple timeframes, using EMA crossovers as trend filters, RSI for momentum confirmation, and ATR for dynamic risk management. It features a separated alert system for precise entry/exit signal management and employs percentage-based money management to control risk.  

#### Strategy Logic  
1. **Trend Identification**: Uses the crossover relationship between fast EMA(9) and slow EMA(21) to determine market trend direction.  
2. **Momentum Confirmation**: RSI indicator (period 14) confirms trend strength, requiring RSI>50 for long trades and RSI<50 for short trades.  
3. **Breakout Signals**: Generates trading signals when price breaks the previous bar's high/low points after trend confirmation.  
4. **Risk Management**: Uses ATR (period 14) to calculate dynamic stop-loss levels with fixed 2% account risk per trade. Take-profit is set at 3 times the stop-loss distance, with trailing stop activated after 50% profit.  
5. **Position Sizing**: Dynamically calculates position size based on stop-loss distance and risk percentage to ensure consistent risk exposure.  

#### Advantages  
1. **Multi-factor Verification**: Combines trend, momentum and price action confirmation for higher signal quality.  
2. **Dynamic Risk Management**: ATR-based stops adapt to market volatility changes, with trailing stops protecting floating profits.  
3. **Scientific Money Management**: Fixed-percentage risk control prevents overtrading, with precise position sizing.  
4. **Clear Visual Signals**: plotshape function provides intuitive visual cues for monitoring.  
5. **Separated Alert System**: Independent entry/exit alerts facilitate automated trading integration.  

#### Risks  
1. **Range-bound Market Risk**: May generate false breakout signals during trendless conditions. Solution: Add ADX filter.  
2. **Parameter Sensitivity**: Fixed parameters may fail in different instruments/market regimes. Solution: Parameter optimization or adaptive settings.  
3. **Gap Risk**: Price gaps may cause slippage. Solution: Reduce position before major news.  
4. **Overfitting Risk**: Historical optimization may not work forward. Solution: Robust out-of-sample testing.  

#### Optimization Directions  
1. **Adaptive Parameters**: Replace fixed parameters with volatility-based adaptive settings.  
2. **Composite Trend Filter**: Add higher timeframe trend confirmation.  
3. **Dynamic Take-profit**: Replace fixed TP ratio with support/resistance or Fibonacci extensions.  
4. **Machine Learning**: Use reinforcement learning to dynamically adjust RSI thresholds and TP/SL ratios.  
5. **Event Filtering**: Integrate economic calendar to adjust risk parameters around major events.  

#### Conclusion  
This is a well-structured trend-following strategy that improves signal reliability through multi-indicator confirmation and controls downside risk with scientific money management. It performs best in trending markets with moderate volatility. Further enhancements in parameter adaptation and market regime detection could significantly improve robustness and adaptability.  
[/trans]



> Source (PineScript)

``` pinescript
// @version=5
strategy("Trend Breakout Strategy with Separated Alerts", overlay=true, initial_capital=10, default_qty_type=strategy.percent_of_equity, default_qty_value=100)

// --- Parameters ---
var float risk_per_trade = 0.02 // 2% risk per trade
var int ema_fast = 9
var int ema_slow = 21
var int rsi_length = 14
var int atr_length = 14
var float atr_multiplier_sl = 2.0 // ATR multiplier for SL
var float tp_ratio = 3.0 // TP to SL ratio = 3:1
var float trail_trigger_ratio = 0.5 // Trailing stop triggers at 50% of TP

// --- Indicators ---
ema9 = ta.ema(close, ema_fast)
ema21 = ta.ema(close, ema_slow)
rsi = ta.rsi(close, rsi_length)
atr = ta.atr(atr_length)

// --- Trend Filter ---
bull_trend = ta.crossover(ema9, ema21) or (ema9 > ema21)
bear_trend = ta.crossunder(ema9, ema21) or (ema9 < ema21)

// --- Entry Conditions ---
long_entry = bull_trend and rsi > 50 and close > high[1]
short_entry = bear_trend and rsi < 50 and close < low[1]

// --- Position Size Calculation ---
equity = strategy.equity
stop_loss_distance = atr * atr_multiplier_sl
risk_amount = equity * risk_per_trade
position_size = risk_amount / stop_loss_distance

// --- SL and TP Levels ---
long_sl = close - stop_loss_distance
long_tp = close + stop_loss_distance * tp_ratio
short_sl = close + stop_loss_distance
short_tp = close - stop_loss_distance * tp_ratio

// --- Trailing Stop (activated after 50% of TP) ---
trail_points = atr * atr_multiplier_sl * tp_ratio * trail_trigger_ratio
trail_offset = atr * atr_multiplier_sl

// --- Entries ---
if long_entry
    strategy.entry("Long", strategy.long, qty=position_size)
    strategy.exit("Long Exit", "Long", stop=long_sl, limit=long_tp, trail_points=trail_points, trail_offset=trail_offset)

if short_entry
    strategy.entry("Short", strategy.short, qty=position_size)
    strategy.exit("Short Exit", "Short", stop=short_sl, limit=short_tp, trail_points=trail_points, trail_offset=trail_offset)

// --- Alert Conditions ---
var bool long_opened = false
var bool short_opened = false

// Track position opening
long_open_alert = long_entry and not long_opened
short_open_alert = short_entry and not short_opened

// Track position closing
long_close_alert = long_opened and strategy.position_size == 0
short_close_alert = short_opened and strategy.position_size == 0

// Update position states
if long_entry
    long_opened := true
if short_entry
    short_opened := true
if strategy.position_size == 0
    long_opened := false
    short_opened := false

// --- Alerts ---
alertcondition(long_open_alert, title="Open Long", message='{"action":"buy","symbol":"{{ticker}}","price":{{close}}}')
alertcondition(long_close_alert, title="Close Long", message='{"action":"close_long","symbol":"{{ticker}}","price":{{close}}}')
alertcondition(short_open_alert, title="Open Short", message='{"action":"sell","symbol":"{{ticker}}","price":{{close}}}')
alertcondition(short_close_alert, title="Close Short", message='{"action":"close_short","symbol":"{{ticker}}","price":{{close}}}')

// --- Visualization ---
plot(ema9, color=color.blue, title="EMA9")
plot(ema21, color=color.red, title="EMA21")
plotshape(long_open_alert, title="Long Entry", location=location.belowbar, color=color.green, style=shape.triangleup, size=size.small)
plotshape(short_open_alert, title="Short Entry", location=location.abovebar, color=color.red, style=shape.triangledown, size=size.small)

```

> Detail

https://www.fmz.com/strategy/491891

> Last Modified

2025-04-24 16:55:42
