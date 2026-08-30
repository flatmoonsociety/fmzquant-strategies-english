
> Name

Momentum-Multi-Indicator-Trend-Following-Strategy-Donchian-Channel-with-SuperTrend-and-Volume-Filter-Entry-System
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d8f58e98e40329cef7b1.png)
![IMG](https://www.fmz.com/upload/asset/2d86e53cedf8ee1abe065.png)


[trans]
#### Overview
This strategy is a trend following trading system based on Donchian Channel breakout, which combines SuperTrend and volume filters to enhance the reliability of trading signals. This strategy mainly identifies potential long trading opportunities by capturing price breakthroughs above historical highs, while using volume confirmation and trend following indicators to filter out false breakout signals. The strategy design is flexible and parameters can be optimized according to different market environments and trading varieties.
#### Strategy Principle
The core logic of the strategy is based on the following key components:
1. Tang Qian Channel: Calculate the highest price and lowest price within the user-defined period to form the upper track, lower track and middle track. When the price breaks through the upper rail, a long entry signal is triggered.
2. Volume filter: By comparing the current trading volume with the 20-period moving average, it ensures that you only enter the market when the trading volume is amplified, improving the reliability of breakthroughs.
3. Super trend indicator: As a trend confirmation tool, it displays green when the trend is bullish and red when the trend is bearish.
4. Flexible stop loss mechanism: Provides four different stop loss options, including lower track stop loss, middle track stop loss, super trend stop loss and percentage trailing stop loss.
#### Strategic Advantages
1. Multiple signal confirmations: Combined with price breakthroughs, volume confirmations and trend indicators, the risk of false breakthroughs is greatly reduced.
2. Strong adaptability: It can adapt to different market environments and trading cycles through parameter adjustment.
3. Perfect risk management: Provides a variety of stop loss options, and you can choose the most suitable stop loss method according to market characteristics.
4. Clear visualization: The strategy interface intuitively displays various indicators to facilitate traders to understand the market status.
5. Flexible backtesting: allows customizing the backtesting time range to facilitate strategy optimization.
#### Strategy Risk
1. Shock market risk: Frequent false breakthrough signals may occur in range-bound market fluctuations.
2. Slippage risk: In a market with poor liquidity, a breakthrough signal may cause the entry price to deviate due to slippage.
3. Risk of excessive filtering: Enabling volume filtering may miss some effective trading opportunities.
4. Parameter sensitivity: The strategy effect is more sensitive to parameter settings and requires careful optimization.
#### Strategy optimization direction
1. Add trend strength filtering: You can add trend strength indicators such as ADX to enter the market only when the trend is strong.
2. Optimize the volume indicator: You can consider using relative volume or volume breakthrough indicators instead of the simple moving average.
3. Add time filtering: Add trading time window settings to avoid periods of greater market volatility.
4. Dynamic parameter optimization: Automatically adjust channel cycle and super trend parameters according to market volatility.
5. Introduce machine learning: Use machine learning algorithms to optimize parameter selection and signal filtering.
#### Summary
This strategy builds a relatively complete trend following trading system by comprehensively using multiple technical indicators. The advantages of the strategy are high signal reliability and flexible risk management, but traders still need to optimize parameters according to specific market characteristics. Through continuous improvement and optimization, this strategy is expected to achieve stable trading results in trending markets. ||
#### Overview
This strategy is a trend-following trading system based on Donchian Channel breakouts, incorporating SuperTrend indicator and volume filter to enhance signal reliability. The strategy primarily identifies potential long trading opportunities by capturing price breakouts above historical highs, while using volume confirmation and trend-following indicators to filter false breakout signals. The strategy design is flexible and can be optimized for different market environments and trading instruments.

#### Strategy Principles
The core logic of the strategy is based on the following key components:
1. Donchian Channel: Calculates the highest and lowest prices within a user-defined period, forming upper, lower, and middle bands. Long entry signals are triggered when price breaks above the upper band.
2. Volume Filter: Compares current volume with its 20-period moving average to ensure entries only occur during volume expansion, improving breakout reliability.
3. SuperTrend Indicator: Serves as a trend confirmation tool, displaying green during bullish trends and red during bearish trends.
4. Flexible Stop-Loss Mechanism: Offers four different stop-loss options, including lower band stop, middle band stop, SuperTrend stop, and percentage trailing stop.

#### Strategy Advantages
1. Multiple Signal Confirmation: Combines price breakouts, volume confirmation, and trend indicators to significantly reduce false breakout risks.
2. High Adaptability: Can be adapted to different market environments and trading timeframes through parameter adjustment.
3. Comprehensive Risk Management: Provides multiple stop-loss options to choose the most suitable method based on market characteristics.
4. Clear Visualization: Strategy interface intuitively displays various indicators, making it easy for traders to understand market conditions.
5. Flexible Backtesting: Allows customization of backtesting date ranges for strategy optimization.

#### Strategy Risks
1. Choppy Market Risk: May generate frequent false breakout signals in range-bound markets.
2. Slippage Risk: In less liquid markets, breakout signals may result in entry prices deviating due to slippage.
3. Over-Filtering Risk: Enabling volume filter might miss some valid trading opportunities.
4. Parameter Sensitivity: Strategy performance is sensitive to parameter settings, requiring careful optimization.

#### Strategy Optimization Directions
1. Add Trend Strength Filter: Can incorporate trend strength indicators like ADX to enter only during strong trends.
2. Optimize Volume Indicator: Consider using relative volume or volume breakout indicators instead of simple moving averages.
3. Add Time Filter: Implement trading time window settings to avoid highly volatile market periods.
4. Dynamic Parameter Optimization: Automatically adjust channel period and SuperTrend parameters based on market volatility.
5. Introduce Machine Learning: Use machine learning algorithms to optimize parameter selection and signal filtering.

#### Summary
This strategy builds a relatively comprehensive trend-following trading system by integrating multiple technical indicators. Its strengths lie in high signal reliability and flexible risk management, though traders still need to optimize parameters according to specific market characteristics. Through continuous improvement and optimization, this strategy has the potential to achieve stable trading results in trending markets.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-10-01 00:00:00
end: 2025-02-19 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Binance","currency":"ETH_USDT"}]
*/

// Breakout trading system based on Donchain channel strategy that works best on a weekly chart and daily charts. Weekly is preferred. 

//@version=5

strategy('Donchian BO with Volume Filter and Supertrend', shorttitle='DBO+Vol+ST', default_qty_type=strategy.percent_of_equity, default_qty_value=2, overlay=true)

// Input options to configure backtest date range
startDate = input.int(title='Start Date', defval=1, minval=1, maxval=31)
startMonth = input.int(title='Start Month', defval=1, minval=1, maxval=12)
startYear = input.int(title='Start Year', defval=2016, minval=1800, maxval=2100)
avgVol = input.int(title="Avg Volume length", defval=20)
srcInput = input.source(close, "Source")

// Volume filter toggle
useVolumeFilter = input.bool(true, title='Enable Volume Filter')

endDate = input.int(title='End Date', defval=1, minval=1, maxval=31)
endMonth = input.int(title='End Month', defval=7, minval=1, maxval=12)
endYear = input.int(title='End Year', defval=2030, minval=1800, maxval=2100)

multiplier = input.int(title='SuperTrend Mult', defval=2, minval=1, maxval=12)
stlen = input.int(title='SuperTrend Length', defval=10, minval=1, maxval=12)

length = input.int(21, minval=1)
exit = input.int(3, minval=1, maxval=4, title='Exit Option')  // Use Option 1 to exit using lower band; Use Option 2 to exit using basis line

lower = ta.lowest(length)
upper = ta.highest(length)
basis = math.avg(upper, lower)

// Plotting the Donchian channel
l = plot(lower, color=color.new(color.blue, 0))
u = plot(upper, color=color.new(color.blue, 0))
plot(basis, color=color.new(color.orange, 0))
fill(u, l, color=color.new(color.blue, 90))

// Check if the current bar is in the date range
inDateRange = time >= timestamp(syminfo.timezone, startYear, startMonth, startDate, 0, 0) and time < timestamp(syminfo.timezone, endYear, endMonth, endDate, 0, 0)

// Long trailing stop-loss percentage
longTrailPerc = input.float(title='Trail Long Loss (%)', minval=0.0, step=0.1, defval=3) * 0.01
longStopPrice = 0.0

longStopPrice := if strategy.position_size > 0
    stopValue = close * (1 - longTrailPerc)
    math.max(stopValue, longStopPrice[1])
else
    0

// Volume filter: 20-period moving average
volumeMA = ta.sma(volume, avgVol)

// Long entry condition: Donchian breakout + volume filter
longCondition = ta.crossover(srcInput, upper[1]) and (not useVolumeFilter or volume > volumeMA)
longsma = ta.sma(close, 200)

if inDateRange and longCondition
    strategy.entry('Long', strategy.long)

// Exit conditions
if inDateRange and exit == 1
    if ta.crossunder(close, lower[1])
        strategy.close('Long')

if inDateRange and exit == 2
    if ta.crossunder(close, basis[1])
        strategy.close('Long')

[superTrend, dir] = ta.supertrend(multiplier, stlen)
if inDateRange and exit == 3
    if ta.crossunder(close, superTrend)
        strategy.close('Long')

if inDateRange and exit == 4
    if strategy.position_size > 0
        strategy.exit(id='XL TRL STP', stop=longStopPrice)

// Short conditions (commented out for now)
shortCondition = ta.crossunder(close, lower[1])

// Exit all positions when date range ends
if not inDateRange
    strategy.close_all()

// --- Add Supertrend Indicator ---
stColor = dir == 1 ? color.red : color.green
plot(superTrend, color=stColor, title="SuperTrend", linewidth=2)

```

> Detail

https://www.fmz.com/strategy/483076

> Last Modified

2025-02-21 11:47:17
