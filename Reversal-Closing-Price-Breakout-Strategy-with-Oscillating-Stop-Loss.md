
> Name

Reversal-Closing-Price-Breakout-Strategy-with-Oscillating-Stop-Loss
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/062409bf8453fa9e8e5779f4e2bb6e26a6773c18d8d806863523a11ccfd70f4e.png)
[trans]

### Overview
This strategy uses the price pattern signal of resistance breakthrough and the risk control mechanism of circular stop loss. It will open a long position after breaking through the resistance level, and open a short position after breaking through the support level. At the same time, set up circular stop loss and stop loss to effectively control risks.
### Strategy Principles
This strategy is mainly based on the following points:
1. Use moving averages to determine trend direction. The fast and slow moving averages are set in the strategy. If the fast moving average crosses the slow moving average, it means long-term bullishness, and if it crosses below, it means long-term bearishness.
2. Resistance breakthrough is a long signal. When the price rises and breaks through the recent high, it is regarded as a signal to break through the resistance level and enter the market long.
3. Support breakout short signal. When the price falls and breaks through the recent low, it is regarded as a signal of breaking through the support level and short entry is made.
4. Set up a circular stop loss. Set a stop loss line after entering the market and adjust it as the price fluctuates so that the stop loss line moves around the price.
5. Stop loss and take profit exit. Stop-loss exit can effectively control risks, and stop-profit exit can lock in profits.
Specifically, this strategy uses the average of high and low prices as the price source, and calculates the fast and slow EMA to determine the trend direction. When the fast line crosses the slow line and a resistance breakthrough signal appears, go long; when the fast line crosses the slow line and a support breakthrough signal appears, go short. After entering the market, use the lowest price within a certain period as the stop loss level, adjust it as the price rises, and set a take profit line to lock in profits. Effectively control risks while gaining profits from trends.
### Advantage Analysis
This strategy has several advantages:
1. Stable profits. By following the trend, you can make profits in the long-term trend at the exponential level.
2. Good risk control. Set up circular stop loss and stop loss to stop loss and exit in time.
3. The signal is accurate. Go long when the resistance level breaks out and go short when the support level breaks out. The signals are accurate and reliable.
4. Simple and easy to operate. The indicators and signal rules are simple and clear, and the parameter settings are not complicated.
5. Adapt to the market. Able to operate on different varieties and under any market conditions.
### Risk Analysis
There are also some risks to be aware of with this strategy:
1. Risk of breakthrough failure. A pullback and retry may occur after the resistance support level is broken, resulting in a stop loss.
2. Parameter optimization risks. Improper parameter settings may result in frequent or insufficient signals. The optimization process requires caution.
3. Risk of indicator failure. Under special market conditions, the EMA indicator may become invalid or delayed.
4. Trend reversal risk. When the long and short direction deviates from the market, losses may increase.
These risks can be controlled and mitigated to a large extent through parameter optimization, appropriately wide stop loss, strict follow-up of signals, etc.
### Optimization direction
This strategy can be further optimized from the following aspects:
1. Time cycle optimization. Adjust the time period parameters for calculating moving averages and price patterns to find the best combination.
2. Optimization of variety adaptability. Adjust parameter settings according to the characteristics of different varieties.
3. Optimize stop loss strategy. Use more stable and accurate stop loss methods, such as trailing stop loss, oscillating stop loss, etc.
4. Optimize the profit-taking strategy. Set up a moving take-profit or an exponential take-profit to maximize profits.
5. Add filter conditions. Add filtering conditions such as trading volume and volatility to eliminate false breakthroughs.
6. Enhance entry signals. Add more indicators or patterns as confirmation of entry signals.
### Summarize
The overall operation of this strategy is smooth, the core idea is clear, and it has strong stability and profitability. Risk control and indicator application are also relatively appropriate, and it is a breakthrough quantitative strategy worth using. Subsequent optimization of parameters and modules can make the strategy more perfect and adaptable to more varieties and complex market environments.
|| 

### Overview  

This strategy utilizes the price breakout signals and oscillating stop loss mechanism for risk management. It goes long when price breaks out the resistance and goes short when price breaks the support. At the same time, oscillating stop loss and profit taking stops are applied for better risk control.

### Strategy Logic

The strategy is based on the following key points:

1. Using MA to determine the trend direction. Fast and slow MAs are plotted, fast MA crossing above slow MA signals bull trend, while crossing below signals bear trend.

2. Resistance breakout long signal. When price surges and breaks recent swing high, it is considered breaking resistance level, going long. 

3. Support breakout short signal. When price drops and breaks recent swing low, it is considered breaking support level, going short.

4. Oscillating stop loss. After entry, stop loss line is set and keeps adjusting based on price fluctuation, forming an oscillating stop loss mechanism.

5. Stop loss and take profit exit. Stop loss exit controls risk, take profit lock in gains.

Specifically, it uses the average of high and low prices as the source, plots fast and slow EMAs to determine trends. When fast EMA goes above slow EMA and resistance breakout signal emerges, it goes long. When fast EMA drops below slow EMA and support breakout shows up, it goes short. After entry, the lowest price in certain periods is set as the stop loss line, keeps adjusting as price rises. Take profit line is plotted to lock in gains. The strategy effectively controls risk meanwhile profit from trends.

### Advantage Analysis

The advantages of this strategy include:

1. Steady profitability. Following trends can make stable gains from long-term trends.  

2. Excellent risk control. Oscillating stop and protective stop quickly cut losses.

3. Accurate signals. Resistance breakout long and support breakout short provide reliable signals.  

4. Simple rules. Indicators and signals are straightforward, easy to follow.

5. Market adaptive. Works well across different products and market conditions.

### Risk Analysis  

Some risks to note for this strategy:

1. Breakout failure risk. Price may have throwback or pullback after initial breakout, triggering stop loss.

2. Parameter optimization risk. Bad parameter tuning leads to too many or too few signals. Optimization needs prudence.

3. Indicator failure risk. In extreme conditions, EMAs may stop working or lag behind price. 

4. Trend reversal risk. Holding position against trend brings accumulating losses when trend reverses.

Proper parameter tuning, wide stop loss, strictly following rules can largely mitigate above risks.

### Optimization Directions

The strategy can be further improved from the following aspects:

1. Timeframe optimization. Adjust calculation periods of MAs and price patterns, find best combinations.

2. Adaptability optimization. Tune parameters for different products. 

3. Stop loss optimization. Test more advanced stop loss methods like trailing stop, Chandelier stop.

4. Take profit optimization. Adopt adaptive or exponential profit taking exits for better reward.

5. Add filters. Add volume, volatility filters to avoid false breakouts.

6. Enhance entry signals. Combine more indicators or patterns to confirm entries.


### Conclusion
This is an effective breakout strategy with good risk control, stable profit model and straightforward logic flow. Fine-tuning and modular enhancement can make it more robust and adaptive to complex markets. It has great application potentials across more products.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_hl2|0|Price source: hl2|high|low|open|close|hlc3|hlcc4|ohlc4|
|v_input_2|0|Order direction: Both|Long|Short|
|v_input_3|80|EMA long period|
|v_input_4|8|EMA short period|
|v_input_5|2|Risk to reward ratio|
|v_input_6|3|Stoploss candle lookback|
|v_input_7|true|Close if EMA crosses in oposite direction|
|v_input_8|true|Allow price retracing|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-03 00:00:00
end: 2023-12-10 00:00:00
period: 30m
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © EduardoMattje

//@version=4
strategy("Reversal closing price", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=10, initial_capital=10000)

src = input(hl2, "Price source")
order_direction = input("Both", "Order direction", options=["Both", "Long", "Short"])

// EMA calculation and plot

ema_long_period = input(80, "EMA long period")
ema_short_period = input(8, "EMA short period")
ema_long = ema(src, ema_long_period)
ema_short = ema(src, ema_short_period)
ema_bull = ema_short > ema_long
ema_bear = ema_short < ema_long
plot(ema_long, "EMA long", ema_bull ? color.green : color.red, 3)
plot(ema_short, "EMA short", ema_bull ? color.green : color.red, 3)

// Settings

risk_reward_ratio = input(2.0, "Risk to reward ratio", minval=1.0, step=0.1)
stop_lookback = input(3, "Stoploss candle lookback", minval=1)
ema_cross_stop = input(true, "Close if EMA crosses in oposite direction")
allow_retracing = input(true, "Allow price retracing")

// RCP calculation

rcp_bull = low[0] < low[1] and low[0] < low[2] and close[0] > close[1]
rcp_bear = high[0] > high[1] and high[0] > high[2] and close[0] < close[1]

// Order placement

in_market = strategy.position_size != 0

long_condition = rcp_bull and ema_bull and not in_market and order_direction != "Short"
short_condition = rcp_bear and ema_bear and not in_market and order_direction != "Long"

bought = strategy.position_size[0] > strategy.position_size[1] and strategy.position_size[1] == 0
sold = strategy.position_size[0] < strategy.position_size[1] and strategy.position_size[1] == 0
closed = not in_market and in_market[1]

long_position = strategy.position_size > 0
short_position = strategy.position_size < 0

buy_price = high + syminfo.mintick
sell_price = low - syminfo.mintick

if long_condition
    strategy.entry("Long", true, stop=buy_price)
if short_condition
    strategy.entry("Short", false, stop=sell_price)
    
if allow_retracing
    better_price_long = barssince(closed) > barssince(long_condition) and barssince(long_condition) >= 1 and not in_market and ema_bull and buy_price < valuewhen(long_condition, buy_price, 0) and buy_price[0] < buy_price[1]
    if better_price_long
        strategy.cancel("Long")
        strategy.entry("Long", true, stop=buy_price)
    
    better_price_short = barssince(closed) > barssince(short_condition) and barssince(short_condition) >= 1 and not in_market and ema_bear and sell_price > valuewhen(short_condition, sell_price, 0) and sell_price[0] > sell_price[1]
    if better_price_short
        strategy.cancel("Short")
        strategy.entry("Short", false, stop=sell_price)

// Stoploss orders

stop_price = long_position ? valuewhen(bought, lowest(stop_lookback)[1] - syminfo.mintick, 0) : short_position ? valuewhen(sold, highest(3)[1] + syminfo.mintick, 0) : na
stop_comment = "Stoploss triggered"
strategy.close("Long", low <= stop_price, stop_comment)
strategy.close("Short", high >= stop_price, stop_comment)
plot(stop_price, "Stop price", color.red, 2, plot.style_linebr)

// EMA cross close orders

if ema_cross_stop
    if long_position and ema_bear
        strategy.close("Long", comment=stop_comment)
    if short_position and ema_bull
        strategy.close("Short", comment=stop_comment)

// Take profit orders

stop_ticks = abs(strategy.position_avg_price - stop_price)
take_profit_price = long_position ? valuewhen(bought, strategy.position_avg_price + stop_ticks * risk_reward_ratio, 0) : short_position ? valuewhen(sold, strategy.position_avg_price  - (stop_ticks * risk_reward_ratio), 0) : na
target_comment = "Take profit"
strategy.close("Long", high >= take_profit_price, target_comment)
strategy.close("Short", low <= take_profit_price, target_comment)
plot(take_profit_price, "Target price", color.green, 2, plot.style_linebr)

```

> Detail

https://www.fmz.com/strategy/434959

> Last Modified

2023-12-11 11:44:49
