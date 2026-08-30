
> Name

Dual-Rail-Trend-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
The dual-track band trend following strategy is a short-term trading strategy based on Bollinger Bands. This strategy uses the upper and lower Bollinger Bands as buying and selling signals to achieve short-term trading.
## Strategy Principle
This strategy mainly includes the following parts:
1. Calculate the middle track, upper track and lower track of Bollinger Bands. The middle track is the n-day simple moving average of the closing price, and the width of the Bollinger Bands is determined by twice the n-day standard deviation of the closing price.
2. When the closing price crosses the lower rail from bottom to top, go long; when the closing price crosses the upper rail from top to bottom, close the position.
3. The n value defaults to 20 days and can also be adjusted according to the market. The change in Bollinger Band width is controlled by the standard deviation multiple, and the default is 2 times.
4. This strategy is simple, direct and easy to implement. Able to effectively track market trends, Profit from the volatility of the market.
## Advantage Analysis
The dual-track belt strategy has the following advantages:
1. Easy to implement, simple and intuitive logic.
2. Able to track market changes in a timely manner and capture short-term trading opportunities.
3. There is a certain mathematical basis for using the statistical characteristics of Bollinger Bands.
4. Prevent entry too early and exit too late.
5. The parameters of Bollinger Bands can be adjusted to adapt to the characteristics of different markets.
6. There is no need to predict market trends, just follow the market.
## Risk Analysis
There are also some risks with this strategy:
1. The Bollinger Bands indicator cannot accurately predict trend reversal points.
2. There may be more false signals.
3. It cannot effectively filter the noise that shakes the market.
4. Bollinger Band parameters need to be determined reasonably, otherwise the strategy performance will be affected.
5. This strategy should be avoided during sideways trading.
6. There is a certain delay and you should pay attention to the tracking error.
Risks can be reduced by adjusting parameters and combining with other indicators.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Filter in combination with other indicators, such as MACD, KDJ, etc., to avoid false signals.
2. Dynamically adjust the Bollinger Band parameters and change the Bollinger Band width according to market conditions.
3. Set stop-loss and stop-profit conditions to reasonably control the risk of a single transaction.
4. Optimize the entry and exit points, for example, let the closing price completely break through the Bollinger Bands before entering the market.
5. Carry out parameter optimization and optimize parameters such as moving average length and standard deviation multiples.
6. Distinguish between the long market and the short market and conduct directional trading.
## Summarize
The double-track band strategy is a simple and practical short-term trading strategy. It uses the statistical characteristics of Bollinger Bands to effectively capture the short-term trend of the market. This strategy is easy to operate and has simple logic, but it also has some flaws. Through further optimization, this strategy can achieve better performance in real trading. Generally speaking, the dual-track belt strategy is suitable for investors who pursue short-term trading opportunities.
|| 


## Overview

The Dual Rail Trend Tracking Strategy is a short-term trading strategy based on Bollinger Bands. This strategy uses the upper and lower rails of the Bollinger Bands as buy and sell signals to implement short-term trading.

## Strategy Principle 

The main components of this strategy are:

1. Calculate the middle, upper and lower rails of the Bollinger Bands. The middle rail is the n-day simple moving average of the closing price, and the width of the Bollinger Bands is determined by twice the n-day standard deviation of the closing price.

2. Go long when the closing price crosses above the lower rail from below, and close the position when the closing price crosses below the upper rail from above.

3. The default n value is 20 days, which can be adjusted based on market conditions. The width of the bands is controlled by the standard deviation multiplier, default to 2x.

4. This strategy is simple and straightforward to implement. It can effectively track market trends and profit from the volatility.

## Advantage Analysis

The Dual Rail strategy has the following advantages:

1. Easy to implement with simple and intuitive logic. 

2. Can timely track market changes and capture short-term trading opportunities.

3. Utilizes the statistical properties of Bollinger Bands, which provides mathematical justification.

4. Prevents premature entry and delayed exit. 

5. The parameters can be adjusted to adapt to different market conditions.

6. No need to predict market trends, just follow the market.

## Risk Analysis

There are also some risks with this strategy:

1. Bollinger Bands cannot accurately predict trend reversal points.

2. There may be more false signals.

3. It cannot effectively filter out the noise in range-bound markets. 

4. Reasonable Bollinger Bands parameters are needed, otherwise it may affect strategy performance.

5. Should avoid using this strategy during market consolidations.

6. There is some lag, tracking error should be monitored.

Risks can be reduced by adjusting parameters, combining with other indicators, etc.

## Optimization Directions

This strategy can be optimized in the following aspects:

1. Combine with other indicators like MACD, KDJ to filter false signals. 

2. Dynamically adjust Bollinger Bands parameters based on changing market conditions.

3. Set stop loss and take profit to properly control single trade risks.

4. Optimize entry and exit points, e.g. wait for complete penetration of bands.

5. Parameter optimization on moving average length, standard deviation multiplier, etc. 

6. Distinguish bull versus bear market for directional trading.

## Summary 

The Dual Rail strategy is a simple and practical short-term trading strategy. It utilizes the statistical properties of Bollinger Bands to effectively capture short-term trends. The strategy is easy to implement with simple logic, but also has some flaws. Further optimizations can improve its performance in live trading. Overall, the Dual Rail strategy suits investors looking for short-term trading opportunities.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|20|length|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_float_1|2|StdDev|
|v_input_int_2|false|Offset|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-18 00:00:00
end: 2023-09-17 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Bollinger Bands Strategy", overlay=true)

length = input.int(20, minval=1)
src = input(close, title="Source")
mult = input.float(2.0, minval=0.001, maxval=50, title="StdDev")
basis = ta.sma(src, length)
dev = mult * ta.stdev(src, length)
upper = basis + dev
lower = basis - dev
offset = input.int(0, "Offset", minval = -500, maxval = 500)

plot(basis, "Basis", color=#FF6D00, offset = offset)
p1 = plot(upper, "Upper", color=#2962FF, offset = offset)
p2 = plot(lower, "Lower", color=#2962FF, offset = offset)
fill(p1, p2, title = "Background", color=color.rgb(33, 150, 243, 95))

// Buy condition: Price crosses below the lower Bollinger Band
buy_condition = ta.crossover(src, lower)
strategy.entry("Buy", strategy.long, when=buy_condition)

// Sell condition: Price crosses above the upper Bollinger Band
sell_condition = ta.crossunder(src, upper)
strategy.close("Buy", when=sell_condition)

```

> Detail

https://www.fmz.com/strategy/427162

> Last Modified

2023-09-18 17:31:43
