
> Name

Dynamic Support-Resistance-SMA-Crossover-Trading-Strategy-Triple-Confirmation-with-Risk-Management-Optimization-Framework
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d8263059260384e8e740.png)
![IMG](https://www.fmz.com/upload/asset/2d8a1e76a5951abb07d04.png)



[trans]
#### Overview
The dynamic support and resistance SMA cross gold trading strategy is a short-term trading method that mainly identifies high-probability trading opportunities through the cross signals of the 10-period and 20-period simple moving averages (SMA), combined with price breakthrough and backtest confirmation mechanisms. The core feature of this strategy is to use a triple confirmation mechanism to screen trading signals, use dynamic support and resistance levels to set stop loss points, and apply a 1:2 risk-reward ratio to determine profit targets, forming a complete trading system framework. The strategy design is particularly suitable for short-term trading in the three-minute chart time period. Through strict entry conditions and precise risk control mechanisms, it improves the success rate of transactions and protects the safety of funds.
#### Strategy Principle
The trading logic of this strategy is based on the combination of three key conditions, forming a strict signal filtering system:
1. **SMA Cross Signal**: The intersection of 10-period SMA and 20-period SMA serves as the initial signal. A bullish signal is formed when the 10-period SMA crosses above the 20-period SMA; a bearish signal is formed when the 10-period SMA crosses below the 20-period SMA.
2. **Price Breakout Confirmation**:
   - The buying condition requires that the closing price exceeds the highest point of the 20-period SMA of the past 3 candlesticks
   - Sell conditions require the closing price to fall below the 20-period SMA low of the past 3 candles
3. **Backtest Confirmation**:
   - The buying condition further requires that the lowest price of the past 3 candlesticks remains above the 20-period SMA
   - The sell condition further requires that the highest price of the past 3 candlesticks remains below the 20-period SMA
In terms of risk management, the strategy uses dynamic support and resistance levels to set stops:
- The stop loss for buy transactions is set at the lowest price of the past 10 candlesticks
- The stop loss for a sell trade is set at the highest price of the past 10 candlesticks
The profit target is calculated based on a fixed risk-reward ratio of 1:2:
- Profit target for buy trade = Entry price + (Risk size × 2)
- Profit target for sell trade = Entry price - (Risk size × 2)
#### Strategic Advantages
An in-depth analysis of the code implementation of this strategy can summarize the following significant advantages:
1. **Multiple confirmation mechanism**: Through triple condition confirmation of SMA cross, price breakthrough and backtest, false signals are greatly reduced and signal quality is improved. This strict screening mechanism can effectively avoid entering the market prematurely in unclear trends.
2. **Dynamic Risk Management**: Stop loss points are automatically adjusted based on recent market fluctuations instead of using fixed points, making risk control more in line with current market conditions. This approach maintains appropriate risk exposure in varying volatility environments.
3. **Proportional risk-reward setting**: A fixed risk-reward ratio of 1:2 ensures that the profit from each successful transaction is enough to offset multiple small losses, and the overall profit can be maintained even if the winning rate is not high.
4. **Parameter-free optimization overfitting**: The strategy uses the classic 10 and 20 period SMA. These standard parameters usually have good universality and reduce the risk of over-optimization and curve fitting.
5. **Clear Visual Signals**: The code contains visual markers for buying and selling signals, making it easy to quickly identify trading opportunities and backtest analysis.
#### Strategy Risk
Although this strategy is well designed, there are some potential risks and limitations:
1. **Poor performance in sideways markets**: In sideways markets that lack a clear trend, SMA cross signals will appear frequently but lack persistence, which may lead to multiple stop loss triggers. The solution is to add a trend strength filter like the ADX indicator and only trade when the trend is clear.
2. **Quick reversal risk**: When the market suddenly reverses, the dynamic stop loss may be set too wide, resulting in larger losses. Consider adding a volatility-adjusted stop-loss mechanism and tightening the stop-loss range in a high-volatility environment.
3. **Signal lag**: The moving average is essentially a lagging indicator, which may result in missing the best entry opportunity near the turning point of the trend. It is recommended to use momentum indicators such as RSI or MACD to identify potential turning points in advance.
4. **Specific Market Dependence**: Code comments imply that this strategy is designed for the gold market and may not be applicable to all trading varieties. The fluctuation characteristics of different markets are quite different, and parameters need to be adjusted accordingly.
5. **Lack of Money Management**: Although the strategy uses a fixed percentage of account equity for trading, it lacks a mechanism to dynamically adjust position size based on winning rate and risk-reward ratio.
#### Optimization direction
Based on strategy code analysis, the following are several potential optimization directions:
1. **Add trend strength filter**: Integrate ADX or similar trend strength indicators, only trade when the trend is fully developed, and avoid frequent false signals in sideways markets. Doing so will improve signal quality and reduce the number of unnecessary trades.
2. **Optimize Time Frames**: Consider adding multiple time frame analysis, using the trend direction of higher time frames as a trade direction filter. For example, only trade when the trend direction of the daily chart is consistent with the signal of the 3-minute chart to increase the success rate.
3. **Dynamic risk-reward ratio**: The risk-reward ratio is adjusted based on market volatility and key support and resistance levels, rather than a fixed 1:2 ratio. Consider a larger profit target in a strong trend and tighten your profit stop in a volatile market.
4. **Add partial profit mechanism**: After reaching a certain profit level, consider closing positions in batches, locking in part of the profits while allowing the remaining positions to continue to make profits. This can be achieved through multiple profit targets.
5. **Trading session filter**: Add a trading session filter for specific markets to avoid market periods with low liquidity or high volatility, such as the Asian trading and European and American cross trading periods in the gold market, which may be more suitable for this strategy.
6. **Increase trading volume confirmation**: Integrate trading volume analysis as an additional confirmation indicator, increase positions on signals supported by high trading volume, and improve signal reliability.
#### Summary
The dynamic support and resistance SMA cross gold trading strategy forms a complete and rigorous trading system by combining technical indicator crossover, price action confirmation and dynamic risk management. Its core advantage is that the triple confirmation mechanism greatly improves signal quality, while the design of dynamic stop loss and fixed risk-reward ratio ensures good fund management.
This strategy is particularly suitable for short-term traders to capture high-probability trading opportunities in volatile markets, but may perform poorly in sideways markets. By adding optimization measures such as trend strength filtering, multi-time frame analysis, and dynamic risk management, the stability and adaptability of the strategy can be further improved.
The most noteworthy thing is that this strategy not only provides a trading signal generation mechanism, but also includes a complete risk control framework, embodying the core concept of professional trading system design—paying equal attention to the quality of entry signals and the fund protection mechanism. For traders looking to find trading opportunities amid short-term fluctuations, this is a clearly structured, logical and easy-to-implement strategy framework.
||
#### Overview
The Dynamic Support-Resistance SMA Crossover Trading Strategy is a short-term trading method that identifies high-probability trading opportunities through the crossover signals of 10-period and 20-period Simple Moving Averages (SMA), combined with price breakout and retest confirmation mechanisms. The core feature of this strategy is its triple confirmation mechanism for filtering trade signals, utilizing dynamic support and resistance levels to set stop-loss points, while applying a 1:2 risk-reward ratio to determine profit targets, forming a complete trading system framework. The strategy is particularly suitable for short-term trading on three-minute chart timeframes, improving trade success rates and protecting capital through strict entry conditions and precise risk control mechanisms.
#### Strategy Principles
The trading logic of this strategy is built upon the combination of three key conditions, forming a strict signal filtering system:

1. **SMA Crossover Signals**: The crossover of the 10-period SMA with the 20-period SMA serves as the initial signal. A bullish signal forms when the 10-period SMA crosses above the 20-period SMA; a bearish signal forms when the 10-period SMA crosses below the 20-period SMA.

2. **Price Breakout Confirmation**:
   - Buy conditions require the closing price to break above the highest point of the 20-period SMA over the past 3 bars
   - Sell conditions require the closing price to break below the lowest point of the 20-period SMA over the past 3 bars

3. **Retest Confirmation**:
   - Buy conditions further require that the lowest price of the past 3 bars remains above the 20-period SMA
   - Sell conditions further require that the highest price of the past 3 bars remains below the 20-period SMA

For risk management, the strategy employs dynamic support and resistance levels to set stop-losses:
- Stop-loss for buy trades is set at the lowest price of the past 10 bars
- Stop-loss for sell trades is set at the highest price of the past 10 bars

Profit targets are calculated based on a fixed 1:2 risk-reward ratio:
- Profit target for buy trades = Entry price + (Risk size × 2)
- Profit target for sell trades = Entry price - (Risk size × 2)

#### Strategy Advantages
Through deep analysis of the strategy's code implementation, the following significant advantages can be identified:

1. **Multiple Confirmation Mechanism**: The triple conditions of SMA crossover, price breakout, and retest significantly reduce false signals and improve signal quality. This strict filtering mechanism effectively prevents premature entry during unclear trends.

2. **Dynamic Risk Management**: Stop-loss points automatically adjust based on recent market volatility, rather than using fixed points, making risk control more aligned with current market conditions. This method maintains appropriate risk exposure in varying volatility environments.

3. **Proportional Risk-Reward Setting**: The fixed 1:2 risk-reward ratio ensures that each successful trade's gains are sufficient to offset multiple small losses, maintaining overall profitability even with a lower win rate.

4. **Avoidance of Parameter Optimization Overfitting**: The strategy uses classic 10 and 20-period SMAs, which typically have good universality, reducing the risk of over-optimization and curve fitting.

5. **Clear Visual Signals**: The code includes visualization markers for buy and sell signals, facilitating quick identification of trading opportunities and backtesting analysis.

#### Strategy Risks
Despite the well-designed nature of this strategy, several potential risks and limitations exist:

1. **Poor Performance in Ranging Markets**: In consolidating markets lacking clear trends, SMA crossover signals appear frequently but lack continuity, potentially triggering multiple stop-losses. A solution is to add a trend strength filter, such as the ADX indicator, trading only when trends are clearly defined.

2. **Rapid Reversal Risk**: When markets suddenly reverse, dynamic stop-losses may be set too wide, resulting in larger losses. Consider adding volatility-adjusted stop-loss mechanisms to tighten stop-loss ranges in high-volatility environments.

3. **Signal Lag**: Moving averages are inherently lagging indicators, potentially causing missed optimal entry opportunities near trend turning points. Consider combining momentum indicators like RSI or MACD to identify potential turning points in advance.

4. **Market-Specific Dependency**: Code comments suggest the strategy is designed for the gold market and may not be applicable to all trading instruments. Different markets have significantly different volatility characteristics, requiring parameter adjustments.

5. **Lack of Comprehensive Money Management**: Although the strategy employs a fixed percentage of account equity for trading, it lacks mechanisms to dynamically adjust position sizes based on win rates and risk-reward ratios.

#### Optimization Directions
Based on the strategy code analysis, here are several potential optimization directions:

1. **Add Trend Strength Filtering**: Integrate ADX or similar trend strength indicators, trading only when trends are sufficiently developed to avoid frequent false signals in ranging markets. This improves signal quality and reduces unnecessary trade frequency.

2. **Optimize Time Frames**: Consider adding multi-timeframe analysis, using higher timeframe trend directions as trade direction filters. For example, only trade when the daily chart trend direction aligns with the 3-minute chart signal, improving success rates.

3. **Dynamic Risk-Reward Ratio**: Adjust risk-reward ratios based on market volatility and key support-resistance levels, rather than a fixed 1:2 ratio. Consider larger profit targets in strong trends and tighter profit-taking in volatile markets.

4. **Add Partial Profit Mechanisms**: After reaching certain profit levels, consider partial position closing to secure profits while allowing remaining positions to continue gaining. This can be implemented through multiple profit targets.

5. **Trading Session Filters**: Add trading session filters for specific markets, avoiding low-liquidity or high-volatility market sessions. For the gold market, Asian sessions and European-American crossover sessions might be more suitable for this strategy.

6. **Add Volume Confirmation**: Integrate volume analysis as an additional confirmation indicator, increasing positions on signals supported by high volume to improve signal reliability.

#### Summary
The Dynamic Support-Resistance SMA Crossover Trading Strategy forms a complete and rigorous trading system by combining technical indicator crossovers, price action confirmation, and dynamic risk management. Its core strength lies in the triple confirmation mechanism substantially improving signal quality, while dynamic stop-losses and fixed risk-reward ratios ensure sound money management.

This strategy is particularly suitable for short-term traders capturing high-probability opportunities in volatile markets but may underperform in consolidating markets. Through optimizations like trend strength filtering, multi-timeframe analysis, and dynamic risk management, its stability and adaptability can be further enhanced.

Most notably, this strategy not only provides a signal generation mechanism but also includes a complete risk control framework, embodying the core philosophy of professional trading system design—equal attention to entry signal quality and capital protection mechanisms. For traders seeking opportunities in short-term volatility, this is a clearly structured, logically rigorous, and easily implementable strategy framework.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-01-01 00:00:00
end: 2025-04-02 00:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BNB_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © DoubleuEdge


//@version=5
strategy("Gold Scalping 3M 10-20 SMA", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=1)

// Moving Averages
sma10 = ta.sma(close, 10)
sma20 = ta.sma(close, 20)

// Support & Resistance Levels (Last 10 bars)
recentLow = ta.lowest(low, 10)  // Dynamic support
recentHigh = ta.highest(high, 10)  // Dynamic resistance

// Buy Entry Conditions
bullishCross = ta.crossover(sma10, sma20)  // 10 SMA crosses above 20 SMA
breakoutUp = close > ta.highest(sma20, 3)  // Breaks recent 3-bar high
retestUp = ta.lowest(low, 3) > sma20  // Retests above 20 SMA
buyCondition = bullishCross and breakoutUp and retestUp

// Sell Entry Conditions
bearishCross = ta.crossunder(sma10, sma20)  // 10 SMA crosses below 20 SMA
breakoutDown = close < ta.lowest(sma20, 3)  // Breaks recent 3-bar low
retestDown = ta.highest(high, 3) < sma20  // Retests below 20 SMA
sellCondition = bearishCross and breakoutDown and retestDown

// Stop Loss & Take Profit (Dynamic)
longSL = recentLow  // SL for Buy = Last 10-bar Low
shortSL = recentHigh  // SL for Sell = Last 10-bar High

riskSizeLong = close - longSL  // Risk for Buy
riskSizeShort = shortSL - close  // Risk for Sell

longTP = close + (riskSizeLong * 2)  // 1:2 RR TP for Buy
shortTP = close - (riskSizeShort * 2)  // 1:2 RR TP for Sell

// Plot Buy/Sell Signals
plotshape(series=buyCondition, location=location.belowbar, color=color.green, style=shape.labelup, title="BUY")
plotshape(series=sellCondition, location=location.abovebar, color=color.red, style=shape.labeldown, title="SELL")

// Execute Trades
strategy.entry("Long", strategy.long, when=buyCondition)
strategy.exit("Exit Long", from_entry="Long", stop=longSL, limit=longTP)

strategy.entry("Short", strategy.short, when=sellCondition)
strategy.exit("Exit Short", from_entry="Short", stop=shortSL, limit=shortTP)

```

> Detail

https://www.fmz.com/strategy/489288

> Last Modified

2025-04-03 10:51:43
