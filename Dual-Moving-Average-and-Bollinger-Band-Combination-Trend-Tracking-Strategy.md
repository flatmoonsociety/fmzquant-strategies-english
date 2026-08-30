
> Name

Dual-Moving-Average-and-Bollinger-Band-Combination-Trend-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/9a2f80880af9c66343.png)
[trans]
## Overview
This strategy combines multiple technical indicators such as double moving averages, relative strength indicator (RSI) and Bollinger Bands, and constructs buy and sell signals based on them. The purpose is to identify potential trend reversal points and overbought and oversold conditions, and track stock price trends for trading.
## Strategy Principle
The main buy signals for this strategy come from the RSI and Bollinger Bands. When the RSI is below the oversold line of 30, it is considered oversold. At this time, if the price approaches or touches the lower Bollinger Band, a buy signal is generated. This indicates that the stock price may reverse and rise.
The main sell signals for this strategy also come from the RSI and Bollinger Bands. When the RSI exceeds the overbought line of 70, it is considered overbought. At this time, if the price is close to or exceeds the Bollinger Band upper limit, a sell signal is generated. This indicates that the stock price may reverse downward.
Additionally, the 20-day and 50-day simple moving averages are calculated in the strategy. They can be used to determine trend direction. When the fast moving average is above the slow moving average, it indicates an upward trend; otherwise, it indicates a downward trend.
## Advantage Analysis
This strategy combines multiple indicators to identify buying and selling points, which can effectively capture price trend reversals and track price changes. Its main advantages are:
1. Use Bollinger Bands to identify overbought and oversold areas. Bollinger Bands define the range of price fluctuations through standard deviation and can well identify price anomalies.
2. The RSI indicator can effectively identify overbought and oversold conditions. RSI above 70 is considered an overbought zone, and below 30 is considered an oversold zone, which can give a signal before the price reverses.
3. Use double moving averages to determine the overall trend direction and avoid trading in markets without trends.
4. By combining multiple indicators, false signals can be filtered and high-probability buying and selling points can be identified.
## Risk Analysis
The main risks of this strategy are:
1. The Bollinger Band parameters are improperly set, and the upper and lower rails cannot effectively define the price fluctuation range. This can result in a large number of false signals.
2. With different RSI parameters, its overbought and oversold judgment criteria will change, and the effect of the signal will also change.
3. If the parameters of the double moving average are different, the overall trend judged by them will also be biased.
4. Strategy signals may lag behind and fail to give instructions at the initial price reversal. This may result in some slippage losses.
5. When the market fluctuates violently, various indicators may fail and cannot effectively identify buying and selling points.
In view of the above risks, optimization can be carried out by adjusting parameters, combining more indicators, etc., to make the strategy more robust.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Use adaptive Bollinger Bands to dynamically adjust parameters according to the degree of market volatility to make the upper and lower tracks more accurate.
2. Add indicator filtering such as VOLUME to only generate signals when trading volume is enlarged to avoid false breakthroughs.
3. Set a price stop loss line and stop the loss promptly when the price moves in an unfavorable direction.
4. Test and optimize trading varieties, trading periods, etc., so that strategy parameters can be adjusted for different situations.
5. Add machine learning algorithms, use historical data training, and automatically optimize parameter settings.
## Summarize
This strategy integrates multiple indicators such as Bollinger Bands, RSI, and double moving averages to establish complete buying and selling rules, which can effectively identify price trends, determine overbought and oversold areas, and provide trading signals before the stock price reverses. By optimizing parameters, adding filter conditions, and setting stop losses, the stability of the strategy can be further improved. Generally speaking, this strategy combines trends and overbought and oversold indicators to capture reversal opportunities, and is worthy of further optimization and verification.
||

## Overview

This strategy combines dual moving averages, relative strength index (RSI) and Bollinger bands and other technical indicators to build buy and sell signals for the purpose of identifying potential trend reversal points and overbought/oversold conditions to track price trends for trading.

## Strategy Principle  

The main buy signals of this strategy come from RSI and Bollinger bands. When RSI is below the oversold line of 30, it is viewed as oversold. At this time, if the price approaches or touches the lower rail of the Bollinger bands, a buy signal is generated. This indicates the price may reverse upward.

The main sell signals also come from RSI and Bollinger bands. When RSI exceeds the overbought line of 70, it is viewed as overbought. At this time, if the price approaches or exceeds the upper rail of the Bollinger bands, a sell signal is generated. This indicates the price may reverse downward.

In addition, the strategy calculates the 20-day and 50-day simple moving averages. They can be used to judge the trend direction. When the fast moving average is above the slow moving average, it indicates an upward trend; otherwise, it indicates a downward trend.

## Advantage Analysis

This strategy combines multiple indicators to identify buy and sell points, which can effectively capture price trend reversals and track price changes. Its main advantages are:

1. Use Bollinger bands to identify overbought/oversold zones. Bollinger bands define price fluctuation ranges well through standard deviation and can identify abnormal price situations.

2. The RSI indicator can effectively identify overbought/oversold status. RSI above 70 is viewed as overbought zone and below 30 as oversold zone, which can signal ahead of price reversal.  

3. The dual moving averages determine the overall trend direction to avoid trading in market without a trend.

4. By combining multiple indicators, false signals can be filtered and high probability buy/sell points can be identified.

## Risk Analysis   

The main risks of this strategy are:

1. Improper Bollinger band parameter settings may fail to effectively define the price fluctuation range. This may generate a lot of false signals.

2. Different RSI parameters lead to different overbought/oversold criteria and signal generation effects.

3. Different dual moving average parameters lead to bias in judging the overall trend. 

4. Strategy signals may lag and fail to give guidance at the very beginning of price reversal. This may lead to certain amount of slippage loss.

5. When the market fluctuates violently, multiple indicators may fail and become ineffective in identifying buy/sell points.

To address the above risks, methods like parameter tuning, combining more indicators can be adopted to optimize the strategy for more robustness.

## Optimization Directions

The strategy can be optimized in the following aspects:

1. Use adaptive Bollinger bands to dynamically adjust parameters based on market volatility to make the upper/lower rails more accurate.

2. Add VOLUME and other indicators for filtration, only generating signals when trading volume amplifies, in order to avoid false breakout.

3. Set price stop loss line and stop loss in time when price runs in unfavorable direction.

4. Conduct tests and optimizations towards trading products, trading sessions etc, so that strategy parameters can be adjusted accordingly.

5. Increase machine learning algorithms, automatically optimizing parameter settings through training over historical data.

## Conclusion  

This strategy integrates Bollinger bands, RSI, dual moving averages and other indicators to establish complete buy and sell rules, which can effectively identify price trends, judge overbought/oversold zones, and give trading signals ahead of price reversal. Through means like parameter optimization, adding filtering conditions, setting stop loss etc, the strategy's stability can be further improved. In general, by combining trend and overbought/oversold indicators, this strategy can capture reversal opportunities and is worth further optimizations and verifications in live trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|BB Length|
|v_input_2|2|BB MultFactor|
|v_input_3|14|RSI Length|
|v_input_4|30|RSI Oversold|
|v_input_5|70|RSI Overbought|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("RSA", overlay=true)

// Bollinger Bands
bb_length = input(20, title="BB Length")
bb_mult = input(2.0, title="BB MultFactor")
bb_basis = sma(close, bb_length)
bb_upper = bb_basis + bb_mult * stdev(close, bb_length)
bb_lower = bb_basis - bb_mult * stdev(close, bb_length)

// RSI
rsi_length = input(14, title="RSI Length")
rsi_oversold = input(30, title="RSI Oversold")
rsi_overbought = input(70, title="RSI Overbought")
rsi_value = rsi(close, rsi_length)

// Buy and Sell Conditions
buy_condition = crossover(rsi_value, rsi_oversold) and (close < bb_lower)
sell_condition = crossunder(rsi_value, rsi_overbought) and (close > bb_upper)

// Add Buy and Sell Signals
if (buy_condition)
    strategy.order("Buy", strategy.long)
if (sell_condition)
    strategy.order("Sell", strategy.short)

// Plot Bollinger Bands
plot(bb_upper, color=color.blue, title="Upper Bollinger Band")
plot(bb_lower, color=color.blue, title="Lower Bollinger Band")

// Plot RSI
plot(rsi_value, color=color.orange, title="RSI")

// Plot Moving Averages
fast_ma = sma(close, 20)
slow_ma = sma(close, 50)
plot(fast_ma, color=color.green, title="Fast MA")
plot(slow_ma, color=color.red, title="Slow MA")

// Plot Trend Lines
trend_line = linreg(close, 50, 0)
plot(trend_line, color=color.purple, title="Trend Line")

```

> Detail

https://www.fmz.com/strategy/442546

> Last Modified

2024-02-22 17:01:05
