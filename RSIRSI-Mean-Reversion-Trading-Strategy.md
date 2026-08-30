
> Name

RSI-Mean-Reversion-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

This strategy is designed based on the moving average regression characteristics of the RSI indicator. When RSI is overbought or oversold, it will return and form a trading opportunity. This strategy uses the RSI indicator to determine the overbought and oversold status, and uses the moving average regression method to establish long and short positions to achieve systematic trading purposes.
Strategy principle:
1. Calculate the RSI indicator value and set the overbought line and oversold line. Typical parameters are 60 for the overbought line and 30 for the oversold line.
2. When RSI falls below the overbought line from top to bottom, perform a selling operation and establish a short position.
3. When RSI breaks through the oversold line from bottom to top, perform a buying operation and establish a long position.
4. The stop-loss line for long positions is the entry price multiplied by (1-stop-loss ratio), and the stop-loss line for short positions is the entry price multiplied by (1+stop-loss ratio).
5. When the price breaks through the stop loss line, stop the loss and exit.
The advantages of this strategy include:
1. Using the regression characteristics of the RSI indicator, you can capture the trading opportunities brought by the trend callback.
2. Using the breakthrough position building method, you can catch the trend turning point in time.
3. Set a stop loss line to control single losses.
Risks of this strategy include:
1. The RSI indicator has a high probability of sending out false signals and should be confirmed in conjunction with other indicators.
2. If the stop loss point is close to the entry point, the loss will be stopped frequently, and the stop loss range should be appropriately relaxed.
3. Improper timing of return trading may result in holding positions for too long.
In short, the RSI moving average reversion strategy trades by capturing the reversion opportunities of the RSI indicator. This strategy can follow the trend and effectively control single losses. However, the reliability of the RSI indicator is low, and investors need to use it prudently, confirm it with other technical indicators, and optimize the stop-loss mechanism in order to obtain long-term stable returns.
||


This strategy is based on the mean reversion characteristics of the RSI indicator. Overbought and oversold RSI tends to revert back, creating trading opportunities. The strategy identifies overbought/oversold states using RSI to establish long/short positions in a systematic way. 

Strategy Logic:

1. Calculate RSI value and set overbought and oversold thresholds, typically 60 and 30. 

2. When RSI crosses down the overbought line, go short. 

3. When RSI crosses up the oversold line, go long.

4. Long stop loss is entry price * (1 - stop loss %). Short stop loss is entry price * (1 + stop loss %).

5. If price hits the stop loss, exit the position.

Advantages:

1. Captures mean reversion opportunities during trend pullbacks using RSI.

2. Breakout trading allows timely entry at trend reversals. 

3. Stop loss controls single trade loss amount.

Risks: 

1. RSI tends to give false signals. Confirm with other indicators.

2. Stop loss being too tight causes excessive stops. Consider widening range.

3. Poor timing of entries may lead to oversized positions.

In summary, the RSI mean reversion strategy trades RSI overextensions. It follows the trend with controlled loss on single trades. But RSI reliability is low. Investors should use it prudently with other confirming indicators, optimized stops, and expect modest long-term returns.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|timestamp(08 Mar 2021 00:00 -0600)|Start Time|
|v_input_2|timestamp(9 Mar 2021 23:59 -0600)|Start Time|
|v_input_3|14|lengthRSI|
|v_input_4_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_5|0|Strategy: Long/Short|Long Only|Short Only|
|v_input_6|5|Stop Loss %|
|v_input_7|30|oversold|
|v_input_8|60|overbought|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-05 00:00:00
end: 2023-09-11 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © relevantLeader16058

//@version=4
strategy(shorttitle='RSI Bot Strategy',title='Quadency Mean Reversion Bot Strategy', overlay=true, initial_capital = 100, process_orders_on_close=true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, commission_type=strategy.commission.percent, commission_value=0.08)

//Backtest dates
start = input(defval = timestamp("08 Mar 2021 00:00 -0600"), title = "Start Time", type = input.time)
finish = input(defval = timestamp("9 Mar 2021 23:59 -0600"), title = "Start Time", type = input.time)
window()  => true       // create function "within window of time"

// Complete Control over RSI inputs and source price calculations
lengthRSI = input(14, minval=1)
source = input(title="Source", type=input.source, defval=close)
strat = input(title="Strategy", defval="Long/Short", options=["Long Only", "Long/Short", "Short Only"])
strat_val = strat == "Long Only" ? 1 : strat == "Long/Short" ? 0 : -1
stoploss = input(5.00, "Stop Loss %")
oversold= input(30)
overbought= input(60)

// Standard RSI Calculation
RSI = rsi(close, lengthRSI)
stLossLong=(1-(stoploss*.01))
stLossShort=(1+(stoploss*.01))

//Long and Short Strategy Logic
GoLong = crossunder(RSI, oversold) and window()
GoShort = crossover(RSI, overbought) and window()

// Strategy Entry and Exit
if (GoLong)
    if strat_val > -1
        strategy.entry("LONG", strategy.long)
    if strat_val < 1
        strategy.close("SHORT")
    

if (GoShort)
    if strat_val > -1
        strategy.close("LONG")
    if strat_val < 1
        strategy.entry("SHORT", strategy.short)


LongStopLoss = barssince(GoLong)<barssince(GoShort) and crossunder(low, valuewhen(GoLong, close, 0)*stLossLong)

ShortStopLoss = barssince(GoLong)>barssince(GoShort) and crossover(high, valuewhen(GoShort, close, 0)*stLossShort)

if (ShortStopLoss)
    strategy.close("SHORT")
    
if (LongStopLoss)
    strategy.close("LONG")





```

> Detail

https://www.fmz.com/strategy/426479

> Last Modified

2023-09-12 14:37:28
