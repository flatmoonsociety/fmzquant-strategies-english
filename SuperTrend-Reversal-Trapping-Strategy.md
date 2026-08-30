
> Name

SuperTrend-Reversal-Trapping-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy determines the current trend direction based on the supertrend indicator and sends trading signals based on the trap candle pattern. It is a trend following strategy. When a trap candle appears in the opposite direction to the supertrend indicator, it indicates that the trend may reverse, and this strategy will seize the reversal opportunity to enter the market.
## Strategy Principle
This strategy first calculates the supertrend indicator to determine the current trend. Green indicates an upward trend and red indicates a downward trend. Then judge whether the K line forms a trap candle pattern, the conditions are: 1) the K line is in the opposite direction to the super trend indicator, 2) the K line is strong (no deviation from the big positive line or closing price), 3) the trading volume of the K line is enlarged. When the above three conditions are met at the same time, it means that a trend reversal may occur, and the strategy is to enter the long position at the high point of the trap candle and the short position at the low point. The stop loss point is set to the opposite side of the trap candle or to the most recent high or low.
Specifically, the strategy calculates the supertrend indicator based on the 10-period ATR to determine the current trend. Then calculate whether the current K line is in the opposite direction to the super trend indicator, and the VOLUME is larger than the previous K line, or whether three consecutive K lines have the same CLOSE direction but a decrease in VOLUME. If the conditions are met and a reversal is considered possible, long positions will be entered at the highest price of the trap K line and short positions will be entered at the lowest price. The stop loss point will be the opening price direction of the trap K line.
This strategy determines the general trend through the super trend indicator and enters the trap candle at the possible reversal point. The target profit comes from the operation of the subsequent trend.
## Advantage Analysis
- Combine trend and pattern judgment to improve trading accuracy
Super trend indicators determine the direction of the general trend, while trap candles identify trend reversal opportunities. Combining trends and patterns can improve the accuracy of judgment.
- Trap candles increase entry confirmation to avoid false breakthroughs
Trap candles are required to be strong in volume to avoid false signals caused by noise. Adding entry confirmation can avoid the risk of chasing tops and digging bottoms.
- The strategy is simple, clear and easy to implement
With supertrend indicators and trap candles as the core, it is very concise and clear, with few parameters and low implementation difficulty.
- Set stop loss points reasonably to control risks
The stop loss point is set to the trap candle price, which can quickly stop the loss and is also in line with the reasonable position after the trend reverses.
## Risk Analysis
- There is a lag in the supertrend indicator
There is a certain lag in judging the trend of the supertrend indicator, and the best entry point for trend reversal may be missed.
- Failure to reverse may expand losses
Reversal signals are not necessarily 100% reliable, and losses may increase if the reversal fails.
- Need to identify appropriate trap forms
Depending on the species and time period, the appropriate trap form may vary. Optimum parameters need to be tested for specific situations.
- Night trading and overnight trading have different characteristics
There are differences in the characteristics of night trading and overnight trading, and the parameters need to be optimized separately.
## Optimization direction
- Optimize parameters considering night trading and overnight differences
For example, the trading volume amplification degree of the trap K line and the day and night parameters can be optimized separately.
- Optimize super trend indicator parameters
Test different ATR cycle parameters to find the optimal parameters for a given variety and generate more accurate supertrend signals.
- Combine more indicators for entry filtering
Indicators such as MACD and KDJ can be added to improve the accuracy of judgment on reversal.
- Add stop loss mechanism
For example, stop loss again after the trend reverses, or use percentage stop loss to control risks.
## Summarize
This strategy integrates super trend indicators and trap candle patterns to enter the market when the trend is reversed. The core idea is simple, clear and easy to implement. However, there is still room for improvement in the accuracy of its trading signals. It is necessary to consider the general trend, night trading differences, stop losses and other aspects for comprehensive optimization to improve the stability of the strategy. If iteratively optimized, this strategy can become a powerful tool for frequent traders.
||


## Overview

This strategy uses the SuperTrend indicator to determine the current trend direction, and generates trading signals based on trapping candlestick patterns. It belongs to trend following strategies. When a trapping candle opposite to the SuperTrend direction forms, it signals a potential trend reversal. The strategy aims to capitalize on the reversal opportunity.

## Strategy Logic

The strategy first calculates the SuperTrend indicator to determine the current trend, with green for uptrend and red for downtrend. It then checks if the candlestick forms a trapping pattern, which requires: 1) the candle is opposite to the SuperTrend direction, 2) the candle is strong (big bullish or close is not diverging), 3) the candle has increasing volume. When all three conditions are met, it signals a likely trend reversal. The strategy goes long at the top of the trapping candle and goes short at the bottom. The stop loss is placed at the opposite side of the trapping candle or recent swing high/low.

Specifically, the SuperTrend is calculated based on 10-period ATR. It then checks if the current candle is opposite to the SuperTrend direction, and its VOLUME is larger than previous candle, or three consecutive candles with same CLOSE direction but decreasing VOLUME. If the criteria are met, it signals reversal and enters long at candle high and enters short at candle low. The stop loss is placed at the opening price direction of the trapping candle. 

The strategy identifies the overall trend with SuperTrend and enters on potential reversal points marked by trapping candles, with the profit target coming from the subsequent trend move.

## Advantage Analysis

- Combine trend and pattern for higher accuracy

SuperTrend determines overall trend, trapping candle signals reversal chance. Combining trend and pattern improves accuracy.

- Trapping candle adds entry confirmation, avoiding false breakout

The strong momentum and increasing volume of trapping candle avoids false signals from noise. The confirmation prevents chasing tops and bottoms.

- Simple and clear logic, easy to implement

With SuperTrend and trapping candle as the core, the strategy is very minimalist, with few parameters and easy to implement.

- Reasonable stop loss setups control risk

The stop loss at trapping candle price allows quick exit and also suits the position post-reversal.

## Risk Analysis

- SuperTrend lags in catching trend reversal

SuperTrend has some lag in detecting trend reversal, thus may miss the best entry timing.

- Failed reversal can amplify losses

Reversal signals are not 100% reliable. Failed reversals can magnify losses.

- Need to identify proper trapping patterns

The optimal trapping pattern may vary between products and timeframes. Requires testing for best parameters per situation.

- Day and night patterns differ

Trading characteristics differ between day and night sessions. Separate parameter optimization is needed.

## Improvement Directions

- Parameter optimization for day and night differences

For example, optimize trapping candle volume increase level separately for day and night.

- Optimize SuperTrend parameters  

Test different ATR periods to find optimal SuperTrend parameters and signals for each product.

- Add more filters for entry

Incorporate additional indicators like MACD, KDJ to improve reversal judgment accuracy.

- Add stop loss mechanisms

Such as re-setting stop loss after reversals, percentage stop loss etc to control risk.

## Summary

This strategy combines SuperTrend and trapping candle patterns to enter on perceived trend reversals. The core idea is simple and clear. But there is room to further improve signal accuracy by comprehensive optimizations across aspects like overall trend, session differences, stop loss etc, to enhance stability. With iterative optimization, it can become a powerful tool for active traders.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|10|ATR Length|
|v_input_int_2|2|Factor|
|v_input_float_1|0.003|Candle Height|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-17 00:00:00
end: 2023-09-24 00:00:00
period: 5m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("SuperTrend Trapping Candle Strategy", shorttitle="ST", margin_long=1, margin_short=1, overlay=true)


// Inputs
atrPeriod = input.int(10, "ATR Length")
factor = input.int(2, "Factor")
candleDivider = input.float(0.003, "Candle Height", step=0.0001)


// Supertrend
[supertrend, direction] = ta.supertrend(factor, atrPeriod)
plot(direction < 0 ? supertrend : na, "Up Trend", color = color.green, style=plot.style_linebr)
plot(direction < 0? na : supertrend, "Down Trend", color = color.red, style=plot.style_linebr)


//Trapping canlde
isUptrend = direction < 0
isDowntrend = direction > 0
isBullsStrengthDecreasing = volume < volume[1] and volume[1] < volume[2] and close > close[1] and close[1] > close[2] and open > open[1] and open[1] > open[2]
isBearsStrengthDecreasing = volume < volume[1] and volume[1] < volume[2] and close < close[1] and close[1] < close[2] and open < open[1] and open[1] < open[2]
isStrongVolume = (volume > volume[1]) or isBullsStrengthDecreasing or isBearsStrengthDecreasing
isSmallCandle = (high - low) < close * candleDivider
isUptrendTrapping = isUptrend and close < open and isStrongVolume and isSmallCandle
isDowntrendTrapping = isDowntrend and close > open and isStrongVolume and isSmallCandle

plotshape(isUptrendTrapping, style=shape.triangleup, location=location.belowbar, color=color.green)
plotshape(isDowntrendTrapping, style=shape.triangledown, location=location.abovebar, color=color.orange)


// Signals
longCondition = isUptrendTrapping
if (longCondition)
    strategy.entry("Long", strategy.long)


shortCondition = isDowntrendTrapping
if (shortCondition)
    strategy.entry("Short", strategy.short)

if open < close
    alert("Seller Trapped.", alert.freq_all)
if close > open
    alert("Buyer Trapped.", alert.freq_all)


```

> Detail

https://www.fmz.com/strategy/427820

> Last Modified

2023-09-25 17:58:05
