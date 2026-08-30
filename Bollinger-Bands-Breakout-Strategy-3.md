
> Name

Simple quantitative trading strategy Bollinger-Bands-Breakout-Strategy based on Bollinger Bands indicator
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/13aaf282bef24a4d763.png)
[trans]
## Overview
The Bollinger Bands Breakout Strategy is a simple quantitative trading strategy based on the Bollinger Bands indicator. This strategy uses the dynamic support and resistance levels provided by the upper and lower Bollinger Bands to set long entry and exit conditions when the price breaks through the upper and lower Bollinger Bands to capture breakthroughs in stock prices.
## Strategy Principle
The Bollinger Bands indicator was proposed by John Bollinger in the 1980s. It consists of an n-day moving average and m times its standard deviation. The moving average can be regarded as the central axis of the price, while the standard deviation can be regarded as the amplitude of price fluctuations. A larger standard deviation indicates more severe price fluctuations; a smaller standard deviation indicates moderate price fluctuations.
The entry conditions for this strategy are: when the closing price falls below the lower Bollinger Band, enter the market long; when the closing price breaks the upper band of the Bollinger Band, enter the market short. The exit conditions are: when a long position exists, the closing price breaks through the upper Bollinger Band and then the position is closed; when a short position exists, the closing price falls below the lower Bollinger Band and then the position is closed.
This strategy is a trend following strategy. By capturing the trend breakthrough of the price breaking through the upper and lower Bollinger Bands, the profit model is to expand the position to make profits through the trending market.
## Strategic Advantages
1. Use Bollinger Bands indicators as dynamic support and resistance levels, avoid using fixed price levels, and adapt to market changes.
2. The strategy refers to trends and volatility. Entscheidungen is not only based on price levels, but also on market volatility, which can reduce false signals.
3. The breakthrough framework is simple and direct, easy to understand and implement
4. Bollinger Band parameters can be flexibly adjusted, suitable for different varieties and parameter markets
## Risk Analysis
1. Improper setting of Bollinger Band indicator parameters may lead to too frequent trading signals and too many unnecessary transactions.
2. Breakthrough signals may be short-term price disturbances that cannot sustain the trend and may result in wrong transactions.
3. The strategy does not consider stop loss, and there are certain decision-making risks and loss control risks.
4. Based only on technical indicators without combining fundamental information, you may miss important fundamental trend turning points.
5. The characteristics of different market varieties are not taken into account, and the profit and loss situation may be affected by specific markets.
## Strategy optimization direction
1. Optimize Bollinger Band parameters and improve parameter robustness
2. Add a stop-loss mechanism to control single losses
3. Combine Bollinger Bands of different time periods to construct multi-period trading decisions
4. Combining trading volume to avoid some false breakthrough signals
5. Add fundamental factor judgment to determine entry timing and position size
6. Test the data of different market varieties and evaluate the adaptability of strategies across varieties
## Summarize
The Bollinger Bands Breakout Strategy is a simple and intuitive trend following strategy. It uses the dynamic support and resistance provided by the Bollinger Bands indicator to determine price trend breakthroughs and construct long position entry and exit conditions. The advantage of the strategy is that the framework is simple, easy to implement, and can capture price trend opportunities. You need to pay attention to risk control and avoid too frequent transactions. Through multi-faceted testing and optimization, the Bollinger Bands breakout strategy can become an effective quantitative trading strategy choice.
||

## Overview  

The Bollinger Bands breakout strategy is a simple quantitative trading strategy based on the Bollinger Bands indicator. The strategy utilizes the dynamic support and resistance levels provided by the upper and lower bands of Bollinger Bands to set entry rules for long positions when prices break out of the bands and exit rules when prices break back through the bands, aiming to capture trend-following opportunities in the price movements.

## Strategy Logic

The Bollinger Bands indicator was developed by John Bollinger in the 1980s. It consists of an n-period moving average and m times standard deviation above and below it. The moving average acts as the midpoint, while the standard deviation accounts for the volatility. High standard deviation values indicate increased volatility, while low values indicate decreased volatility.

The entry condition for this strategy is: a long position will be taken when the closing price breaks below the lower Bollinger band; a short position will be taken when the closing price breaks above the upper Bollinger band. The exit rules are: for existing long positions, liquidate when closing price breaks back above the upper band; for existing short positions, cover when closing price breaks back below the lower band.  

This is a trend-following strategy. By capturing trend continuation signaled by the breaking of Bollinger Bands, it aims to profit from sustained directional price movements.

## Advantages  

1. Using Bollinger Bands as dynamic support/resistance levels instead of fixed prices makes the strategy adaptive to evolving market conditions.

2. Decisions are based on both price levels and volatility conditions, avoiding some false signals.

3. The breakout framework is simple and intuitive.  

4. Flexible tuning of parameters makes the strategy adaptable across products and markets.

## Risks

1. Poor parameter tuning of indicators may cause too frequent trading and unnecessary costs.

2. Breakout signals may just be short-term price fluctuations instead of sustainable trends. 

3. The lack of stop loss exposes the strategy to uncontrolled loss risks.

4. The purely technical system misses fundamental trend reversals.

5. Performance may vary across different products without adjustments.

## Enhancement Opportunities

1. Optimize parameters to enhance robustness.

2. Incorporate stop loss orders to limit losses.

3. Build multi-timeframe system to improve decisions. 

4. Add volume filters to avoid false signals.

5. Complement fundamentals to better time entries and size positions.

6. Evaluate strategy on more products to test adaptiveness.

## Summary

The Bollinger Bands breakout strategy provides a simple trend-following approach by riding momentum signaled by indicator-based breakouts. Its strength lies in the dynamic identification of trend continuations. Proper risk controls and robustness enhancements can turn improve it into a viable systematic strategy.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|20|Bollinger Bands Length|
|v_input_string_1|0|Basis MA Type: SMA|EMA|SMMA (RMA)|WMA|VWMA|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_float_1|2|StdDev Multiplier|
|v_input_int_2|false|Offset|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-20 00:00:00
end: 2024-02-19 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Bollinger Bands Strategy", overlay=true)

length = input.int(20, title="Bollinger Bands Length", minval=1)
maType = input.string("SMA", title="Basis MA Type", options=["SMA", "EMA", "SMMA (RMA)", "WMA", "VWMA"])
src = input(close, title="Source")
mult = input.float(2.0, title="StdDev Multiplier", minval=0.001, maxval=50)
offset = input.int(0, title="Offset", minval=-500, maxval=500)

ma(source, length, _type) =>
    switch _type
        "SMA" => ta.sma(source, length)
        "EMA" => ta.ema(source, length)
        "SMMA (RMA)" => ta.rma(source, length)
        "WMA" => ta.wma(source, length)
        "VWMA" => ta.vwma(source, length)

basis = ma(src, length, maType)
dev = mult * ta.stdev(src, length)
upper = basis + dev + offset
lower = basis - dev - offset

// Define strategy entry and exit conditions
strategy.entry("Buy", strategy.long, when=close < lower)
strategy.close("Buy", when=close > upper)

strategy.entry("Sell", strategy.short, when=close > upper)
strategy.close("Sell", when=close < lower)

// Plotting the Bollinger Bands
plot(basis, color=color.blue, title="Basis")
plot(upper, color=color.red, title="Upper Band")
plot(lower, color=color.green, title="Lower Band")

```

> Detail

https://www.fmz.com/strategy/442259

> Last Modified

2024-02-20 15:53:12
