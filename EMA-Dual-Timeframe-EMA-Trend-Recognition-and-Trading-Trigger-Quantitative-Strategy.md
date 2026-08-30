
> Name

Dual-Timeframe-EMA-Trend-Recognition-and-Trading-Trigger-Quantitative-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d8eb81322e5459be97b4.png)
![IMG](https://www.fmz.com/upload/asset/2d8064867e92f17509108.png)

[trans]

#### Overview
The dual time frame EMA trend identification and trading trigger quantitative strategy is a trend following trading system that combines the daily and hourly time periods. This strategy mainly uses exponential moving averages (EMA) on different time periods to identify the overall trend direction of the market and generate accurate trading signals. The core idea of ​​strategic design is to "go with the trend" - use a longer time period (daily line) to determine the overall trend direction, while using a shorter time period (hourly line) to find the best entry point, supplemented by volatility filtering and fixed stop-loss mechanisms to ensure risk control.
#### Strategy Principle
The core principle of this strategy is based on multiple time frame analysis and EMA crossover signals. The specific working principle is as follows:
1. **Trend identification (daily level)**:
   - Use the relative positions of the 5-period short-term EMA and the 30-period long-term EMA on the daily time frame to determine the overall trend.
   - When the short-term EMA (5) is above the long-term EMA (30), an uptrend is determined
   - When the short-term EMA (5) is below the long-term EMA (30), a downtrend is determined
2. **Trading signal generation (hourly level)**:
   - On the hourly time frame, use the intersection of the 12-period short-term EMA and the 26-period long-term EMA to generate trading signals
   - Buy signal: Triggered when the hourly short-term EMA crosses the long-term EMA upward and the daily trend is upward
   - Sell signal: Triggered when the hourly short-term EMA crosses the long-term EMA downward and the daily trend is downward
3. **Volatility trigger mechanism**:
   - Additional trading trigger conditions based on price volatility are set
   - High volatility rising: If the price rises more than 5% within a single K-line and the daily trend is upward, a long signal is triggered
   - High Volatility Decline: If the price falls by more than 5% within a single K-line and the daily trend is downward, a short signal is triggered.
4. **Stop loss calculation**:
   - Long trade: Stop loss is set at the lowest point of the past 10 candlesticks
   - Short trade: Stop loss is set at the highest point of the past 10 candlesticks
5. **Transaction Execution**:
   - Enter long positions when a buy signal or high volatility uptrend conditions are met
   - Enter short positions when a sell signal or high volatility downturn condition is met
   - Exit the transaction according to the calculated stop loss point respectively
In terms of core code implementation, the strategy uses the request.security function to obtain EMA values ​​from different time periods, and then uses the cross judgment functions ta.crossover and ta.crossunder to detect EMA crossing situations. By combining daily trends with hourly signals, counter-trend transactions are effectively filtered out and transaction quality is improved.
#### Strategic Advantages
After in-depth analysis of the strategy code, this quantitative trading system has the following significant advantages:
1. **Multiple time frame analysis**: Combining the two time periods of daily and hourly lines, it can not only grasp the direction of the general trend, but also accurately capture the entry opportunity, effectively balancing the trading frequency and success rate.
2. **Trend Confirmation Mechanism**: By requiring hourly trading signals to be consistent with the daily trend direction, counter-trend transactions are effectively filtered and false signals are reduced.
3. **Multi-dimensional trigger conditions**: In addition to conventional EMA cross signals, a trigger mechanism based on volatility is also added, which can capture sudden strong price fluctuations and improve the adaptability of the strategy.
4. **Dynamic stop loss setting**: The stop loss point is automatically adjusted based on recent market fluctuations (the highest/lowest points of the past 10 K lines), providing targeted risk control according to different market conditions.
5. **Two-way trading capability**: Supports both long and short transactions, and can generate profit opportunities in different market environments.
6. **Visual feedback**: The strategy provides four EMA line chart displays of different colors to facilitate traders to intuitively judge the current market conditions and strategy signals.
7. **Simple and clear parameters**: Only four main parameters are used (two EMA lengths for each of the two time periods), which reduces the risk of over-fitting and facilitates optimization and adjustment.
#### Strategy Risk
Although this strategy is well designed, it still has the following potential risks:
1. **Poor performance in oscillatory markets**: As a trend following strategy, in a market environment that is sideways or frequently oscillating, it may generate more false signals, leading to continuous stop losses.
   - Solution: Consider adding additional sideways identification indicators (such as ADX or volatility indicators), and suspend trading when sideways markets are identified.
2. **Limitations of fixed volatility trigger threshold**: The 5% fixed volatility threshold may be too high or too low under different varieties or different market environments.
   - Workaround: Consider making the volatility threshold dynamic, such as based on a multiple of ATR (true range) or a percentage of historical volatility.
3. **Stop loss settings may be too loose**: Using the extreme values ​​of the past 10 K lines as stop loss may lead to the stop loss position being too far away in some cases, increasing the risk of a single transaction.
   - Solution: A stop loss mechanism based on ATR can be introduced, or a hybrid strategy that combines fixed percentage stop loss and dynamic stop loss.
4. **EMA parameters are fixed**: The EMA parameters used in the strategy are fixed and may not be suitable for all market environments.
   - Solution: Consider implementing a parameter adaptive mechanism to automatically adjust the EMA length according to market volatility.
5. **Lack of profit acquisition mechanism**: The strategy defines clear entry and stop loss conditions, but lacks a profit-taking mechanism, which may lead to profit taking.
   - Solution: Add a trailing stop or profit-taking conditions based on technical indicators, such as price breaking another moving average or reaching a certain profit percentage.
#### Optimization direction
Based on strategic analysis, the following are several feasible optimization directions:
1. **Add trend strength filter**:
   - Introduce ADX (Average Trend Index) to measure trend strength and only execute trades when the ADX value is above a certain threshold
   - This can filter out weak trend signals in volatile markets and reduce losses caused by false breakthroughs
2. **Dynamic Volatility Threshold**:
   - Change the fixed 5% volatility trigger threshold to a dynamic threshold based on ATR, such as 1.5 times or 2 times the current ATR value
   - This can better adapt to different market environments and the fluctuation characteristics of different underlying assets
3. **Improve stop loss mechanism**:
   - Introducing a trailing stop function that automatically adjusts the stop loss position as the price moves in a favorable direction
   - Consider using a Trailing Stop or a Smart Stop based on support/resistance levels
4. **Add profit-taking conditions**:
   - Set a target price based on risk-reward ratio (such as 1:2 or 1:3 risk-reward ratio)
   - Implement partial position management, allowing positions to be closed in batches at different price levels
5. **Add transaction volume confirmation**:
   - Add trading volume confirmation conditions when generating trading signals, requiring a simultaneous increase in trading volume
   - This helps to verify the effectiveness of price breakthroughs and reduce losses caused by false breakthroughs
6. **Parameter optimization and adaptation**:
   - Implement an adaptive adjustment mechanism for EMA parameters and dynamically adjust the EMA length according to market fluctuations
   - Consider using machine learning methods to find optimal parameter combinations under different market environments
7. **Add market environment classification**:
   - Introducing the market environment classification function to divide the market into different states such as trend market and shock market
   - Adopt different trading parameters or trading logic according to different market environments
The implementation of these optimization directions will help improve the robustness and adaptability of the strategy, allowing it to maintain good performance in more market environments.
#### Summary
The dual time frame EMA trend identification and trading trigger quantitative strategy is a comprehensive trading system that combines trend tracking and momentum trading concepts. The overall trend direction is determined through daily EMAs, and hourly EMAs generate precise entry signals. At the same time, combined with volatility trigger conditions and dynamic stop-loss mechanisms, a relatively complete trading framework is constructed.
The main advantage of the strategy lies in its multi-time frame analysis capabilities and trend confirmation mechanism, which can effectively filter counter-trend transactions and reduce false signals. At the same time, its simple parameter design and two-way transaction capabilities make it highly practical and adaptable.
However, this strategy may not perform well in volatile markets, and there is room for optimization of the fixed volatility threshold and stop-loss mechanism. By adding trend strength filtering, dynamic volatility thresholds, improving stop loss mechanisms and adding market environment classification and other optimization measures, the strategy performance is expected to be further improved.
For traders looking to combine broad trends with precise entries, this is a basic strategy framework worth considering that can be further customized and optimized based on personal trading style and market characteristics. ||
#### Overview
The Dual Timeframe EMA Trend Recognition and Trading Trigger Quantitative Strategy is a trend-following trading system that combines two time periods: daily and hourly charts. This strategy primarily utilizes Exponential Moving Averages (EMAs) on different timeframes to identify overall market trend direction and generate precise trading signals. The core concept of the strategy design is "trend following" - using a longer timeframe (daily) to determine the overall trend direction, while utilizing a shorter timeframe (hourly) to find optimal entry points, complemented by volatility filtering and fixed stop-loss mechanisms to ensure risk control.

#### Strategy Principles
The core principles of this strategy are based on multi-timeframe analysis and EMA crossover signals. The specific working mechanism is as follows:

1. **Trend Identification (Daily Level)**:
   - Uses the relative position of 5-period short-term EMA and 30-period long-term EMA on the daily timeframe to determine overall trend
   - When short-term EMA(5) is above long-term EMA(30), an uptrend is confirmed
   - When short-term EMA(5) is below long-term EMA(30), a downtrend is confirmed

2. **Trade Signal Generation (Hourly Level)**:
   - On the hourly timeframe, uses crossovers between 12-period short-term EMA and 26-period long-term EMA to generate trading signals
   - Buy Signal: When hourly short-term EMA crosses above long-term EMA AND daily trend is up
   - Sell Signal: When hourly short-term EMA crosses below long-term EMA AND daily trend is down

3. **Volatility Trigger Mechanism**:
   - Additional trade triggers based on price volatility are set up
   - High Volatility Uptrend: If price rises more than 5% within a single candle and daily trend is up, triggers a long signal
   - High Volatility Downtrend: If price falls more than 5% within a single candle and daily trend is down, triggers a short signal

4. **Stop Loss Calculation**:
   - Long Trades: Stop loss set at the lowest point of the past 10 candles
   - Short Trades: Stop loss set at the highest point of the past 10 candles

5. **Trade Execution**:
   - Enter long position when buy signal or high volatility uptrend conditions are met
   - Enter short position when sell signal or high volatility downtrend conditions are met
   - Exit trades according to calculated stop-loss levels

In the core code implementation, the strategy uses the request.security function to obtain EMA values from different timeframes, then utilizes the crossover detection functions ta.crossover and ta.crossunder to detect EMA crossovers. By combining daily trends with hourly signals, counter-trend trades are effectively filtered out, improving trade quality.

#### Strategy Advantages
After in-depth analysis of the strategy code, this quantitative trading system has the following significant advantages:

1. **Multi-Timeframe Analysis**: Combines daily and hourly timeframes, capable of both capturing the major trend direction and precisely timing entries, effectively balancing trading frequency and success rate.

2. **Trend Confirmation Mechanism**: By requiring hourly trading signals to align with the daily trend direction, counter-trend trades are effectively filtered out, reducing false signals.

3. **Multi-dimensional Trigger Conditions**: In addition to conventional EMA crossover signals, a volatility-based trigger mechanism is added, capable of capturing sudden strong price movements, enhancing strategy adaptability.

4. **Dynamic Stop-Loss Setting**: Stop-loss points automatically adjust based on recent market volatility (highest/lowest points of the past 10 candles), providing targeted risk control for different market conditions.

5. **Bi-directional Trading Capability**: Supports both long and short trading, generating profit opportunities in different market environments.

6. **Visual Feedback**: The strategy provides four differently colored EMA lines on the chart, allowing traders to intuitively judge current market conditions and strategy signals.

7. **Simple and Clear Parameters**: Uses only four main parameters (two EMA lengths for each of two timeframes), reducing the risk of overfitting while facilitating optimization and adjustment.

#### Strategy Risks
Despite its sophisticated design, this strategy still has the following potential risks:

1. **Poor Performance in Oscillating Markets**: As a trend-following strategy, it may generate numerous false signals in sideways or frequently oscillating market environments, leading to consecutive stop-losses.
   - Solution: Consider adding supplementary sideways market identification indicators (such as ADX or volatility indicators), and pause trading when sideways markets are identified.

2. **Limitations of Fixed Volatility Trigger Threshold**: The fixed 5% volatility threshold may be too high or too low for different instruments or market environments.
   - Solution: Consider making the volatility threshold dynamic, such as based on multiples of ATR (Average True Range) or percentages of historical volatility.

3. **Stop-Loss Settings May Be Too Loose**: Using extremes from the past 10 candles as stop-losses may in some cases result in stop-loss points that are too distant, increasing per-trade risk.
   - Solution: Introduce ATR-based stop-loss mechanisms, or implement a hybrid strategy combining fixed percentage stops with dynamic stops.

4. **Fixed EMA Parameters**: The EMA parameters used in the strategy are fixed, which may not be suitable for all market environments.
   - Solution: Consider implementing parameter adaptive mechanisms to automatically adjust EMA lengths based on market volatility.

5. **Lack of Profit-Taking Mechanism**: The strategy defines clear entry and stop-loss conditions, but lacks profit-taking mechanisms, potentially leading to profit giveback.
   - Solution: Add trailing stops or technical indicator-based profit-taking conditions, such as price breaking through another moving average or reaching a certain profit percentage.

#### Optimization Directions
Based on strategy analysis, here are several feasible optimization directions:

1. **Add Trend Strength Filtering**:
   - Introduce ADX (Average Directional Index) to measure trend strength, only executing trades when ADX values exceed a specific threshold
   - This can filter out weak trend signals in oscillating markets, reducing losses from false breakouts

2. **Dynamic Volatility Threshold**:
   - Change the fixed 5% volatility trigger threshold to an ATR-based dynamic threshold, such as 1.5x or 2x the current ATR value
   - This better adapts to different market environments and volatility characteristics of different instruments

3. **Improve Stop-Loss Mechanism**:
   - Introduce trailing stop functionality that automatically adjusts stop-loss positions as price moves favorably
   - Consider using trailing stops or support/resistance-based intelligent stops

4. **Add Profit-Taking Conditions**:
   - Set target price levels based on risk-reward ratios (such as 1:2 or 1:3)
   - Implement partial position management, allowing gradual closing of positions at different price levels

5. **Add Volume Confirmation**:
   - Add volume confirmation conditions when generating trade signals, requiring synchronized increases in volume
   - This helps verify the validity of price breakouts, reducing losses from false breakouts

6. **Parameter Optimization and Adaptation**:
   - Implement adaptive adjustment mechanisms for EMA parameters, dynamically adjusting EMA lengths based on market volatility conditions
   - Consider using machine learning methods to find optimal parameter combinations for different market environments

7. **Add Market Environment Classification**:
   - Introduce market environment classification functionality, categorizing markets into trending, oscillating, etc.
   - Adopt different trading parameters or trading logic based on different market environments

Implementation of these optimization directions will help improve the strategy's robustness and adaptability, enabling it to maintain good performance across more market environments.

#### Summary
The Dual Timeframe EMA Trend Recognition and Trading Trigger Quantitative Strategy is a comprehensive trading system combining trend-following and momentum trading concepts. By using daily EMAs to determine overall trend direction and hourly EMAs to generate precise entry signals, while incorporating volatility trigger conditions and dynamic stop-loss mechanisms, it constructs a relatively complete trading framework.

The strategy's main advantages lie in its multi-timeframe analysis capability and trend confirmation mechanism, effectively filtering out counter-trend trades and reducing false signals. Meanwhile, its simple parameter design and bi-directional trading capability give it strong practicality and adaptability.

However, the strategy may underperform in oscillating markets, and its fixed volatility threshold and stop-loss mechanisms have room for optimization. Through adding trend strength filtering, dynamic volatility thresholds, improved stop-loss mechanisms, and market environment classification, strategy performance can be further enhanced.

For traders seeking to combine major trends with precise entries, this is a foundational strategy framework worth considering, which can be further customized and optimized according to personal trading style and market characteristics.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-03-03 00:00:00
end: 2024-12-17 00:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("EMA Trend & Trigger Strategy", overlay=true)

// Define EMA lengths for 1D timeframe
shortEmaLength1D = 5
longEmaLength1D = 30

// Define EMA lengths for 1H timeframe
shortEmaLength1H = 12
longEmaLength1H = 26

// Get EMAs for 1D timeframe (trend identification)
emashort1D = request.security(syminfo.tickerid, "1D", ta.ema(close, shortEmaLength1D))
emalong1D = request.security(syminfo.tickerid, "1D", ta.ema(close, longEmaLength1D))

// Get EMAs for 1H timeframe (trade triggers)
emashort1H = request.security(syminfo.tickerid, "60", ta.ema(close, shortEmaLength1H))
emalong1H = request.security(syminfo.tickerid, "60", ta.ema(close, longEmaLength1H))

// Determine trend based on 1D EMAs
uptrend = emashort1D > emalong1D
downtrend = emashort1D < emalong1D

// Define crossover conditions for 1H timeframe
buySignal = ta.crossover(emashort1H, emalong1H) and uptrend
sellSignal = ta.crossunder(emashort1H, emalong1H) and downtrend

// Volatility-based trigger (5% bar change)
priceChange = (close - open) / open * 100
highVolatilityUp = priceChange > 5 and uptrend
highVolatilityDown = priceChange < -5 and downtrend

// Stop Loss Calculation (based on local bottom/peak)
localBottom = ta.lowest(low, 10) // Last 10 bars lowest point
localPeak = ta.highest(high, 10) // Last 10 bars highest point

// Execute Trades with Stop Loss
if (buySignal or highVolatilityUp)
    strategy.entry("Long", strategy.long)
    strategy.exit("Long Exit", from_entry="Long", stop=localBottom)
if (sellSignal or highVolatilityDown)
    strategy.entry("Short", strategy.short)
    strategy.exit("Short Exit", from_entry="Short", stop=localPeak)

// Plot EMAs on the chart
plot(emashort1D, title="Short EMA (1D)", color=color.blue)
plot(emalong1D, title="Long EMA (1D)", color=color.red)
plot(emashort1H, title="Short EMA (1H)", color=color.green)
plot(emalong1H, title="Long EMA (1H)", color=color.orange)

```

> Detail

https://www.fmz.com/strategy/484589

> Last Modified

2025-03-03 10:28:34
