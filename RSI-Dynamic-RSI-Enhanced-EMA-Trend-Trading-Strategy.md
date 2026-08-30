
> Name

Dynamic RSI Enhanced Index Moving Average Trend Trading Strategy-Dynamic-RSI-Enhanced-EMA-Trend-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/c988f3d6af83b7f219.png)

[trans]
#### Overview
This strategy is a dynamic trend following system that combines the Exponential Moving Average (EMA) and the Relative Strength Index (RSI). It identifies trend direction through 9-period and 21-period EMA crossovers and uses RSI as a trend confirmation indicator. The strategy also includes a complete money management system, including the setting of dynamic stop loss and profit targets.
#### Strategy Principle
The core logic of the strategy is based on the following key elements:
1. Use the crossover of short-term (9-period) and long-term (21-period) EMA to capture changes in trend
2. Confirm the trend through the 14-period RSI indicator. It is required to do long when RSI>50 and short when RSI<50.
3. Adopt a fixed point stop loss setting (default 30 points), and dynamically calculate the position size based on the risk amount
4. Use fund management parameters to dynamically calculate profit target prices
5. Real-time display of entry marks, target prices and stop loss positions on the chart
#### Strategic Advantages
1. Combined with trend and momentum indicators, it improves the reliability of trading signals
2. A complete fund management system that can flexibly adjust risks according to account size
3. Clear visual feedback system, including transaction failure mark
4. Parameters can be fully customized to adapt to different trading styles
5. Automate entry and exit to reduce human intervention
#### Strategy Risk
1. As a lagging indicator, EMA may produce delayed signals in highly volatile markets.
2. Frequent false breakthrough signals may occur in sideways markets
3. Fixed pip stops may not be flexible enough when volatility changes
4. Parameters need to be carefully adjusted to suit different market conditions
5. Possible risk of slippage in a low liquidity environment
#### Strategy optimization direction
1. Introduce adaptive stop loss mechanism, such as dynamic stop loss based on ATR
2. Add market volatility filter to adjust strategy parameters during periods of high volatility
3. Add trading time filtering to avoid trading during unfavorable hours
4. Develop a smarter position management system that takes into account market volatility
5. Introduce additional indicators to filter out false signals
#### Summary
This strategy builds a complete trend following system by combining EMA crossovers and RSI confirmations. Its main advantage is that it organically combines technical analysis with risk management, and has good scalability and adaptability. Although there are some inherent risks, through continuous optimization and parameter adjustment, this strategy can provide traders with a robust trading framework.
||

#### Overview
This strategy is a dynamic trend following system that combines Exponential Moving Averages (EMA) with Relative Strength Index (RSI). It identifies trend direction through 9-period and 21-period EMA crossovers, using RSI as trend confirmation. The strategy includes a comprehensive money management system with dynamic stop-loss and profit target settings.

#### Strategy Principles
The core logic is based on several key elements:
1. Using short-term (9-period) and long-term (21-period) EMA crossovers to capture trend changes
2. Confirming trends with 14-period RSI, requiring RSI>50 for longs and RSI<50 for shorts
3. Implementing fixed-point stop-losses (default 30 points) with dynamic position sizing based on risk amount
4. Calculating profit targets dynamically using money management parameters
5. Displaying real-time entry markers, target prices, and stop-loss levels on the chart

#### Strategy Advantages
1. Combines trend and momentum indicators for improved signal reliability
2. Complete money management system adaptable to account size
3. Clear visual feedback system including trade failure markers
4. Fully customizable parameters to suit different trading styles
5. Automated entry and exit execution reducing manual intervention

#### Strategy Risks
1. EMA as a lagging indicator may generate delayed signals in volatile markets
2. Frequent false breakout signals possible in ranging markets
3. Fixed-point stop-losses may lack flexibility during volatility changes
4. Careful parameter adjustment needed for different market conditions
5. Potential slippage risks in low liquidity environments

#### Strategy Optimization Directions
1. Introduce adaptive stop-loss mechanisms, such as ATR-based dynamic stops
2. Add market volatility filters to adjust strategy parameters during high volatility
3. Implement trading time filters to avoid unfavorable periods
4. Develop smarter position sizing system considering market volatility
5. Incorporate additional indicators to filter false signals

#### Summary
This strategy establishes a complete trend following system by combining EMA crossovers with RSI confirmation. Its main strength lies in the organic integration of technical analysis and risk management, offering good scalability and adaptability. While inherent risks exist, through continuous optimization and parameter adjustment, the strategy can provide traders with a robust trading framework.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-10 00:00:00
end: 2025-02-08 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Lukhi24

//@version=6
strategy("Lukhi EMA Crossover_TWL educational strategy", overlay=true)

// Input Parameters
capital = input.float(15000, title="Capital (₹)", tooltip="Total capital")
risk_per_trade = input.float(1000, title="Risk per Trade (₹)", tooltip="Risk per trade amount")
target_per_trade = input.float(5000, title="Take Profit per Trade (₹)", tooltip="Target profit per trade")
lot_size = input.int(1, title="Lot Size", tooltip="Nifty option lot size")
stop_loss_distance = input.float(30, title="Stop Loss Distance (Points)", tooltip="Fixed stop-loss in points")

// EMA Parameters
short_ema_length = input.int(9, title="Short EMA Length")
long_ema_length = input.int(21, title="Long EMA Length")

// RSI Parameters
rsi_length = input.int(14, title="RSI Length")
rsi_overbought = input.float(70, title="RSI Overbought Level")
rsi_oversold = input.float(30, title="RSI Oversold Level")

// Calculate EMAs and RSI
ema_short = ta.ema(close, short_ema_length)
ema_long = ta.ema(close, long_ema_length)
rsi = ta.rsi(close, rsi_length)

// Buy and Sell Signals
buy_signal = ta.crossover(ema_short, ema_long) and rsi > 50
sell_signal = ta.crossunder(ema_short, ema_long) and rsi < 50

// Plot EMAs
plot(ema_short, color=color.blue, title="EMA Short")
plot(ema_long, color=color.orange, title="EMA Long")

// Position Size Calculation
position_size = risk_per_trade / stop_loss_distance

// Stop Loss and Take Profit Levels
long_stop_loss = close - stop_loss_distance
long_take_profit = close + (target_per_trade / position_size)

short_stop_loss = close + stop_loss_distance
short_take_profit = close - (target_per_trade / position_size)

// Entry and Exit Logic
if buy_signal
    strategy.entry("Buy", strategy.long, qty=lot_size)
    strategy.exit("Exit Buy", "Buy", stop=long_stop_loss, limit=long_take_profit)

if sell_signal
    strategy.entry("Sell", strategy.short, qty=lot_size)
    strategy.exit("Exit Sell", "Sell", stop=short_stop_loss, limit=short_take_profit)

// Add Entry Signal Labels
var label long_label = na
var label short_label = na

if buy_signal
    label.delete(long_label)
    long_label := label.new(bar_index,close,text="BUY\nEntry: " + str.tostring(close, "#.##") + "\nTarget: " + str.tostring(long_take_profit, "#.##") + "\nSL: " + str.tostring(long_stop_loss, "#.##"),style=label.style_label_up,color=color.rgb(12, 90, 90, 73),textcolor=#010000)

if sell_signal
    label.delete(short_label)
    short_label := label.new(bar_index,close,text="SELL\nEntry: " + str.tostring(close, "#.##") + "\nTarget: " + str.tostring(short_take_profit, "#.##") + "\nSL: " + str.tostring(short_stop_loss, "#.##"),style=label.style_label_down,color=#5d371752,textcolor=#000000)

// Trade Failure Indicators
long_trade_loss = strategy.position_size > 0 and close <= long_stop_loss
short_trade_loss = strategy.position_size < 0 and close >= short_stop_loss

plotshape(long_trade_loss, location=location.belowbar, color=color.red, style=shape.cross, title="Long Trade Failed", text="SL Hit")
plotshape(short_trade_loss, location=location.abovebar, color=color.red, style=shape.cross, title="Short Trade Failed", text="SL Hit")

```

> Detail

https://www.fmz.com/strategy/481347

> Last Modified

2025-02-10 14:29:19
