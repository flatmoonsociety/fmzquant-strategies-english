
> Name

Triple-Standard-Deviation-Bollinger-Bands-Breakout-Strategy-with-100-Day-Moving-Average-Optimization
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/17f81e20df59e3921d6.png)

[trans]
#### Overview
This strategy is a quantitative trading strategy based on the Bollinger Band breakthrough, using an upper track of 3 times the standard deviation and a lower track of 1 times the standard deviation, and combining the 100-day moving average as the middle track. This strategy mainly captures the long-term trend by detecting price breaks above the upper band and uses the lower band as a stop loss signal. The core idea of ​​the strategy is to enter the market when there is a strong breakthrough and stop losses promptly when the price falls below the lower track, thereby achieving risk-controllable trend following.
#### Strategy Principle
The core principle of the strategy is based on the statistical properties of Bollinger Bands. The upper track adopts 3 times the standard deviation, which means that under the assumption of normal distribution, the probability of price breaking through the upper track is only 0.15%. Therefore, when a breakthrough occurs, it often indicates the formation of a significant trend. The mid-track uses the 100-day moving average, which is long enough to effectively filter out short-term market noise. The lower track uses 1 times the standard deviation as the stop loss line. This setting is relatively conservative and helps to stop losses in time. The strategy sends a long signal when the price breaks through the upper band, and closes the position when the price falls below the lower band.
#### Strategic Advantages
1. Strong trend grasping ability: Through the setting of 3 times standard deviation, important trend breakthrough opportunities can be effectively captured.
2. Reasonable risk control: Using 1 times the standard deviation as the stop loss line is more conservative in risk control.
3. The parameters are highly adjustable: the standard deviation multiples of the upper and lower rails and the moving average period can be adjusted according to different market characteristics.
4. Strong systematicity: The strategy logic is clear, the backtesting function is perfect, and the trading performance can be accurately counted.
5. Wide adaptability: It can be applied to many fields such as stock market and cryptocurrency market.
#### Strategy Risk
1. Risk of false breakthrough: The market may fall rapidly after a short-term breakthrough, resulting in false signals.
2. Large retracements: Large retracements may occur in violently volatile markets.
3. Lagging risk: The 100-day moving average has a certain lag and may miss some rapid market trends.
4. Market environment dependence: Frequent entry and exit may occur in volatile markets, resulting in excessive transaction costs.
#### Strategy optimization direction
1. Introducing volume confirmation: A volume breakthrough confirmation mechanism can be added to improve signal reliability.
2. Optimize the stop loss mechanism: You can consider introducing trailing stop loss or ATR dynamic stop loss to improve the flexibility of stop loss.
3. Add trend filtering: You can add long-term trend judgment indicators and only trade in the main trend direction.
4. Optimize position management: the position size can be dynamically adjusted according to the strength of the breakthrough.
5. Add time filtering: you can avoid trading during certain market periods.
#### Summary
This is a well designed and logical trend following strategy. Through the statistical characteristics of Bollinger Bands and the trend tracking characteristics of moving averages, important breakthrough opportunities in the market can be effectively captured. Although there is a certain risk of retracement, it still has good practical value through reasonable stop loss setting and risk control. The room for further optimization mainly lies in signal confirmation, stop loss mechanism and position management. ||
#### Overview
This strategy is a quantitative trading system based on Bollinger Bands breakout, utilizing 3 standard deviations for the upper band and 1 standard deviation for the lower band, combined with a 100-day moving average as the middle band. The strategy primarily captures long-term trends by detecting price breakouts above the upper band and uses the lower band as a stop-loss signal. The core concept is to enter positions during strong breakouts and exit when prices fall below the lower band, achieving controlled risk trend following.

#### Strategy Principles
The core principle is based on the statistical properties of Bollinger Bands. The upper band uses 3 standard deviations, meaning under normal distribution assumptions, the probability of price breaking above this level is only 0.15%, suggesting significant trend formation when breakouts occur. The middle band uses a 100-day moving average, a period long enough to effectively filter short-term market noise. The lower band uses 1 standard deviation as a stop-loss line, a relatively conservative setting that helps with timely exit. The strategy generates long signals when price breaks above the upper band and exits when price falls below the lower band.

#### Strategy Advantages
1. Strong trend capture capability: The 3 standard deviation setting effectively captures significant trend breakout opportunities.
2. Reasonable risk control: Using 1 standard deviation as the stop-loss line provides conservative risk management.
3. High parameter adaptability: The standard deviation multipliers and moving average period can be adjusted for different market characteristics.
4. Systematic approach: Clear strategy logic with comprehensive backtesting capabilities for accurate performance tracking.
5. Wide applicability: Can be applied to various markets including stocks and cryptocurrencies.

#### Strategy Risks
1. False breakout risk: Markets may show short-term breakouts followed by quick reversals, leading to false signals.
2. Significant drawdowns: Large drawdowns may occur in highly volatile markets.
3. Lag risk: The 100-day moving average has inherent lag, potentially missing some rapid market moves.
4. Market environment dependency: May generate excessive trades in ranging markets, leading to high transaction costs.

#### Strategy Optimization Directions
1. Incorporate volume confirmation: Add volume breakout confirmation mechanism to improve signal reliability.
2. Optimize stop-loss mechanism: Consider implementing trailing stops or ATR-based dynamic stops for more flexible exit management.
3. Add trend filters: Incorporate long-term trend identification indicators to trade only in the primary trend direction.
4. Improve position management: Dynamically adjust position sizes based on breakout strength.
5. Add time filters: Avoid trading during specific market periods.

#### Summary
This is a well-designed trend following strategy with clear logic. Through the statistical properties of Bollinger Bands and the trend-following characteristics of moving averages, it effectively captures significant market breakout opportunities. While there are drawdown risks, the strategy maintains practical value through reasonable stop-loss settings and risk control. Further optimization potential lies in signal confirmation, stop-loss mechanisms, and position management aspects.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-11-12 00:00:00
end: 2024-12-11 08:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © MounirTrades007

// @version=6
strategy("Bollinger Bands", overlay=true, initial_capital=100000, default_qty_type=strategy.percent_of_equity, default_qty_value=200)

// Get user input
var g_bb        = "Bollinger Band Settings"
upperBandSD     = input.float(title="Upper Band Std Dev", defval=3.0, tooltip="Upper band's standard deviation multiplier", group=g_bb)
lowerBandSD     = input.float(title="Lower Band Std Dev", defval=1.0, tooltip="Lower band's standard deviation multiplier", group=g_bb)
maPeriod        = input.int(title="Middle Band MA Length", defval=100, tooltip="Middle band's SMA period length", group=g_bb)
var g_tester    = "Backtester Settings"
drawTester      = input.bool(title="Draw Backtester", defval=true, group=g_tester, tooltip="Turn on/off inbuilt backtester display")

// Get Bollinger Bands
[bbIgnore1, bbHigh, bbIgnore2] = ta.bb(close, maPeriod, upperBandSD)
[bbMid, bbIgnore3, bbLow]      = ta.bb(close, maPeriod, lowerBandSD)

// Prepare trade persistent variables
drawEntry   = false
drawExit    = false

// Detect bollinger breakout
if close > bbHigh and barstate.isconfirmed and strategy.position_size == 0
    drawEntry := true
    strategy.entry(id="Trade", direction=strategy.long)
    alert("Bollinger Breakout Detected for " + syminfo.ticker, alert.freq_once_per_bar_close)

// Detect bollinger sell signal
if close < bbLow and barstate.isconfirmed and strategy.position_size != 0
    drawExit := true
    strategy.close(id="Trade")
    alert("Bollinger Exit detected for " + syminfo.ticker, alert.freq_once_per_bar_close)

// Draw bollinger bands
plot(bbMid, color=color.blue, title="Middle SMA")
plot(bbHigh, color=color.green, title="Upper Band")
plot(bbLow, color=color.red, title="Lower Band")

// Draw signals
plotshape(drawEntry, style=shape.triangleup, color=color.green, location=location.belowbar, size=size.normal, title="Buy Signal")
plotshape(drawExit, style=shape.xcross, color=color.red, location=location.belowbar, size=size.normal, title="Sell Signal")

// // =============================================================================
// // START BACKTEST CODE
// // =============================================================================

// // Prepare stats table
// var table testTable = table.new(position.top_right, 2, 2, border_width=1)
// f_fillCell(_table, _column, _row, _title, _value, _bgcolor, _txtcolor) =>
//     _cellText = _title + "\n" + _value
//     table.cell(_table, _column, _row, _cellText, bgcolor=_bgcolor, text_color=_txtcolor)

// // Draw stats table
// var bgcolor = color.black
// if barstate.islastconfirmedhistory
//     if drawTester
//         dollarReturn = strategy.equity - strategy.initial_capital
//         f_fillCell(testTable, 0, 0, "Total Trades:", str.tostring(strategy.closedtrades), bgcolor, color.white)
//         f_fillCell(testTable, 0, 1, "Win Rate:", str.tostring(strategy.wintrades / strategy.closedtrades * 100, "##.##") + "%", bgcolor, color.white)
//         f_fillCell(testTable, 1, 0, "Equity:", "$" + str.tostring(strategy.equity, "###,###.##"), bgcolor, color.white)
//         f_fillCell(testTable, 1, 1, "Return:", str.tostring((strategy.netprofit / strategy.initial_capital) * 100, "##.##") + "%", dollarReturn > 0 ? color.green : color.red, color.white)

// // =============================================================================
// // END BACKTEST CODE
// // =============================================================================
```

> Detail

https://www.fmz.com/strategy/474971

> Last Modified

2024-12-13 11:20:13
