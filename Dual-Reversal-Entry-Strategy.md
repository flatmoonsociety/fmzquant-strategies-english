
> Name

Dual-Reversal-Entry-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/b7b3c9ca796a6499b5bc0b8d27acb301a0c0badbaa828c06cdacbfdad059f54b.png)

[trans]


## Overview
The double reversal entry strategy combines the reversal signals of MACD and Stochastic RSI to accurately do long and short positions at the trend reversal point, which is a reversal trading strategy.
## Strategy Principle
The strategy consists of the following components:
1. Use the difference of the MACD indicator to break through the 0 axis offline to determine the trend reversal.
2. Use the Stochastic RSI indicator to determine whether it is overbought or oversold. The Stochastic RSI indicator combines the overbought and oversold principles of the RSI indicator. When the Stochastic RSI is above 70, it is overbought, and below 30 is oversold.
3. When the difference crosses the 0 axis offline (representing a bull reversal signal) and the Stochastic RSI indicator shows oversold, a buy signal is generated; when the difference crosses the 0 axis offline (representing a short reversal signal) and the Stochastic RSI indicator shows overbought, a sell signal is generated.
4. This strategy has both indicator drawing and transaction execution modes. In indicator mode, reversal signals are marked with triangles. In strategy mode, open a long or short position when a reversal signal appears.
By combining the reversal signal of MACD and the overbought and oversold signal of Stochastic RSI, you can improve the accuracy of long and short positions and seize better entry opportunities at trend reversal points.
## Strategic Advantages
- Combined dual indicator filtering to improve the accuracy of long and short positions
The double reversal entry strategy uses a combination of MACD and Stochastic RSI to perform double filtering to ensure that trading signals are generated only after the trend reverses, thus improving the accuracy of long and short positions and reducing the probability of false signals.
- Reversal trading, suitable for bear market conditions
This strategy is a reversal strategy, which mainly opens positions at trend reversal points. This reversal strategy is suitable for the volatile market with frequent rises and falls in the bear market, and can make profits when the trend reverses at each small level.
- No need to judge the trend direction, suitable for novices
The double reversal entry strategy does not require pre-judgment of the direction of the general trend, but places orders directly when the local reversal occurs. It is simple and easy to use, and is suitable for novices to learn and use.
- Flexible choice of strategy mode or indicator mode
This strategy can flexibly select strategy mode or indicator mode through a switch, making it more flexible to use. Indicator mode can be used for observation and analysis, and strategy mode can automatically execute transactions.
## Strategy Risk
- Reversal strategy, higher risk
Since reversal trading does not consider the direction of the general trend, the risk of trading is greater in big rises and falls, and the probability of losses for continuous reverse openings is high. A combination of trend trading strategies is needed to reduce risk.
-Double indicator combination makes parameter optimization more difficult
Since this strategy uses two indicators and multiple parameters, it is difficult to optimize the parameter combination. Inappropriate parameter combinations may lead to frequent transactions or insufficient signals. It requires sufficient repeated testing and optimization.
- High frequency trading account required
The double reversal admission strategy is a high-frequency trading strategy and requires the support of a trading account with high handling fees and low spreads, otherwise transaction fees may offset most of the profits.
## Strategy optimization direction
- Optimize indicator parameter combinations
You can try different parameter combinations to find the best MACD and Stochastic RSI parameters to make your trading signals more accurate. For example, you can optimize the fast and slow moving average periods of MACD, the lookback period of Stochastic, etc.
- Integrate trend filtering
Trend indicators can be added to the strategy, and reversal signals will only be considered when the trend direction is consistent to avoid counter-trend trading. For example, combine the MA indicator to determine the long-term trend.
- Add stop loss mechanism
You can set a trailing stop loss or a percentage stop loss to control a single loss. You can also consider adding reverse positions to optimize the efficiency of capital use.
- Optimize entry conditions
In addition to reversal signals, other entry conditions can be strengthened, such as amplification of trading volume, breakthrough of a certain moving average, etc., to reduce the false alarm rate of entry.
## Summarize
The dual reversal entry strategy uses a combination of dual indicators to determine the local reversal point to open a position and place orders. The idea is novel and reliable. It is suitable for the market environment of frequent bear market fluctuations and is also suitable for novices to practice repeated backtesting. However, this strategy has higher risks and requires full testing of optimization parameters, supplemented by trend judgment and risk control mechanisms, in order to achieve stable profits in real trading.
||

## Overview

The Dual Reversal Entry strategy generates entries by combining reversal signals from the MACD and Stochastic RSI indicators to accurately go long and short at trend reversal points. It belongs to the class of reversal trading strategies.

## Strategy Logic

The strategy consists of the following components:

1. Using the MACD indicator's crossover of the zero line to determine trend reversal. 

2. Using the Stochastic RSI indicator to identify overbought and oversold conditions. Stochastic RSI combines RSI overbought/oversold principles, above 70 is overbought and below 30 is oversold.

3. When the MACD line crosses above zero (bullish reversal signal) and Stochastic RSI shows oversold, a buy signal is generated. When the MACD line crosses below zero (bearish reversal signal) and Stochastic RSI shows overbought, a sell signal is generated.

4. The strategy has both indicator plotting mode and execution mode. In indicator mode, reversal signals are marked with triangles. In strategy mode, long/short positions are opened on reversal signals.

Combining the MACD reversal signal with Stochastic RSI overbought/oversold levels improves the accuracy of entries. It provides good timing for entries at trend reversal points. 

## Advantages

- Dual indicator filtering improves entry accuracy

The dual reversal filters ensure entries are taken only after trend reversal, reducing false signals and improving entry accuracy.

- Reversal trading works for choppy/ranging markets 

As a reversal strategy, it excels in choppy bear market conditions with frequent ups and downs and allows winning trades at each minor swing reversal.

- Beginner friendly without trend bias 

It directly trades all reversals without the need to determine the major trend, simple to use for beginners.

- Flexible indicator or strategy modes

The modes allow flexible usage for analysis or automated executions.

## Risks

- Higher risk of reversal trading 

Without considering major trend, reversal trading has higher risk in strong trending markets, with likely consecutive losses opening countertrend. Need to combine with trend strategies.

- Difficult multi-parameter optimization

The multiple parameters of dual indicators make optimization challenging. Inappropriate parameters may cause over-trading or insufficient signals. Requires extensive testing.

- Requires high-frequency trading account

The high-frequency strategy needs low-cost trading accounts to support, otherwise fees may offset profits.

## Enhancement Opportunities

- Optimize indicator parameters

Testing different parameter combinations to find the optimal settings for reliable signals. E.g. MACD periods, Stochastic lookback.

- Add trend filter 

Adding a trend indicator and taking reversal signals only in trend direction avoids counter-trend trades. E.g. using MA to determine long-term trend.

- Implement stop loss

Adding stop loss by price or percentage to control risk on trades. Consider partial profit taking and adding to loser.

- Tighten entry conditions 

Additional entry filters like volume spike or crossing moving average to reduce false entries.

## Conclusion

The dual reversal entry strategy provides a novel and reliable approach to trade local reversals. It excels in choppy bear market conditions but has higher risks. Extensive optimization, trend filters and risk controls are needed to profit consistently when live trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_bool_1|true|Strategy Mode|
|v_input_1|12|MACD Fast Period|
|v_input_2|26|MACD Slow Period|
|v_input_3|9|MACD Signal Period|
|v_input_4|70|Stochastic RSI Period|
|v_input_5|30|%K Period|
|v_input_6|30|%D Period|
|v_input_7|70|Stochastic Overbought Level|
|v_input_8|30|Stochastic Oversold Level|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-06 00:00:00
end: 2023-11-12 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy('RB Reversal Tabs Strategy', overlay=true)
//Developer: Andrew Palladino
//Owner: Rob Booker
//Date Modified: 11/25/2018
//Updated to Pinescript V5 and transformed into a Strategy by: Powerscooter	11/25/2022

StrategyMode = input.bool(true,"Strategy Mode")
macd_fast_period = input(title='MACD Fast Period', defval=12)
macd_slow_period = input(title='MACD Slow Period', defval=26)
macd_signal_period = input(title='MACD Signal Period', defval=9)
stoch_period = input(title='Stochastic RSI Period', defval=70)
prc_k_period = input(title='%K Period', defval=30)
prc_d_period = input(title='%D Period', defval=30)
stoch_ob = input(title='Stochastic Overbought Level', defval=70)
stoch_os = input(title='Stochastic Oversold Level', defval=30)

[macd_line, signal_line, hist_line] = ta.macd(close, macd_fast_period, macd_slow_period, macd_signal_period)

fast_prc_k = 100 * (close - ta.lowest(low, stoch_period)) / (ta.highest(high, stoch_period) - ta.lowest(low, stoch_period))
fast_prc_d = ta.sma(fast_prc_k, prc_d_period)

slow_prc_k = ta.sma(fast_prc_k, prc_k_period)
slow_prc_d = ta.sma(slow_prc_k, prc_d_period)

full_prc_k = ta.sma(fast_prc_k, prc_k_period)
full_prc_d = ta.sma(full_prc_k, prc_d_period)

is_buy_reversal = ta.crossover(macd_line, 0) and full_prc_k < stoch_os
is_sell_reversal = ta.crossunder(macd_line, 0) and full_prc_k > stoch_ob

plotshape(is_buy_reversal and not StrategyMode, style=shape.triangleup, color=color.new(color.green, 0), size=size.small, location=location.belowbar)
plotshape(is_sell_reversal and not StrategyMode, style=shape.triangledown, color=color.new(color.red, 0), size=size.small, location=location.abovebar)

//Orders
if is_buy_reversal and StrategyMode
	strategy.entry("Long",strategy.long)
if is_sell_reversal and StrategyMode
	strategy.entry("Short",strategy.short)
//plot(full_prc_k, color=blue)
//plot(full_prc_d, color=red)
//plot(macd_line, color=blue)
```

> Detail

https://www.fmz.com/strategy/431971

> Last Modified

2023-11-13 17:56:24
