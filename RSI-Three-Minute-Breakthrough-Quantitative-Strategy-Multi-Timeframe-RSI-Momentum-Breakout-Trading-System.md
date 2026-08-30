
> Name

Three-Minute-Breakthrough Quantitative-Strategy-Multi-Timeframe-RSI-Momentum-Breakout-Trading-System
> Author

ianzeng123

> Strategy Description

![IMG](assets/images/f6c947d7cffcb172c162d598844aea363d6c4487a586d77c8b7c002fd32839ed.png)
![IMG](assets/images/e7b1385585252454306652018ba37db445ed03e23904770e364ff746e0f67e61.png)



[trans]
#### Overview
This quantitative strategy is a multi-period breakout trading system developed based on Pine Script v5, which combines the analysis advantages of the two time frames of 3 minutes and 1 minute. The core idea of ​​the strategy is to identify key price highs (peaks) and lows (troughs) on the 3-minute chart and trade after confirmation via the momentum indicator on the 1-minute chart. This strategy uses the 60-period exponential moving average (EMA) as the main trend indicator and provides momentum confirmation signals through the relative strength index (RSI), forming a complete trend-following and breakout trading system.
#### Strategy Principle
The trading logic of this strategy is mainly divided into three key parts: peak detection, trough confirmation and entry conditions.
First, the system obtains the price data of the 3-minute period through the request.security function and calculates the 60-period EMA. Peak detection adopts a multi-condition verification mechanism. The judgment standard is: a certain price bar must be above the EMA, and the highest price of the bar must be higher than the highest price of the two previous and subsequent bars (i.e. comparison of 2, 3, 4 periods forward and 1 period backward). This design ensures that true local high points are captured.
Secondly, the trough detection uses the continuous falling bar counting method. When the price falls below the EMA and there are at least 3 consecutive falling bars, the system will record the lowest point during this period as the trough. This method effectively identifies the bottom area for short-term adjustments.
Finally, entry conditions are confirmed on the 1-minute chart, including: price closes above the open (positive line), price breaks above the previously identified peak, the 180-period EMA (corresponding to the 60-period EMA on the 3-minute chart) slopes upward, and the RSI is above its 9-period moving average and trending upward. Only when all these conditions are met simultaneously will the system generate a buy signal. The strategy uses the trough as the stop loss level and automatically closes the position when the price falls below the trough.
#### Strategic Advantages
This quantitative breakout strategy has several significant advantages:
1. **Multi-period analysis framework**: Combining the 3-minute and 1-minute time frames, it can not only capture the larger trend, but also accurately enter the market, reducing the risk of false breakthroughs. This design balances signal quality and response speed.
2. **Complete entry confirmation mechanism**: It not only relies on price breakthroughs, but also combines EMA trend direction and RSI momentum indicators for multiple confirmations, which greatly reduces the possibility of false breakthrough trading.
3. **Clear Risk Management**: Using the identified troughs as stop loss points sets clear risk boundaries for each transaction, helping to control single transaction losses.
4. **Dynamic adaptation to market conditions**: By identifying peaks and valleys in real time, the strategy can adapt to different market fluctuation conditions without relying on fixed parameter adjustments.
5. **Combining trend and momentum**: Use EMA to determine the overall trend direction, and use RSI to confirm price momentum to avoid erroneous transactions when there is no trend or the trend is weakening.
#### Strategy Risk
Although this strategy is well designed, there are still potential risks:
1. **Time Period Dependence**: Strategy performance is highly dependent on the selected time period (3 minutes and 1 minute). Under different market conditions, these time frames may no longer be optimal, resulting in reduced strategy performance.
2. **Rapid Volatility Market Risk**: In a highly volatile market, the price may quickly break through the peak and then quickly retrace, resulting in a loss even though the entry signal is triggered.
3. **Stop loss setting risk**: Using the valley value as the stop loss may cause the stop loss to be too wide, increasing the potential loss of a single transaction. This risk is particularly significant in highly volatile markets.
4. **Continuous signal accumulation**: In a strong trending market, multiple consecutive entry signals may be generated. If there is no position management mechanism, it may lead to over-trading and improper fund allocation.
5. **Parameter sensitivity**: The selection of 60-period EMA and RSI parameters (14,9) may not be suitable for all market environments, and improper parameter adjustment may cause significant fluctuations in strategy performance.
Methods to address these risks include: adding an adaptive parameter adjustment mechanism, adding filters to reduce weak market trading, implementing fixed percentage stop loss instead of valley stop loss, introducing a position management system and setting a limit on the maximum number of daily transactions.
#### Optimization direction
This strategy has the following directions worthy of optimization:
1. **Adaptive parameter system**: The current strategy uses fixed 60-period EMA and RSI (14,9) parameters. A feasible optimization is to introduce an adaptive parameter adjustment mechanism based on market volatility, such as using a longer period EMA to reduce noise in high-volatility markets.
2. **Added trading filters**: You can add filtering conditions such as trading period filtering (avoiding low liquidity periods), market type identification (distinguishing trending/concussive markets), and trading volume confirmation to improve signal quality.
3. **Improved Stop Loss Strategy**: The current trough stop may be too wide or too narrow. You can consider setting a dynamic stop loss in combination with ATR (average true range), or use a trailing stop loss method to better protect profits.
4. **Add profit target setting**: The current strategy only has stop loss and no take profit mechanism. The risk-reward ratio can be set based on the distance between peaks and troughs, or a dynamic profit target such as the ATR multiple of the top N swings can be used.
5. **Integrated position management system**: Dynamically adjust the transaction size based on the strength of trading signals (such as RSI reading strength, breakthrough amplitude) and market volatility to better manage capital risks.
The implementation of these optimization directions can not only improve the original effectiveness of the strategy, but also make it more adaptable to different market environments and improve the overall stability and long-term profitability.
#### Summarize
The Three-Minute Breakout Quantitative Strategy is a well-designed multi-period trading system that combines mid-term (3-minute) trend analysis with short-term (1-minute) momentum confirmation to create a trading method that can both capture trends and enable precise entry. The core advantage of this strategy lies in its multi-level confirmation mechanism and clear risk management framework, which effectively reduces the possibility of false breakout trading.
The strategy's shortcomings mainly focus on parameter fixity and the flexibility of the stop-loss mechanism, but these issues can be solved through an adaptive parameter system, improved risk management methods and more comprehensive market filters. Through these optimizations, the strategy has the potential to develop into a more adaptable and risk-managed trading system.
For traders who want to capture breakthrough opportunities in short-cycle markets, this strategy provides a structured framework, but attention should be paid to necessary parameter adjustments and strategy optimization based on specific trading varieties and market environments to obtain the best trading results.
||
#### Overview
This quantitative strategy is a multi-timeframe breakout trading system developed using Pine Script v5, combining the analytical advantages of 3-minute and 1-minute timeframes. The core approach involves identifying key price peaks (swing highs) and dips (swing lows) on the 3-minute chart, and executing trades on the 1-minute chart after momentum confirmation. The strategy employs a 60-period Exponential Moving Average (EMA) as the primary trend indicator and uses the Relative Strength Index (RSI) to provide momentum confirmation signals, forming a comprehensive trading system that combines trend following with breakout principles.

#### Strategy Principles

The trading logic of this strategy is divided into three key components: peak detection, dip confirmation, and entry conditions.

First, the system obtains 3-minute period price data through the request.security function and calculates a 60-period EMA. Peak detection employs a multi-condition verification mechanism where a price bar must be above the EMA, and its high must exceed the highs of surrounding bars (comparing 2, 3, 4 periods back and 1 period forward). This design ensures the capture of genuine local highs.

Second, dip detection uses a consecutive declining bar counting method. When the price falls below the EMA and exhibits at least 3 consecutive declining bars, the system records the lowest point during this period as the dip. This method effectively identifies bottom areas of short-term corrections.

Finally, entry conditions are confirmed on the 1-minute chart, including: closing price higher than opening price (bullish candle), price breaking above the previously identified peak, 180-period EMA (corresponding to the 60-period EMA on the 3-minute chart) sloping upward, and RSI above its 9-period average and in an uptrend. Only when all these conditions are simultaneously met does the system generate a buy signal. The strategy uses the dip level as a stop-loss, automatically closing positions when the price falls below this level.

#### Strategy Advantages

This quantitative breakout strategy offers several significant advantages:

1. **Multi-timeframe Analysis Framework**: Combining 3-minute and 1-minute timeframes allows for capturing larger trends while enabling precise entries, reducing false breakout risks. This design balances signal quality with response speed.

2. **Comprehensive Entry Confirmation Mechanism**: Rather than relying solely on price breakouts, it incorporates EMA trend direction and RSI momentum indicators for multiple confirmations, significantly reducing the possibility of false breakout trades.

3. **Clear Risk Management**: Using identified dips as stop-loss points establishes clear risk boundaries for each trade, helping to control single-trade losses.

4. **Dynamic Adaptation to Market Conditions**: By identifying peaks and dips in real-time, the strategy can self-adapt to different market volatility conditions without relying on fixed parameter adjustments.

5. **Trend and Momentum Combination**: The strategy determines overall trend direction through EMA while confirming price momentum with RSI, avoiding erroneous trades during trendless periods or when trends are weakening.

#### Strategy Risks

Despite its well-designed structure, the strategy carries the following potential risks:

1. **Timeframe Dependency**: Strategy performance is highly dependent on the selected timeframes (3-minute and 1-minute). In different market environments, these timeframes may no longer be optimal, leading to decreased strategy performance.

2. **Rapid Fluctuation Market Risk**: In highly volatile markets, prices may quickly break through peaks and then rapidly retrace, triggering entry signals that ultimately result in losses.

3. **Stop-Loss Positioning Risk**: Using dips as stop-losses may result in excessively wide stop levels, increasing potential losses on individual trades. This risk is particularly significant in markets with extreme volatility.

4. **Consecutive Signal Accumulation**: Strong trending markets may generate multiple consecutive entry signals, potentially leading to overtrading and improper capital allocation if position management mechanisms are absent.

5. **Parameter Sensitivity**: The choice of 60-period EMA and RSI parameters (14,9) may not be suitable for all market environments, and improper parameter adjustment could lead to significant fluctuations in strategy performance.

Solutions to these risks include: implementing adaptive parameter adjustment mechanisms, adding filters to reduce trading in weak markets, implementing fixed percentage stop-losses instead of dip-based stops, introducing position management systems, and setting daily maximum trade limits.

#### Optimization Directions

The strategy presents several worthwhile optimization opportunities:

1. **Adaptive Parameter System**: The current strategy uses fixed 60-period EMA and RSI(14,9) parameters. A viable optimization would be to introduce a volatility-based adaptive parameter adjustment mechanism, such as using longer-period EMAs in high-volatility markets to reduce noise.

2. **Additional Trading Filters**: Trading session filters (avoiding low-liquidity periods), market type identification (distinguishing between trending/ranging markets), and volume confirmation could be added to improve signal quality.

3. **Improved Stop-Loss Strategy**: The current dip-based stop-loss may be either too wide or too narrow. Consider incorporating ATR (Average True Range) for dynamic stop-loss setting, or using trailing stops to better protect profits.

4. **Profit Target Implementation**: The strategy currently has stop-losses but no profit-taking mechanism. Risk-reward ratios could be established based on the distance between peaks and dips, or dynamic profit targets such as multiples of ATR over the previous N fluctuations could be used.

5. **Position Sizing System Integration**: Dynamically adjust trade size based on signal strength (such as RSI reading intensity, breakout magnitude) and market volatility to better manage capital risk.

Implementing these optimizations would not only enhance the strategy's existing effectiveness but also make it more adaptable to different market environments, improving overall robustness and long-term profitability.

#### Summary

The Three-Minute Breakthrough Quantitative Strategy is an elegantly designed multi-timeframe trading system that creates a trading method capable of both capturing trends and executing precise entries by combining medium-term (3-minute) trend analysis with short-term (1-minute) momentum confirmation. The strategy's core strengths lie in its multi-level confirmation mechanism and clear risk management framework, effectively reducing the possibility of false breakout trades.

The strategy's limitations primarily center on parameter fixity and stop-loss mechanism flexibility, but these issues can be addressed through adaptive parameter systems, improved risk management methods, and more comprehensive market filters. With these optimizations, the strategy has the potential to evolve into a trading system with stronger adaptability and more refined risk management.

For traders looking to capture breakout opportunities in short-term markets, this strategy provides a structured framework, but it's important to note the necessity of parameter adjustments and strategy optimizations based on specific trading instruments and market environments to achieve optimal trading results.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-03-20 00:00:00
end: 2025-03-25 00:00:00
period: 10m
basePeriod: 10m
exchanges: [{"eid":"Futures_Binance","currency":"ETH_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © adamkiil79
//@version=5
//@version=5
strategy("3min Breakout Strategy", overlay=true)

// Fetch 3-minute timeframe data
close_3min = request.security(syminfo.tickerid, "3", close)
high_3min = request.security(syminfo.tickerid, "3", high)
low_3min = request.security(syminfo.tickerid, "3", low)
open_3min = request.security(syminfo.tickerid, "3", open)

// Calculate 60-period EMA on 3-minute data
ema60_3min = ta.ema(close_3min, 60)

// Detect peaks on 3-minute data
aboveEMA_3min = close_3min > ema60_3min
peakConfirmed_3min = aboveEMA_3min[2] and high_3min[2] > high_3min[3] and high_3min[2] > high_3min[4] and high_3min[2] > high_3min[1] and high_3min[2] > high_3min[0]

// Persistent variables for peak and dip levels
var float peak_level_3min = na
var float dip_level_3min = na
var bool in_dip_sequence_3min = false
var int down_candle_count_3min = 0

// Peak detection logic
if peakConfirmed_3min
    peak_level_3min := high_3min[2]
    in_dip_sequence_3min := false
    down_candle_count_3min := 0

// Dip detection logic
else if close_3min <= ema60_3min and not na(peak_level_3min)
    if not in_dip_sequence_3min
        in_dip_sequence_3min := true
        down_candle_count_3min := close_3min < open_3min ? 1 : 0
    else
        if close_3min < open_3min
            down_candle_count_3min := down_candle_count_3min + 1
        else
            down_candle_count_3min := 0
        if down_candle_count_3min >= 3
            dip_level_3min := ta.lowest(low_3min, down_candle_count_3min)
else
    in_dip_sequence_3min := false

// 1-minute indicators for entry confirmation
ema180 = ta.ema(close, 180)  // Roughly aligns with 60-period EMA on 3-min
rsi = ta.rsi(close, 14)
rsi_signal = ta.ema(rsi, 9)

// Entry condition: Break above peak with bullish signals
entry_condition = close > open and close > peak_level_3min and ema180 > ema180[1] and rsi > rsi_signal and rsi > rsi[1]

// Enter trades only when levels are defined
if not na(peak_level_3min) and not na(dip_level_3min) and entry_condition
    strategy.entry("Buy", strategy.long, stop=dip_level_3min)

// Exit condition: Price falls below dip level
if strategy.position_size > 0 and close < dip_level_3min
    strategy.close("Buy")

// Plot EMA for reference
plot(ema180, color=color.orange, linewidth=2, title="180 EMA")
```

> Detail

https://www.fmz.com/strategy/488529

> Last Modified

2025-03-28 16:39:58
