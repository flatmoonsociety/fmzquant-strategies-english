
> Name

Swing-Trading-Strategy Swing-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
This is a trend following strategy based on moving average crossovers, combined with stop-loss and take-profit management and leverage, designed to identify trends in a variety of markets and maximize profits.
## Strategy Principle
This strategy uses the crossover of a fast moving average and a slow moving average as a trading signal. When the fast moving average crosses the slow moving average, take a long position; when the fast moving average crosses below the slow moving average, take a short position.
In order to filter out noise trades that are not in the main trend, the strategy also introduces the 200-day moving average as a trend filter. Trading signals are only issued when the price is above or below the 200-day moving average.
The strategy adopts a range trading stop loss strategy. After the transaction, a fixed ratio of stop loss and take profit levels will be set. For example, stop loss is set to 1% and take profit is 1%. When the price hits the stop loss or take profit price, the position will be closed.
In order to amplify trading profits, the strategy uses leverage. According to the characteristics of different markets, an appropriate leverage ratio can be selected, such as 10 times leverage.
## Advantage Analysis
- One of the advantages of the strategy is that it can identify trends in a variety of markets, including cryptocurrency, stock and futures markets, expanding the applicability of the strategy.
- Applying fast and slow moving average crossovers and trend filtering can better identify the trend direction and obtain a better winning rate in trending markets.
- Using the interval stop-loss and take-profit strategy can control single losses within a tolerable range, which is conducive to the stable operation of the strategy.
- The leverage effect can amplify trading profits, thereby making full use of the advantages of the strategy.
- Visual interface design, using different background colors to identify long and short markets, users can intuitively judge the current market situation.
## Risk Analysis
- The strategy is based on trend trading ideas, and the trading effect will be compromised in a volatile market. Position size should be appropriately controlled.
- There is a risk of arbitrage with a fixed proportion of stop loss and take profit, and the stop loss and take profit range should be adjusted according to the specific market.
- Leverage magnifies the size of the transaction and also magnifies the risk of the transaction. Leverage ratio needs to be controlled to avoid exceeding the acceptable loss range.
- The moving average itself has hysteresis, and there may be a delay in trading signals.
## Optimization direction
- You can study the strategy performance under different parameter combinations and select the faster and slower moving average lengths with better parameter combinations.
- Can be combined with other indicators or models as filter signals to improve strategy accuracy. For example, introduce ATR stop loss, RSI indicator, etc.
- You can study trend identification indicators, such as DC indicators, etc., to further enhance the strategy's ability to judge trends.
- Can be combined with machine learning models to optimize strategic signals and identify more effective trading opportunities.
- You can consider dynamically adjusting the stop loss and take profit range, and set a more reasonable stop loss and take profit based on volatility and market conditions.

## Summarize
This strategy adopts a more scientific and systematic trend tracking method as a whole, supplemented by stop-loss, take-profit and leverage to control risks and amplify returns. This strategy can be widely applied to a variety of markets and is expected to obtain stable excess returns. However, it is still necessary to pay attention to parameter optimization, risk control and strategy updates in order to operate effectively in the long term.
||


## Overview

This is a trend-following strategy based on moving average crossover, combined with stop loss/take profit management and leverage effect, aiming to identify trends across multiple markets and maximize profits.

## Strategy Logic

The strategy uses crossover of fast and slow moving averages as trading signals. It goes long when the fast MA crosses above the slow MA, and goes short when the fast MA crosses below the slow MA.

To filter out noise trades from minor trends, it also uses a 200-day MA as a trend filter. Trade signals are only generated when the price is above or below the 200-day MA.

The strategy uses range trading stops. After entry, fixed percentage stop loss and take profit levels are set, e.g. 1% stop loss and 1% take profit. Positions will be closed when price hits the stop loss or take profit.

Leverage effect is employed to amplify trading profits. Based on different market characteristics, appropriate leverage ratios can be selected, e.g. 10x.

## Advantage Analysis 

- One advantage is that it can identify trends across multiple markets including crypto, stocks and futures, making the strategy widely applicable.

- Using fast/slow MA crossover and trend filter can better identify trend direction and achieve good win rate in trending markets.

- Range trading stops help control single trade loss within bearable range, allowing stable running of the strategy. 

- Leverage effect amplifies trading profits, making full use of the strategy edge.

- Visual interface design with different background colors for bull/bear markets offers intuitive market insight.

## Risk Analysis

- The strategy is trend-following so may underperform in choppy, range-bound markets. Position sizing should be controlled.

- Fixed percentage stop loss/take profit carries risk of getting stopped out. Levels should be adjusted based on specific market volatility.

- Leverage amplifies position size as well as risks. Leverage ratio should be controlled to avoid oversized losses.

- Lagging nature of moving averages may cause delayed trade signals.

## Optimization Directions

- Test different parameter combinations and select optimal fast/slow MA lengths.

- Incorporate other indicators or models as filter signals to improve accuracy, e.g. ATR stops, RSI etc.

- Research other trend identification tools like ADX to further enhance trend capturing ability.

- Use machine learning models to optimize strategy signals and find more effective entry/exit points.

- Consider dynamic stop loss/take profit based on volatility and market conditions for more sensible stops.

## Summary

The strategy employs a systematic trend-following approach and uses stops/take profit and leverage to control risk and magnify profits. It is widely applicable across markets with potential for steady alpha. Attention should still be paid to parameter optimization, risk control and strategy iteration for long-term success.

[/trans]


> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0|Source MA Type: EMA|SMA|
|v_input_2|50|Source MA Length|
|v_input_3|20|Fast MA Length|
|v_input_4|50|Slow MA Length|
|v_input_5|true|Trend Filter|
|v_input_6|0|Trend Filter MA Type: EMA|SMA|
|v_input_7|200|Trend Filter MA Period|
|v_input_8|true|Show MAs|
|v_input_9|false|Swing Trading|
|v_input_10|true|(?Backtest Control)Stop Loss (in %)|
|v_input_11|true|Take Profit (in %)|
|v_input_12|10|Leverage|
|v_input_13|timestamp(2021 01 01)|Backtest Start Time|
|v_input_14|timestamp(2021 12 31)|Backtest End Time|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-10 00:00:00
end: 2023-10-10 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

////////////////////////////////////////////////////////////////////////////////
// Bozz Strategy
// Developed for Godstime
// Version 1.1
// 11/28/2021
////////////////////////////////////////////////////////////////////////////////

//@version=4
// strategy("Bozz Strategy", "", true, default_qty_type=strategy.percent_of_equity, default_qty_value=100, margin_long=0, margin_short=0)

// ----------------------------- Inputs ------------------------------------- //
source_ma_type = input("EMA", "Source MA Type", options=["SMA", "EMA"])
source_ma_length = input(50, "Source MA Length")
fast_ma_length = input(20, "Fast MA Length")
slow_ma_length = input(50, "Slow MA Length")
use_trend_filter = input(true, "Trend Filter")
trend_filter_ma_type = input("EMA", "Trend Filter MA Type", options=["SMA", "EMA"])
trend_filter_ma_length = input(200, "Trend Filter MA Period")
show_mas = input(true, "Show MAs")
swing_trading_mode = input(false, "Swing Trading")

// -------------------------- Calculations ---------------------------------- //
fast_ma = ema(close, fast_ma_length)
slow_ma = ema(close, slow_ma_length)
source_ma = source_ma_type == "EMA"? ema(close, source_ma_length): 
                                     sma(close, source_ma_length)
trend_filter_ma = trend_filter_ma_type == "EMA"? ema(close, trend_filter_ma_length): 
                                                 sma(close, trend_filter_ma_length)

// --------------------------- Conditions ----------------------------------- //
uptrend = not use_trend_filter or close > trend_filter_ma
buy_cond = crossover(fast_ma, slow_ma) and uptrend

downtrend = not use_trend_filter or close < trend_filter_ma
sell_cond = crossunder(fast_ma, slow_ma) and downtrend

// ---------------------------- Plotting ------------------------------------ //
bgcolor(use_trend_filter and downtrend? color.red: use_trend_filter? color.green: na)
plot(show_mas? fast_ma: na, "Fast MA", color.green)
plot(show_mas? slow_ma: na, "Slow MA", color.red)
plot(show_mas? source_ma: na, "Source MA", color.purple)
plot(show_mas? trend_filter_ma: na, "Trend Filter MA", color.blue)


// ---------------------------- Trading  ------------------------------------ //
// Inputs
sl_perc = input(1.0, "Stop Loss (in %)", group="Backtest Control")/100
tp_perc = input(1.0, "Take Profit (in %)", group="Backtest Control")/100
leverage = input(10, "Leverage", maxval=100, group="Backtest Control")
bt_start_time = input(timestamp("2021 01 01"), "Backtest Start Time", input.time, group="Backtest Control")
bt_end_time = input(timestamp("2021 12 31"), "Backtest End Time", input.time, group="Backtest Control")

// Trading Window
in_trading_window = true
trade_qty = (strategy.equity * leverage) / close 

// Long Side
strategy.entry("Long Entry", strategy.long,  when=buy_cond and in_trading_window)
long_tp = strategy.position_avg_price * (1 + tp_perc)
long_sl = strategy.position_avg_price * (1 - sl_perc)
if not swing_trading_mode
    strategy.exit("Long Exit", "Long Entry", limit=long_tp, stop=long_sl)

// Short Side
strategy.entry("Short Entry", strategy.short, when=sell_cond and in_trading_window)
short_tp = strategy.position_avg_price * (1 - tp_perc)
short_sl = strategy.position_avg_price * (1 + sl_perc)
if not swing_trading_mode
    strategy.exit("Short Exit", "Short Entry", limit=short_tp, stop=short_sl)

// End of trading window close
strategy.close_all(when=not in_trading_window)
```

> Detail

https://www.fmz.com/strategy/428985

> Last Modified

2023-10-11 16:29:37
