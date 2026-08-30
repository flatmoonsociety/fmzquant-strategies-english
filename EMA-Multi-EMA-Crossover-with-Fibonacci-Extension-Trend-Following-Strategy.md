
> Name

Multi-EMA-Crossover-with-Fibonacci-Extension-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/13984da6547d556328d.png)

[trans]

#### Overview
This strategy is a trend following system that combines multiple exponential moving average (EMA) crossovers and Fibonacci extension levels. It utilizes the interaction between EMAs of different periods to identify potential trend starts and ends, while using Fibonacci extension levels to identify profit targets. The strategy also includes specific stop-loss rules to manage risk and protect profits.
#### Strategy Principle
The core of this strategy is to utilize EMA crossovers across multiple time frames to capture the beginning and end of a trend. Specifically, it uses 5-, 10-, and 30-period EMAs. The strategy consists of four different entry conditions, each designed to capture a different market scenario:
1. The first entry condition is triggered when the price touches or falls below the 30-period EMA, but then closes above it, while the 10-period EMA is higher than the 5-period EMA, and the 30-period EMA is 1% lower than the 5-period EMA.
2. When the 5-period EMA crosses above the 30-period EMA, and the 30-period EMA has crossed below the 5-period EMA in the past 6 K lines, the second entry condition is triggered.
3. The highest price of the current two K lines is lower than their respective 5-period EMA, and the 5-period EMA is lower than the 10-period EMA, and the 10-period EMA is lower than the 30-period EMA. At the same time, when the highest price of the previous K line is lower than the current closing price, the third entry condition is triggered.
4. When the 10-period EMA crosses above the 30-period EMA, and the 5-period EMA has crossed above the 30-period EMA in the past 4 K lines, and the current values ​​of the 10-period EMA and the 5-period EMA are both higher than their previous values, the fourth entry condition is triggered.
For stop losses, the strategy sets specific rules for different entry conditions:
- For the first condition, if the 30-period EMA crosses the 10-period EMA, close the position.
- For other conditions, if the closing price falls below the lowest point of the first three candlesticks, the position will be closed.
Profit targets are set based on Fibonacci extension levels, including 0.618, 0.786, 1.0 and 1.618 levels. When the price reaches these levels, the strategy closes the position according to specific rules.
In addition, the strategy also includes a profit locking condition: if the lowest price of the two recent K lines is higher than the 5-period EMA, and the EMA is in an ascending order (5 > 10 > 30), the position will be closed to lock in profits.
#### Strategic Advantages
1. Multiple confirmations: By using multiple EMAs and multiple entry conditions, the strategy is able to more accurately identify the start and continuation of a trend. This multiple confirmation mechanism can reduce false signals and improve the accuracy of transactions.
2. Strong adaptability: Four different entry conditions enable the strategy to adapt to different market environments. Whether it is a rapid breakthrough or a slow trend formation, trading opportunities can be captured.
3. Risk management: The strategy includes specific stop-loss rules, which help control the risk of each transaction. Different entry conditions correspond to different stop-loss strategies, indicating that the strategy attaches great importance to risk management.
4. Clear profit target: Using Fibonacci extension levels as profit targets provides traders with a clear exit point. This helps avoid taking profits too early or holding on to them too long.
5. Profit Protection: Profit lock conditions help protect earned profits when the trend may reverse, which is an important aspect that many trend following strategies overlook.
6. Combination of technical indicators: The strategy combines EMA and Fibonacci tools, taking advantage of the advantages of these two popular technical analysis tools.
#### Strategy Risk
1. Overtrading: Multiple entry conditions can lead to overtrading, especially in volatile markets. This may increase transaction costs and may lead to more false signals.
2. Parameter sensitivity: The strategy uses multiple fixed EMA periods and percentage thresholds. These parameters may need to be adjusted based on different markets and time frames, otherwise it may result in poor performance of the strategy.
3. Trend dependence: As a trend following strategy, it may not perform well in sideways or volatile markets. In these market environments, multiple false signals and small losses may occur.
4. Lagging: EMA is essentially a lagging indicator. In a rapidly changing market, strategies may not be able to capture trend turning points in time.
5. Complexity: The multiple conditions and rules of the strategy increase its complexity, which may make the strategy difficult to understand and maintain, and also increases the risk of overfitting.
#### Strategy optimization direction
1. Dynamic parameter adjustment: Consider introducing an adaptive mechanism to dynamically adjust the EMA cycle and other parameters according to market volatility. This can improve the adaptability of the strategy in different market environments.
2. Add trading volume indicators: Combining trading volume analysis can improve the accuracy of entry and exit decisions. For example, an increase in volume on entry can be required to confirm the strength of the trend.
3. Market environment filtering: Introduce a market environment identification mechanism, such as using ATR (average true range) or volatility indicators to suspend trading in market environments that are not suitable for trend tracking.
4. Optimize the stop loss mechanism: Consider using trailing stop loss instead of fixed stop loss. This protects profits while allowing them to continue to grow.
5. Add time filtering: restricting transactions in specific time periods and avoiding time periods with greater volatility or poor liquidity can improve the stability of the strategy.
6. Introducing machine learning: Using machine learning algorithms to optimize parameter selection and entry decisions can improve the adaptability and performance of the strategy.
7. Multi-time frame analysis: Combining trend analysis with longer time frames can improve the accuracy of entry decisions and avoid entry when the main trend is reversed.
#### Summarize
This Multiple EMA Crossover combined with Fibonacci Extensions trend following strategy demonstrates a comprehensive trading system that combines multiple technical indicators and trading concepts. By using multiple EMAs and entry conditions, the strategy attempts to strike a balance between capturing trends and reducing false signals. The use of Fibonacci extension levels provides an objective basis for profit target setting, while specific stop loss and profit locking rules reflect the emphasis on risk management.
Although the strategy has the advantages of multiple confirmations and strong adaptability, its complexity and sensitivity to parameter selection also bring certain challenges. In order to further improve the robustness and performance of the strategy, you can consider introducing optimization directions such as dynamic parameter adjustment, market environment filtering, and multi-time frame analysis.
Overall, this strategy provides an interesting framework for trend following, but traders need to perform sufficient backtesting and parameter optimization when applying it, and make appropriate adjustments based on specific markets and trading styles. With continuous monitoring and optimization, this strategy has the potential to become an effective trend following tool.
||

#### Overview

This strategy is a trend following system that combines multiple Exponential Moving Average (EMA) crossovers with Fibonacci extension levels. It utilizes the interaction between EMAs of different periods to identify potential trend beginnings and endings, while using Fibonacci extension levels to determine profit targets. The strategy also incorporates specific stop-loss rules to manage risk and protect profits.

#### Strategy Principles

The core of this strategy lies in using EMA crossovers across multiple timeframes to capture the initiation and termination of trends. Specifically, it employs 5-period, 10-period, and 30-period EMAs. The strategy includes four different entry conditions, each designed to capture different market scenarios:

1. The first entry condition is triggered when the price touches or falls below the 30-period EMA but subsequently closes above it, while the 10-period EMA is above the 5-period EMA, and the 30-period EMA is 1% lower than the 5-period EMA.

2. The second entry condition is triggered when the 5-period EMA crosses above the 30-period EMA, and the 30-period EMA has crossed below the 5-period EMA within the last 6 bars.

3. The third entry condition is triggered when the highs of the previous two bars are below their respective 5-period EMAs, the 5-period EMA is below the 10-period EMA, which is below the 30-period EMA, and the high of the previous bar is below the current close.

4. The fourth entry condition is triggered when the 10-period EMA crosses above the 30-period EMA, the 5-period EMA has crossed above the 30-period EMA within the last 4 bars, and both the 10-period and 5-period EMAs' current values are higher than their previous values.

For stop-loss, the strategy sets specific rules for different entry conditions:

- For the first condition, the position is closed if the 30-period EMA crosses above the 10-period EMA.
- For other conditions, the position is closed if the closing price falls below the lowest low of the previous three bars.

Profit targets are set based on Fibonacci extension levels, including 0.618, 0.786, 1.0, and 1.618 levels. The strategy closes positions when these levels are reached, according to specific rules.

Additionally, the strategy includes a profit lock condition: if the lows of the last two bars are above the 5-period EMA and the EMAs are aligned in ascending order (5 > 10 > 30), the position is closed to lock in profits.

#### Strategy Advantages

1. Multiple Confirmations: By using multiple EMAs and entry conditions, the strategy can more accurately identify the start and continuation of trends. This multi-confirmation mechanism can reduce false signals and improve trading accuracy.

2. High Adaptability: Four different entry conditions allow the strategy to adapt to various market environments, capturing trading opportunities whether in rapid breakouts or slow trend formations.

3. Risk Management: The strategy includes specific stop-loss rules, which helps control risk for each trade. Different entry conditions correspond to different stop-loss strategies, indicating the strategy's emphasis on risk management.

4. Clear Profit Targets: Using Fibonacci extension levels as profit targets provides traders with clear exit points. This helps avoid premature profit-taking or holding positions for too long.

5. Profit Protection: The profit lock condition helps protect gained profits when the trend might reverse, an important aspect often overlooked by many trend-following strategies.

6. Combination of Technical Indicators: The strategy combines EMAs and Fibonacci tools, leveraging the strengths of these two popular technical analysis tools.

#### Strategy Risks

1. Overtrading: Multiple entry conditions may lead to overtrading, especially in highly volatile markets. This could increase transaction costs and potentially lead to more false signals.

2. Parameter Sensitivity: The strategy uses multiple fixed EMA periods and percentage thresholds. These parameters may need to be adjusted for different markets and timeframes, otherwise, they might lead to poor strategy performance.

3. Trend Dependency: As a trend-following strategy, it may perform poorly in ranging or oscillating markets. In these market environments, it may generate multiple false signals and small losses.

4. Lag: EMAs are inherently lagging indicators. In rapidly changing markets, the strategy may not be able to capture trend turning points in a timely manner.

5. Complexity: The strategy's multiple conditions and rules increase its complexity, which may make it difficult to understand and maintain, and also increases the risk of overfitting.

#### Strategy Optimization Directions

1. Dynamic Parameter Adjustment: Consider introducing an adaptive mechanism to dynamically adjust EMA periods and other parameters based on market volatility. This can improve the strategy's adaptability in different market environments.

2. Incorporate Volume Indicators: Combining volume analysis can improve the accuracy of entry and exit decisions. For example, requiring increased volume at entry to confirm trend strength.

3. Market Environment Filtering: Introduce a market environment identification mechanism, such as using ATR (Average True Range) or volatility indicators, to pause trading in environments unsuitable for trend following.

4. Optimize Stop-Loss Mechanism: Consider using trailing stops instead of fixed stops. This can protect profits while allowing them to continue growing.

5. Add Time Filtering: Limit trading to specific time periods, avoiding highly volatile or low liquidity periods, which can improve strategy stability.

6. Introduce Machine Learning: Use machine learning algorithms to optimize parameter selection and entry decisions, which can improve the strategy's adaptability and performance.

7. Multi-Timeframe Analysis: Incorporate trend analysis from longer timeframes to improve entry decision accuracy and avoid entering against the main trend.

#### Conclusion

This Multi-EMA Crossover with Fibonacci Extension Trend Following Strategy demonstrates a comprehensive trading system that combines multiple technical indicators and trading concepts. By using multiple EMAs and entry conditions, the strategy attempts to strike a balance between capturing trends and reducing false signals. The use of Fibonacci extension levels provides an objective basis for setting profit targets, while specific stop-loss and profit locking rules reflect an emphasis on risk management.

Although the strategy has advantages in multiple confirmations and high adaptability, its complexity and sensitivity to parameter selection also present certain challenges. To further improve the strategy's robustness and performance, considerations can be given to introducing dynamic parameter adjustment, market environment filtering, and multi-timeframe analysis as optimization directions.

Overall, this strategy provides an interesting framework for trend following, but traders need to conduct thorough backtesting and parameter optimization when applying it in practice, and make appropriate adjustments based on specific markets and trading styles. Through continuous monitoring and optimization, this strategy has the potential to become an effective trend-following tool.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-06-01 00:00:00
end: 2024-06-30 23:59:59
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("EMA Combined Strategy with Specific Stop Loss", overlay=true)

// Define the EMAs
ema30 = ta.ema(close, 30)
ema10 = ta.ema(close, 10)
ema5 = ta.ema(close, 5)

// Define the conditions for opening an order
open_condition1 = low <= ema30 and close > ema30  and ema10 > ema5 and ema30 * 1.01 < ema5
open_condition2 = ta.crossover(ema5, ema30) and (ta.crossover(ema30[1], ema5[1]) or ta.crossover(ema30[2], ema5[2]) or ta.crossover(ema30[3], ema5[3]) or ta.crossover(ema30[4], ema5[4])  or ta.crossover(ema30[5], ema5[5]) or ta.crossover(ema30[6], ema5[6]) )
open_condition3 = high[2] < ema5[2] and high[1] < ema5[1] and ema5 < ema10 and ema10 < ema30 and high[1] < close 
open_condition4 = ta.crossover(ema10, ema30) and (ta.crossover(ema5[0], ema30[0]) or ta.crossover(ema5[1], ema30[1]) or ta.crossover(ema10[2], ema30[2]) or ta.crossover(ema10[3], ema30[3])) and ema10[1] < ema10 and ema5[1] <ema5

// Calculate the lowest low of the previous two bars
lowest_low_prev_two_bars = ta.lowest(low, 3)

// Track the entry price and the lowest low of the previous two bars for open_condition3
var float entry_price = na
var float low_entry_price = na
var float entry_lowest_low1 = na
var float entry_lowest_low2 = na
var float entry_lowest_low3 = na
var float entry_lowest_low4 = na

var bool order1 = false
var bool order2 = false
var bool order3 = false
var bool order4 = false
// Fibonacci extension levels based on the last significant swing
var float fib_extension_level_0_618 = na
var float fib_extension_level_0_786 = na
var float fib_extension_level_1 = na
var float fib_extension_level_1_618 = na

    // Calculate Fibonacci extension levels
var float swing_low = na
var float swing_high = na
// Here we assume the latest swing low and swing high, adjust based on your logic
swing_low := ta.lowest(low, 20)
swing_high := ta.highest(high, 20)

// Open a long order when any of the conditions are met
if open_condition1 and not order2 and not order1 and not order3 and not order4
    strategy.entry("Long", strategy.long, comment="<ema30")
    entry_lowest_low1 := lowest_low_prev_two_bars
    low_entry_price := low
    fib_extension_level_0_618 := low_entry_price + (swing_high - swing_low) * 0.618
    fib_extension_level_0_786:= low_entry_price + (swing_high - swing_low) * 0.786
    fib_extension_level_1:= low_entry_price + (swing_high - swing_low) * 1
    fib_extension_level_1:= low_entry_price + (swing_high - swing_low) * 1.618
    entry_price := close
    order1 := true
if open_condition2 and not order2 and not order1 and not order3 and not order4
    strategy.entry("Long", strategy.long, comment="ema5xema30")
    entry_lowest_low2 := lowest_low_prev_two_bars
    low_entry_price := low
    fib_extension_level_0_618 := low_entry_price + (swing_high - swing_low) * 0.618
    fib_extension_level_0_786:= low_entry_price + (swing_high - swing_low) * 0.786
    fib_extension_level_1:= low_entry_price + (swing_high - swing_low) * 1
    fib_extension_level_1:= low_entry_price + (swing_high - swing_low) * 1.618
    entry_price := close
    order2 := true

if open_condition3 and not order2 and not order1 and not order3 and not order4
    strategy.entry("Long", strategy.long, comment="high<ema5")
    entry_price := close
    low_entry_price := low
    entry_lowest_low3 := lowest_low_prev_two_bars
    fib_extension_level_0_618 := low_entry_price + (swing_high - swing_low) * 0.618
    fib_extension_level_0_786:= low_entry_price + (swing_high - swing_low) * 0.786
    fib_extension_level_1:= low_entry_price + (swing_high - swing_low) * 1
    fib_extension_level_1:= low_entry_price + (swing_high - swing_low) * 1.618
    order3 := true

if open_condition4 and not order2 and not order1 and not order3 and not order4
    strategy.entry("Long", strategy.long, comment="high<ema5444")
    entry_price := close
    low_entry_price := low
    entry_lowest_low4 := lowest_low_prev_two_bars
    fib_extension_level_0_618 := low_entry_price + (swing_high - swing_low) * 0.618
    fib_extension_level_0_786:= low_entry_price + (swing_high - swing_low) * 0.786
    fib_extension_level_1:= low_entry_price + (swing_high - swing_low) * 1
    fib_extension_level_1:= low_entry_price + (swing_high - swing_low) * 1.618
    order4 := true




// Set a stop loss only if the order was opened with the specified conditions
if (not na(entry_price))
    if order1
        if ta.crossover(ema30,ema10)
            strategy.close("Long", comment="stop loss1" )
            entry_price := na
            order1 := false
            low_entry_price := na


    if order2
        if close < entry_lowest_low2
            strategy.close("Long", comment="stop loss2" )
            entry_price := na
            order2 := false
            low_entry_price := na

    if order3
        if close < entry_lowest_low3
            strategy.close("Long", comment="stop loss3" )
            entry_price := na
            order3 := false
            low_entry_price := na

    if order4
        if close < entry_lowest_low4
            strategy.close("Long", comment="stop loss4" )
            entry_price := na
            order4 := false
            low_entry_price := na


    if   low[1] > ema5[1] and low > ema5  and ema5 > ema10 and ema10 > ema30 
        strategy.close("Long", comment="profit low > ema5")
        entry_price := na
        order1 := false
        order2 := false
        order3 := false
        order4 := false
        low_entry_price := na

    // Take profit at Fibonacci extension levels
    if high >= fib_extension_level_0_618 and close <= fib_extension_level_0_618
        strategy.close("Long", comment="at 0.618 Fib")
        entry_price := na
        order1 := false
        order2 := false
        order3 := false
        order4 := false
        low_entry_price := na

    if  high >= fib_extension_level_0_786 and close < fib_extension_level_0_786
        strategy.close("Long", comment="at 0.786 Fib")
        entry_price := na
        order1 := false
        order2 := false
        order3 := false
        order4 := false
        low_entry_price := na

    if  high >= fib_extension_level_1 and close < fib_extension_level_1
        strategy.close("Long", comment="at 1 Fib")
        entry_price := na
        order1 := false
        order2 := false
        order3 := false
        order4 := false
        low_entry_price := na
    if  high >= fib_extension_level_1_618
        strategy.close("Long", comment="at 1 Fib")
        entry_price := na
        order1 := false
        order2 := false
        order3 := false
        order4 := false
        low_entry_price := na


// Plot the EMAs for visual reference
plot(ema30, color=color.blue, title="EMA 30")
plot(ema10, color=color.orange, title="EMA 10")
plot(ema5, color=color.red, title="EMA 5")
```

> Detail

https://www.fmz.com/strategy/458063

> Last Modified

2024-07-29 16:42:56
