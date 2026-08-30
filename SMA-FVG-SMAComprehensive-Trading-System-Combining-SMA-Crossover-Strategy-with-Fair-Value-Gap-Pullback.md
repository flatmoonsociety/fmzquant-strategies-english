
> Name

Comprehensive-Trading-System-Combining-SMA-Crossover-Strategy-with-Fair-Value-Gap-Pullback
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/4758000693aed791e6322ce1eafe09c11ff836a99ebffdbf07d0ce53b917f8bd.png)

[trans]

#### Overview
This strategy is a comprehensive trading system that combines a Simple Moving Average (SMA) crossover and a Fair Value Gap (FVG) retracement. It utilizes the crossover of the 8-period and 20-period SMAs to identify potential trend changes, while utilizing FVG to determine more precise entry points. This approach is designed to capture changes in market trends while optimizing entry timing by waiting for price to pull back into key support/resistance areas.
#### Strategy Principle
1. SMA Crossover: Use 8-period and 20-period simple moving averages. When the short-term SMA crosses above the long-term SMA, it is considered a bullish signal; when the short-term SMA crosses below the long-term SMA, it is considered a bearish signal.
2. Fair value gap (FVG): FVG refers to the price range formed when the high point of the current candle is higher than the high point of the previous candle and the low point of the current candle is lower than the low point of the previous candle. This range is considered the market's search for "fair value."
3. Admission conditions:
   - Long: Enter when a bullish SMA crossover occurs and price retraces to the low of FVG.
   - Short: Enter when a bearish SMA cross occurs and price rebounds to the high of FVG.
4. Exit conditions: Close the position when an SMA cross occurs in the opposite direction.
#### Strategic Advantages
1. Combination of trend following and callback: By combining SMA crossover and FVG callback, the strategy can not only capture the general trend, but also enter the market at a more favorable price level.
2. Reduce false signals: Waiting for the price to pull back to FVG can filter out some possible false cross signals and improve the accuracy of trading.
3. Risk management: Using FVG as an entry point can naturally provide a tighter stop loss position, helping to control risk.
4. Strong adaptability: By adjusting the SMA cycle and FVG parameters, the strategy can adapt to different market environments and trading varieties.
5. Objectivity: Based on clear technical indicators and price action, reducing the impact of subjective judgment.
#### Strategy Risk
1. Shock market risk: In sideways or choppy markets, frequent SMA crossovers may lead to excessive trading and losses.
2. Lagging: As a lagging indicator, SMA may miss some opportunities in the early stages of the trend.
3. False breakthrough risk: The price may briefly break through FVG and then fall back, resulting in a false signal.
4. Market gap risk: In a highly volatile market, the price may jump over the FVG area, resulting in missed trading opportunities.
5. Parameter sensitivity: Strategy performance may be sensitive to the SMA cycle and FVG definition parameters, which need to be carefully optimized.
#### Strategy optimization direction
1. Dynamic SMA cycle: You can consider dynamically adjusting the SMA cycle based on market volatility to adapt to different market conditions.
2. Add filter conditions: Introduce additional technical indicators (such as RSI or MACD) to confirm trends and reduce false signals.
3. Improve the definition of FVG: You can try to use multiple K lines to define FVG, or consider trading volume to verify the effectiveness of FVG.
4. Optimize the exit strategy: Trailing stop loss or dynamic stop loss based on volatility can be introduced to better protect profits.
5. Add time filtering: Considering the formation time of FVG, it may be necessary to set a time window to ensure the effectiveness of FVG.
6. Risk management optimization: Dynamically adjust position size according to market volatility to achieve more sophisticated risk control.
#### Summarize
"Integrated trading system combining SMA crossover strategy with fair value gap callback" is an intelligent trading strategy that combines trend following and price callbacks. By combining SMA crossover signals and FVG retracements, this strategy aims to trade at better price levels early in a trend. Although the strategy has the potential to capture trends and optimize entry points, it still faces challenges such as volatile markets and parameter optimization. Through further optimization and improvements, such as dynamically adjusting parameters, adding filtering conditions and improving risk management, the strategy is expected to achieve more robust performance in various market environments. When traders use this strategy, they should fully understand its principles and make appropriate adjustments and tests based on specific trading varieties and market conditions.
||

#### Overview

This strategy is a comprehensive trading system that combines Simple Moving Average (SMA) crossovers with Fair Value Gap (FVG) pullbacks. It utilizes the crossover of 8-period and 20-period SMAs to identify potential trend changes, while using FVGs to determine more precise entry points. This approach aims to capture market trend shifts while optimizing entry timing by waiting for price pullbacks to key support/resistance areas.

#### Strategy Principles

1. SMA Crossover: Uses 8-period and 20-period simple moving averages. A bullish signal is generated when the short-term SMA crosses above the long-term SMA, and a bearish signal when the short-term SMA crosses below the long-term SMA.

2. Fair Value Gap (FVG): An FVG is formed when the current candle's high is higher than the previous candle's high, and the current candle's low is lower than the previous candle's low. This price range is considered where the market is seeking "fair value."

3. Entry Conditions:
   - Long: Enter when a bullish SMA crossover occurs and price pulls back to the low of the FVG.
   - Short: Enter when a bearish SMA crossover occurs and price rebounds to the high of the FVG.

4. Exit Conditions: Close positions when an opposite SMA crossover occurs.

#### Strategy Advantages

1. Combines Trend Following and Pullbacks: By integrating SMA crossovers and FVG pullbacks, the strategy can capture major trends while entering at more favorable price levels.

2. Reduces False Signals: Waiting for price to pull back to the FVG can filter out some potential false crossover signals, improving trade accuracy.

3. Risk Management: Using FVGs as entry points naturally provides tighter stop-loss placements, helping to control risk.

4. Adaptability: The strategy can be adapted to different market environments and trading instruments by adjusting SMA periods and FVG parameters.

5. Objectivity: Based on clear technical indicators and price action, reducing the impact of subjective judgement.

#### Strategy Risks

1. Choppy Market Risk: In range-bound or choppy markets, frequent SMA crossovers may lead to excessive trading and losses.

2. Lag: As a lagging indicator, SMAs may miss some opportunities at the beginning of trends.

3. False Breakout Risk: Price may briefly break through the FVG and then retreat, causing false signals.

4. Market Gap Risk: In volatile markets, price may gap over the FVG area, leading to missed trading opportunities.

5. Parameter Sensitivity: Strategy performance may be sensitive to SMA periods and FVG definition parameters, requiring careful optimization.

#### Strategy Optimization Directions

1. Dynamic SMA Periods: Consider dynamically adjusting SMA periods based on market volatility to adapt to different market conditions.

2. Additional Filters: Introduce extra technical indicators (such as RSI or MACD) to confirm trends and reduce false signals.

3. Improve FVG Definition: Try using multiple candles to define FVGs, or consider volume to validate FVG effectiveness.

4. Optimize Exit Strategy: Implement trailing stops or volatility-based dynamic stops to better protect profits.

5. Add Time Filters: Consider the formation time of FVGs, potentially setting a time window to ensure FVG validity.

6. Risk Management Optimization: Dynamically adjust position sizes based on market volatility for more refined risk control.

#### Conclusion

The "Comprehensive Trading System Combining SMA Crossover Strategy with Fair Value Gap Pullback" is an intelligent trading strategy that fuses trend following with price pullbacks. By combining SMA crossover signals and FVG pullbacks, the strategy aims to trade at more optimal price levels in the early stages of trends. While the strategy has the potential to capture trends and optimize entry points, it still faces challenges such as choppy markets and parameter optimization. Through further optimization and improvements, such as dynamic parameter adjustments, additional filtering conditions, and enhanced risk management, this strategy has the potential to achieve more robust performance across various market environments. Traders using this strategy should fully understand its principles and make appropriate adjustments and tests based on specific trading instruments and market conditions.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-07-25 00:00:00
end: 2024-07-30 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("8 SMA and 20 SMA with FVG Pullback", overlay=true)

// Input parameters
smaShortLength = input.int(8, title="Short SMA Length")
smaLongLength = input.int(20, title="Long SMA Length")

// Calculate SMAs
smaShort = ta.sma(close, smaShortLength)
smaLong = ta.sma(close, smaLongLength)

// Plot SMAs
plot(smaShort, title="8 SMA", color=color.blue)
plot(smaLong, title="20 SMA", color=color.red)

// Identify SMA crossovers
longCondition = ta.crossover(smaShort, smaLong)
shortCondition = ta.crossunder(smaShort, smaLong)

// Fair Value Gaps (FVG) logic
var float fvgHigh = na
var float fvgLow = na

if (ta.valuewhen(high[1] < high and low[1] > low, high, 0) and ta.valuewhen(high[1] < high and low[1] > low, low, 0))
    fvgHigh := high
    fvgLow := low

plot(fvgHigh, title="FVG High", color=color.purple, linewidth=1, style=plot.style_line)
plot(fvgLow, title="FVG Low", color=color.orange, linewidth=1, style=plot.style_line)

// Entry conditions
if (longCondition)
    if (low <= fvgLow)
        strategy.entry("Long", strategy.long)
        
if (shortCondition)
    if (high >= fvgHigh)
        strategy.entry("Short", strategy.short)
        
// Exit conditions (optional, you can modify these as per your risk management strategy)
if (ta.crossunder(smaShort, smaLong))
    strategy.close("Long")
    
if (ta.crossover(smaShort, smaLong))
    strategy.close("Short")

```

> Detail

https://www.fmz.com/strategy/458272

> Last Modified

2024-07-31 14:38:42
