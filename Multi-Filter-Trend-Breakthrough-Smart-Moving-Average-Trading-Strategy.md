
> Name

Multi-Filter Trend Breakthrough Smart Moving Average Trading Strategy-Multi-Filter-Trend-Breakthrough-Smart-Moving-Average-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/15f8c9b62ce2d302bab.png)

[trans]
#### Overview
This strategy is a trend breakout trading system based on multiple technical indicator filters. It comprehensively uses multiple technical indicators such as exponential moving average (EMA), volume weighted average price (VWAP), relative strength index (RSI), average trend index (ADX), etc., and filters out false breakthroughs through multiple signal confirmations to improve the accuracy of transactions. This strategy also combines trend judgment with a higher time period and adopts a dynamic stop-loss and take-profit scheme based on ATR to achieve effective risk control.
#### Strategy Principle
The core logic of the strategy is based on the following key elements:
1. Trend judgment system: Use the 9-period and 21-period EMA crossovers to capture short-term trend changes, while referring to the 15-minute period 50-period EMA to confirm the larger trend direction.
2. Price momentum confirmation: Use the RSI indicator for momentum confirmation. Longs require RSI>55, and shorts require RSI<45.
3. Trend strength verification: The ADX indicator is introduced to judge the trend strength, and ADX>25 is required to ensure the validity of the trend.
4. Price position verification: Use VWAP as a reference for price position, requiring the price to be at the correct VWAP position.
5. Trading volume confirmation: The trading volume is required to be greater than 1.5 times the 10-period average trading volume to ensure sufficient market participation.
6. Risk management: Dynamically calculate the position size based on a fixed ratio of the total account value and ATR, using 1.5 times ATR as stop loss and 3 times ATR as take profit.
#### Strategic Advantages
1. The multiple signal confirmation mechanism greatly reduces the interference of false signals.
2. Combined with high and low time period analysis, the accuracy of trend judgment is improved.
3. Dynamic position management and stop-loss and stop-profit settings achieve good risk control.
4. Use volume breakthroughs as transaction confirmation to improve the reliability of transactions.
5. The strategy parameters are highly adjustable and easy to optimize according to different market conditions.
#### Strategy Risk
1. Multiple filters may lead to missing some effective trading opportunities.
2. Frequent trading signals may occur in volatile markets.
3. Parameter optimization may lead to overfitting of historical data.
4. ATR stop loss may be too large in high volatility markets.
#### Strategy optimization direction
1. Introduce an adaptive parameter mechanism to dynamically adjust various parameters according to market conditions.
2. Add a market environment identification module and use different parameter combinations in different market environments.
3. Add trading time filtering to avoid periods of greater volatility.
4. Optimize the stop-loss and take-profit ratios and consider dynamic adjustments based on market volatility.
5. Increase the graded judgment of trend intensity and adopt different position management strategies under different intensities.
#### Summary
This strategy builds a relatively complete trading system through the coordination of multiple technical indicators. Its core advantage is to improve the accuracy of transactions through multi-dimensional signal confirmation, while using scientific risk management methods to protect the safety of funds. Although there are certain limitations, through continuous optimization and improvement, this strategy is expected to achieve stable returns in actual transactions. ||
#### Overview
This strategy is a trend breakthrough trading system based on multiple technical indicator filters. It combines multiple technical indicators including Exponential Moving Average (EMA), Volume Weighted Average Price (VWAP), Relative Strength Index (RSI), Average Directional Index (ADX), etc., to filter false breakouts through multiple signal confirmations and improve trading accuracy. The strategy also incorporates higher timeframe trend judgment and employs an ATR-based dynamic stop-loss and take-profit scheme for effective risk control.

#### Strategy Principles
The core logic of the strategy is based on the following key elements:
1. Trend Judgment System: Uses 9-period and 21-period EMA crossovers to capture short-term trend changes, while referencing 15-minute timeframe 50-period EMA to confirm larger trend direction.
2. Price Momentum Confirmation: Uses RSI indicator for momentum confirmation, requiring RSI>55 for longs and RSI<45 for shorts.
3. Trend Strength Verification: Incorporates ADX indicator to judge trend strength, requiring ADX>25 to ensure trend validity.
4. Price Position Verification: Uses VWAP as a reference for price position, requiring price to be in the correct VWAP position.
5. Volume Confirmation: Requires trading volume to be 1.5 times greater than 10-period average volume to ensure sufficient market participation.
6. Risk Management: Dynamically calculates position size based on fixed percentage of account equity and ATR, using 1.5x ATR for stop-loss and 3x ATR for take-profit.

#### Strategy Advantages
1. Multiple signal confirmation mechanism greatly reduces interference from false signals.
2. Combination of higher and lower timeframe analysis improves trend judgment accuracy.
3. Dynamic position management and stop-loss/take-profit settings achieve good risk control.
4. Usage of volume breakout as trade confirmation improves trading reliability.
5. Strong parameter adjustability facilitates optimization for different market conditions.

#### Strategy Risks
1. Multiple filters may cause missing some valid trading opportunities.
2. May generate frequent trading signals in ranging markets.
3. Parameter optimization may lead to overfitting historical data.
4. ATR stops may be too wide in highly volatile markets.

#### Strategy Optimization Directions
1. Introduce adaptive parameter mechanism to dynamically adjust parameters based on market conditions.
2. Add market environment recognition module to use different parameter combinations in different market environments.
3. Include trading time filters to avoid highly volatile periods.
4. Optimize stop-loss and take-profit ratios, considering dynamic adjustment based on market volatility.
5. Add trend strength grading to adopt different position management strategies at different strength levels.

#### Summary
This strategy constructs a relatively complete trading system through the synergy of multiple technical indicators. Its core advantage lies in improving trading accuracy through multi-dimensional signal confirmation while employing scientific risk management methods to protect capital safety. Although certain limitations exist, through continuous optimization and improvement, this strategy has the potential to achieve stable returns in actual trading.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-11-19 00:00:00
end: 2024-12-18 08:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Trend-Filtered Scalping Strategy", overlay=true, shorttitle="TFSS")

// Inputs
emaShort     = input.int(9, title="EMA Short", minval=1)
emaLong      = input.int(21, title="EMA Long", minval=1)
rsiLength    = input.int(14, title="RSI Length", minval=1)
atrLength    = input.int(14, title="ATR Length", minval=1)
adxLength    = input.int(20, title="ADX Length", minval=1)
adxSmoothing = input.int(14, title="ADX Smoothing", minval=1)
volMultiplier = input.float(1.5, title="Volume Spike Multiplier", minval=1.0)
riskPercent  = input.float(1, title="Risk % of Equity", minval=0.1, step=0.1)

// Higher Time Frame for Trend Filter
htfTimeframe = input.timeframe("15", title="Higher Time Frame")
ema50HTF     = request.security(syminfo.tickerid, htfTimeframe, ta.ema(close, 50))

// Indicators
ema9  = ta.ema(close, emaShort)
ema21 = ta.ema(close, emaLong)
vwap  = ta.vwap(close)
rsi   = ta.rsi(close, rsiLength)
atr   = ta.atr(atrLength)
volAvg = ta.sma(volume, 10)

// ADX Calculation with Smoothing
[_, _, adx] = ta.dmi(adxLength, adxSmoothing)

// Entry Conditions
longCondition = (ta.crossover(ema9, ema21) and close > vwap and rsi > 55 and adx > 25 and close > ema50HTF and volume > volAvg * volMultiplier)
shortCondition = (ta.crossunder(ema9, ema21) and close < vwap and rsi < 45 and adx > 25 and close < ema50HTF and volume > volAvg * volMultiplier)

// Position Sizing Based on Risk %
capitalPerTrade = (strategy.equity * (riskPercent / 100)) / atr
longStop  = close - 1.5 * atr
longTarget = close + 3 * atr
shortStop = close + 1.5 * atr
shortTarget = close - 3 * atr

// Entry Logic
if longCondition and not strategy.opentrades
    strategy.entry("Long", strategy.long, qty=capitalPerTrade)
    strategy.exit("Exit Long", from_entry="Long", stop=longStop, limit=longTarget)

if shortCondition and not strategy.opentrades
    strategy.entry("Short", strategy.short, qty=capitalPerTrade)
    strategy.exit("Exit Short", from_entry="Short", stop=shortStop, limit=shortTarget)

// Alerts
alertcondition(longCondition, title="Long Entry Alert", message="Long Condition Triggered!")
alertcondition(shortCondition, title="Short Entry Alert", message="Short Condition Triggered!")

// Plot Indicators
plot(ema9, title="EMA 9", color=color.green)
plot(ema21, title="EMA 21", color=color.red)
plot(vwap, title="VWAP", color=color.blue)
plot(ema50HTF, title="HTF EMA 50", color=color.purple)
hline(55, "RSI Long Threshold", color=color.green)
hline(45, "RSI Short Threshold", color=color.red)

```

> Detail

https://www.fmz.com/strategy/475618

> Last Modified

2024-12-20 15:49:05
