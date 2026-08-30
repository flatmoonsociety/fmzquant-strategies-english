
> Name

Bollinger Band Overbought Oversold Strategy-Bollinger-Band-Overbought-Oversold-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/8b2aea24d519bd0e575345edd3dd6dec78a6e6fe7a1f0ac611fc18344606185a.png)

[trans]
#### Overview
The Bollinger Bands overbought and oversold strategy is a trading method based on the principles of price fluctuations and mean reversion. This strategy utilizes the Bollinger Bands and %B indicators to identify overbought and oversold conditions in the market and to look for potential buying opportunities in long-term uptrends. The core idea of ​​the strategy is to buy when prices are at a relatively low level and sell when prices reach a relatively high level, thereby capturing the gains from short-term price rebounds.
#### Strategy Principle
The strategy works based on several key elements:
1. Trend confirmation: Use the 200-day simple moving average (SMA) as a reference for long-term trends. The strategy will only consider taking trades if the closing price is above the 200-day SMA to ensure alignment with the main market trend.
2. Oversold conditions: Use the %B indicator to determine the oversold condition. When the %B value is below 0.2 for three consecutive days, it is considered to be an oversold condition. The %B indicator measures the position of the current price relative to the Bollinger Bands. Below 0.2 indicates that the price is close to the lower track and is in a potential oversold area.
3. Entry signal: When trend confirmation and oversold conditions are met, establish a long position at the close of the day.
4. Exit signal: When the %B value closes higher than 0.8, close the position and leave the market. This indicates that the price is close to the upper Bollinger Band and may have entered the overbought zone.
#### Strategic Advantages
1. Combination of trend following and reversal: Through the filtering of 200-day SMA, the strategy not only captures short-term reversal, but also ensures consistency with the long-term trend, reducing the risk of counter-trend trading.
2. Objective entry and exit conditions: Using the %B indicator provides clear entry and exit signals, reducing the bias caused by subjective judgment.
3. Mean reversion principle: The strategy takes advantage of the common mean reversion phenomenon in financial markets and trades when prices deviate far from the mean, thereby increasing the probability of profit.
4. Strong adaptability: Bollinger Bands will automatically adjust according to market volatility, allowing the strategy to adapt to different market environments.
#### Strategy Risk
1. False signal risk: In violently volatile or sideways markets, frequent false signals may occur, leading to frequent transactions and capital losses.
2. Trend turning risk: Although the 200-day SMA is used as a filter, the strategy may produce inaccurate signals near major trend turning points.
3. Lack of stop loss mechanism: There is no stop loss in the basic strategy, which may result in greater losses when the market continues to decline.
4. Market collapse risk: When the market falls sharply, the strategy may frequently trigger buy signals, causing serious financial losses.
#### Strategy optimization direction
1. Introduce dynamic stop loss: You can consider using ATR (average true range) to set dynamic stop loss to better control risks.
2. Optimize entry conditions: Additional technical indicators, such as RSI or MACD, can be added to confirm oversold conditions and reduce false signals.
3. Adjust the %B threshold: The entry and exit thresholds of %B can be dynamically adjusted according to different market environments and trading varieties.
4. Add trading volume analysis: Combining trading volume indicators can improve the reliability of signals, especially when judging market reversals.
5. Achieve opening and closing positions in batches: You can consider trading in batches when conditions are met, instead of opening or closing all positions at once.
#### Summarize
The Bollinger Bands overbought and oversold strategy is a trading method that combines trend following and mean reversion. By utilizing the Bollinger Bands and %B indicators, this strategy aims to capture short-term price rebound opportunities in the market. Although the strategy has the advantages of objectivity and adaptability, it still faces challenges such as false signals and lack of risk control. By introducing dynamic stop loss, optimizing entry conditions and combining other technical indicators, the stability and profitability of the strategy can be further improved. Traders should fully test and optimize strategy parameters before real trading to adapt to different market environments and personal risk preferences.
|| 

#### Overview

The Bollinger Band Overbought/Oversold Strategy is a trading method based on price volatility and mean reversion principles. This strategy utilizes Bollinger Bands and the %B indicator to identify overbought and oversold conditions in the market, seeking potential buying opportunities within a long-term uptrend. The core idea is to buy when prices are relatively low and sell when they reach relatively high levels, thus capturing gains from short-term price rebounds.

#### Strategy Principles

The strategy operates on the following key elements:

1. Trend Confirmation: A 200-day Simple Moving Average (SMA) is used as a reference for the long-term trend. The strategy only considers trades when the closing price is above the 200-day SMA, ensuring alignment with the primary market trend.

2. Oversold Condition: The %B indicator is used to determine oversold states. An oversold condition is considered met when the %B value remains below 0.2 for three consecutive days. The %B indicator measures the current price position relative to the Bollinger Bands, with values below 0.2 indicating proximity to the lower band and potential oversold territory.

3. Entry Signal: A long position is established at the close when both trend confirmation and oversold conditions are met.

4. Exit Signal: The position is closed when the %B value closes above 0.8, indicating that the price has potentially entered overbought territory near the upper Bollinger Band.

#### Strategy Advantages

1. Combination of Trend Following and Reversal: By filtering with the 200-day SMA, the strategy ensures consistency with the long-term trend while capturing short-term reversals, reducing the risk of counter-trend trading.

2. Objective Entry and Exit Conditions: The use of the %B indicator provides clear entry and exit signals, minimizing bias from subjective judgments.

3. Mean Reversion Principle: The strategy leverages the common mean reversion phenomenon in financial markets, trading when prices deviate significantly from the mean, thereby increasing profit probability.

4. High Adaptability: Bollinger Bands automatically adjust to market volatility, allowing the strategy to adapt to different market environments.

#### Strategy Risks

1. False Signal Risk: In highly volatile or sideways markets, frequent false signals may lead to excessive trading and capital losses.

2. Trend Reversal Risk: Although the 200-day SMA is used as a filter, the strategy may generate inaccurate signals near major trend reversal points.

3. Lack of Stop-Loss Mechanism: The basic strategy does not incorporate a stop-loss, which may result in substantial losses during sustained market downturns.

4. Market Crash Risk: During significant market declines, the strategy may frequently trigger buy signals, potentially causing severe capital losses.

#### Strategy Optimization Directions

1. Introduce Dynamic Stop-Loss: Consider using the Average True Range (ATR) to set dynamic stop-losses for better risk control.

2. Optimize Entry Conditions: Additional technical indicators, such as RSI or MACD, could be incorporated to confirm oversold conditions and reduce false signals.

3. Adjust %B Thresholds: Dynamically adjust the %B entry and exit thresholds based on different market environments and trading instruments.

4. Incorporate Volume Analysis: Integrating volume indicators can enhance signal reliability, especially when identifying market reversals.

5. Implement Gradual Position Building and Closing: Consider entering and exiting positions in stages rather than all at once when conditions are met.

#### Conclusion

The Bollinger Band Overbought/Oversold Strategy is a trading method that combines trend following and mean reversion. By leveraging Bollinger Bands and the %B indicator, this strategy aims to capture short-term price rebound opportunities in the market. While the strategy boasts objectivity and high adaptability, it still faces challenges such as false signals and lack of risk control. By introducing dynamic stop-losses, optimizing entry conditions, and incorporating other technical indicators, the strategy's stability and profitability can be further improved. Traders should thoroughly test and optimize strategy parameters before live trading to adapt to different market environments and personal risk preferences.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-09-24 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © EdgeTools

//@version=5
strategy("Larry Connors %b Strategy (Bollinger Band)", overlay=false)

// Parameters for moving averages and Bollinger Bands
sma200 = ta.sma(close, 200)
length = 20  // Bollinger Band period
src = close  // Source for Bollinger Bands
mult = 2.0   // Bollinger Band standard deviation multiplier

// Calculate Bollinger Bands and %b
basis = ta.sma(src, length)
dev = ta.stdev(src, length)
upperBand = basis + mult * dev
lowerBand = basis - mult * dev
percentB = (close - lowerBand) / (upperBand - lowerBand)

// Conditions for the strategy
condition1 = close > sma200  // Condition 1: Close is above the 200-day moving average

// %b must be below 0.2 for the last three consecutive days
condition2 = percentB[2] < 0.2 and percentB[1] < 0.2 and percentB < 0.2

// Combined buy condition
buyCondition = condition1 and condition2

// Sell condition: %b closes above 0.8
sellCondition = percentB > 0.8

// Execute buy signal when buy condition is met
if buyCondition
    strategy.entry("Buy", strategy.long)

// Execute sell signal when the sell condition is met
if sellCondition
    strategy.close("Buy")

// Plotting Bollinger Bands
plot(upperBand, color=color.new(color.rgb(255, 0, 0), 50), title="Upper Bollinger Band")  // Red color with 50% transparency
plot(lowerBand, color=color.new(color.rgb(0, 255, 0), 50), title="Lower Bollinger Band")  // Green color with 50% transparency
plot(basis, color=color.rgb(0, 0, 255), title="Middle Bollinger Band")  // Blue color

// Plot %b value for visual confirmation
plot(percentB, color=color.rgb(128, 0, 128), linewidth=2, title="%b Value")  // Purple color

// Additional lines to improve visualization
hline(0.2, "Oversold (0.2)", color=color.rgb(255, 165, 0), linestyle=hline.style_dashed)  // Orange dashed line at 0.2
hline(0.8, "Overbought (0.8)", color=color.rgb(255, 105, 180), linestyle=hline.style_dashed)  // Pink dashed line at 0.8

// Set background color when a position is open
bgcolor(strategy.opentrades > 0 ? color.new(color.green, 50) : na)
```

> Detail

https://www.fmz.com/strategy/468349

> Last Modified

2024-09-26 17:18:11
