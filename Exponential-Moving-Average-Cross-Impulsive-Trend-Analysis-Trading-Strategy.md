
> Name

Exponential-Moving-Average-Cross-Impulsive-Trend-Analysis-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/104a3014c9a3495ef39.png)

[trans]
#### Overview
This strategy is a trend following trading system based on the Exponential Moving Average (EMA) and the Impulse Correction Model (ICM). It captures market trend changes by identifying price crossovers with EMA and subsequent pulse-correction-pulse patterns, and executes trades when specific conditions are met. The system uses a fixed risk-benefit ratio to manage stop loss and take profit for each trade.
#### Strategy Principle
The core logic of the strategy is based on the following key components:
1. Use the 10-period EMA as a reference indicator for trend direction
2. Look for impulse-correction-impulse patterns within 3 periods after price crosses the EMA
3. Long entry conditions:
   - Price crosses EMA
   - The first K line is a bullish pulse (the increase is greater than the preset value)
   - The second candle is a bearish correction (the closing price is lower than the opening price)
   - The third candlestick is a bullish pulse and breaks the high of the first two candlesticks
4. The entry conditions for short positions are opposite to those for long positions.
5. Automatically set stop loss and take profit positions using a fixed risk-reward ratio (default 3 times)
#### Strategic Advantages
1. Combine technical indicators and price patterns to provide more reliable trading signals
2. Confirm trend continuity through pulse-correction-pulse patterns
3. Using a fixed risk-return ratio for position management is conducive to long-term stable returns.
4. The entry logic is clear and easy to understand and execute.
5. Applicable to different trading varieties and time periods
#### Strategy Risk
1. Frequent false breakthrough signals may occur in a volatile market
2. A fixed risk-benefit ratio may not be suitable for all market environments
3. The choice of EMA parameters and pulse amplitude thresholds will affect strategy performance
4. Continuous violent fluctuations may lead to unreasonable stop loss positions.
5. A rapid market reversal may cause a large retracement
#### Strategy optimization direction
1. Introduce volatility indicator to dynamically adjust pulse amplitude threshold
2. Add trend strength filter to reduce false breakouts
3. Dynamically adjust the risk-return ratio based on market characteristics
4. Add time filtering to avoid trading at unfavorable times
5. Combined with trading volume indicators to improve signal reliability
#### Summary
This strategy builds a logical and clear trend following system by combining EMA and impulse correction models. Its advantages are clear signals and controllable risks, but it still needs to be optimized according to specific market characteristics. By adding appropriate filtering conditions and dynamic parameter adjustment mechanisms, the stability and profitability of the strategy can be further improved. ||
#### Overview
This strategy is a trend-following trading system based on Exponential Moving Average (EMA) and Impulse Correction Model (ICM). It captures market trend changes by identifying price-EMA crossovers and subsequent impulse-correction-impulse patterns, executing trades when specific conditions are met. The system employs a fixed risk-reward ratio to manage stop-loss and take-profit levels for each trade.

#### Strategy Principles
The core logic of the strategy is based on the following key components:
1. Uses 10-period EMA as a reference indicator for trend direction
2. Looks for impulse-correction-impulse patterns within 3 periods after price-EMA crossover
3. Long entry conditions:
   - Price crosses above EMA
   - First candle is a bullish impulse (rise exceeds preset value)
   - Second candle is a bearish correction (close below open)
   - Third candle is a bullish impulse breaking above previous two candles' highs
4. Short entry conditions are opposite to long conditions
5. Uses fixed risk-reward ratio (default 3x) to automatically set stop-loss and take-profit levels

#### Strategy Advantages
1. Combines technical indicators and price patterns for more reliable trading signals
2. Confirms trend continuation through impulse-correction-impulse pattern
3. Uses fixed risk-reward ratio for position management, promoting long-term stable returns
4. Clear entry logic, easy to understand and execute
5. Applicable to different trading instruments and timeframes

#### Strategy Risks
1. May generate frequent false breakout signals in ranging markets
2. Fixed risk-reward ratio may not suit all market conditions
3. EMA parameters and impulse threshold selection affect strategy performance
4. Continuous violent fluctuations may lead to inappropriate stop-loss placement
5. Rapid market reversals may cause significant drawdowns

#### Strategy Optimization Directions
1. Introduce volatility indicators to dynamically adjust impulse threshold
2. Add trend strength filters to reduce false breakouts
3. Dynamically adjust risk-reward ratio based on market characteristics
4. Add time filters to avoid trading during unfavorable periods
5. Incorporate volume indicators to improve signal reliability

#### Summary
The strategy constructs a logically clear trend-following system by combining EMA and impulse correction model. Its advantages lie in clear signals and controllable risk, but optimization based on specific market characteristics is still needed. Through adding appropriate filtering conditions and dynamic parameter adjustment mechanisms, the strategy's stability and profitability can be further improved.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-19 00:00:00
end: 2025-02-17 00:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("EMA Cross Impulsive Strategy", overlay=true, margin_long=100, margin_short=100)

// Parameters
emaLength = input.int(10, title="EMA Length")
impulsiveBodyTicks = input.int(10, title="Minimum Impulsive Candle Body (Ticks)")
rMultiplier = input.int(3, title="Risk Reward Multiplier")

// Calculate EMA
ema10 = ta.ema(close, emaLength)

// Cross conditions
crossUp = ta.crossover(close, ema10)
crossDown = ta.crossunder(close, ema10)

// Impulsive and correction conditions
tickSize = syminfo.mintick
impulsiveBodyMin = impulsiveBodyTicks * tickSize

isImpulsiveBullish = (close > open) and (close - open >= impulsiveBodyMin)
isImpulsiveBearish = (close < open) and (open - close >= impulsiveBodyMin)
isCorrectionBearish = (close < open)
isCorrectionBullish = (close > open)

// Long setup tracking
var int barsSinceLongCross = 0
var bool impulsive1Long = false
var bool correctionLong = false
var bool impulsive2Long = false

if crossUp
    barsSinceLongCross := 0
    impulsive1Long := false
    correctionLong := false
    impulsive2Long := false
else
    barsSinceLongCross := barsSinceLongCross + 1

if barsSinceLongCross == 1
    impulsive1Long := isImpulsiveBullish

if barsSinceLongCross == 2
    correctionLong := isCorrectionBearish

if barsSinceLongCross == 3
    impulsive2Long := isImpulsiveBullish and (close > math.max(high[1], high[2]))

// Short setup tracking
var int barsSinceShortCross = 0
var bool impulsive1Short = false
var bool correctionShort = false
var bool impulsive2Short = false

if crossDown
    barsSinceShortCross := 0
    impulsive1Short := false
    correctionShort := false
    impulsive2Short := false
else
    barsSinceShortCross := barsSinceShortCross + 1

if barsSinceShortCross == 1
    impulsive1Short := isImpulsiveBearish

if barsSinceShortCross == 2
    correctionShort := isCorrectionBullish

if barsSinceShortCross == 3
    impulsive2Short := isImpulsiveBearish and (close < math.min(low[1], low[2]))

// Execute trades
if barsSinceLongCross == 3 and impulsive1Long and correctionLong and impulsive2Long
    strategy.entry("Long", strategy.long)
    strategy.exit("Exit Long", "Long", stop=low, profit=close + (close - low) * rMultiplier)

if barsSinceShortCross == 3 and impulsive1Short and correctionShort and impulsive2Short
    strategy.entry("Short", strategy.short)
    strategy.exit("Exit Short", "Short", stop=high, profit=close - (high - close) * rMultiplier)

// Plot EMA
plot(ema10, color=color.blue, title="10 EMA")
```

> Detail

https://www.fmz.com/strategy/482501

> Last Modified

2025-02-18 17:41:28
