
> Name

Wick-Reversal-Pattern-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
The pattern reversal strategy detects the K-line pattern, identifies the turning point when the price changes from rising to falling or from falling to rising, and performs buying or selling operations near the turning point. This strategy mainly uses the proportional relationship between the shadow line and the entity to determine price reversal signals.
## Strategy Principle
The core logic of this strategy is to detect the proportional relationship between the shadow part and the real part of the K line to determine whether there is a price reversal pattern.
When a falling K line appears, if the lower shadow line of the K line is longer and the upper shadow line and the entity are shorter, it means that the K line has strong buying power and may reverse to rise. Specifically, it detects that the closing price is higher than the opening price, and the length of the lower shadow is greater than a certain multiple of the length of the upper shadow and the real body, then a long signal is generated.
On the contrary, when a rising K line appears, if the upper shadow line of the K line is longer and the lower shadow line and the entity are shorter, it means that the K line has strong selling power and may reverse to decline. Specifically, it detects that the closing price is lower than the opening price, and the length of the upper shadow line is greater than a certain multiple of the length of the lower shadow line and the real body, then a short signal is generated.
In addition, if the difference between the opening price and the closing price is very small, but the shadow line is long, a reversal signal may also be generated.
When detecting a reversal signal, it will also be filtered in conjunction with the average K-line range. A signal will only be generated when the K-line range is greater than the average.
## Strategic Advantages
- Use the proportional relationship between shadow lines and entities to capture reversal patterns and identify reversal points
- Detect both long and short reversal patterns simultaneously
- Combined with K-line average range filtering to avoid generating false signals in volatile markets
- Simple and clear morphological recognition logic, easy to understand and implement
## Strategy Risk
- The parameter setting of the ratio of shadow line to entity requires experience. Improper use may result in missing reversals or generating false signals.
- Only relying on a single K-line pattern to judge reversal can easily be misled by local shocks.
- Failure to judge trends may result in losses due to counter-trend operations.
You can consider combining trend indicators to avoid contrarian operations. Reversal signals can also be confirmed by combining them with other technical indicators. Parameter settings can be optimized through backtesting to obtain better parameter combinations.
## Strategy optimization direction
- Can be combined with trend indicators to confirm that the reversal direction is consistent with the trend and avoid counter-trend operations
- Can be combined with other technical indicators, such as magnetic lines, Bollinger Bands, etc., to confirm reversal signals
- Machine learning methods can be used to automatically optimize the parameters of the shadow line and entity ratio
- You can set stop loss and take profit conditions after reversal to optimize the exit mechanism
## Summarize
The pattern reversal strategy uses a relatively simple pattern recognition method to effectively identify price reversal patterns and capture turning points. However, relying solely on a single K-line pattern can easily lead to misjudgment. It needs to be used in combination with other technical indicators and trend judgment can be added to avoid counter-trend operations and thereby improve the stability of the strategy. In addition, parameter optimization and stop loss/take profit settings are also directions for further improving the strategy. In short, the form flipping strategy provides us with a simple and practical idea, but it needs to be combined with other technical means to achieve maximum effect.
||

## Overview

The wick reversal pattern strategy identifies reversal points where the price switches from an uptrend to a downtrend or vice versa by detecting candlestick patterns. It enters long or short positions around the reversal points mainly based on the ratio between candle wicks and bodies.

## Strategy Logic

The core logic of this strategy is to detect the ratio between candle wick and body to identify potential reversal patterns. 

When there is a bearish candle, if the lower wick is much longer than the upper wick and body, it indicates strong buying pressure and the price may reverse to upside. Specifically, it detects long lower wick compared to upper wick and body by a certain multiplier to generate long signals.

Conversely, when there is a bullish candle, if the upper wick is much longer than the lower wick and body, it indicates strong selling pressure and the price may reverse to downside. Specifically, it detects long upper wick compared to lower wick and body by a certain multiplier to generate short signals.

Besides, a long wick with tiny body could also produce reversal signals.

The detection is filtered by comparing against average candle range to avoid false signals during sideways markets. Only candles with range greater than average will produce signals.

## Advantages

- Detect reversal patterns by comparing wick and body ratios 
- Identify both long and short reversal signals
- Avoid false signals during sideways with average range filter
- Simple and intuitive pattern recognition logic

## Risks

- Wick and body ratio parameters need fine tuning based on experience
- Judging reversal merely based on single candle pattern can be misled by local fluctuations
- Lack of trend bias may cause losses from counter trend trades

Consider incorporating trend indicators to avoid counter trend trades. Combining with other technical indicators may help confirm signals. Parameters can be optimized through backtesting.

## Enhancement

- Add trend bias to ensure reversals align with trend direction
- Incorporate other indicators like Bollinger Bands to confirm signals
- Utilize machine learning to auto optimize wick and body ratio parameters
- Set stop loss and take profit after reversal to optimize exits

## Summary

The wick reversal pattern strategy effectively identifies reversal patterns and catches turning points using simple pattern recognition. However, relying solely on single candle patterns can be misleading. Combining with other technical indicators and adding trend bias helps avoid counter trend trades and improves strategy stability. Parameter optimization and stop loss/take profit also help further enhance the strategy. In summary, the wick reversal strategy provides a simple and practical idea but needs to be complemented with other techniques to maximize performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|3.25|wickMultiplier|
|v_input_2|0.35|bodyPercentage|
|v_input_3|50|barsBack|
|v_input_4|1.1|bodyMultiplier|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-08 00:00:00
end: 2023-10-15 00:00:00
period: 3m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © adiwajshing

//@version=4
strategy("Wick Reversal Signal", overlay=true)

wickMultiplier = input(3.25)
bodyPercentage = input(0.35)
barsBack = input(50)
bodyMultiplier = input(1.1)

myCandleSize = high-low
averageCandleSize = rma(myCandleSize, barsBack)

longSignal = close > open and open-low >= (close-open)*wickMultiplier and high-close <= (high-low)*bodyPercentage and high-low >= averageCandleSize*bodyMultiplier
longSignal := longSignal or (close < open and close-low >= (open-close)*wickMultiplier and high-close <= (high-low)*bodyPercentage and high-low >= averageCandleSize*bodyMultiplier)
longSignal := longSignal or (abs(close-open) < 0.01 and close != high and high-low >= (high-close)*wickMultiplier and high-close <= (high-low)*bodyPercentage and high-low >= averageCandleSize*bodyMultiplier)

shortSignal = close < open and high-open >= (open-close)*wickMultiplier and close-low <= (high-low)*bodyPercentage and high-low >= averageCandleSize*bodyMultiplier
shortSignal := shortSignal or (close > open and high-close >= (close-open)*wickMultiplier and close-low <= (high-low)*bodyPercentage and high-low >= averageCandleSize*bodyMultiplier)
shortSignal := shortSignal or (abs(close-open) < 0.01 and close != low and high-low >= (close-low)*wickMultiplier and close-low <= (high-low)*bodyPercentage and high-low >= averageCandleSize*bodyMultiplier)

plotshape(longSignal, style=shape.triangleup, size=size.normal)
plotshape(shortSignal, style=shape.triangledown, size=size.normal)

strategy.entry("LONG", strategy.long, when=longSignal)
strategy.entry("SHORT", strategy.short, when=shortSignal)
```

> Detail

https://www.fmz.com/strategy/429333

> Last Modified

2023-10-16 08:58:12
