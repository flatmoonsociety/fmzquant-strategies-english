
> Name

Dual-Moving-Average-Trend-Following-Strategy-with-RSI-Filter
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/f226ed38aa82383ba4.png)

[trans]
#### Overview
This strategy is a trend following trading system that combines the Simple Moving Average (SMA) and the Relative Strength Index (RSI). It mainly uses the 200-period SMA to identify uptrends and uses RSI as a filter to optimize entry timing. The strategy also includes take-profit and stop-loss mechanisms to control risk and lock in profits.
#### Strategy Principle
The core logic of this strategy includes the following key elements:
1. Trend identification: Use the 200-period SMA as an indicator of long-term trends. When price crosses and remains above the SMA, it is considered a potential uptrend.
2. Entry confirmation: The price is required to remain above the SMA for at least 30 consecutive periods (minutes) to ensure the stability of the trend.
3. RSI filtering: Using the 14-period RSI indicator, entry is only allowed when the RSI is below 30 (oversold area), which helps capture potential rebound opportunities.
4. Risk management: Set a stop loss level of 0.5% to limit the maximum loss in a single transaction.
5. Profit target: Set a 2% take-profit level to automatically close the position when the expected profit is reached.
The strategy execution process is as follows:
- When the price crosses the 200SMA and maintains it for more than 30 periods, and the RSI is below 30, open a long position.
- During the position holding period, if the price reaches 102% of the entry price (stop profit) or falls below 99.5% of the entry price (stop loss), the position will be automatically closed.
- After closing the position, the system resets and waits for the next eligible entry opportunity.
#### Strategic Advantages
1. Trend following: Using long-term SMA to capture the main trend will help you profit from a strong uptrend.
2. Entry optimization: The price is required to remain above the SMA for 30 periods, which helps to filter out false breakthroughs and improve the quality of entry.
3. Reversal capture: Combined with RSI oversold conditions, it helps capture potential rebound opportunities in the early stages of a trend.
4. Risk control: Set a clear stop loss level, effectively limiting the maximum risk of each transaction.
5. Profit locking: The preset profit-taking level ensures that profits are automatically locked when the expected profit is reached.
6. Objectivity: The strategy rules are clear, reducing the emotional impact of subjective judgment.
7. Quantifiable: Strategy parameters can be backtested and optimized through historical data.
#### Strategy Risk
1. False breakthroughs: In sideways or volatile markets, frequent false breakthroughs may occur, leading to continuous stop losses.
2. Lagging: As a lagging indicator, SMA may miss some opportunities at the beginning of the trend or maintain positions at the end of the trend.
3. RSI Limits: Strict RSI conditions may miss some good entry opportunities, especially during strong rises.
4. Fixed take profit and stop loss: The preset percentage may not apply to all market conditions and may be triggered prematurely in volatile markets.
5. Single direction: The strategy is only long and cannot profit from the falling market.
6. Parameter sensitivity: Strategy performance may be sensitive to changes in parameters such as SMA period, confirmation period and RSI settings.
7. Market adaptability: Strategies may perform well in certain markets or time frames, but may not be suitable in all situations.
#### Strategy optimization direction
1. Dynamic take-profit and stop-loss: Consider using ATR (average true range) to set dynamic take-profit and stop-loss levels to adapt to different market fluctuations.
2. Multi-period confirmation: Introduce a confirmation mechanism of multiple time frames, such as entering the market only when the conditions of the daily and hourly lines are met at the same time, to improve signal reliability.
3. Trend strength filter: Add ADX (average trend indicator) to measure trend strength, and only enter the market during strong trends.
4. Volatility adjustment: dynamically adjust parameters according to market volatility, such as increasing the confirmation period during low volatility periods and reducing the confirmation period during high volatility periods.
5. Add a short-selling mechanism: consider shorting when the price falls below the SMA and the RSI is overbought, so that the strategy can profit in a two-way market.
6. Optimize the use of RSI: Consider using RSI divergence or combining it with other indicators (such as MACD) to enhance the reliability of entry signals.
7. Introduce trading volume confirmation: Add trading volume analysis to ensure that breakthroughs or reversals are supported by sufficient trading volume.
8. Time filtering: Add a time filter to avoid trading during known periods of low liquidity.
9. Fund management optimization: Realize dynamic position management and adjust the risk exposure of each transaction according to account size and market fluctuations.
10. Add indicator combinations: Consider combining Bollinger Bands, Fibonacci retracement and other technical indicators to build a more comprehensive trading system.
#### Summarize
"Double Moving Average Trend Following Strategy with RSI Filter" is a quantitative trading strategy that combines the ideas of trend following and momentum reversal. By utilizing the 200-period SMA to identify long-term trends and optimizing entry timing combined with oversold conditions on the RSI, this strategy aims to capture potential rebound opportunities in strong uptrends. The built-in stop-profit and stop-loss mechanisms help control risks and lock in profits, making it a relatively comprehensive trading system.
However, this strategy also has some limitations, such as it may be affected by false breakthroughs and is limited to long transactions. In order to further improve the robustness and adaptability of the strategy, it is recommended to consider the introduction of dynamic stop-profit and stop-loss, multi-period confirmation, trend intensity filtering and other optimization measures. In addition, adding a short-selling mechanism and optimizing fund management strategies may also significantly improve the overall performance of the system.
Overall, this strategy provides a good starting point for trend following and momentum trading. Through continuous backtesting, optimization and real-time verification, traders can further improve and customize this strategy according to specific market environments and personal risk preferences to achieve better trading results.
||

#### Overview

This strategy is a trend-following trading system that combines a Simple Moving Average (SMA) with the Relative Strength Index (RSI). It primarily uses a 200-period SMA to identify uptrends and employs the RSI as a filter to optimize entry timing. The strategy also incorporates take-profit and stop-loss mechanisms to control risk and lock in profits.

#### Strategy Principles

The core logic of this strategy includes the following key elements:

1. Trend Identification: Uses a 200-period SMA as an indicator of long-term trends. When the price crosses above and remains above the SMA, it is considered a potential uptrend.

2. Entry Confirmation: Requires the price to stay above the SMA for at least 30 consecutive periods (minutes) to ensure trend stability.

3. RSI Filter: Uses a 14-period RSI indicator, allowing entry only when the RSI is below 30 (oversold region), which helps capture potential rebound opportunities.

4. Risk Management: Sets a 0.5% stop-loss level to limit the maximum loss per trade.

5. Profit Target: Sets a 2% take-profit level to automatically close positions when the expected return is achieved.

The strategy execution process is as follows:
- Open a long position when the price crosses above the 200 SMA and stays above it for more than 30 periods, while the RSI is below 30.
- During the holding period, automatically close the position if the price reaches 102% of the entry price (take profit) or falls below 99.5% of the entry price (stop loss).
- After closing the position, the system resets and waits for the next entry opportunity that meets the conditions.

#### Strategy Advantages

1. Trend Following: Utilizes long-term SMA to capture major trends, helping to profit in strong upward markets.

2. Entry Optimization: Requiring the price to stay above the SMA for 30 periods helps filter out false breakouts, improving entry quality.

3. Reversal Capture: Combining RSI oversold conditions helps capture potential rebound opportunities at the beginning of trends.

4. Risk Control: Setting a clear stop-loss level effectively limits the maximum risk for each trade.

5. Profit Locking: Preset take-profit level ensures automatic profit locking when expected returns are achieved.

6. Objectivity: Clear strategy rules reduce the emotional impact of subjective judgments.

7. Quantifiable: Strategy parameters can be backtested and optimized using historical data.

#### Strategy Risks

1. False Breakouts: In sideways or choppy markets, frequent false breakouts may lead to consecutive stop losses.

2. Lag: SMA as a lagging indicator may miss some opportunities at the beginning of trends or maintain positions when trends end.

3. RSI Limitations: Strict RSI conditions may miss some good entry opportunities, especially in strong uptrends.

4. Fixed Take-Profit and Stop-Loss: Preset percentages may not be suitable for all market conditions and may trigger too early in highly volatile markets.

5. Single Direction: The strategy only goes long, unable to profit in downward trends.

6. Parameter Sensitivity: Strategy performance may be sensitive to changes in SMA period, confirmation period, and RSI settings.

7. Market Adaptability: The strategy may perform well in certain specific markets or timeframes but may not be applicable to all situations.

#### Strategy Optimization Directions

1. Dynamic Take-Profit and Stop-Loss: Consider using ATR (Average True Range) to set dynamic take-profit and stop-loss levels to adapt to different market volatility conditions.

2. Multi-Timeframe Confirmation: Introduce confirmation mechanisms across multiple timeframes, such as requiring conditions to be met on both daily and hourly charts before entry, to improve signal reliability.

3. Trend Strength Filter: Add ADX (Average Directional Index) to measure trend strength and only enter during strong trends.

4. Volatility Adjustment: Dynamically adjust parameters based on market volatility, such as increasing confirmation periods during low volatility and decreasing them during high volatility.

5. Add Short Selling Mechanism: Consider short selling when price falls below SMA and RSI is overbought, allowing the strategy to profit in both directions.

6. Optimize RSI Usage: Consider using RSI divergence or combining it with other indicators (such as MACD) to enhance entry signal reliability.

7. Introduce Volume Confirmation: Add volume analysis to ensure breakouts or reversals are supported by sufficient trading volume.

8. Time Filter: Add a time filter to avoid trading during known low liquidity periods.

9. Money Management Optimization: Implement dynamic position sizing, adjusting risk exposure for each trade based on account size and market volatility.

10. Increase Indicator Combination: Consider combining other technical indicators such as Bollinger Bands and Fibonacci retracements to build a more comprehensive trading system.

#### Conclusion

The "Dual Moving Average Trend Following Strategy with RSI Filter" is a quantitative trading strategy that combines trend-following and momentum reversal ideas. By using a 200-period SMA to identify long-term trends and combining RSI oversold conditions to optimize entry timing, this strategy aims to capture potential rebound opportunities in strong uptrends. The built-in take-profit and stop-loss mechanisms help control risk and lock in profits, making it a relatively comprehensive trading system.

However, the strategy also has some limitations, such as being susceptible to false breakouts and being limited to long-only trades. To further improve the strategy's robustness and adaptability, it is recommended to consider introducing dynamic take-profit and stop-loss levels, multi-timeframe confirmation, trend strength filtering, and other optimization measures. Additionally, adding a short-selling mechanism and optimizing money management strategies could significantly enhance the overall performance of the system.

In summary, this strategy provides a good starting point for trend following and momentum trading. Through continuous backtesting, optimization, and live trading validation, traders can further refine and customize this strategy based on specific market environments and individual risk preferences to achieve better trading results.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-07-21 00:00:00
end: 2024-07-28 00:00:00
period: 5m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("SMA 200 with RSI Filter", overlay=true)

// Inputs
smaLength = input.int(200, title="SMA Length")
confirmBars = input.int(30, title="Confirmation Bars (30 minutes)")
takeProfitPerc = input.float(2.0, title="Take Profit (%)", step=0.1) / 100
stopLossPerc = input.float(0.5, title="Stop Loss (%)", step=0.1) / 100
rsiLength = input.int(14, title="RSI Length")
rsiOverbought = input.int(70, title="RSI Overbought Level")
rsiOversold = input.int(30, title="RSI Oversold Level")

// Calculate SMA
sma = ta.sma(close, smaLength)

// Calculate RSI
rsi = ta.rsi(close, rsiLength)

// Buy condition
priceAboveSMA = close > sma
aboveSMAcount = ta.barssince(priceAboveSMA == false)
rsiCondition = rsi < rsiOversold
enterLongCondition = priceAboveSMA and aboveSMAcount >= confirmBars and rsiCondition

// Track entry price for calculating take profit and stop loss levels
var float entryPrice = na
if (enterLongCondition and na(entryPrice))
    entryPrice := close

// Ensure the entryPrice is only set when a position is opened
if (strategy.opentrades == 0)
    entryPrice := na

takeProfitLevel = entryPrice * (1 + takeProfitPerc)
stopLossLevel = entryPrice * (1 - stopLossPerc)

// Exit conditions
takeProfitCondition = close >= takeProfitLevel
stopLossCondition = close <= stopLossLevel

// Plot SMA and RSI
plot(sma, title="SMA 200", color=color.blue)
hline(rsiOverbought, "Overbought", color=color.red)
hline(rsiOversold, "Oversold", color=color.green)
plot(rsi, title="RSI", color=color.purple)

// Plot shapes for entries and exits
plotshape(series=enterLongCondition, location=location.belowbar, color=color.green, style=shape.labelup, text="BUY")
plotshape(series=takeProfitCondition, location=location.abovebar, color=color.red, style=shape.labeldown, text="TP")
plotshape(series=stopLossCondition, location=location.abovebar, color=color.red, style=shape.labeldown, text="SL")

// Strategy entry and exit
if (enterLongCondition)
    strategy.entry("Long", strategy.long, comment="SMA200LE")

if (takeProfitCondition or stopLossCondition)
    strategy.close("Long", when=takeProfitCondition or stopLossCondition)

// Reset entry price after position is closed
if (strategy.position_size == 0)
    entryPrice := na

```

> Detail

https://www.fmz.com/strategy/458064

> Last Modified

2024-07-29 16:45:59
