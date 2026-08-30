
> Name

EMA mean reversion trading strategy EMA-Mean-Reversion-Trading-Strategy
> Author

ChaoZhang

> Strategy Description


![IMG](assets/images/616a289b0384add7756c3872e5a855933a3487a89bdc9e17642cb2420cbf8198.png)
[trans]


## Overview
The EMA mean reversion trading strategy is a trading strategy that opens and closes positions based on the degree to which the price deviates from the moving average. It uses the percentage difference between the EMA and the current price as a signal to open a position, and uses trailing stop loss to manage the position.
## Strategy Principle
This strategy uses EMA as a moving average indicator and calculates the percentage difference between the current price and the EMA. When the price is far enough away from the EMA (9% by default), a long position will be opened; when the price is close enough to the EMA (1% by default), the position will be closed. After opening a position, it will use running stop loss to lock in profits, and gradually raise the stop loss line as profits increase.
Specifically, the strategy mainly includes the following components:
1. Calculate the EMA moving average. You can configure the period (default 200), data source (closing price), and calculation method (EMA, SMA, RMA, WMA).
2. Calculate the percentage difference between the current price and the EMA. Pay attention to the handling of positive and negative values.
3. Open a position based on the gap ratio. The threshold for opening a long position is 9% (configurable), and the threshold for opening a short position is 9% (configurable).
4. Support trapezoidal position opening. You can configure the number of steps of the trapezoid and the gradient of each step.
5. Trail the stop loss after opening the position. The threshold for starting stop loss (default profit 1%) and tracking range (default 1%) can be configured.
6. Close the position according to the gap ratio. The threshold for closing long positions is 1% (configurable), and the same applies to short positions.
7. Cancellation of unconcluded orders. When the price approaches the EMA again, unfilled orders will be cancelled.
8. Configurable stop loss percentage.
9. Support backtesting and real-time trading.
## Advantage Analysis
This strategy has the following advantages:
1. Use the concept of moving average reversion to open a position when the price deviates from the moving average and close the position when it returns, which is in line with trend trading theory.
2. The parameters for position opening, stop loss, and position closing can be configured in detail to adapt to different market environments.
3. Trapezoidal position opening allows you to open positions in batches to reduce the cost of a single transaction.
4. Running stop loss can lock in profits and manage risks.
5. There is a lot of room for optimization. You can adjust the moving average parameters or the gap between opening and closing positions to adapt to different market conditions.
6. Supports the mainstream programming language Pine Script and can be used directly in TradingView.
7. Intuitive chart display for easy observation and analysis.
## Risk Analysis
This strategy also has the following risks:
1. Backtest data fitting risk. Parameter optimization may over-fit the backtest data, and the actual effect is questionable.
2. Risk of moving average failure. The price may deviate significantly from the moving average for a long period of time and be unable to return.
3. Risk of stop loss being exceeded. The market is violent and the stop loss point may be breached.
4. Transactions are frequent and the transaction fee burden is heavy.
5. A longer observation period is required, and emergencies have a greater impact.
Corresponding risk management:
1. Carry out more parameter tuning to ensure robust parameters. Verify effectiveness in multiple markets.
2. Reasonably configure the moving average period, not too short or too long.
3. Appropriately relax the stop loss range to prevent being trapped.
4. Appropriately relax the conditions for opening positions and reduce the frequency of transactions.
5. Combine more indicators to improve the ability to adapt to emergencies.
## Optimization direction
This strategy can be optimized in the following areas:
1. Add filtering conditions, such as trading volume, Bollinger Bands, RSI and other indicators to reduce false signals.
2. Add compound moving averages, such as double EMA systems, to increase the probability of trend trading.
3. Optimize stop loss strategies, such as adaptive stop loss, Chandelier Exit, etc., to further limit risks.
4. Add automatic parameter optimization function to automatically find better parameter combinations.
5. Add machine learning prediction to assist in judging the probability of price leaving the moving average.
6. Consider cross-session trading and use night trading or pre-market information to plan ahead.
7. Integrate stock pools, automatically select and trade stocks, and expand strategy capacity.
## Summarize
The EMA mean reversion strategy is a trend following strategy based on the price moving average reversion characteristics. It makes reasonable use of the statistical characteristics of moving averages to determine trend turning points, and uses stop loss to control risks. Compared with the traditional moving average trading strategy, it pays more attention to dynamic tracking and stop loss, rather than rigid opening and closing of positions. This strategy can enrich the trend tracking strategy portfolio, but it needs to pay attention to backtest optimization issues and control the trading frequency. If we can continue to optimize the stop loss mechanism and improve the quality of opening positions, the actual results may be even better.
||


## Overview

The EMA mean reversion trading strategy opens and closes positions based on the degree to which price diverges from the EMA. It uses the percentage difference between price and EMA as the entry signal and trailing stop loss to manage positions.

## Strategy Logic

The strategy uses EMA as the benchmark and calculates the percentage difference between current price and EMA. It goes long when the price is far enough from the EMA (default 9%), and closes position when price gets close enough to the EMA (default 1%). After opening positions, it uses trailing stop loss to lock in profit as it increases. 

Specifically, the strategy includes the following components:

1. Calculate EMA. The period (default 200), source (close price) and method (EMA, SMA, RMA, WMA) are configurable.

2. Calculate the percentage difference between current price and EMA. Pay attention to the positive/negative sign. 

3. Open positions based on difference threshold. Default long entry is 9% and short entry is 9%.

4. Support ladder entry. The number of rungs and percentage step per rung can be configured.

5. Use trailing stop loss after entry. The threshold to start trailing (default 1% profit) and trailing percentage (default 1%) are configurable.

6. Close positions based on difference threshold. Default exit is 1% for both long and short.  

7. Cancel unfilled orders when price reverts to EMA. 

8. Configurable stop loss percentage.

9. Support backtesting and live trading.

## Advantage Analysis

The advantages of this strategy:

1. Utilize mean reversion concept to trade trend based on EMA deviation. Aligns with trend trading theory.

2. Entry, stop loss, exit parameters are configurable to adapt to different market conditions.

3. Ladder entry allows gradual position build up and reduces cost.

4. Trailing stop locks in profit and manages risk.

5. Highly optimizable by adjusting EMA parameters or entry/exit thresholds.

6. Pine Script allows straightforward use in TradingView.

7. Intuitive charting for observation and analysis.

## Risk Analysis

The risks of this strategy:

1. Backtest overfitting risk. Parameter optimization may overfit backtest data and underperform in live trading.

2. EMA failure risk. Price may deviate from EMA for extended periods. 

3. Stop loss getting run over risk. Stop loss may get penetrated by volatile moves.

4. High trading frequency leads to higher commission costs.

5. Require longer lookback period. More susceptible to sudden events.

Risk management:

1. Robust parameter selection through optimization and multi-market verification.

2. Reasonable EMA period, not too short or too long.

3. Wider stop loss buffer to prevent getting stopped out prematurely. 

4. Less aggressive entry rules to reduce trade frequency.

5. Incorporate additional indicators like volume, Bollinger Bands, RSI to adapt to events.

## Optimization Directions

The strategy can be improved in the following aspects:

1. Add filters like volume, Bollinger Bands, RSI to reduce false signals.

2. Add dual EMA for higher probability trend trading.

3. Enhance stop loss with adaptive stops, Chandelier Exits to further limit risk.

4. Add auto parameter optimization to find better parameter sets.

5. Incorporate machine learning for chance of EMA deviation.

6. Consider intraday or overnight position to take advantage of gaps.

7. Integrate stock universe selection for larger capacity.

## Conclusion

The EMA mean reversion strategy trades based on the mean reverting behavior of prices around a moving average. It utilizes the statistical properties of EMA rationally to identify trend changes and uses stop loss to control risk. Compared to traditional moving average strategies, it focuses more on dynamic trailing stops than rigid entry and exit rules. The strategy can complement trend following strategies, but requires caution on curve fitting and controlling trade frequency. Further improvements on stop loss and entry quality may lead to better live performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_timeframe_1||(?EMA Settings)Timeframe|
|v_input_int_1|200|Length|
|v_input_string_1|0|Type: EMA|SMA|RMA|WMA|
|v_input_source_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_float_1|9|(?Entry Settings)Long Position Entry Trigger|
|v_input_float_2|9|Short Position Entry Trigger|
|v_input_float_3|true|Close Position Trigger|
|v_input_float_4|4|Cancel Unfilled Entries Trigger|
|v_input_bool_1|true|Ladder Into Positions|
|v_input_int_2|4|    Ladder Rungs|
|v_input_float_5|0.5|    Ladder Step (%)|
|v_input_float_6|4|Stop Loss (%)|
|v_input_float_7|true|Start Trailing After (%)|
|v_input_float_8|true|Trail Behind (%)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-19 00:00:00
end: 2023-10-25 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © jordanfray

//@version=5
strategy(title="EMA Mean Reversion Strategy", overlay=true, max_bars_back=5000, default_qty_type=strategy.percent_of_equity, default_qty_value=100,initial_capital=100000, commission_type=strategy.commission.percent, commission_value=0.05, backtest_fill_limits_assumption=2)


// Indenting Classs
indent_1 = " "
indent_2 = "  "
indent_3 = "   "
indent_4 = "    "


// Tooltips
longEntryToolTip = "When the percentage that the price is away from the selected EMA reaches this point, a long postion will open."
shortEntryToolTip = "When the percentage that the price is away from the selected EMA reaches this point, a short postion will open."
closeEntryToolTip = "When the percentage that the price is away from the selected EMA reaches this point, open postion will close."
ladderInToolTip = "Enable this to use the laddering settings below."
cancelEntryToolTip = "When the percentage that the price is away from the selected EMA reaches this point, any unfilled entries will be canceled."

// Group Titles
group_one_title = "EMA Settings"
group_two_title = "Entry Settings"


// Colors
blue = color.new(#00A5FF,0)
lightBlue = color.new(#00A5FF,90)
green = color.new(#2DBD85,0)
gray_80 =  color.new(#7F7F7F,80)
gray_60 =  color.new(#7F7F7F,60)
gray_40 =  color.new(#7F7F7F,40)
white = color.new(#ffffff,0)
red = color.new(#E02A4A,0)
transparent = color.new(#000000,100)


// Strategy Settings
EMAtimeframe = input.timeframe(defval="", title="Timeframe", group=group_one_title)
EMAlength = input.int(defval=200, minval=1, title="Length", group=group_one_title)
EMAtype = input.string(defval="EMA", options = ["EMA", "SMA", "RMA", "WMA"], title="Type", group=group_one_title)
EMAsource = input.source(defval=close, title="Source", group=group_one_title)

openLongEntryAbove = input.float(defval=9, title="Long Position Entry Trigger", tooltip=longEntryToolTip, group=group_two_title)
openEntryEntryAbove = input.float(defval=9, title="Short Position Entry Trigger", tooltip=shortEntryToolTip, group=group_two_title)
closeEntryBelow = input.float(defval=1.0, title="Close Position Trigger", tooltip=closeEntryToolTip, group=group_two_title)
cancelEntryBelow = input.float(defval=4, title="Cancel Unfilled Entries Trigger", tooltip=cancelEntryToolTip, group=group_two_title)

enableLaddering = input.bool(defval=true, title="Ladder Into Positions", tooltip=ladderInToolTip, group=group_two_title)
ladderRungs = input.int(defval=4, minval=2, maxval=4, step=1, title=indent_4+"Ladder Rungs", group=group_two_title)
ladderStep = input.float(defval=.5, title=indent_4+"Ladder Step (%)", step=.1, group=group_two_title)/100
stop_loss_val = input.float(defval=4.0, title="Stop Loss (%)", step=0.1, group=group_two_title)/100
start_trailing_after = input.float(defval=1, title="Start Trailing After (%)", step=0.1, group=group_two_title)/100
trail_behind = input.float(defval=1, title="Trail Behind (%)", step=0.1, group=group_two_title)/100

// Calculate trailing stop values
long_start_trailing_val = strategy.position_avg_price + (strategy.position_avg_price * start_trailing_after)
long_trail_behind_val = close - (strategy.position_avg_price * trail_behind)
long_stop_loss = strategy.position_avg_price * (1.0 - stop_loss_val)
short_start_trailing_val = strategy.position_avg_price - (strategy.position_avg_price * start_trailing_after)
short_trail_behind_val = close + (strategy.position_avg_price * trail_behind)
short_stop_loss = strategy.position_avg_price * (1 + stop_loss_val)


// Calulate EMA
EMA = switch EMAtype
    "EMA" => ta.ema(EMAsource, EMAlength)
    "SMA" => ta.sma(EMAsource, EMAlength)
    "RMA" => ta.rma(EMAsource, EMAlength)
    "WMA" => ta.wma(EMAsource, EMAlength)
    => na
EMA_ = EMAtimeframe == timeframe.period ? EMA : request.security(syminfo.ticker, EMAtimeframe, EMA[1], lookahead = barmerge.lookahead_on)
plot(EMA_, title="EMA", linewidth=2, color=blue, editable=true)

EMA_cloud_upper_band_val = EMA_ + (EMA_ * openLongEntryAbove/100)
EMA_cloud_lower_band_val = EMA_ - (EMA_ * openLongEntryAbove/100)
EMA_cloud_upper_band = plot(EMA_cloud_upper_band_val, title="EMA Cloud Upper Band", color=blue)
EMA_cloud_lower_band = plot(EMA_cloud_lower_band_val, title="EMA Cloud Upper Band", color=blue)
fill(EMA_cloud_upper_band, EMA_cloud_lower_band, editable=false, color=lightBlue)

distance_from_EMA = ((close - EMA_)/close)*100
if distance_from_EMA < 0
    distance_from_EMA := distance_from_EMA * -1

// Calulate Ladder Entries
long_ladder_1_limit_price = close - (close * 1 * ladderStep)
long_ladder_2_limit_price = close - (close * 2 * ladderStep)
long_ladder_3_limit_price = close - (close * 3 * ladderStep)
long_ladder_4_limit_price = close - (close * 4 * ladderStep)

short_ladder_1_limit_price = close + (close * 1 * ladderStep)
short_ladder_2_limit_price = close + (close * 2 * ladderStep)
short_ladder_3_limit_price = close + (close * 3 * ladderStep)
short_ladder_4_limit_price = close + (close * 4 * ladderStep)

var position_qty = strategy.equity/close
if enableLaddering
    position_qty := (strategy.equity/close) / ladderRungs
else
    position_qty := strategy.equity/close
    
plot(position_qty, color=white)
//plot(strategy.equity, color=green)

// Entry Conditions
currently_in_a_postion = strategy.position_size != 0
currently_in_a_long_postion = strategy.position_size > 0
currently_in_a_short_postion = strategy.position_size < 0
average_price = strategy.position_avg_price

bars_since_entry = currently_in_a_postion ? bar_index - strategy.opentrades.entry_bar_index(strategy.opentrades - 1) + 1 : 5
long_run_up = ta.highest(high, bar_index == 0 ? 5000: bars_since_entry)
long_run_up_line = plot(long_run_up, style=plot.style_stepline, editable=false, color=currently_in_a_long_postion ? green : transparent)
start_trailing_long_entry = currently_in_a_long_postion and long_run_up > long_start_trailing_val
long_trailing_stop = start_trailing_long_entry ? long_run_up - (long_run_up * trail_behind) : long_stop_loss
long_trailing_stop_line = plot(long_trailing_stop, style=plot.style_stepline, editable=false, color=currently_in_a_long_postion ? long_trailing_stop > strategy.position_avg_price ? green : red : transparent)

short_run_up = ta.lowest(low, bar_index == 0 ? 5000: bars_since_entry)
short_run_up_line = plot(short_run_up, style=plot.style_stepline, editable=false, color=currently_in_a_short_postion ? green : transparent)
start_trailing_short_entry = currently_in_a_short_postion and short_run_up < short_start_trailing_val
short_trailing_stop = start_trailing_short_entry ? short_run_up + (short_run_up * trail_behind) : short_stop_loss
short_trailing_stop_line = plot(short_trailing_stop, style=plot.style_stepline, editable=false, color=currently_in_a_short_postion ? short_trailing_stop < strategy.position_avg_price ? green : red : transparent)

long_conditions_met = distance_from_EMA > openLongEntryAbove and close < EMA_ and not currently_in_a_postion
short_conditions_met = distance_from_EMA > openEntryEntryAbove and close > EMA_ and not currently_in_a_postion
close_long_entries = distance_from_EMA <= closeEntryBelow or close <= long_trailing_stop
close_short_entries = distance_from_EMA <= closeEntryBelow or close >= short_trailing_stop
cancel_entries = distance_from_EMA <= cancelEntryBelow

plotshape(long_conditions_met ? close : na, style=shape.diamond, title="Long Conditions Met" )
plotshape(short_conditions_met ? close : na, style=shape.diamond, title="Short Conditions Met" )
plot(average_price,style=plot.style_stepline, editable=false, color=currently_in_a_postion ? blue : transparent)

// Long Entry
if enableLaddering
    if ladderRungs == 2
        strategy.entry(id="Long Ladder 1", direction=strategy.long, qty=position_qty, limit=long_ladder_1_limit_price, when=long_conditions_met)
        strategy.entry(id="Long Ladder 2", direction=strategy.long, qty=position_qty, limit=long_ladder_2_limit_price, when=long_conditions_met)
    else if ladderRungs == 3
        strategy.entry(id="Long Ladder 1", direction=strategy.long, qty=position_qty, limit=long_ladder_1_limit_price, when=long_conditions_met)
        strategy.entry(id="Long Ladder 2", direction=strategy.long, qty=position_qty, limit=long_ladder_2_limit_price, when=long_conditions_met)
        strategy.entry(id="Long Ladder 3", direction=strategy.long, qty=position_qty, limit=long_ladder_3_limit_price, when=long_conditions_met)
    else if ladderRungs == 4
        strategy.entry(id="Long Ladder 1", direction=strategy.long, qty=position_qty, limit=long_ladder_1_limit_price, when=long_conditions_met)
        strategy.entry(id="Long Ladder 2", direction=strategy.long, qty=position_qty, limit=long_ladder_2_limit_price, when=long_conditions_met)
        strategy.entry(id="Long Ladder 3", direction=strategy.long, qty=position_qty, limit=long_ladder_3_limit_price, when=long_conditions_met)
        strategy.entry(id="Long Ladder 4", direction=strategy.long, qty=position_qty, limit=long_ladder_4_limit_price, when=long_conditions_met)
    
    strategy.exit(id="Close Long Ladder 1", from_entry="Long Ladder 1", stop=long_trailing_stop, limit=long_trailing_stop, when=close_long_entries)
    strategy.exit(id="Close Long Ladder 2", from_entry="Long Ladder 2", stop=long_trailing_stop, limit=long_trailing_stop, when=close_long_entries)
    strategy.exit(id="Close Long Ladder 3", from_entry="Long Ladder 3", stop=long_trailing_stop, limit=long_trailing_stop, when=close_long_entries)
    strategy.exit(id="Close Long Ladder 4", from_entry="Long Ladder 4", stop=long_trailing_stop, limit=long_trailing_stop, when=close_long_entries)
    
    strategy.cancel(id="Long Ladder 1", when=cancel_entries)
    strategy.cancel(id="Long Ladder 2", when=cancel_entries)
    strategy.cancel(id="Long Ladder 3", when=cancel_entries)
    strategy.cancel(id="Long Ladder 4", when=cancel_entries)
else
    strategy.entry(id="Long", direction=strategy.long, qty=100, when=long_conditions_met)
    strategy.exit(id="Close Long", from_entry="Long", stop=long_stop_loss, limit=EMA_, when=close_long_entries)
    strategy.cancel(id="Long", when=cancel_entries)

// Short Entry
if enableLaddering
    if ladderRungs == 2
        strategy.entry(id="Short Ladder 1", direction=strategy.short, qty=position_qty, limit=short_ladder_1_limit_price, when=short_conditions_met)
        strategy.entry(id="Short Ladder 2", direction=strategy.short, qty=position_qty, limit=short_ladder_2_limit_price, when=short_conditions_met)
    else if ladderRungs == 3
        strategy.entry(id="Short Ladder 1", direction=strategy.short, qty=position_qty, limit=short_ladder_1_limit_price, when=short_conditions_met)
        strategy.entry(id="Short Ladder 2", direction=strategy.short, qty=position_qty, limit=short_ladder_2_limit_price, when=short_conditions_met)
        strategy.entry(id="Short Ladder 3", direction=strategy.short, qty=position_qty, limit=short_ladder_3_limit_price, when=short_conditions_met)
    else if ladderRungs == 4
        strategy.entry(id="Short Ladder 1", direction=strategy.short, qty=position_qty, limit=short_ladder_1_limit_price, when=short_conditions_met)
        strategy.entry(id="Short Ladder 2", direction=strategy.short, qty=position_qty, limit=short_ladder_2_limit_price, when=short_conditions_met)
        strategy.entry(id="Short Ladder 3", direction=strategy.short, qty=position_qty, limit=short_ladder_3_limit_price, when=short_conditions_met)
        strategy.entry(id="Short Ladder 4", direction=strategy.short, qty=position_qty, limit=short_ladder_4_limit_price, when=short_conditions_met)
    
    strategy.exit(id="Close Short Ladder 1", from_entry="Short Ladder 1", stop=short_trailing_stop, limit=EMA_, when=close_short_entries)
    strategy.exit(id="Close Short Ladder 2", from_entry="Short Ladder 2", stop=short_trailing_stop, limit=EMA_, when=close_short_entries)
    strategy.exit(id="Close Short Ladder 3", from_entry="Short Ladder 3", stop=short_trailing_stop, limit=EMA_, when=close_short_entries)
    strategy.exit(id="Close Short Ladder 4", from_entry="Short Ladder 4", stop=short_trailing_stop, limit=EMA_, when=close_short_entries)
    
    strategy.cancel(id="Short Ladder 1", when=cancel_entries)
    strategy.cancel(id="Short Ladder 2", when=cancel_entries)
    strategy.cancel(id="Short Ladder 3", when=cancel_entries)
    strategy.cancel(id="Short Ladder 4", when=cancel_entries)
else
    strategy.entry(id="Short", direction=strategy.short, when=short_conditions_met)
    strategy.exit(id="Close Short", from_entry="Short", limit=EMA_, when=close_short_entries)
    strategy.cancel(id="Short", when=cancel_entries)


```

> Detail

https://www.fmz.com/strategy/430247

> Last Modified

2023-10-26 15:33:50
