
> Name

VWAP trading strategy and volume anomaly monitoringVWAP-Trading-Strategy-with-Volume-Anomaly-Detection
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/5f0ed5b4b166d3e829.png)

[trans]
#### Overview
The strategy is based on multiple VWAP (Volume Weighted Average Price) levels, including the open, high, low, and VWAP of candles with abnormally high volume. The strategy uses VWAP as support and resistance levels, taking into account volume anomalies. When the price breaks through the VWAP level and meets certain conditions, the strategy generates a trading signal. In addition, this strategy also uses the RSI indicator to detect changes in momentum as a condition for closing positions.
#### Strategy Principle
1. Calculate multiple VWAP levels, including opening price VWAP, highest price VWAP, lowest price VWAP and VWAP of abnormally high volume candlesticks.
2. Detect candles with abnormally high volume and reset the accumulation variable of the VWAP with abnormally high volume on that candle.
3. Set the deviation value above and below the VWAP level as the trigger condition for the trading signal.
4. Check if there is a gap in price on the other side of the VWAP to avoid false signals.
5. Based on the price position relative to VWAP and the relationship between the closing price and the opening price, multiple trading signals are generated, including Wick (shadow line) and Crossover (crossover).
6. Use the RSI indicator to detect changes in momentum. When the RSI exceeds 70 or falls below 30, close the corresponding trade.
#### Advantage Analysis
1. This strategy utilizes multiple VWAP levels to provide more comprehensive support and resistance information.
2. By detecting candles with abnormally high trading volume, the strategy can capture important changes in the market.
3. Setting the deviation value can filter out some noise signals and improve the quality of trading signals.
4. Taking into account the price gap situation on the other side of VWAP, avoiding some false signals.
5. Generate multiple trading signals based on the relative position of price and VWAP and the relationship between closing price and opening price, increasing the flexibility of the strategy.
6. Using the RSI indicator as the closing condition can help the strategy exit the transaction in time when the momentum changes.
#### Risk Analysis
1. This strategy relies on the VWAP level. If the market experiences extreme conditions, VWAP may lose its effectiveness.
2. The judgment of abnormally high trading volume is based on a fixed threshold and may not be adaptable to different market conditions.
3. The setting of the deviation value may need to be adjusted according to different markets and trading types.
4. This strategy generates multiple trading signals, which may lead to over-trading and high trading costs.
5. The RSI indicator may produce lagging closing signals, causing the strategy to bear greater risks.
#### Optimization direction
1. Optimize the calculation method of VWAP level, such as considering a longer time period or using a weighting method.
2. Optimize the judgment criteria for abnormally high trading volume, such as using adaptive thresholds or combining other trading volume indicators.
3. Perform parameter optimization on the deviation value to find the best deviation amplitude.
4. Introduce risk management measures, such as setting stop loss and take profit, to control the risk exposure of a single transaction.
5. Try other momentum indicators or combine multiple indicators to get more accurate closing signals.
6. Filter trading signals to reduce excessive trading and lower transaction costs.
#### Summary
This strategy utilizes multiple VWAP levels and volume anomaly detection to generate diverse trading signals. By considering the relative position of price to VWAP, the relationship between closing and opening prices, and the RSI indicator, the strategy attempts to capture important changes in the market and exit trades in a timely manner. However, this strategy also has some risks, such as adaptability to extreme market conditions, over-trading, and delayed closing signals. In order to further improve, you can consider optimizing the calculation method of VWAP, the judgment criteria of abnormal trading volume, the setting of deviation values, and introducing risk management measures and more indicator combinations. Overall, this strategy provides a good starting point for VWAP-based trading, but it still needs to be optimized and adjusted based on actual market conditions.
|| 

#### Overview
This strategy is based on multiple VWAP (Volume Weighted Average Price) levels, including the open price, high price, low price, and the VWAP of candles with abnormally high volume. The strategy utilizes VWAP levels as support and resistance, while also considering abnormal volume situations. When the price breaks through VWAP levels and meets certain conditions, the strategy generates trading signals. Additionally, the strategy uses the RSI indicator to detect momentum changes as an exit condition.

#### Strategy Principles
1. Calculate multiple VWAP levels, including the open price VWAP, high price VWAP, low price VWAP, and the VWAP of candles with abnormally high volume.
2. Detect candles with abnormally high volume and reset the cumulative variables for the abnormally high volume VWAP on those candles.
3. Set displacement values above and below the VWAP levels as trigger conditions for trading signals.
4. Check for gaps on the opposite side of the VWAP to avoid false signals.
5. Generate multiple trading signals based on the price position relative to VWAP and the relationship between the closing price and the opening price, including Wick and Crossover types.
6. Use the RSI indicator to detect momentum changes and close corresponding trades when RSI exceeds 70 or falls below 30.

#### Advantage Analysis
1. The strategy utilizes multiple VWAP levels, providing more comprehensive support and resistance information.
2. By detecting candles with abnormally high volume, the strategy can capture significant market changes.
3. Setting displacement values can filter out some noise signals and improve the quality of trading signals.
4. The strategy considers gap situations on the opposite side of VWAP, avoiding some false signals.
5. Multiple trading signals are generated based on the price position relative to VWAP and the relationship between the closing price and the opening price, increasing the flexibility of the strategy.
6. Using the RSI indicator as an exit condition can help the strategy exit trades in a timely manner when momentum changes.

#### Risk Analysis
1. The strategy relies on VWAP levels, which may lose effectiveness during extreme market conditions.
2. The judgment of abnormally high volume is based on a fixed threshold, which may not adapt to different market situations.
3. The setting of displacement values may need to be adjusted according to different markets and trading instruments.
4. The strategy generates multiple trading signals, which may lead to overtrading and high transaction costs.
5. The RSI indicator may produce lagging exit signals, causing the strategy to bear greater risks.

#### Optimization Directions
1. Optimize the calculation method of VWAP levels, such as considering longer time periods or using weighted methods.
2. Optimize the judgment criteria for abnormally high volume, such as adopting adaptive thresholds or combining with other volume indicators.
3. Perform parameter optimization on displacement values to find the optimal deviation range.
4. Introduce risk management measures, such as setting stop-loss and take-profit levels, to control the risk exposure of individual trades.
5. Try other momentum indicators or combine multiple indicators to obtain more accurate exit signals.
6. Filter trading signals to reduce overtrading and lower transaction costs.

#### Summary
This strategy utilizes multiple VWAP levels and abnormal volume detection to generate diverse trading signals. By considering the relative position of price to VWAP, the relationship between the closing price and the opening price, and the RSI indicator, the strategy attempts to capture significant market changes and exit trades in a timely manner. However, the strategy also has some risks, such as adaptability to extreme market conditions, overtrading, and lagging exit signals. To further improve the strategy, one can consider optimizing the calculation method of VWAP, the judgment criteria for abnormal volume, the setting of displacement values, and introducing risk management measures and more indicator combinations. Overall, this strategy provides a good starting point for VWAP-based trading but still requires optimization and adjustment based on actual market conditions.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-05-30 00:00:00
end: 2024-06-06 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("5 Anchored VWAP Strategy with Abnormally High Volume Candle", overlay=true)

// Initialize VWAP variables
var float vwap_open = na
var float vwap_high = na
var float vwap_low = na
var float vwap_high_volume = na

var float cum_v_open = 0
var float cum_v_high = 0
var float cum_v_low = 0
var float cum_v_high_volume = 0

var float cum_pv_open = 0
var float cum_pv_high = 0
var float cum_pv_low = 0
var float cum_pv_high_volume = 0

var float highest_volume = 0

// Initialize YTD high and low variables
var float ytd_high = na
var float ytd_low = na

// Parameters for abnormal volume detection
length = 20
volume_threshold = 2.0

// Displacement parameters
displacement_percentage = 0.01 // 1% displacement

// Calculate average volume
avg_volume = ta.sma(volume, length)

// Check if it's the first day of the year
is_first_day_of_year = year(time) != year(time[1])

// Reset YTD high and low on the first day of the year
if is_first_day_of_year
    ytd_high := high
    ytd_low := low

// Update YTD high and low
ytd_high := na(ytd_high) ? high : math.max(ytd_high, high)
ytd_low := na(ytd_low) ? low : math.min(ytd_low, low)

// Update cumulative variables for open VWAP
cum_v_open += volume
cum_pv_open += close * volume
if cum_v_open != 0
    vwap_open := cum_pv_open / cum_v_open

// Update cumulative variables for high VWAP
if high == ytd_high
    cum_v_high := 0
    cum_pv_high := 0

cum_v_high += volume
cum_pv_high += close * volume
if cum_v_high != 0
    vwap_high := cum_pv_high / cum_v_high

// Update cumulative variables for low VWAP
if low == ytd_low
    cum_v_low := 0
    cum_pv_low := 0

cum_v_low += volume
cum_pv_low += close * volume
if cum_v_low != 0
    vwap_low := cum_pv_low / cum_v_low

// Check for new high-volume candle that is also abnormally high and reset cumulative variables for high-volume VWAP
new_high_volume = false
if volume > highest_volume and volume > volume_threshold * avg_volume
    highest_volume := volume
    cum_v_high_volume := 0
    cum_pv_high_volume := 0
    new_high_volume := true

cum_v_high_volume += volume
cum_pv_high_volume += close * volume
if cum_v_high_volume != 0
    vwap_high_volume := cum_pv_high_volume / cum_v_high_volume

// Plot VWAPs
plot(vwap_open, color=color.red, linewidth=2, title="VWAP Open")
plot(vwap_high, color=color.green, linewidth=2, title="VWAP High")
plot(vwap_low, color=color.blue, linewidth=2, title="VWAP Low")
plot(vwap_high_volume, color=color.purple, linewidth=2, title="VWAP High Volume")

// Plot a vertical line on the chart only when a new high-volume VWAP anchor occurs
bgcolor(new_high_volume ? color.new(color.purple, 90) : na, offset=-1)

// Calculate displacement amounts
displacement_amount_open = vwap_open * displacement_percentage
displacement_amount_high = vwap_high * displacement_percentage
displacement_amount_low = vwap_low * displacement_percentage
displacement_amount_high_volume = vwap_high_volume * displacement_percentage

// Check for gaps on the opposite side of a VWAP
gap_up_opposite_open = na(close[1]) ? false : (open > close[1] and open < vwap_open and close[1] > vwap_open)
gap_down_opposite_open = na(close[1]) ? false : (open < close[1] and open > vwap_open and close[1] < vwap_open)

gap_up_opposite_high = na(close[1]) ? false : (open > close[1] and open < vwap_high and close[1] > vwap_high)
gap_down_opposite_high = na(close[1]) ? false : (open < close[1] and open > vwap_high and close[1] < vwap_high)

gap_up_opposite_low = na(close[1]) ? false : (open > close[1] and open < vwap_low and close[1] > vwap_low)
gap_down_opposite_low = na(close[1]) ? false : (open < close[1] and open > vwap_low and close[1] < vwap_low)

gap_up_opposite_high_volume = na(close[1]) ? false : (open > close[1] and open < vwap_high_volume and close[1] > vwap_high_volume)
gap_down_opposite_high_volume = na(close[1]) ? false : (open < close[1] and open > vwap_high_volume and close[1] < vwap_high_volume)

// RSI calculation for momentum change detection
rsi = ta.rsi(close, 14)
long_exit_condition = rsi > 70
short_exit_condition = rsi < 30

// Debugging Plots
plotshape(not gap_up_opposite_open and not gap_down_opposite_open and close > vwap_open and low < vwap_open - displacement_amount_open and close[1] < vwap_open, style=shape.triangledown, location=location.abovebar, color=color.red, size=size.small, title="Open Long Signal")
plotshape(not gap_up_opposite_open and not gap_down_opposite_open and close < vwap_open and high > vwap_open + displacement_amount_open and close[1] > vwap_open, style=shape.triangleup, location=location.belowbar, color=color.green, size=size.small, title="Open Short Signal")

plotshape(not gap_up_opposite_high and not gap_down_opposite_high and close > vwap_high and low < vwap_high - displacement_amount_high and close[1] < vwap_high, style=shape.triangledown, location=location.abovebar, color=color.blue, size=size.small, title="High Long Signal")
plotshape(not gap_up_opposite_high and not gap_down_opposite_high and close < vwap_high and high > vwap_high + displacement_amount_high and close[1] > vwap_high, style=shape.triangleup, location=location.belowbar, color=color.orange, size=size.small, title="High Short Signal")

plotshape(not gap_up_opposite_low and not gap_down_opposite_low and close > vwap_low and low < vwap_low - displacement_amount_low and close[1] < vwap_low, style=shape.triangledown, location=location.abovebar, color=color.purple, size=size.small, title="Low Long Signal")
plotshape(not gap_up_opposite_low and not gap_down_opposite_low and close < vwap_low and high > vwap_low + displacement_amount_low and close[1] > vwap_low, style=shape.triangleup, location=location.belowbar, color=color.yellow, size=size.small, title="Low Short Signal")

plotshape(not gap_up_opposite_high_volume and not gap_down_opposite_high_volume and close > vwap_high_volume and low < vwap_high_volume - displacement_amount_high_volume and close[1] < vwap_high_volume, style=shape.triangledown, location=location.abovebar, color=color.teal, size=size.small, title="High Volume Long Signal")
plotshape(not gap_up_opposite_high_volume and not gap_down_opposite_high_volume and close < vwap_high_volume and high > vwap_high_volume + displacement_amount_high_volume and close[1] > vwap_high_volume, style=shape.triangleup, location=location.belowbar, color=color.fuchsia, size=size.small, title="High Volume Short Signal")

// Trading signals based on VWAP support/resistance with displacement, no gaps on the opposite side, and bounce conditions
if not gap_up_opposite_open and not gap_down_opposite_open
    if (close > vwap_open and low < vwap_open)
        if close > open
            strategy.entry("Long_Open_Wick", strategy.long, comment="Wick")
        else
            strategy.entry("Long_Open_Crossover", strategy.long, comment="Crossover")
    
    if (close < vwap_open and high > vwap_open)
        if close < open
            strategy.entry("Short_Open_Wick", strategy.short, comment="Wick")
        else
            strategy.entry("Short_Open_Crossover", strategy.short, comment="Crossover")

if not gap_up_opposite_high and not gap_down_opposite_high
    if (close > vwap_high and low < vwap_high)
        if close > open
            strategy.entry("Long_High_Wick", strategy.long, comment="Wick")
        else
            strategy.entry("Long_High_Crossover", strategy.long, comment="Crossover")
    
    if (close < vwap_high and high > vwap_high)
        if close < open
            strategy.entry("Short_High_Wick", strategy.short, comment="Wick")
        else
            strategy.entry("Short_High_Crossover", strategy.short, comment="Crossover")

if not gap_up_opposite_low and not gap_down_opposite_low
    if (close > vwap_low and low < vwap_low)
        if close > open
            strategy.entry("Long_Low_Wick", strategy.long, comment="Wick")
        else
            strategy.entry("Long_Low_Crossover", strategy.long, comment="Crossover")
    
    if (close < vwap_low and high > vwap_low)
        if close < open
            strategy.entry("Short_Low_Wick", strategy.short, comment="Wick")
        else
            strategy.entry("Short_Low_Crossover", strategy.short, comment="Crossover")

if not gap_up_opposite_high_volume and not gap_down_opposite_high_volume
    if (close > vwap_high_volume and low < vwap_high_volume)
        if close > open
            strategy.entry("Long_High_Volume_Wick", strategy.long, comment="Wick")
        else
            strategy.entry("Long_High_Volume_Crossover", strategy.long, comment="Crossover")
    
    if (close < vwap_high_volume and high > vwap_high_volume)
        if close < open
            strategy.entry("Short_High_Volume_Wick", strategy.short, comment="Wick")
        else
            strategy.entry("Short_High_Volume_Crossover", strategy.short, comment="Crossover")

// Exit trades based on RSI momentum change
if strategy.position_size > 0 and long_exit_condition
    strategy.close("Long_Open_Wick")
    strategy.close("Long_Open_Crossover")
    strategy.close("Long_High_Wick")
    strategy.close("Long_High_Crossover")
    strategy.close("Long_Low_Wick")
    strategy.close("Long_Low_Crossover")
    strategy.close("Long_High_Volume_Wick")
    strategy.close("Long_High_Volume_Crossover")

if strategy.position_size < 0 and short_exit_condition
    strategy.close("Short_Open_Wick")
    strategy.close("Short_Open_Crossover")
    strategy.close("Short_High_Wick")
    strategy.close("Short_High_Crossover")
    strategy.close("Short_Low_Wick")
    strategy.close("Short_Low_Crossover")
    strategy.close("Short_High_Volume_Wick")
    strategy.close("Short_High_Volume_Crossover")
```

> Detail

https://www.fmz.com/strategy/453659

> Last Modified

2024-06-07 15:44:04
