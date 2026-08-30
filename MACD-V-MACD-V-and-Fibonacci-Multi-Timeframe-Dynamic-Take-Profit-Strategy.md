
> Name

MACD-V and Fibonacci Multi-Timeframe Dynamic Take Profit Strategy-MACD-V-and-Fibonacci-Multi-Timeframe-Dynamic-Take-Profit-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/173e5a45d8d645ba166.png)

[trans]

#### Overview
This strategy uses MACD-V (MACD with ATR Volatility) and Fibonacci retracements to make trading decisions on multiple time frames. It calculates MACD-V and Fibonacci levels for different time frames, and then decides to open and close positions based on the relationship between the current price and Fibonacci levels and the value of MACD-V. This strategy is designed to capture market trends and pullbacks while controlling risk.
#### Strategy Principle
1. Calculate the MACD-V indicator in different time frames (such as 5 minutes and 30 minutes). MACD-V introduces ATR volatility adjustment based on MACD to adapt to different market conditions.
2. Calculate the highest price and lowest price of a certain period in the past (such as 9 periods) on a high-level time frame (such as 30 minutes), and then calculate the Fibonacci retracement level based on this interval.
3. Based on the relationship between the current closing price and Fibonacci level, as well as the value and change direction of MACD-V, determine whether the opening conditions are met. For example, open a short position when the price retraces around the 38.2% Fibonacci level and MACD-V moves downward between -50 and 150.
4. After opening a position, use trailing stop to protect profits and control risks. The position of the moving take profit is dynamically adjusted based on price movement and strategy parameters.
5. If the price hits the trailing stop or fixed stop level, close the position.
#### Advantage Analysis
1. The strategy uses multi-time frame analysis to more comprehensively grasp market trends and fluctuations.
2. The MACD-V indicator takes into account price volatility and can work effectively in both trending and volatile markets.
3. Fibonacci levels can well capture key support and resistance areas of price and provide a reference for trading decisions.
4. Moving take profit can continue to make profits when the trend continues, and at the same time close positions promptly when the price reverses to control risks.
5. The strategy logic is clear, parameters are adjustable, and adaptability is strong.
#### Risk Analysis
1. The strategy may experience frequent transactions in volatile markets, resulting in high transaction costs.
2. Relying on technical indicators to judge trends may lead to misjudgments when the market experiences false breakthroughs or continues to fluctuate.
3. Fixed stop loss positions may not be able to respond to extreme market conditions in time, resulting in larger losses.
4. Improper parameter selection may lead to poor strategy performance.
#### Optimization direction
1. Introduce more time frames and indicators, such as longer period MA, to improve the accuracy of trend judgment.
2. Optimize position management, such as dynamically adjusting position size based on ATR or price range.
3. Set different parameter combinations for different market conditions to improve adaptability.
4. On the basis of trailing stop-profit, introduce trailing stop-loss to better control downside risks.
5. Conduct backtesting and parameter optimization on the strategy to find the best parameter combination.
#### Summary
This strategy uses MACD-V and Fibonacci retracement levels in multiple time frames to determine trends and opening opportunities, and uses moving take-profit to dynamically control risks and profits. The strategy has clear logic and strong adaptability, but in volatile markets there may be risks of frequent transactions and misjudgments. By introducing more indicators, optimizing position management and stop-loss logic, and optimizing parameters, the robustness and profitability of the strategy can be further improved.
#### grateful
The MACD-v indicator used in this strategy is credited to the original author, Alex Spiroglou. For more details you can refer to his work: [MACD-v.](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4099617)
||

#### Overview
This strategy uses MACD-V (MACD with ATR volatility) and Fibonacci retracements to make trading decisions across multiple timeframes. It calculates MACD-V and Fibonacci levels on different timeframes, then decides whether to open or close positions based on the current price's relationship to the Fibonacci levels and the values of MACD-V. The strategy aims to capture market trends and retracements while controlling risk.

#### Strategy Principles
1. Calculate MACD-V indicator on different timeframes (e.g., 5-minute and 30-minute). MACD-V introduces ATR volatility adjustment to the standard MACD to adapt to different market conditions.
2. On a higher timeframe (e.g., 30-minute), calculate the highest high and lowest low of the past certain periods (e.g., 9 periods), then calculate Fibonacci retracement levels based on this range.
3. Determine whether to open a position based on the relationship between the current closing price and Fibonacci levels, as well as the value and direction of MACD-V. For example, when the price retraces to around the 38.2% Fibonacci level and MACD-V is moving downward between -50 and 150, open a short position.
4. After opening a position, use a trailing stop to protect profits and control risk. The trailing stop's position is dynamically adjusted based on price movement and strategy parameters.
5. If the price hits the trailing stop or fixed stop loss level, close the position.

#### Advantage Analysis
1. The strategy employs multi-timeframe analysis, providing a more comprehensive understanding of market trends and fluctuations.
2. The MACD-V indicator considers price volatility, making it effective in both trending and ranging markets.
3. Fibonacci levels can effectively capture key support and resistance areas, providing reference for trading decisions.
4. Trailing stops allow for continued profitability during trend continuation while timely closing positions during price reversals, controlling risk.
5. The strategy logic is clear, parameters are adjustable, and adaptability is strong.

#### Risk Analysis
1. The strategy may experience frequent trading in ranging markets, leading to high transaction costs.
2. Relying on technical indicators to judge trends may result in misjudgment when the market experiences false breakouts or prolonged oscillation.
3. Fixed stop loss positions may not respond timely to extreme market conditions, leading to significant losses.
4. Improper parameter selection may result in poor strategy performance.

#### Optimization Directions
1. Introduce more timeframes and indicators, such as longer-period MAs, to improve the accuracy of trend judgment.
2. Optimize position management, such as dynamically adjusting position size based on ATR or price range.
3. Set different parameter combinations for different market conditions to improve adaptability.
4. In addition to trailing stops, introduce trailing stop losses to better control downside risk.
5. Backtest and optimize parameters to find the best parameter combination.

#### Summary
This strategy uses MACD-V and Fibonacci retracement levels across multiple timeframes to determine trends and entry timing, and employs trailing stops to dynamically control risk and profit. The strategy logic is clear and adaptable, but may experience frequent trading and misjudgment risks in ranging markets. By introducing more indicators, optimizing position management and stop loss logic, and optimizing parameters, the strategy's robustness and profitability can be further improved.

#### Acknowledgment

The MACD-v indicator used in this strategy is credited to Alex Spiroglou, the original creator. For more details, you can refer to his work: [MACD-v.](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4099617)
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-03-26 00:00:00
end: 2024-04-25 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © catikur

//@version=5
strategy("Advanced MACD-V and Fibonacci Strategy with EMA Trailing TP", overlay=true, default_qty_type = strategy.percent_of_equity, default_qty_value=1000, margin_long=1./10*50, margin_short=1./10*50, slippage=0, commission_type=strategy.commission.percent, commission_value=0.05)

// Parametreler
fast_len = input.int(12, title="Fast Length", minval=1, group="MACD-V Settings")
slow_len = input.int(26, title="Slow Length", minval=1, group="MACD-V Settings")
signal_len = input.int(9, title="Signal Smoothing", minval=1, group="MACD-V Settings")
atr_len = input.int(26, title="ATR Length", minval=1, group="MACD-V Settings")
source = input.source(close, title="Source", group="MACD-V Settings")

//ema_length = input.int(20, title="EMA Length for Trailing TP", group="Trailing TP Settings")
trailing_profit = input.float(1000, title="Trailing Profit", minval=0.01, maxval=1000000, step=0.01, group="Trailing TP Settings")
trailing_offset = input.float(30000, title="Trailing Offset", minval=0.01, maxval=1000000, step=0.01, group="Trailing TP Settings")
trailing_factor = input.float(0.01, title="Trailing Factor", minval=0.01, maxval=1000000, step=0.01, group="Trailing TP Settings")
fix_loss = input.float(20000, title="Fix Loss", minval=0.01, maxval=1000000, step=0.01, group="Trailing TP Settings")

fib_lookback = input.int(9, title="Fibonacci Lookback Periods", minval=1, group="Fibonacci Settings")

macd_tf = input.timeframe("5", title="MACD Timeframe", group="Timeframe Settings")
fib_tf = input.timeframe("30", title="Fibonacci Timeframe", group="Timeframe Settings")
//ema_tf = input.timeframe("30", title="EMA Timeframe for Trailing TP", group="Timeframe Settings")




// MACD-V Hesaplama
atr = ta.atr(atr_len)
ema_slow = ta.ema(source, slow_len)
ema_fast = ta.ema(source, fast_len)

atr_tf = request.security(syminfo.tickerid, macd_tf , atr)
ema_slow_tf = request.security(syminfo.tickerid, macd_tf , ema_slow)
ema_fast_tf = request.security(syminfo.tickerid, macd_tf , ema_fast)

macd = ( ema_fast_tf - ema_slow_tf ) / atr_tf * 100
signal = ta.ema(macd, signal_len)
hist = macd - signal
hist_prev = hist[1]

// log.info("MACD {0} ", macd)
// log.info("Signal {0} ", signal)
// log.info("Histogram {0} ", hist)
// log.info("Previous Histogram {0} ", hist_prev)

// EMA for Trailing TP
//ema_trailing_tf = ta.ema(close, ema_length)

//ema_trailing = request.security(syminfo.tickerid, ema_tf, ema_trailing_tf)

//log.info("EMA Trailing {0} ", ema_trailing)

// Fibonacci Seviyeleri

high_val_tf = ta.highest(high, fib_lookback)
low_val_tf = ta.lowest(low, fib_lookback)

h1 = request.security(syminfo.tickerid, fib_tf, high_val_tf)
l1 = request.security(syminfo.tickerid, fib_tf, low_val_tf)

fark = h1 - l1

//Low ile fark
hl236 = l1 + fark * 0.236
hl382 = l1 + fark * 0.382
hl500 = l1 + fark * 0.5
hl618 = l1 + fark * 0.618
hl786 = l1 + fark * 0.786
//High ile fark
lh236 = h1 - fark * 0.236
lh382 = h1 - fark * 0.382
lh500 = h1 - fark * 0.5
lh618 = h1 - fark * 0.618
lh786 = h1 - fark * 0.786

hbars_tf = -ta.highestbars(high, fib_lookback)
lbars_tf = -ta.lowestbars(low, fib_lookback)

hbars = request.security(syminfo.tickerid, fib_tf , hbars_tf)
lbars = request.security(syminfo.tickerid, fib_tf , lbars_tf)

fib_236 = hbars > lbars ? hl236 : lh236
fib_382 = hbars > lbars ? hl382 : lh382
fib_500 = hbars > lbars ? hl500 : lh500
fib_618 = hbars > lbars ? hl618 : lh618
fib_786 = hbars > lbars ? hl786 : lh786

// log.info("Fibo 382 {0} ", fib_382)
// log.info("Fibo 618 {0} ", fib_618)

// Keep track of the strategy's highest and lowest net profit
var highestNetProfit = 0.0
var lowestNetProfit  = 0.0

var bool sell_retracing = false
var bool sell_reversing = false
var bool buy_rebound = false
var bool buy_rallying = false

// Satış Koşulları
sell_retracing := (signal > -20) and (macd > -50 and macd < 150) and (macd < signal) and (hist < hist_prev) and (close < fib_382)
sell_reversing := (macd > -150 and macd < -50) and (macd < signal) and (hist < hist_prev) and (close < fib_618)

// log.info("Retracing var mi: {0} ", sell_retracing)
// log.info("Reversing var mi: {0} ", sell_reversing)

// Alım Koşulları
buy_rebound := (signal < 20) and (macd > -150 and macd < 50) and (macd > signal) and (hist > hist_prev) and ((fib_618 < close) or ((fib_618 > close ) and (close > fib_382)))
buy_rallying := (macd > 50 and macd < 150) and (macd > signal) and (hist > hist_prev) and (close > fib_618)

// log.info("Rallying var mi: {0} ", buy_rallying)
// log.info("Rebound var mi: {0} ", buy_rebound)

// Emirleri Yerleştirme
if (sell_retracing == true and strategy.opentrades == 0 )
    strategy.entry("sell_retracing", strategy.short)

if (sell_reversing == true and strategy.opentrades == 0 )
    strategy.entry("sell_reversing", strategy.short)

if (buy_rebound == true and strategy.opentrades == 0 )
    strategy.entry("buy_rebound", strategy.long)

if (buy_rallying == true and strategy.opentrades == 0 )
    strategy.entry("buy_rallying", strategy.long)


// log.info("open order: {0} ", strategy.opentrades )


highestNetProfit := math.max(highestNetProfit, strategy.netprofit)
lowestNetProfit  := math.min(lowestNetProfit, strategy.netprofit)




// Plot the net profit, as well as its highest and lowest value
//plot(strategy.netprofit, style=plot.style_area, title="Net profit",
//     color=strategy.netprofit > 0 ? color.green : color.red)

//plot(highestNetProfit, color=color.green, title="Highest net profit")
//plot(lowestNetProfit, color=color.red, title="Lowest net profit")

// Trailing Take Profit
//long_trailing_stop = ema_trailing * trailing_factor
//short_trailing_stop = ema_trailing / trailing_factor

//log.info("long trailing stop {0} ", long_trailing_stop)
//log.info("short trailing stop {0} ", short_trailing_stop)
//log.info("avg price {0} ", strategy.position_avg_price)
//trail_price1 = strategy.position_avg_price * (1 + trailing_factor)
//trail_price2 = strategy.position_avg_price * (1 - trailing_factor)
// log.info("position_size {0} ", strategy.position_size)

// Trailing Take Profit
var float long_trailing_stop = 0.0
var float short_trailing_stop = 0.0

//if (strategy.position_size > 0)
 //   long_trailing_stop := math.max(long_trailing_stop, close * (1 + trailing_factor))  // Yeni bir maksimum değer belirlendiğinde güncelle
//if (strategy.position_size < 0)
 //  short_trailing_stop := math.min(short_trailing_stop, close * (1 - trailing_factor))  // Yeni bir minimum değer belirlendiğinde güncelle

//log.info("long trailing {0} ", long_trailing_stop)
// log.info("trailing factor{0} ", trailing_factor)
//log.info("short trailing {0} ", short_trailing_stop)

if (strategy.position_size != 0 )
    strategy.exit("Exit Long", from_entry="buy_rebound", trail_points = trailing_profit, trail_offset = trailing_offset, loss = fix_loss)
    strategy.exit("Exit Long", from_entry="buy_rallying", trail_points = trailing_profit, trail_offset = trailing_offset, loss = fix_loss)
    strategy.exit("Exit Short", from_entry="sell_retracing", trail_points = trailing_profit, trail_offset = trailing_offset, loss = fix_loss)
    strategy.exit("Exit Short", from_entry="sell_reversing", trail_points = trailing_profit, trail_offset = trailing_offset, loss = fix_loss)
```

> Detail

https://www.fmz.com/strategy/449508

> Last Modified

2024-06-25 11:28:55
