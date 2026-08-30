
> Name

ADX Trend Breakout Momentum Trading Strategy-ADX-Trend-Breakout-Momentum-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/ad55f971e73fad8e30.png)

[trans]
#### Overview
This is a quantitative trading strategy based on the Average Trend Index (ADX) and price breakouts. This strategy mainly monitors the value of the ADX indicator to determine the strength of the market trend, and combines price breakthrough signals to capture market momentum. Strategies are set up to run within specific trading hours, and manage risk through stop losses and daily trade limits.
#### Strategy Principle
The core logic of the strategy includes the following key elements:
1. ADX indicator monitoring: Use the ADX indicator to evaluate the strength of the market trend. When the ADX value is lower than 17.5, it indicates that the market may be about to form a new trend.
2. Price breakthrough judgment: The strategy will track the highest closing price in the past 34 periods and trigger a trading signal when the current price breaks through the resistance level.
3. Trading session management: The strategy only runs within the designated trading session (0730-1430) to avoid the risk of low liquidity periods.
4. Risk control mechanism:
   - Set a fixed USD stop loss to limit losses on a single trade
   - Limit to 3 trades per trading session
   - Automatic closing of all positions at the end of the trading session
#### Strategic Advantages
1. Trend catching ability: Through the combination of ADX indicator and price breakthrough, it can effectively identify the early stage of market trend.
2. Perfect risk management: including multi-level risk control measures, such as fixed stop loss, transaction limit and automatic closing mechanism.
3. High degree of automation: The strategy logic is clear and fully automated transactions are realized without manual intervention.
4. Strong adaptability: parameters can be adjusted according to different market conditions, such as stop loss amount, lookback period, etc.
#### Strategy Risk
1. False breakout risk: In a volatile market, false breakout may occur, leading to continuous stop losses.
2. Parameter dependence: The effect of the strategy depends heavily on the settings of the ADX threshold and lookback period.
3. Period restrictions: Trading only during specific periods may miss opportunities in other periods.
4. Stop Loss Settings: Fixed USD stops may not be flexible enough in different volatility environments.
#### Strategy optimization direction
1. Dynamic stop loss: It is recommended to change the fixed dollar stop loss to a dynamic stop loss based on ATR to adapt to different market fluctuation environments.
2. Market environment filtering: Add a volatility filter to adjust or suspend trading in high volatility environments.
3. Entry optimization: You can consider increasing trading volume confirmation to improve the reliability of breakthrough signals.
4. Dynamic parameter adjustment: realize the adaptive adjustment mechanism of ADX threshold and lookback period.
#### Summary
This is a trend following strategy with complete structure and clear logic. By combining the ADX indicator with price breakouts, capture market trend opportunities within an effective risk management framework. Although there is some room for optimization, the basic framework of the strategy is robust and suitable as a basic component of a quantitative trading system. It is recommended that traders conduct sufficient backtesting and parameter optimization before placing a real offer, and make targeted improvements based on specific market conditions.
|| 

#### Overview
This is a quantitative trading strategy based on the Average Directional Index (ADX) and price breakouts. The strategy primarily monitors ADX indicator values to assess market trend strength and combines price breakout signals to capture market momentum. The strategy operates within specific trading sessions and implements risk management through stop-loss and daily trade limits.

#### Strategy Principles
The core logic includes the following key elements:
1. ADX Monitoring: Uses the ADX indicator to evaluate trend strength, with ADX values below 17.5 indicating potential new trend formation.
2. Price Breakout Detection: Tracks the highest closing price over the past 34 periods, triggering trade signals when current price breaks above this resistance.
3. Session Management: Operates only during specified trading hours (0730-1430) to avoid low liquidity periods.
4. Risk Control Mechanisms:
   - Fixed dollar stop-loss to limit single trade losses
   - Maximum of 3 trades per session limit
   - Automatic position closure at session end

#### Strategy Advantages
1. Trend Capture Capability: Effectively identifies early trend stages through ADX indicator and price breakout combination.
2. Comprehensive Risk Management: Multiple risk control measures including fixed stop-loss, trade limits, and auto-close mechanism.
3. High Automation: Clear strategy logic enables fully automated trading without manual intervention.
4. Strong Adaptability: Parameters can be adjusted for different market conditions.

#### Strategy Risks
1. False Breakout Risk: May experience consecutive stops in ranging markets.
2. Parameter Dependency: Strategy effectiveness heavily relies on ADX threshold and lookback period settings.
3. Time Restrictions: Trading only during specific sessions may miss opportunities.
4. Stop-Loss Configuration: Fixed dollar stops may lack flexibility in different volatility environments.

#### Optimization Directions
1. Dynamic Stop-Loss: Recommend implementing ATR-based dynamic stops for different market volatility conditions.
2. Market Environment Filter: Add volatility filters to adjust or pause trading in high volatility environments.
3. Entry Optimization: Consider adding volume confirmation to improve breakout signal reliability.
4. Dynamic Parameter Adjustment: Implement adaptive adjustment mechanisms for ADX thresholds and lookback periods.

#### Summary
This is a well-structured trend-following strategy with clear logic. It captures market trends by combining ADX indicators with price breakouts under an effective risk management framework. While there is room for optimization, the strategy's foundation is robust and suitable as a basic component of a quantitative trading system. Traders are advised to conduct thorough backtesting and parameter optimization before live trading, and make specific improvements based on market conditions.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-11-27 00:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © HuntGatherTrade
// ========================
// NQ 30 minute, ES 30 minute

//@version=5
strategy("ADX Breakout", overlay=false, initial_capital=25000, default_qty_value=1)

// ===============================
// Input parameters
// ===============================
stopLoss = input(1000.0, title="Stop Loss ($)", group="Exits")
session = input("0730-1430:1234567", group="Trade Session")
highestLB = input(34, title="Highest lookback window", group="Indicator values")

// ===============================
// Trade Session Handling
// ===============================
t = time(timeframe.period, session)

// Reset numTrades at the start of each session
var int numTrades = 0
is_new_session = ta.change(time("D")) != 0
if is_new_session
    numTrades := 0

// ===============================
// Entry Conditions
// ===============================
[plusDI, minusDI, adxValue] = ta.dmi(50, 14)
entryCondition = (close >= ta.highest(close, highestLB)[1]) and (adxValue < 17.5) and (strategy.position_size == 0) and (numTrades < 3) and not na(t)

// ===============================
// 7. Execute Entry
// ===============================
var float stopPricePlot = na

if entryCondition
    entryPrice = close + syminfo.mintick
    strategy.entry("Long Entry", strategy.long, stop=entryPrice)
    //stopPrice = strategy.position_avg_price - (stopLoss / syminfo.pointvalue)
    //strategy.exit("Stop Loss", "Long Entry", stop=stopPrice)
    numTrades += 1

if (strategy.position_size > 0) and (strategy.position_size[1] == 0)
    stopPoints = stopLoss / syminfo.pointvalue
    stopPrice = strategy.position_avg_price - stopPoints
    stopPrice := math.round(stopPrice / syminfo.mintick) * syminfo.mintick
    strategy.exit("Stop Loss", from_entry="Long Entry", stop=stopPrice)


if ta.change(strategy.opentrades) == 1
    float entryPrice = strategy.opentrades.entry_price(0)
    stopPricePlot := entryPrice - (stopLoss / syminfo.pointvalue)

if ta.change(strategy.closedtrades) == 1
    stopPricePlot   := na

plot(stopPricePlot, "Stop-loss level", color.red, 1, plot.style_linebr)

// ===============================
// Exit at End of Session
// ===============================
if na(t) and strategy.position_size != 0
    strategy.close_all(comment="End of Day Exit")
```

> Detail

https://www.fmz.com/strategy/473247

> Last Modified

2024-11-28 15:44:59
