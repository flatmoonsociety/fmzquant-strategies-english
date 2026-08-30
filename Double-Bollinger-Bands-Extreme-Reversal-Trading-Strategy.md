
> Name

Double-Bollinger-Bands-Extreme-Reversal-Trading-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d8ecd435c200d5cfce62.png)
![IMG](https://www.fmz.com/upload/asset/2d912ab43ee11636949b1.png)


[trans]## Overview
The Double Bollinger Bands extreme reversal trading strategy is a quantitative trading method based on statistical principles. It identifies the extreme fluctuation areas of the market and captures high-probability reversal trading opportunities by setting two sets of Bollinger Bands with different standard deviation multiples (2 times the standard deviation and 3 times the standard deviation). This strategy builds a structured risk-return framework by using extreme conditions when price hits or crosses 3x SD Bollinger Bands as trading signal triggers, and uses 2x SD Bollinger Bands as profit-taking areas.
The core assumption of this strategy is that when the price reaches a statistically extreme area (outside the 3x standard deviation Bollinger Band), the market will tend to have a mean reversion trend. Therefore, reversal opportunities can be captured by longing the breakthrough of the 3x standard deviation Bollinger Band below and shorting the breakout of the upper 3x standard deviation Bollinger Band. At the same time, the strategy enables traders to intuitively identify trading opportunities through visual marking of buy and sell signals, dynamic Bollinger Band drawing, and candlestick coloring when price hits extreme levels of volatility.
## Strategy Principle
The working principle of the Double Bollinger Bands Extreme Value Reversal trading strategy is based on the following core components:
1. **Double Bollinger Bands Settings**:
   - Level 1: Based on the 20-period moving average (SMA) plus or minus 2 times the standard deviation
   - Second level: Based on the 20-period moving average (SMA) plus or minus 3 times the standard deviation
2. **Admission conditions**:
   - Long entry: the price crosses the lower 3 times standard deviation Bollinger Band (lower2) upwards
   - Short entry: the price crosses the upper 3 times standard deviation Bollinger Band (upper2) downwards
3. **Exit Conditions**:
   - Long exit: the price crosses the upper 2 times standard deviation Bollinger Band (upper1) upwards
   - Short exit: the price crosses the lower 2 times standard deviation Bollinger Band (lower1) downwards
4. **Visual aids**:
   - Bollinger Band Drawing: Different colors distinguish Bollinger Bands with different standard deviation multiples
   - Buy and sell signal mark: Display buy or sell mark when entry conditions are met
   - Candlestick Coloring: Color candlesticks white when price hits 3x standard deviation Bollinger Bands, emphasizing extreme price areas
From the perspective of code implementation, the strategy first calculates a simple moving average based on 20 periods as the middle track of the Bollinger Bands, and then calculates 2 times and 3 times the standard deviation as a measure of the fluctuation range, thereby constructing a two-layer Bollinger Bands system. The trading signal uses the ta.crossover and ta.crossunder functions to identify the intersection between the price and the Bollinger Bands to achieve accurate entry and exit timing judgments.
## Strategic Advantages
1. **Statistical Basics**: This strategy is based on the normal distribution principle in statistics, using standard deviation to quantify market volatility, and has a solid theoretical foundation. Under the assumption of normal distribution, the probability that the price is outside 3 times the standard deviation is only about 0.3%, providing a very high probability of reversal opportunity.
2. **Clear entry and exit rules**: The strategy defines clear entry and exit conditions, reducing the interference of subjective judgment and helping to maintain trading discipline.
3. **Risk Control Structured**: By using 3x standard deviation Bollinger Bands as entry points and 2x standard deviation Bollinger Bands as exit points, the strategy has a built-in risk management framework so that each trade has a good risk-return ratio.
4. **Adapt to different market environments**: This strategy can not only capture mean reversion opportunities in volatile markets, but also enter through extreme reversal points in trending markets, showing strong adaptability.
5. **Rich visual feedback**: Through Bollinger Band visualization, trading signal markers and candlestick coloring of special price levels, the strategy provides rich visual feedback to help traders quickly identify and evaluate trading opportunities.
6. **Simple parameters**: The strategy only needs to set one main parameter, the Bollinger Band length, which is simple to operate and reduces the risk of over-optimization.
## Strategy Risk
1. **False breakthrough risk**: The price may briefly cross the 3 times standard deviation Bollinger Band and then immediately return, causing a false signal. The solution is to add a confirmation indicator or set a time filter that requires the price to stay in a specific area for a minimum time.
2. **Counter-trend trading risk when the trend is strong**: In a strong trending market, prices may continue to operate in extreme areas, resulting in continuous losses. The solution is to combine trend indicators (such as moving average direction or ADX indicator) and only trade in the direction consistent with the main trend.
3. **Black swan event risk**: Market emergencies may cause violent price fluctuations beyond normal statistical distribution assumptions. The solution is to set a fixed stop loss, or use a volatility filter to pause trading during periods of extreme volatility.
4. **Parameter Stability Risk**: The fixed 20 period and 2/3 times standard deviation settings may not work for all markets and time frames. The solution is to backtest different parameter combinations to find the optimal parameters for a specific market, or consider using adaptive Bollinger Band width.
5. **Over-trading in a high-volatility environment**: In a high-volatility environment, prices may frequently hit extreme Bollinger Bands, generating too many trading signals. The solution is to include trading frequency limits or volatility filters.
## Strategy optimization direction
1. **Add Trending Filter**:
   Combine with trend indicators (such as longer-period moving averages or the ADX indicator) to filter trading signals to only trade in the direction of the trend or to reinforce signals that are consistent with the trend. Such optimization can significantly reduce losses caused by contrarian trading.
2. **Adaptive Bollinger Bands Parameters**:
   Change the fixed Bollinger Band length and standard deviation multiple to adaptive parameters based on market volatility, such as reducing the standard deviation multiple in a low-volatility environment and increasing the standard deviation multiple in a high-volatility environment. This allows the strategy to better adapt to different market conditions.
3. **Add transaction volume filter**:
   Adding a trading volume confirmation mechanism will only enter the market when a price breakthrough is accompanied by a large enough trading volume, which can reduce the risk of false breakthroughs.
4. **Add time filter**:
   Implementing time filtering function to avoid the release of major economic data or specific periods of high volatility can reduce false signals caused by market noise.
5. **Stop Loss and Partial Profit Strategy**:
   Adding dynamic stop-loss settings and partial profit-taking features, such as partial closing of positions when the price returns to the mid-range (SMA), can improve the overall risk-adjusted return of the strategy.
6. **Optimize exit logic**:
   The current strategy uses a fixed 2 times standard deviation Bollinger Band as the exit point. You can consider dynamically adjusting the exit point according to the market status, or combining other technical indicators to optimize the exit timing.
## Summarize
The Double Bollinger Bands extreme value reversal trading strategy is a quantitative trading method that combines statistical principles and technical analysis to obtain profits by identifying reversal opportunities when the price reaches the extreme statistical area (3 times the standard deviation). This strategy has clear rules, a good risk control structure and rich visual feedback, making it suitable for traders who are confident in mean reversion.
However, this strategy also faces risks such as false breakouts, contrarian trading, and parameter stability. The robustness and profitability of the strategy can be further improved by adding trend filtering, adaptive parameters, volume confirmation and improved stop-loss and take-profit strategies.
Overall, this is a well-designed basic strategy framework that can be used both on its own and as part of a more complex trading system. This is a strategic option worth considering for traders seeking to identify market extreme reversal opportunities based on statistical methods. || ## Overview
The Double Bollinger Bands Extreme Reversal Trading Strategy is a quantitative trading approach based on statistical principles that identifies high-probability reversal opportunities by utilizing two sets of Bollinger Bands with different standard deviation multipliers (2SD and 3SD). This strategy triggers entry signals when price touches or crosses the extreme 3SD Bollinger Bands and uses the 2SD Bollinger Bands as profit-taking zones, thus creating a structured risk-reward framework.

The core assumption of this strategy is that when prices reach statistically extreme areas (beyond the 3SD Bollinger Bands), markets tend to exhibit mean reversion tendencies. Therefore, opportunities can be captured by going long when price breaks above the lower 3SD band and going short when price breaks below the upper 3SD band. Additionally, the strategy incorporates visual buy/sell signal markers, dynamic Bollinger Band plotting, and candle coloring when price touches extreme volatility levels, allowing traders to visually identify trading opportunities.

## Strategy Principles

The Double Bollinger Bands Extreme Reversal Trading Strategy operates based on the following core components:

1. **Dual Bollinger Bands Setup**:
   - First Layer: Based on a 20-period Simple Moving Average (SMA) plus/minus 2 standard deviations
   - Second Layer: Based on a 20-period Simple Moving Average (SMA) plus/minus 3 standard deviations

2. **Entry Conditions**:
   - Long Entry: Price crosses above the lower 3SD Bollinger Band (lower2)
   - Short Entry: Price crosses below the upper 3SD Bollinger Band (upper2)

3. **Exit Conditions**:
   - Long Exit: Price crosses above the upper 2SD Bollinger Band (upper1)
   - Short Exit: Price crosses below the lower 2SD Bollinger Band (lower1)

4. **Visual Aids**:
   - Bollinger Bands Plotting: Different colors to distinguish different standard deviation multipliers
   - Buy/Sell Signal Markers: Displays buy or sell markers when entry conditions are met
   - Candle Coloring: When price touches the 3SD Bollinger Bands, candles are colored white to emphasize extreme price zones

From the code implementation, the strategy first calculates a 20-period simple moving average as the middle band of the Bollinger Bands, then calculates 2SD and 3SD to measure volatility range, thus constructing the dual Bollinger Bands system. Trading signals are identified through the ta.crossover and ta.crossunder functions to detect price crossovers with the Bollinger Bands, enabling precise entry and exit timing.

## Strategy Advantages

1. **Statistical Foundation**: The strategy is based on the principles of normal distribution in statistics, using standard deviation to quantify market volatility, providing a solid theoretical foundation. Under normal distribution assumptions, the probability of price being outside the 3SD bands is only about 0.3%, offering high-probability reversal opportunities.

2. **Clear Entry and Exit Rules**: The strategy defines precise entry and exit conditions, reducing the interference of subjective judgment and helping maintain trading discipline.

3. **Structured Risk Control**: By using the 3SD Bollinger Bands as entry points and the 2SD Bollinger Bands as exit points, the strategy incorporates a risk management framework, ensuring a favorable risk-reward ratio for each trade.

4. **Adaptability to Different Market Environments**: The strategy can capture mean reversion opportunities in ranging markets and enter at extreme reversal points in trending markets, demonstrating strong adaptability.

5. **Rich Visual Feedback**: Through Bollinger Bands visualization, trade signal markers, and candle coloring at special price levels, the strategy provides rich visual feedback, helping traders quickly identify and evaluate trading opportunities.

6. **Simple Parameters**: The strategy primarily requires setting only one main parameter - the Bollinger Bands length, making it simple to operate and reducing the risk of over-optimization.

## Strategy Risks

1. **False Breakout Risk**: Price may briefly cross the 3SD Bollinger Bands and then immediately revert, generating false signals. A solution is to add confirmation indicators or set time filters, requiring the price to stay in the specific zone for a minimum time.

2. **Counter-Trend Trading Risk in Strong Trends**: In strong trending markets, prices may continue to run in extreme zones, causing consecutive losses. A solution is to combine trend indicators (such as moving average direction or ADX indicator) and only trade in the direction consistent with the main trend.

3. **Black Swan Event Risk**: Sudden market events may cause violent price fluctuations beyond normal statistical distribution assumptions. Solutions include setting fixed stop losses or using volatility filters to pause trading during periods of extreme volatility.

4. **Parameter Stability Risk**: The fixed 20-period and 2/3SD settings may not be applicable to all markets and timeframes. Solutions include backtesting different parameter combinations to find optimal parameters for specific markets or considering adaptive Bollinger Bands width.

5. **Excessive Trading in High Volatility Environments**: In high volatility environments, prices may frequently touch extreme Bollinger Bands, generating too many trading signals. Solutions include adding trade frequency limits or volatility filter conditions.

## Strategy Optimization Directions

1. **Add Trend Filters**:
   Incorporate trend indicators (such as longer-period moving average direction or ADX indicator) to filter trading signals, only trading in the trend direction or strengthening signals consistent with the trend. This optimization can significantly reduce losses from counter-trend trading.

2. **Adaptive Bollinger Bands Parameters**:
   Change the fixed Bollinger Bands length and standard deviation multipliers to adaptive parameters based on market volatility, such as reducing standard deviation multipliers in low volatility environments and increasing them in high volatility environments. This allows the strategy to better adapt to different market states.

3. **Add Volume Filters**:
   Incorporate volume confirmation mechanisms, only entering when price breakouts are accompanied by sufficient trading volume, which can reduce the risk of false breakouts.

4. **Add Time Filters**:
   Implement time filtering functionality to avoid major economic data releases or specific high volatility periods, which can reduce erroneous signals caused by market noise.

5. **Stop Loss and Partial Profit Strategy**:
   Add dynamic stop loss settings and partial profit features, such as partially closing positions when price returns to the middle band (SMA), which can improve the strategy's overall risk-adjusted returns.

6. **Optimize Exit Logic**:
   The current strategy uses fixed 2SD Bollinger Bands as exit points. Consider dynamically adjusting exit points based on market conditions or combining other technical indicators to optimize exit timing.

## Summary

The Double Bollinger Bands Extreme Reversal Trading Strategy is a quantitative trading method that combines statistical principles with technical analysis, capturing reversal opportunities when prices reach extreme statistical areas (3SD). The strategy features clear rules, good risk control structure, and rich visual feedback, suitable for traders who have confidence in mean reversion.

However, the strategy also faces risks such as false breakouts, counter-trend trading, and parameter stability issues. By adding trend filters, adaptive parameters, volume confirmation, and improved stop-loss and profit-taking strategies, the robustness and profitability of the strategy can be further enhanced.

Overall, this is a well-designed basic strategy framework that can be used independently or as part of a more complex trading system. For traders seeking to identify market extreme reversal opportunities based on statistical methods, this is a strategy worth considering.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-03-04 00:00:00
end: 2024-07-02 00:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"ETH_USDT"}]
*/

//@version=5
strategy("Double Bollinger Bands Strategy with Signals (By Rolwin)", overlay=true)

// Input settings
length = input(20, title="Bollinger Bands Length")
src = close

// Bollinger Bands (Standard Deviation Levels)
bb1_mult = 2.0
bb2_mult = 3.0
basis = ta.sma(src, length)
dev1 = bb1_mult * ta.stdev(src, length)
dev2 = bb2_mult * ta.stdev(src, length)

// Band Levels
upper1 = basis + dev1
lower1 = basis - dev1
upper2 = basis + dev2
lower2 = basis - dev2

// **Trading Conditions**
longCondition = ta.crossover(src, lower2)  // Price crosses above lower 3SD band
shortCondition = ta.crossunder(src, upper2)  // Price crosses below upper 3SD band

// **Exit Conditions**
exitLong = ta.crossover(src, upper1)  // Exit long at upper 2SD band
exitShort = ta.crossunder(src, lower1)  // Exit short at lower 2SD band

// **Execute trades**
strategy.entry("Long", strategy.long, when=longCondition)
strategy.entry("Short", strategy.short, when=shortCondition)

strategy.close("Long", when=exitLong)
strategy.close("Short", when=exitShort)

// **Plot Bollinger Bands**
plot(upper1, color=color.blue, title="Upper Band (2 SD)")
plot(lower1, color=color.blue, title="Lower Band (2 SD)")
plot(upper2, color=color.red, title="Upper Band (3 SD)")
plot(lower2, color=color.red, title="Lower Band (3 SD)")
plot(basis, color=color.gray, title="Middle Band (SMA)")

// **Plot Buy & Sell Signals**
plotshape(longCondition, location=location.belowbar, color=color.green, style=shape.labelup, size=size.small, title="BUY Signal")
plotshape(shortCondition, location=location.abovebar, color=color.red, style=shape.labeldown, size=size.small, title="SELL Signal")

// **Candle Coloring for 3SD Touch**
touches3SD = (src >= upper2) or (src <= lower2)
barcolor(touches3SD ? color.white : na)  // Change to white if touching 3SD band

```

> Detail

https://www.fmz.com/strategy/484919

> Last Modified

2025-03-05 10:10:08
