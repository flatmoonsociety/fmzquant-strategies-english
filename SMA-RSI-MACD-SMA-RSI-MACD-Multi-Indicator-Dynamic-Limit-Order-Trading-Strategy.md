
> Name

SMA-RSI-MACD multi-indicator combination dynamic limit trading strategy-SMA-RSI-MACD-Multi-Indicator-Dynamic-Limit-Order-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/e0d84f565484ad917c4e41450b43f9445fb7f6aac5e074f93d66da59c57edcbd.png)

[trans]
#### Overview
This strategy is a trading system that combines multiple technical indicators. It is mainly based on the triple signal confirmation of EMA moving average crossover, RSI oversold and MACD golden cross to open positions, and manages risks through dynamic limit order entry and multiple exit mechanisms. The strategy uses the 9-period and 21-period exponential moving averages (EMA) as the main trend indicator, combines the relative strength index (RSI) and the moving average convergence divergence indicator (MACD) to filter trading signals, and controls risks by setting the limit order distance and fixed take-profit and stop-loss points.
#### Strategy Principle
The core trading logic of the strategy includes the following key parts:
1. The entry signal is triggered when the 9-period EMA crosses the 21-period EMA.
2. Set the entry price at a specified number of points below the 9-period EMA.
3. Transaction confirmation must meet both the RSI below the set threshold and the MACD golden cross.
4. Exit signals include MACD dead cross, fixed take-profit and stop-loss points, and closing forced closing.
5. Trading hours are limited to after 9:30 am and before 3:10 pm
The strategy adopts the entry method of limit order, which can open a position at a better price position, and improve the accuracy of transactions through the cooperation of multiple technical indicators.
#### Strategic Advantages
1. Multiple signal confirmation mechanism improves the reliability of transactions
2. Limit order entry can get a better transaction price
3. Fixed take-profit and stop-loss points facilitate risk control
4. Forced liquidation at closing to avoid overnight risks
5. Trading time limits avoid opening fluctuations
6. EMA indicator responds faster to trends
7. The cooperation of RSI and MACD can filter out false signals
#### Strategy Risk
1. Multiple signal confirmations may result in missing some trading opportunities
2. Limit orders may not be filled due to rapid price increases
3. Fixed point stop loss may result in larger losses during periods of high volatility.
4. The MACD signal may lag
5. The strategy does not consider the impact of changes in market volatility
6. Parameter optimization may involve the risk of overfitting
#### Strategy optimization direction
1. Introduce adaptive stop-loss and take-profit points and dynamically adjust them according to market volatility
2. Add trading volume indicators as auxiliary confirmation signals
3. Consider adding a trend strength filter
4. Optimize the calculation method of limit order distance and consider using ATR dynamic adjustment
5. Add market sentiment indicators to filter out adverse market conditions
6. Add a position management mechanism to adjust the opening amount according to signal strength
#### Summary
This is a multi-indicator trading strategy with a complete structure and clear logic, which uses the moving average system to identify trends, RSI and MACD to filter signals, limit orders and multiple stop-loss mechanisms to control risks. The advantages of the strategy are high signal reliability and perfect risk control, but there are also problems such as signal lag and parameter optimization. By introducing dynamic parameter adjustment and adding auxiliary indicators, the strategy still has greater room for optimization. Suitable for prudent investors in market environments with clear trends.
|| 

#### Overview
This strategy is a multi-technical indicator trading system that primarily uses EMA crossover, RSI oversold conditions, and MACD golden cross for trade confirmation. It employs dynamic limit orders for entry and multiple exit mechanisms for risk management. The strategy uses 9-period and 21-period Exponential Moving Averages (EMA) as primary trend indicators, combined with Relative Strength Index (RSI) and Moving Average Convergence Divergence (MACD) to filter trading signals.

#### Strategy Principles
The core trading logic includes the following key components:
1. Entry signals are triggered when 9-period EMA crosses above 21-period EMA
2. Entry price is set as a limit order below the 9-period EMA at a specified offset
3. Trade confirmation requires RSI below threshold and MACD golden cross
4. Exit signals include MACD death cross, fixed profit/loss points, and forced closing at market end
5. Trading time is restricted between 9:30 AM and 3:10 PM

The strategy uses limit orders for entry to achieve better entry prices and combines multiple technical indicators to improve trading accuracy.

#### Strategy Advantages
1. Multiple signal confirmation mechanism improves trade reliability
2. Limit order entries provide better execution prices
3. Fixed profit/loss points facilitate risk control
4. Forced closing at market end eliminates overnight risk
5. Trading time restrictions avoid opening volatility
6. EMA indicators provide faster trend response
7. RSI and MACD combination helps filter false signals

#### Strategy Risks
1. Multiple signal confirmation may cause missed opportunities
2. Limit orders might not execute in rapid price movements
3. Fixed point stops may result in larger losses during high volatility
4. MACD signals may lag behind price action
5. Strategy doesn't account for changes in market volatility
6. Parameter optimization may lead to overfitting

#### Strategy Optimization Directions
1. Introduce adaptive stop-loss and take-profit points based on market volatility
2. Add volume indicators as additional confirmation signals
3. Consider adding trend strength filters
4. Optimize limit order offset calculation using ATR
5. Include market sentiment indicators to filter unfavorable conditions
6. Add position sizing mechanism based on signal strength

#### Summary
This is a well-structured multi-indicator trading strategy that identifies trends using moving averages, filters signals with RSI and MACD, and controls risk through limit orders and multiple stop mechanisms. The strategy's strengths lie in its signal reliability and comprehensive risk control, though it faces challenges with signal lag and parameter optimization. There is significant room for improvement through dynamic parameter adjustment and additional auxiliary indicators. It is suitable for conservative investors in trending market conditions.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-12-09 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("SMA 9 & 21 with RSI and MACD Buy Strategy", overlay=true)

// Inputs for Simple Moving Averages
sma_short = ta.ema(close, 9)
sma_long = ta.ema(close, 21)

// Plotting SMA
plot(sma_short, color=color.green, title="SMA 9")
plot(sma_long, color=color.red, title="SMA 21")

// RSI Calculation
rsi_length = input.int(14, title="RSI Length")
rsi_threshold = input.int(70, title="RSI Threshold")
rsi = ta.rsi(close, rsi_length)

// MACD Calculation
macd_fast = input.int(8, title="MACD Fast Length")
macd_slow = input.int(18, title="MACD Slow Length")
macd_signal = input.int(6, title="MACD Signal Length")
[macd_line, signal_line, _] = ta.macd(close, macd_fast, macd_slow, macd_signal)

// Inputs for Limit Order Offset
limit_offset = input.int(50, title="Limit Order Offset", minval=1)  // 50 points below 9 EMA

// User input for specific date
simulationStartDate = input(timestamp("2024-12-01 00:00"), title="Simulation Start Date", group = "Simulation Dates")
simulationEndDate = input(timestamp("2024-12-30 00:00"), title="Simulation End Date", group = "Simulation Dates")

// Declare limit_price as float
var float limit_price = na

// Calculate Limit Order Price
if (sma_short[1] < sma_long[1] and sma_short > sma_long)  // 9 EMA crosses above 21 EMA
    limit_price := sma_short - limit_offset

// Buy Signal Condition (only on the specified date)
buy_condition = not na(limit_price) and rsi < rsi_threshold and ta.crossover(macd_line, signal_line) 

// Sell Signal Condition (MACD crossover down)
sell_condition = ta.crossunder(macd_line, signal_line)

// Track Entry Price for Point-Based Exit
var float entry_price = na

if (buy_condition )
    strategy.order("Buy", strategy.long, comment="Limit Order at 9 EMA - Offset", limit=limit_price)
    label.new(bar_index, limit_price, "Limit Buy", style=label.style_label_up, color=color.green, textcolor=color.white)
    entry_price := limit_price  // Set entry price

// Exit Conditions
exit_by_macd = sell_condition
exit_by_points = not na(entry_price) and ((close >= entry_price + 12) or (close <= entry_price - 12))  // Adjust as per exit points

// Exit all positions at the end of the day
if hour == 15 and minute > 10 and strategy.position_size > 0
    strategy.close_all()  // Close all positions at the end of the day
    strategy.cancel_all()  

// Exit based on sell signal or point movement
if (exit_by_macd or exit_by_points  and strategy.position_size > 0 )
    strategy.close("Buy")
    label.new(bar_index, close, "Close", style=label.style_label_down, color=color.red, textcolor=color.white)

 
```

> Detail

https://www.fmz.com/strategy/474678

> Last Modified

2024-12-11 15:15:49
