
> Name

Dynamic resistance and support double K-line pattern ATR risk control quantitative trading strategy-Dynamic-Resistance-and-Support-Dual-Candlestick-Pattern-ATR-Risk-Management-Quantitative-Trading-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d862475d1334442aff65.png)
![IMG](https://www.fmz.com/upload/asset/2d96bf84997df3b3847bd.png)

[trans]

#### Overview
"Double K-line form ATR risk control quantitative trading strategy of dynamic resistance and support" is a trading system that combines a variety of classic indicators in technical analysis. This strategy is mainly based on the dynamic identification of support and resistance levels, combined with the strong reversal signal of the Engulfing Pattern, and risk management through the ATR (Average True Range) indicator. This strategy integrates the three dimensions of price structure, candlestick pattern recognition and volatility analysis in trading decisions, and improves the reliability of trading signals through multiple confirmations. The strategy design adopts a dynamic support and resistance level calculation method, which can be flexibly adapted to different market environments through the lookback period parameter. At the same time, a fixed ratio of risk-return ratio of 1:2 is used to set stop loss and profit targets, which reflects the strict risk management concept.
#### Strategy Principle
The core principles of this strategy are based on three main technical elements: support and resistance level judgment, candle chart pattern identification, and ATR risk management.
First, the strategy determines dynamic resistance and support levels by calculating the highest and lowest prices over a specified lookback period (50 periods by default). These price levels have historically had a significant impact on market movements and may come into play again. The resistance level (Resistance) is determined by the highest price during the lookback period, indicating the area where the seller's power is concentrated; the support level (Support) is determined by the lowest price during the lookback period, indicating the area where the buyer's power is concentrated.
Secondly, the strategy identifies two powerful reversal patterns - Bullish Engulfing and Bearish Engulfing. The bullish engulfing pattern appears during a decline and consists of a small negative line followed by a larger positive line. The real body of the second positive line completely covers ("engulfs") the real body of the previous negative line, indicating that the power of the buyer has defeated the power of the seller, and may indicate that the trend is reversing upward. The bearish engulfing pattern, on the other hand, appears during an uptrend and consists of a small positive line followed by a larger negative line. It also indicates a shift in power and may indicate a trend reversal to the downside.
Third, the entry signal needs to meet the dual conditions of form confirmation and price position:
- Buy signal: A bullish engulfing pattern must occur simultaneously with the current close above support.
- Sell signal: Bearish engulfing pattern must occur simultaneously with current close below resistance
Finally, the strategy uses the ATR indicator for risk management. ATR measures market volatility and is used to set stop losses that adapt to current market conditions. The stop-loss distance is set to 1.5 times the ATR value, and the profit target is set to 2 times the stop-loss distance, forming a risk-return ratio of 1:2, which is in line with the principle of positive expected value trading.
#### Strategic Advantages
1. **Multi-dimensional signal confirmation mechanism**: The strategy combines support and resistance levels and pattern recognition, requiring multiple conditions to be met at the same time to generate a trading signal, which can effectively reduce erroneous transactions. Signals are generated only when the price is in a technically favorable position (above support or below resistance) and a clear reversal pattern appears, increasing signal reliability.
2. **Dynamic adaptation to market structure**: Support and resistance levels are based on dynamic calculations rather than fixed values, and can be automatically adjusted as the market evolves, allowing the strategy to remain effective in different market cycles and volatile environments.
3. **Volatility-based risk management**: Use ATR for stop loss settings to ensure that risk control adapts to the current market volatility and avoids the problem of the stop loss being too tight (triggered due to normal fluctuations) or too loose (excessive losses).
4. **Strict risk-return settings**: Using a risk-reward ratio of 1:2, even if the winning rate is only 40%, profits can still be achieved from the perspective of mathematical expectation value, enhancing the long-term stability of the strategy.
5. **Visual and intuitive trading signals**: The strategy clearly marks buying and selling signals, support and resistance levels on the chart, allowing traders to intuitively understand the market structure and trading logic, and facilitate real-time decision-making and later analysis.
6. **Flexible and adjustable parameters**: Key parameters (lookback period, ATR cycle, risk multiple) can be adjusted according to different market characteristics and personal risk preferences to enhance strategy adaptability.
#### Strategy Risk
1. **Delay in identification of support and resistance levels**: There is a lag in using historical high/low points to calculate support and resistance levels. In a rapid breakthrough market, it may cause signal lag, miss the best entry point or generate unnecessary transactions. Improved methods may consider introducing a trend strength filter or combining it with other technical indicators.
2. **Limitations of pattern recognition**: Simply relying on double K-line patterns may be too simplistic, and there are many false breakthroughs and false signals in the market. It is recommended to add trading volume confirmation or other technical indicators as auxiliary filtering conditions.
3. **Hidden dangers of fixed risk-reward ratio**: Although a risk-reward ratio of 2:1 is theoretically feasible, not all market environments are suitable for this fixed ratio. In a strong trending market, profits may be made prematurely; in a range-bound market, profit targets may be difficult to achieve. Consider dynamically adjusting the risk-reward ratio based on market conditions.
4. **Parameter Sensitivity**: Strategy performance may be highly sensitive to key parameters (especially the length of the lookback period). A lookback period that is too short may cause support and resistance levels to change frequently, while a lookback period that is too long may make the identified support and resistance levels less relevant to the current market. A comprehensive backtest is recommended to optimize parameter settings under different market conditions.
5. **Lack of market environment adaptability**: The strategy does not distinguish between trend and consolidation market environments and may generate too many false signals in certain market conditions. It is recommended to introduce a trend identification mechanism and apply different trading logic in different market environments.
6. **Lack of fund management mechanism**: The code does not contain position size management logic, which may lead to incomplete risk control. It is recommended to integrate a fund management module to dynamically adjust the transaction size based on account size and current volatility.
#### Optimization direction
1. **Introduction of trend filter**: The current strategy is suitable for mid-term reversal trading, but may frequently trigger reversal signals in strong trending markets. It is recommended to add trend identification components (such as moving average systems or ADX indicators), trade only in the direction of the trend or use different parameter settings to adapt to different trend strengths.
2. **Improve pattern recognition**: Pattern recognition capabilities can be expanded to include other high-probability reversal patterns such as hammer lines, star patterns, etc., or introduce a pattern confirmation mechanism, such as requiring subsequent K lines to continue to confirm the reversal direction.
3. **Dynamic Risk Management**: Consider dynamically adjusting the risk-reward ratio based on market volatility and trend strength, using looser profit targets in strong trending markets and more conservative settings in volatile markets.
4. **Increase Volume Confirmation**: Pattern signals combined with volume changes are usually more reliable. Volume conditions can be added, such as requiring a significant increase in volume when the pattern occurs, to confirm price momentum.
5. **Multi-time frame analysis**: Introduce a multi-time frame confirmation mechanism to ensure that the trading direction is consistent with the higher time frame trend and avoid reverse trading in the general trend.
6. **Introduction of historical form performance statistics**: Code can be added to track the historical performance of forms under different market conditions, establish a dynamic probability model, and adjust signal credibility according to current market characteristics.
7. **Add fund management module**: Realize dynamic position management based on account size, volatility and continuous losses, and control the risk of a single transaction to not exceed a fixed proportion of total capital (such as 1-2%).
#### Summary
"Double K-line form ATR risk control quantitative trading strategy of dynamic resistance and support" demonstrates a trading system design idea with clear structure and rigorous logic. This strategy creates a multi-dimensional confirmation trading system by combining price structure analysis (support and resistance levels), pattern recognition (engulfing patterns) and scientific risk management (stop loss setting based on ATR). The main advantage of the strategy lies in its signal confirmation mechanism and risk control to adapt to market fluctuations, but it also has limitations in terms of delay in identifying support and resistance and adaptability to the market environment.
This strategy has the potential to further improve performance and adaptability by introducing optimization directions such as trend filtering, improved pattern recognition, dynamic risk management and multi-time frame analysis. In particular, the addition of a fund management module and a market status recognition mechanism will elevate the strategy from a technical analysis tool to a complete trading system. This strategy is particularly suitable for mid-term traders looking for reversal opportunities. Under reasonable expectation management, it is expected to achieve long-term stable trading performance.
Ultimately, the success of any trading strategy depends not only on the technical design of the strategy itself, but also on the trader's in-depth understanding of the market and confidence in the logic of the strategy. Optimum performance of a strategy can only be achieved by fully understanding its principles, accepting its limitations, and maintaining trading discipline. ||
#### Overview
The "Dynamic Resistance and Support Dual Candlestick Pattern ATR Risk Management Quantitative Trading Strategy" is a trading system that combines multiple classic indicators from technical analysis. This strategy is primarily based on the dynamic identification of support and resistance levels, integrated with the powerful reversal signal of Engulfing Patterns, and employs the ATR (Average True Range) indicator for risk management. The strategy fuses three dimensions in its trading decisions: price structure, candlestick pattern recognition, and volatility analysis, using multiple confirmations to increase the reliability of trading signals. The strategy design employs a dynamic method for calculating support and resistance levels, which can flexibly adapt to different market environments through the lookback period parameter, while using a fixed risk-reward ratio of 1:2 to set stop-loss and take-profit targets, embodying a strict risk management philosophy.

#### Strategy Principles
The core principles of this strategy are based on three key technical elements: support and resistance level determination, candlestick pattern recognition, and ATR risk management.

First, the strategy determines dynamic resistance and support levels by calculating the highest and lowest prices within a specified lookback period (default 50 periods). These price levels have historically had a significant impact on market movements and may do so again. The resistance level is determined by the highest price within the lookback period, representing areas of concentrated selling pressure; the support level is determined by the lowest price within the lookback period, representing areas of concentrated buying pressure.

Second, the strategy identifies two powerful reversal patterns—Bullish Engulfing and Bearish Engulfing. A Bullish Engulfing pattern appears during a downtrend, consisting of a small bearish candle followed by a larger bullish candle, where the body of the second bullish candle completely covers ("engulfs") the body of the previous bearish candle, indicating that buying pressure has overcome selling pressure and potentially signaling an upward trend reversal. A Bearish Engulfing pattern is the opposite, appearing during an uptrend, consisting of a small bullish candle followed by a larger bearish candle, similarly indicating a shift in power and potentially signaling a downward trend reversal.

Third, entry signals must simultaneously meet both pattern confirmation and price position conditions:
- Buy signal: Must have both a Bullish Engulfing pattern and the current closing price above the support level
- Sell signal: Must have both a Bearish Engulfing pattern and the current closing price below the resistance level

Finally, the strategy uses the ATR indicator for risk management. ATR measures market volatility and is used to set stop-loss positions that adapt to current market conditions. The stop-loss distance is set at 1.5 times the ATR value, and the profit target is set at twice the stop-loss distance, forming a 1:2 risk-reward ratio, which conforms to the positive expectancy trading principle.

#### Strategy Advantages
1. **Multi-dimensional signal confirmation mechanism**: The strategy combines support/resistance levels and pattern recognition, requiring multiple conditions to be met simultaneously to generate trading signals, effectively reducing erroneous trades. Signals are only generated when the price is at a technically favorable position (above support or below resistance) and clear reversal patterns appear, increasing signal reliability.

2. **Dynamic adaptation to market structure**: Support and resistance levels are based on dynamic calculations rather than fixed values, allowing them to automatically adjust as the market evolves, keeping the strategy effective across different market cycles and volatility environments.

3. **Volatility-based risk management**: Using ATR for stop-loss settings ensures risk control adapts to current market volatility, avoiding stop-losses that are too tight (triggered by normal fluctuations) or too loose (excessive losses).

4. **Strict risk-reward settings**: Employing a 1:2 risk-reward ratio means that even with a win rate of only 40%, the strategy can still achieve profitability from a mathematical expectancy perspective, enhancing long-term stability.

5. **Visually intuitive trading signals**: The strategy clearly marks buy and sell signals and support/resistance levels on the chart, allowing traders to intuitively understand market structure and trading logic, facilitating real-time decision-making and subsequent analysis.

6. **Flexible adjustable parameters**: Key parameters (lookback period, ATR period, risk multiplier) can all be adjusted according to different market characteristics and personal risk preferences, enhancing strategy adaptability.

#### Strategy Risks
1. **Delayed support and resistance level identification**: Using historical highs/lows to calculate support and resistance levels has inherent lag, which may lead to delayed signals in rapidly breaking markets, missing optimal entry points or generating unnecessary trades. Improvement methods could include introducing trend strength filters or combining with other technical indicators.

2. **Limitations of pattern recognition**: Relying solely on dual candlestick patterns may be overly simplistic, as markets contain many false breakouts and deceptive signals. It is advisable to add volume confirmation or other technical indicators as auxiliary filtering conditions.

3. **Pitfalls of fixed risk-reward ratios**: Although a 2:1 risk-reward ratio is theoretically viable, not all market environments are suitable for this fixed ratio. In strong trending markets, it may take profits too early; in range-bound markets, profit targets may be difficult to reach. Consider dynamically adjusting the risk-reward ratio based on market conditions.

4. **Parameter sensitivity**: Strategy performance may be highly sensitive to key parameters (especially lookback period length). Too short a lookback period may cause support and resistance levels to change frequently, while too long may reduce the relevance of identified support and resistance levels to the current market. Comprehensive backtesting is recommended to optimize parameter settings for different market conditions.

5. **Lack of market environment adaptability**: The strategy does not differentiate between trending and consolidating market environments, potentially generating too many false signals in certain market states. Consider introducing trend identification mechanisms to apply different trading logic in different market environments.

6. **Lack of money management mechanism**: The code does not include position sizing logic, which may lead to incomplete risk control. Consider integrating a money management module to dynamically adjust trading size based on account size and current volatility.

#### Optimization Directions
1. **Introduce trend filters**: The current strategy is suitable for medium-term reversal trading but may frequently trigger counter-trend signals in strong trending markets. Consider adding trend identification components (such as moving average systems or ADX indicators) to trade only in the trend direction or use different parameter settings for different trend strengths.

2. **Enhance pattern recognition**: Pattern recognition capabilities could be expanded to include other high-probability reversal patterns such as hammer lines, star formations, etc., or introduce pattern confirmation mechanisms, such as requiring subsequent candles to continue confirming the reversal direction.

3. **Dynamic risk management**: Consider dynamically adjusting the risk-reward ratio based on market volatility and trend strength, using more relaxed profit targets in strong trending markets and more conservative settings in oscillating markets.

4. **Add volume confirmation**: Pattern signals combined with volume changes are usually more reliable. Volume conditions could be added, such as requiring significantly increased volume when patterns appear, to confirm price momentum.

5. **Multi-timeframe analysis**: Introduce multi-timeframe confirmation mechanisms to ensure the trading direction aligns with higher timeframe trends, avoiding counter-trend trading within larger trends.

6. **Incorporate historical pattern performance statistics**: Code could be added to track the historical performance of patterns under different market conditions, establishing a dynamic probability model to adjust signal credibility based on current market characteristics.

7. **Add money management module**: Implement dynamic position management based on account size, volatility, and consecutive losses, controlling single trade risk to not exceed a fixed percentage (e.g., 1-2%) of total capital.

#### Conclusion
The "Dynamic Resistance and Support Dual Candlestick Pattern ATR Risk Management Quantitative Trading Strategy" demonstrates a trading system design approach with clear structure and rigorous logic. By combining price structure analysis (support and resistance levels), pattern recognition (engulfing patterns), and scientific risk management (ATR-based stop-loss settings), this strategy creates a multi-dimensional confirmation trading system. The strategy's main advantages lie in its signal confirmation mechanism and volatility-adaptive risk control, though it also has limitations in areas such as delayed support/resistance identification and market environment adaptability.

Through the introduction of trend filtering, enhanced pattern recognition, dynamic risk management, and multi-timeframe analysis, this strategy has the potential to further improve its performance and adaptability. Particularly, adding money management modules and market state recognition mechanisms would elevate this strategy from a technical analysis tool to a complete trading system. This strategy is especially suitable for medium-term traders looking for reversal opportunities, and with reasonable expectancy management, it has the potential to achieve long-term stable trading performance.

Ultimately, the success of any trading strategy depends not only on the technical design of the strategy itself but also on the trader's deep understanding of the market and confidence in the strategy logic. Only by fully understanding the strategy principles, accepting its limitations, and maintaining trading discipline can the optimal performance of the strategy be achieved.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-03-24 00:00:00
end: 2025-03-23 00:00:00
period: 3d
basePeriod: 3d
exchanges: [{"eid":"Futures_Binance","currency":"BNB_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © watcharaphon0619

//@version=5
strategy("Ai ProSR V.1", overlay=true)

// Define parameters
lookback = input(50, title="Lookback Period for S/R")
atrLength = input(14, title="ATR Length")
atrMultiplier = input(1.5, title="ATR Multiplier for Stop Loss")

// Calculate ATR (Average True Range)
atr = ta.atr(atrLength)

// Find the highest and lowest points over the lookback period (Support/Resistance levels)
resistance = ta.highest(high, lookback)
support = ta.lowest(low, lookback)

// Display support and resistance on the chart
plot(resistance, color=color.red, linewidth=2, title="Resistance")
plot(support, color=color.green, linewidth=2, title="Support")

// Bullish Engulfing condition (Buy signal)
bullishEngulfing = (close[1] < open[1]) and (close > open) and (close > open[1]) and (open < close[1])

// Bearish Engulfing condition (Sell signal)
bearishEngulfing = (close[1] > open[1]) and (close < open) and (close < open[1]) and (open > close[1])

// Trading conditions: 2-candlestick pattern + Support/Resistance levels
buyCondition = bullishEngulfing and (close > support)  // Buy when Bullish Engulfing appears and price is above support
sellCondition = bearishEngulfing and (close < resistance)  // Sell when Bearish Engulfing appears and price is below resistance

// Display Buy and Sell signals on the chart
plotshape(series=buyCondition, title="Buy Signal", location=location.belowbar, color=color.green, style=shape.labelup, text="BUY")
plotshape(series=sellCondition, title="Sell Signal", location=location.abovebar, color=color.red, style=shape.labeldown, text="SELL")

// Stop Loss and Take Profit levels
stopLoss = atr * atrMultiplier
takeProfit = stopLoss * 2  // Risk-Reward Ratio 1:2

// Entry and exit conditions
if (buyCondition)
    strategy.entry("Buy", strategy.long)
    strategy.exit("Take Profit/Stop Loss", "Buy", stop=close - stopLoss, limit=close + takeProfit)

if (sellCondition)
    strategy.entry("Sell", strategy.short)
    strategy.exit("Take Profit/Stop Loss", "Sell", stop=close + stopLoss, limit=close - takeProfit)

```

> Detail

https://www.fmz.com/strategy/488021

> Last Modified

2025-03-24 14:24:55
