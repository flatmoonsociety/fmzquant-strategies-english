
> Name

Simple-Momentum-Strategy-Based-on-SMA-EMA-and-Volume
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/3402cd830e0045ee891a6f47edffbc85ba1fd9047c2bfdf17e684cf637f489ac.png)

[trans]

### Overview
This strategy is a simple intraday momentum strategy that is not short (only long, not short). It uses SMA, EMA, and volume indicators to try to enter the market at the best time (i.e. when price and momentum are rising at the same time). Its advantage is that it is simple to implement and has certain ability to identify trends.
### Strategy Principles
The transaction Einty signal generation logic of this strategy is: when the SMA indicator is higher than the EMA indicator and 3 consecutive K lines or 4 consecutive K lines form an upward trend, and the lowest price of the middle K line is higher than the opening price of the rising K line, an Entry signal is generated.
The Exit signal generation logic is: when the SMA indicator crosses the EMA indicator, an Exit signal is generated.
This strategy only goes long, not short. Its Entry and Exit logic has certain ability to identify the continued upward trend.
### Advantage Analysis
This strategy has the following advantages:
1. The strategy logic is simple and easy to understand and implement;
2. It uses common technical indicators such as SMA, EMA and trading volume, and the parameters can be adjusted flexibly;
3. Have a certain ability to identify the continuing upward trend and be able to seize some opportunities in the trend.
### Risk Analysis
This strategy also has the following risks:
1. Unable to identify a downward or consolidating market, which may lead to a larger retracement;
2. Unable to take advantage of short-selling opportunities, unable to hedge against recessionary trends, and may miss better profit opportunities;
3. The trading volume indicator does not work well for high-frequency data, and parameters need to be adjusted;
4. Stop loss can be used to control risks.
### Optimization direction
This strategy can be optimized from the following aspects:
1. Increase short trading opportunities, realize long and short two-way trading, and take advantage of recessionary trends for arbitrage;
2. Use more advanced indicators such as MACD, RSI and other combination strategies to improve your ability to judge trends;
3. Optimize stop loss logic and reduce retracement risk;
4. Adjust parameters, test data of different periods, and find the best parameter combination.
### Summarize
Overall, this strategy is a very simple trend following strategy that uses SMA, EMA and volume indicators to determine entry timing. Its advantage is that it is simple and easy to implement, and is suitable for entry-level learning, but it cannot identify consolidation and downward trends, and there are certain risks. Improvements can be obtained by introducing short positions, optimizing indicators and stops.
||


### Overview

This is a simple intraday momentum strategy that only goes long and does not short. It utilizes SMA, EMA and volume indicators to attempt entering the market at the optimal timing when both price and momentum are trending up. Its advantage is being simple while having some trend recognition capability.

### Strategy Principle  

The entry signal logic is: when SMA is higher than EMA, and there is a consecutive 3-bar or 4-bar uptrend pattern, with the lowest price of the middle bars being higher than the open price of the starter uptrend bar, an entry signal is generated.  

The exit signal logic is: when SMA crosses below EMA, an exit signal is generated.

This strategy only goes long and does not short. Its entry and exit logic has some capability in recognizing persistent uptrends.

### Advantage Analysis

The advantages of this strategy:

1. The logic is simple and easy to understand and implement;

2. Utilizes common technical indicators like SMA, EMA and volume for flexibility in parameter tuning;  

3. Has some capability in catching some opportunities during persistent uptrends.

### Risk Analysis  

The risks of this strategy:

1. Inability to detect downtrends or consolidation markets, leading to large drawdowns;

2. Inability to utilize shorting opportunities, unable to hedge against downtrends, missing good profit chances;

3. Volume indicator does not work well on high frequency data, parameters need adjustment;  

4. Can use stop loss to control risks.

### Optimization Directions   

This strategy can be optimized in the following aspects:

1. Adding shorting capability for mean reversion opportunities;  

2. Using more advanced indicators like MACD and RSI for better trend detection;

3. Optimizing stop loss logic to reduce drawdowns;

4. Tuning parameters and testing different timeframes to find optimal parameter sets.


### Conclusion  

In summary this is a very simple trend following strategy utilizing SMA, EMA and volume for entry timing. Its advantage is being simple and easy to implement, good for beginners to learn, but it cannot detect consolidation or downtrends and has risks. Improvements can be made by introducing shorting, optimizing indicators and stop loss etc.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|SMA (small length)|
|v_input_2|20|EMA (large length)|
|v_input_3|10|Volume Trigger|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-07 00:00:00
end: 2023-12-02 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © slip_stream

//@version=4

// Simple strategy for riding the momentum and optimising the timings of truer/longer price moves upwards for an long posistions on a daily basis (can be used, but with less effect
// on other time frames. Volume settings would have to be adjusted by the user accordingly. (short positions are not used).
// This strategy has default settings of a short(er) SMA of 10, a long(er) EMA of 20, and Volume trigger of 10 units and above. All these settings can be changed by the user
// using the GUI settings and not having to change the script.

// The strategy will only open a long position when there is a clear indication that price momentum is upwards through the SMA moving and remaining above the EMA (mandatory) and price period indicators
// of either 1) a standard 3 bar movement upwards, 2) a standard but "aggressive" 3 or 4 bar play where the low of the middle resting bars can be equal to or higher than (i.e. not
// the more standard low of about half) of the opening of the ignition bar. The "aggression" of the 3/4 bar play was done in order to counteract the conservatisme of having a mandatory
// SMA remaining higher than the EMA (this would have to be changed in the script by the user if they want to optimise to their own specifications. However, be warned, all programmatic
// settings for the maximum acceptable low of the middle resting bars runs a risk of ignoring good entry points due to the low being minutely e.g. 0.01%, lower than the user defined setting)


strategy(title = "Simple Momentum Strategy Based on SMA, EMA and Volume", overlay = true, pyramiding = 1, initial_capital = 100000, currency = currency.USD)


// Obtain inputs
sma_length = input(defval = 10, minval=1, type = input.integer, title = "SMA (small length)")
ema_length = input(defval = 20,minval=1, type = input.integer, title = "EMA (large length)")
volume_trigger = input(defval = 10, title = "Volume Trigger", type = input.integer)
sma_line = sma(close, sma_length)
ema_line = ema(close, ema_length)


// plot SMA and EMA lines with a cross for when they intersect
plot(sma_line, color = #8b0000, title = "SMA")
plot(ema_line, color = #e3d024, title = "EMA")
plot(cross(sma_line, ema_line) ? sma_line : na, style = plot.style_cross, linewidth = 4, color = color.white)


// Create variables
// variables to check if trade should be entered
//three consecutive bar bar moves upwards and volume of at least one bar is more than 10
enter_trade_3_bar_up = sma_line > ema_line and close[1] >= close [2] and close[3] >= close[4] and close[2] >= close[3] and (volume[1] >= volume_trigger or volume[2] >= volume_trigger or volume[3] >= volume_trigger)
// aggressive three bar play that ensures the low of the middle bar is equal to or greater than the open of the instigator bar. Volume is not taken into consideration (i.e. aggressive/risky)
enter_3_bar_play = sma_line > ema_line and close[1] > close[3] and low[2] >= open[3]
// aggressive four bar play similar to the 3 bar play above
enter_4_bar_play = sma_line > ema_line and close[1] > close[4] and low[2] >= open[4]
trade_entry_criteria = enter_trade_3_bar_up or enter_3_bar_play or enter_4_bar_play // has one of the trade entry criterias returned true?

// exit criteria for the trade: when the sma line goes under the ema line
trade_exit_criteria = crossunder (sma_line, ema_line)


if (year >= 2019)
    strategy.entry(id = "long", long = true, qty = 1, when = trade_entry_criteria)
    strategy.close(id = "long", when = trade_exit_criteria, qty = 1)
    // for when you want to brute force close all open positions: strategy.close_all (when = trade_exit_criteria)
```

> Detail

https://www.fmz.com/strategy/434676

> Last Modified

2023-12-08 11:15:30
