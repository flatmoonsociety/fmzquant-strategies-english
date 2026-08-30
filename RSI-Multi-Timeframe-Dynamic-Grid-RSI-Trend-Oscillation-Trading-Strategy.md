
> Name

Multi-Timeframe-Dynamic-Grid-RSI-Trend-Oscillation-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/16d612cc8d52842ebe4.png)

[trans]
#### Overview
This strategy is a composite strategy that combines the multi-time period RSI indicator and the dynamic grid trading system. It identifies market overbought and oversold conditions by analyzing the RSI indicator values ​​in three different time periods, and uses a dynamic grid system based on ATR for position management. The strategy also includes risk control mechanisms such as daily take-profit and maximum drawdown protection, which can effectively balance returns and risks.
#### Strategy Principle
The core logic of the strategy includes the following key parts:
1. Multi-time period analysis - Simultaneously monitor the RSI indicators of the current period, 60 minutes and 240 minutes. The transaction will only be triggered when overbought or oversold signals appear in all three periods.
2. Dynamic grid system - Use ATR as the volatility reference to dynamically calculate the grid spacing. When the price moves in an unfavorable direction, increase the position according to the set multiplier factor.
3. Position management - Based on 1% of the account equity as the basic position, and control the magnitude of the grid's position increase through the lot_multiplier parameter.
4. Risk control - including daily take-profit target, maximum drawdown protection of 2% of account equity, and reverse signal closing mechanism.
#### Strategic Advantages
1. Multi-dimensional signal confirmation - By analyzing the RSI indicator of multiple time periods, false signals can be effectively reduced.
2. Flexible position management - the dynamic grid system can adaptively adjust the grid spacing according to market fluctuations.
3. Complete risk control - daily take-profit and maximum drawdown protection mechanisms effectively control risks.
4. Highly customizable - Provides multiple adjustable parameters to facilitate optimization of strategies according to different market environments.
#### Strategy Risk
1. Trend risk - In strong trending markets, grid strategies may face sustained losses. It is recommended to add a trend filter.
2. Fund management risk - Multiple grids may lead to overuse of funds. It is recommended to strictly control the maximum number of grid layers.
3. Parameter sensitivity - Strategy performance is more sensitive to parameter settings. Adequate parameter optimization testing is recommended.
#### Strategy optimization direction
1. Trend identification enhancement - trend indicators such as moving averages can be added as filters.
2. Dynamic parameter adjustment - Automatically adjust RSI thresholds and grid parameters based on market volatility.
3. Stop loss optimization - independent stop loss levels can be set for each grid position.
4. Time filtering - Add trading time filtering to avoid low liquidity periods.
#### Summary
This strategy creates a balanced trading plan by combining multi-time period RSI analysis and a dynamic grid trading system. The complete risk control mechanism and flexible parameter settings make it suitable for different market environments. Through the suggested optimization direction, the stability and profitability of the strategy can be further improved.
|| 

#### Overview
This strategy is a sophisticated trading system that combines multi-timeframe RSI analysis with a dynamic grid trading system. It identifies market overbought and oversold conditions by analyzing RSI values across three different timeframes while using an ATR-based dynamic grid system for position management. The strategy also incorporates daily profit targets and maximum drawdown protection mechanisms to effectively balance returns and risks.

#### Strategy Principles
The core logic includes several key components:
1. Multi-timeframe Analysis - Monitors RSI indicators across current, 60-minute, and 240-minute timeframes, triggering trades only when all three periods show overbought or oversold signals.
2. Dynamic Grid System - Uses ATR as volatility reference to dynamically calculate grid spacing. Increases position size with a multiplier factor when price moves against the position.
3. Position Management - Uses 1% of account equity as base position size, controlled by lot_multiplier parameter for grid scaling.
4. Risk Control - Includes daily profit target, 2% account equity maximum drawdown protection, and reverse signal closure mechanism.

#### Strategy Advantages
1. Multi-dimensional Signal Confirmation - Reduces false signals through analysis of multiple timeframe RSI indicators.
2. Flexible Position Management - Dynamic grid system adapts to market volatility.
3. Comprehensive Risk Control - Daily profit target and maximum drawdown protection effectively manage risk.
4. Highly Customizable - Multiple adjustable parameters for different market environments.

#### Strategy Risks
1. Trend Risk - Grid strategy may face continuous losses in strong trend markets. Consider adding trend filters.
2. Capital Management Risk - Multiple grids may lead to excessive capital usage. Strictly control maximum grid levels.
3. Parameter Sensitivity - Strategy performance is sensitive to parameter settings. Thorough parameter optimization testing recommended.

#### Strategy Optimization Directions
1. Trend Recognition Enhancement - Add moving averages or other trend indicators as filters.
2. Dynamic Parameter Adjustment - Automatically adjust RSI thresholds and grid parameters based on market volatility.
3. Stop Loss Optimization - Implement individual stop loss levels for each grid position.
4. Time Filtering - Add trading time filters to avoid low liquidity periods.

#### Summary
This strategy creates a balanced trading approach by combining multi-timeframe RSI analysis with a dynamic grid trading system. Its comprehensive risk control mechanisms and flexible parameter settings make it suitable for various market environments. The strategy's stability and profitability can be further enhanced through the suggested optimization directions.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-10 00:00:00
end: 2025-02-08 08:00:00
period: 3h
basePeriod: 3h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Multi-Timeframe RSI Grid Strategy with Arrows", overlay=true)

// Input parameters
rsi_length = input.int(14, "RSI Length")
oversold = input.int(30, "Oversold Level")
overbought = input.int(70, "Overbought Level")
higher_tf1 = input.string("60", "Higher Timeframe 1")
higher_tf2 = input.string("240", "Higher Timeframe 2")
grid_factor = input.float(1.2, "Grid Multiplication Factor", step=0.1)
lot_multiplier = input.float(1.5, "Lot Multiplication Factor", step=0.1)
max_grid = input.int(5, "Maximum Grid Levels")
daily_target = input.float(4.0, "Daily Profit Target (%)", step=0.5)
atr_length = input.int(14, "ATR Length")

// Calculate RSI values
current_rsi = ta.rsi(close, rsi_length)
higher_tf1_rsi = request.security(syminfo.tickerid, higher_tf1, ta.rsi(close, rsi_length))
higher_tf2_rsi = request.security(syminfo.tickerid, higher_tf2, ta.rsi(close, rsi_length))

// Grid system variables
var int grid_level = 0
var float last_entry_price = na
var float base_size = strategy.equity * 0.01 / close
var float daily_profit_target = strategy.equity * (daily_target / 100)
var bool target_reached = false

// ATR for grid spacing
atr = ta.atr(atr_length)
grid_space = atr * grid_factor

// Daily reset
new_day = ta.change(time("D"))
if new_day
    daily_profit_target := strategy.equity * (daily_target / 100)
    target_reached := false
    grid_level := 0
    last_entry_price := na

// Trading conditions
buy_condition = current_rsi < oversold and higher_tf1_rsi < oversold and higher_tf2_rsi < oversold
sell_condition = current_rsi > overbought and higher_tf1_rsi > overbought and higher_tf2_rsi > overbought

// Reverse signal detection
reverse_long_to_short = sell_condition and strategy.position_size > 0
reverse_short_to_long = buy_condition and strategy.position_size < 0

// Close all trades on reverse signals
if reverse_long_to_short or reverse_short_to_long
    strategy.close_all()
    grid_level := 0
    last_entry_price := na

// Grid management logic
if strategy.position_size == 0
    grid_level := 0
    last_entry_price := na

if strategy.position_size > 0 and not reverse_long_to_short
    if close < last_entry_price - grid_space and grid_level < max_grid and not target_reached
        strategy.entry("Long Grid " + str.tostring(grid_level), strategy.long, qty=base_size * math.pow(lot_multiplier, grid_level))
        grid_level += 1
        last_entry_price := close

if strategy.position_size < 0 and not reverse_short_to_long
    if close > last_entry_price + grid_space and grid_level < max_grid and not target_reached
        strategy.entry("Short Grid " + str.tostring(grid_level), strategy.short, qty=base_size * math.pow(lot_multiplier, grid_level))
        grid_level += 1
        last_entry_price := close

// Initial entry
if buy_condition and strategy.position_size == 0 and not target_reached
    strategy.entry("Long", strategy.long, qty=base_size)
    grid_level := 1
    last_entry_price := close

if sell_condition and strategy.position_size == 0 and not target_reached
    strategy.entry("Short", strategy.short, qty=base_size)
    grid_level := 1
    last_entry_price := close

// Profit target check
current_profit = strategy.netprofit + strategy.openprofit
if current_profit >= daily_profit_target and not target_reached
    strategy.close_all()
    target_reached := true

// Drawdown protection
if strategy.openprofit < -(0.02 * strategy.equity)  // 2% drawdown protection
    strategy.close_all()
    grid_level := 0
    last_entry_price := na

// Plot Buy and Sell Arrows
plotshape(series=buy_condition and strategy.position_size == 0, title="Buy Signal", location=location.belowbar, color=color.green, style=shape.labelup, text="BUY", size=size.small)
plotshape(series=sell_condition and strategy.position_size == 0, title="Sell Signal", location=location.abovebar, color=color.red, style=shape.labeldown, text="SELL", size=size.small)

// Plotting RSI
plot(current_rsi, "Current RSI", color=color.blue)
plot(higher_tf1_rsi, "HTF1 RSI", color=color.red)
plot(higher_tf2_rsi, "HTF2 RSI", color=color.green)
hline(oversold, "Oversold", color=color.gray)
hline(overbought, "Overbought", color=color.gray)
```

> Detail

https://www.fmz.com/strategy/481371

> Last Modified

2025-02-10 15:19:45
