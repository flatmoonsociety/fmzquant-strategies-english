
> Name

Multi-Moving-Average-Trend-Filter-Crossover-Quantitative-Trading-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d831093eeae1af362172.png)
![IMG](https://www.fmz.com/upload/asset/2d8a524f5d0816590e1cb.png)



[trans]

#### Strategy Overview
The multiple moving average filtered trend cross quantitative trading strategy is a comprehensive trend tracking system that cleverly combines a variety of moving averages and volume weighted average price (VWAP) to capture mid- to long-term trend changes in the market. The strategy relies primarily on exponential moving average (EMA) crossover signals as the primary entry trigger, while utilizing VWAP and simple moving averages (SMA) as filters to reduce false signals and confirm the broader market trend direction. In addition, the strategy is designed with a fast EMA crossover as a sensitive exit mechanism, allowing the system to quickly close positions when the market reverses, while avoiding premature exits during strong trends. The strategy also includes a direct reversal mechanism, which allows direct switching from long to short or from short to long when market conditions change, improving the strategy's adaptability in volatile markets.
#### Strategy Principle
The core principle of this strategy is trend identification and confirmation based on multi-level time frames. Specifically, the strategy works as follows:
1. **Trend Identification**: Use the 17-period and 31-period EMA crossovers to detect mid-term momentum changes. When the short-term EMA crosses above the long-term EMA, it indicates that an upward trend may occur; when the short-term EMA crosses below the long-term EMA, it indicates that a downtrend may occur.
2. **Trend Confirmation**: Use VWAP and 69-period SMA as additional filtering conditions to confirm the trend. This requires price to be above (for long signals) or below (for short signals) these indicators to reduce false signals in sideways or weakly trending markets.
3. **Entry logic**:
   - Long entry: When the 17-period EMA crosses above the 31-period EMA, and the price is higher than both VWAP and the 69-period SMA, the system opens a long position.
   - Short entry: When the 17-period EMA crosses below the 31-period EMA, and the price is below both VWAP and the 69-period SMA, the system opens a short position.
4. **Exit mechanism**: The strategy uses the more sensitive short-term EMA (8-period and 9-period) crossover as an exit signal, allowing the system to respond quickly to short-term market reversals.
   - Long exit: When the 8-period EMA crosses below the 9-period EMA and there is no short entry signal, close the long position.
   - Short exit: When the 8-period EMA crosses the 9-period EMA and there is no long entry signal, close the short position.
5. **Reversal Mechanism**: The strategy allows direct reversal of positions. If a long position is currently held and a short entry condition is triggered, the long position will be closed first and then a short position will be opened (or vice versa). This mechanism increases the flexibility of the strategy in rapidly changing markets.
6. **Code Implementation**: The strategy uses Boolean variables to track the current position status (`long_active` and `short_active`, and perform corresponding trading operations when the conditions are met. In addition, the strategy also visually displays various indicators and intersections, making it easier for traders to monitor market conditions.
#### Strategic Advantages
1. **Multi-layer filtering system**: A multi-layer confirmation system is built by combining EMA crossover, VWAP and SMA filters, which significantly reduces the generation of false signals and improves the stability and reliability of the strategy.
2. **Flexible reversal mechanism**: The strategy can directly switch from long to short (or from short to long) according to market conditions without waiting for an independent exit signal before entering the market. This design allows for faster position adjustment when the trend reverses, reducing potential losses.
3. **Separated entry and exit logic**: Using EMA pairs of different periods as entry and exit signals optimizes the timing of transactions. The longer period EMA (17 and 31) is used to capture mid-term trend changes as entry signals, while the shorter period EMA (8 and 9) is used for sensitive exits, providing a faster risk control response while maintaining trend following capabilities.
4. **Comprehensive Trend Confirmation**: By combining the relative positions of price, VWAP and SMA, the strategy is able to confirm trends in multiple dimensions, which helps reduce erroneous trades during market sideways or weak trends.
5. **Visual Assistance**: The strategy provides a wealth of visual indicators, including various EMA, SMA, VWAP and key cross point markers, allowing traders to intuitively understand and monitor market conditions and strategy signals.
6. **Parameter Adjustability**: Various parameters of the strategy (such as the period of EMA and SMA) can be customized through the input box, allowing traders to optimize and adjust according to different market environments and trading varieties.
#### Strategy Risk
1. **Lagging risk**: Since the strategy uses multiple moving averages and filter conditions, entry signals may be relatively lagging, especially in rapidly changing markets. This can miss the initial stages of a trend, reducing potential gains. The solution is to adjust the periods of EMA and SMA according to the volatility characteristics of the specific market, using shorter periods for fast markets.
2. **Multiple Condition Limitations**: The strategy’s multiple entry conditions (EMA crossover plus price position relative to VWAP and SMA) may reduce trading frequency, resulting in missing some potentially beneficial trading opportunities. Consideration may be given to appropriately relaxing certain conditions under specific market circumstances, or developing alternative rules to increase trading opportunities.
3. **Lack of clear stop loss mechanism**: The strategy only relies on the EMA crossover as an exit signal and does not set a clear stop loss or take profit level. Under extreme market conditions, this can result in larger losses. It is recommended to implement additional risk management measures such as ATR-based dynamic stop loss or fixed percentage stop loss.
4. **Parameter Sensitivity**: Strategy performance is highly dependent on the selected EMA and SMA periods. The default parameters (17, 31, 8, 9, 69) may not be suitable for all assets or timeframes. The solution is to adjust parameters for specific trading instruments and market conditions through backtest optimization, or to implement an adaptive parameter adjustment mechanism.
5. **Risk of changes in market nature**: When the market changes from trend to shock or from shock to trend, the strategy may perform poorly. The solution is to add market environment detection mechanisms, such as volatility filters or trend strength indicators, and dynamically adjust strategy parameters or trading rules under different market environments.
6. **Transaction Cost Impact**: Frequent reversal trades may increase transaction costs, especially in low-volatility markets. It is recommended to consider transaction costs in the strategy and possibly limit too frequent reversal trades under certain conditions.
#### Strategy optimization direction
1. **Adaptive parameter adjustment**: Implement the adaptive adjustment mechanism of EMA and SMA cycles, and dynamically adjust parameters according to market volatility or trend strength. For example, use shorter periods in markets with higher volatility and longer periods in markets with lower volatility. This allows the strategy to better adapt to different market environments, reducing lag and increasing responsiveness.
2. **Add stop loss and take profit mechanism**: Introduce dynamic stop loss or fixed proportion stop loss based on ATR (true fluctuation range) into the strategy, as well as corresponding take profit settings. This can help control the maximum risk on a single trade and prevent excessive losses in extreme market conditions, while locking in profits from trends.
3. **Add trading volume filter**: Incorporate trading volume analysis into the strategy and only execute trades when trading volume is sufficient or a specific pattern is present. This helps improve the quality of signals and reduces the impact of slippage and false breakouts caused by low liquidity.
4. **Integrated market environment analysis**: Add market environment identification mechanisms, such as volatility indicators, trend strength indicators or cyclical analysis. Apply different trading rules or parameter settings under different market environments (trend, shock, high volatility, low volatility) to improve the adaptability of the strategy.
5. **Optimize reversal logic**: Improve the current direct reversal mechanism, possibly introducing additional confirmation conditions or delaying reversal execution to reduce too frequent reversal transactions in sideways markets. For example, one could require that the strength of a reversal signal exceed a certain threshold, or that additional market characteristics be observed before a reversal.
6. **Partial Position Management**: Implement more complex position management, such as entering and exiting the market in batches or adjusting the position size based on signal strength. This reduces the risk of cross-margin trading while maintaining full exposure to strong trends.
7. **Time filtering**: Add time filtering function to avoid trading during specific time periods when market volatility is particularly low or high. This is particularly valuable for markets that trade around the clock, such as cryptocurrencies, to avoid trading during periods of illiquidity or unusual volatility.
8. **Multiple Time Frame Analysis**: Integrate multiple time frame analysis and use trend information from longer time periods to filter or enhance signals in the current time frame. This helps align trades with the larger market trend and reduces the risk of trading against the trend.
#### Summarize
The multiple moving average filtered trend crossover quantitative trading strategy is a well-designed trend tracking system that combines multiple moving averages and VWAP to provide a trading framework that can both capture trends and manage risks. The core advantage of this strategy lies in its multi-layer filtering system and flexible reversal mechanism, allowing it to effectively adapt to different market environments.
However, this strategy also has risks such as hysteresis, parameter sensitivity and the lack of a clear stop loss mechanism. By implementing recommended optimization measures such as adaptive parameter adjustments, adding stop-loss mechanisms, integrating market environment analysis and improving position management, the robustness and performance of the strategy can be significantly improved.
Overall, this is a trading strategy with a solid foundation and is particularly suitable for mid- to long-term trend following. This strategy provides a good starting point for traders looking to capture clear trends while reducing the impact of false signals. With proper parameter tuning and optimization for specific markets and personal risk preferences, this strategy has the potential to become a valuable asset in a trader's toolbox. ||
#### Strategy Overview

The Multi-Moving Average Trend Filter Crossover Quantitative Trading Strategy is a comprehensive trend-following system that cleverly combines multiple moving averages and Volume Weighted Average Price (VWAP) to capture medium to long-term market trend changes. The strategy primarily relies on Exponential Moving Average (EMA) crossover signals as the main entry trigger conditions, while utilizing VWAP and Simple Moving Average (SMA) as filters to reduce false signals and confirm the broader market trend direction. Additionally, the strategy incorporates fast EMA crossovers as a sensitive exit mechanism, allowing the system to quickly close positions during market reversals while avoiding premature exits during strong trends. The strategy also features a direct reversal mechanism, allowing switching from long to short, or from short to long when market conditions change, enhancing the strategy's adaptability in volatile markets.

#### Strategy Principles

The core principle of this strategy is based on trend identification and confirmation across multiple timeframes. Specifically, the strategy operates as follows:

1. **Trend Identification**: Uses 17-period and 31-period EMA crossovers to detect medium-term momentum shifts. When the shorter-term EMA crosses above the longer-term EMA, it indicates a potential uptrend; when the shorter-term EMA crosses below the longer-term EMA, it indicates a potential downtrend.

2. **Trend Confirmation**: Employs VWAP and 69-period SMA as additional filtering conditions to confirm the trend. This requires the price to be above these indicators (for long signals) or below them (for short signals), reducing false signals in ranging or weak trend markets.

3. **Entry Logic**:
   - Long Entry: When the 17-period EMA crosses above the 31-period EMA, and the price is simultaneously above both VWAP and the 69-period SMA, the system opens a long position.
   - Short Entry: When the 17-period EMA crosses below the 31-period EMA, and the price is simultaneously below both VWAP and the 69-period SMA, the system opens a short position.

4. **Exit Mechanism**: The strategy uses more sensitive short-term EMAs (8-period and 9-period) crossovers as exit signals, allowing the system to respond quickly to short-term market reversals.
   - Long Exit: When the 8-period EMA crosses below the 9-period EMA, and there is no short entry signal, the long position is closed.
   - Short Exit: When the 8-period EMA crosses above the 9-period EMA, and there is no long entry signal, the short position is closed.

5. **Reversal Mechanism**: The strategy allows for direct position reversals. If a long position is currently held but a short entry condition is triggered, the system will first close the long position and then open a short position (and vice versa). This mechanism enhances the strategy's flexibility in rapidly changing markets.

6. **Code Implementation**: The strategy uses boolean variables to track the current position status (`long_active` and `short_active`) and executes appropriate trading operations when conditions are met. Additionally, the strategy visualizes various indicators and crossover points to help traders monitor market conditions.

#### Strategy Advantages

1. **Multi-Layer Filtering System**: Combines EMA crossovers, VWAP, and SMA filters to build a multi-layered confirmation system, significantly reducing false signals and improving the strategy's stability and reliability.

2. **Flexible Reversal Mechanism**: The strategy can directly switch from long to short (or from short to long) based on market conditions, without waiting for an independent exit signal before re-entry. This design allows for faster position adjustment during trend reversals, reducing potential losses.

3. **Separate Entry and Exit Logic**: Uses different periods of EMA pairs for entry and exit signals, optimizing trade timing. Longer period EMAs (17 and 31) are used to capture medium-term trend changes for entries, while shorter period EMAs (8 and 9) provide sensitive exits, offering fast risk control response while maintaining trend-following capabilities.

4. **Comprehensive Trend Confirmation**: By combining the relative position of price to VWAP and SMA, the strategy can confirm trends across multiple dimensions, helping reduce erroneous trades during market ranging or weak trends.

5. **Visual Assistance**: The strategy provides rich visual indicators, including various EMAs, SMA, VWAP, and markers for key crossover points, allowing traders to intuitively understand and monitor market conditions and strategy signals.

6. **Parameter Adjustability**: The strategy's parameters (such as EMA and SMA periods) can be customized through input fields, allowing traders to optimize adjustments based on different market environments and trading instruments.

#### Strategy Risks

1. **Lag Risk**: Due to the use of multiple moving averages and filtering conditions, entry signals may be relatively delayed, especially in rapidly changing markets. This may miss the initial phase of trends, reducing potential returns. The solution is to adjust EMA and SMA periods based on the volatility characteristics of specific markets, using shorter periods for faster markets.

2. **Multiple Condition Restrictions**: The strategy's multiple entry conditions (EMA crossover plus price position relative to VWAP and SMA) may reduce trading frequency, causing missed potential favorable trading opportunities. Consider relaxing certain conditions in specific market environments or developing alternative rules to increase trading opportunities.

3. **Lack of Explicit Stop-Loss Mechanism**: The strategy relies solely on EMA crossovers as exit signals without setting explicit stop-loss or take-profit levels. In extreme market conditions, this may lead to larger losses. It is recommended to implement additional risk management measures, such as ATR-based dynamic stop-losses or fixed percentage stop-losses.

4. **Parameter Sensitivity**: Strategy performance is highly dependent on the selected EMA and SMA periods. Default parameters (17, 31, 8, 9, 69) may not be suitable for all assets or timeframes. The solution is to adjust parameters through backtesting optimization for specific trading instruments and market conditions, or implement adaptive parameter adjustment mechanisms.

5. **Market Regime Change Risk**: The strategy may perform poorly when markets transition from trending to ranging or vice versa. The solution is to add market environment detection mechanisms, such as volatility filters or trend strength indicators, to dynamically adjust strategy parameters or trading rules in different market environments.

6. **Trading Cost Impact**: Frequent reversal trades may increase trading costs, especially in low-volatility markets. It is advisable to consider trading costs in the strategy and potentially limit overly frequent reversal trades under certain conditions.

#### Strategy Optimization Directions

1. **Adaptive Parameter Adjustment**: Implement an adaptive adjustment mechanism for EMA and SMA periods, dynamically adjusting parameters based on market volatility or trend strength. For example, use shorter periods in higher volatility markets and longer periods in lower volatility markets. This allows the strategy to better adapt to different market environments, reducing lag and improving response speed.

2. **Add Stop-Loss and Take-Profit Mechanisms**: Introduce ATR (Average True Range)-based dynamic stop-losses or fixed percentage stop-losses into the strategy, along with corresponding take-profit settings. This helps control maximum risk per trade, preventing excessive losses under extreme market conditions while locking in profits during trends.

3. **Add Volume Filters**: Incorporate volume analysis into the strategy, executing trades only when volume is sufficient or displays specific patterns. This helps improve signal quality and reduce the impact of low liquidity leading to slippage and false breakouts.

4. **Integrate Market Environment Analysis**: Add market environment recognition mechanisms, such as volatility indicators, trend strength indicators, or cyclical analysis. Apply different trading rules or parameter settings in different market environments (trending, ranging, high volatility, low volatility) to improve the strategy's adaptability.

5. **Optimize Reversal Logic**: Improve the current direct reversal mechanism, potentially introducing additional confirmation conditions or delayed reversal execution to reduce overly frequent reversal trades in ranging markets. For example, require reversal signal strength to exceed a threshold or observe additional market characteristics before reversing.

6. **Partial Position Management**: Implement more complex position management, such as phased entries/exits or adjusting position size based on signal strength. This reduces the risk of all-in trading while maintaining full exposure to strong trends.

7. **Time Filtering**: Add time filtering functionality to avoid trading during specific time periods when market volatility is particularly low or high. This is especially valuable for 24/7 markets like cryptocurrencies, avoiding trades during periods of insufficient liquidity or abnormal volatility.

8. **Multi-Timeframe Analysis**: Integrate multi-timeframe analysis, using trend information from longer time periods to filter or enhance signals in the current timeframe. This helps align trades with larger market trends, reducing the risk of counter-trend trading.

#### Summary

The Multi-Moving Average Trend Filter Crossover Quantitative Trading Strategy is a well-designed trend-following system that provides a trading framework capable of both capturing trends and managing risk by combining multiple moving averages and VWAP. The core strengths of the strategy lie in its multi-layer filtering system and flexible reversal mechanism, allowing it to effectively adapt to different market environments.

However, the strategy also faces risks such as lag, parameter sensitivity, and lack of explicit stop-loss mechanisms. By implementing the suggested optimization measures, such as adaptive parameter adjustment, adding stop-loss mechanisms, integrating market environment analysis, and improving position management, the strategy's robustness and performance can be significantly enhanced.

Overall, this is a trading strategy with a solid foundation, particularly suitable for medium to long-term trend following. For traders seeking to capture clear trends while reducing the impact of false signals, this strategy provides a good starting point. Through appropriate parameter adjustments and optimizations targeted at specific markets and personal risk preferences, this strategy has the potential to become a valuable asset in a trader's toolkit.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-02-20 00:00:00
end: 2025-04-07 00:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"ETH_USDT"}]
*/

//@version=5
strategy("EMA+SMA+VWAP Trading Strategy ", overlay=true)

// Inputs
emaShortPeriod = input.int(17, title="EMA Entry Short")
emaLongPeriod = input.int(31, title="EMA Entry Long")
smaPeriod = input.int(69, title="SMA Longest")
emaShortPeriod2 = input.int(8, title="EMA Exit Small")
emaShortPeriod3 = input.int(9, title="EMA Exit Long")

// Calculate Indicators
emaShort = ta.ema(close, emaShortPeriod)
emaShort2 = ta.ema(close, emaShortPeriod2)
emaShort3 = ta.ema(close, emaShortPeriod3)
emaLong = ta.ema(close, emaLongPeriod)
vwap = ta.vwap(hlc3)
smalong = ta.sma(close, smaPeriod)

// Define Conditions
long_condition = ta.crossover(emaShort, emaLong) and close > vwap and close > smalong
short_condition = ta.crossunder(emaShort, emaLong) and close < vwap and close < smalong
long_exit_condition = ta.crossunder(emaShort2, emaShort3)
short_exit_condition = ta.crossover(emaShort2, emaShort3)

// Position Tracking
var bool long_active = false
var bool short_active = false

// Execute Trades with Reversal Logic
// Long Entry: Open long and close short if active
if long_condition
    if short_active
        strategy.close("Short")  // Close short (buy to cover)
        short_active := false
    if not long_active
        strategy.entry("Long", strategy.long)  // Open long
        long_active := true

// Short Entry: Open short and close long if active
if short_condition
    if long_active
        strategy.close("Long")  // Close long (sell)
        long_active := false
    if not short_active
        strategy.entry("Short", strategy.short)  // Open short
        short_active := true

// Normal Exits (no reversal)
if long_active and long_exit_condition and not short_condition
    strategy.close("Long")  // Sell to close long
    long_active := false

if short_active and short_exit_condition and not long_condition
    strategy.close("Short")  // Buy to close short
    short_active := false

// Plot Indicators
plot(emaShort, color=color.rgb(48, 240, 23), title="EMA Short")
plot(emaLong, color=color.rgb(39, 209, 252), title="EMA Long")
plot(vwap, color=color.rgb(8, 128, 175), title="VWAP")
plot(smalong, color=color.rgb(194, 12, 51), linewidth=2, title="SMA Long")
plot(ta.cross(emaShort, emaLong) ? emaShort : na, style=plot.style_cross, color=color.rgb(126, 248, 45), linewidth=3, title="EMA Cross")
plot(emaShort2, color=color.rgb(222, 23, 240), title="EMA Short 2")
plot(emaShort3, color=color.rgb(234, 148, 255), title="EMA Short 3")
plot(ta.cross(emaShort2, emaShort3) ? emaShort : na, style=plot.style_cross, color=color.rgb(250, 170, 230), linewidth=3, title="EMA Cross")
```

> Detail

https://www.fmz.com/strategy/489736

> Last Modified

2025-04-08 10:18:57
