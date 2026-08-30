
> Name

Gap-Trading-Moving-Average-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/a65dfb914c8088f7422ee17ba2bbaec982d31082d574610bab40b09149bfa56b.png)

[trans]

This article provides a detailed analysis of the tracking moving average gap strategy written by Noro. This strategy calculates the deviation of the closing price from the simple moving average to determine the timing of a turning point in the market trend and achieves buying low and selling high.
#### Strategy Principle
The strategy first calculates the 3-day simple moving average SMA. Then calculate the ratio of the closing price close to sma, and then subtract 1 to get an indicator ind. When ind goes above the preset parameter limit, it indicates that the closing price has significantly exceeded sma, so consider going long; when ind goes below -limit, it indicates that the closing price has been significantly lower than sma, so consider going short.
The strategy also plots the 0 axis, the limit axis and the -limit axis. When the ind indicator is in different areas, it is colored with different colors to assist judgment. When the ind indicator crosses limit or -limit, it indicates a long or short signal.
When a long or short signal is generated, the strategy will first close the position in the opposite direction, and then open a long or short position. When the ind indicator returns to the 0 axis, all positions will be closed.
#### Strategic Advantages
1. Using the gap principle, when the price clearly deviates from the moving average, a counter-trend operation is adopted. This is different from trend following. The gap strategy seeks to capture the turning point.
2. Draw the indicator axis and visually judge the position and crossing of the indicator.
3. Optimized the position closing logic. Only open a new position in reverse direction after closing the current position to avoid unnecessary reverse positions.
4. Set a trading time range to avoid unnecessary overnight positions.
5. Allows you to set the trading switch for both long and short sides, you can only do long or only short.
#### Strategy Risk
1. The tracking moving average strategy is prone to multiple losing transactions and is suitable for patient positions.
2. As a judgment indicator, the moving average lacks flexibility and cannot reflect price changes in a timely manner.
3. The preset parameter limit is relatively static and needs to be adjusted under different varieties and market environments.
4. Tracking moving averages cannot identify intra-trend fluctuations and should be used in conjunction with fluctuation indicators, etc.
5. Position holding rules need to be optimized, such as setting stop loss and take profit; or only catching gaps in the early stages of the trend.
#### Strategy optimization direction
1. You can test different parameter settings, such as SMA period; or use adaptive moving averages such as exponential moving average.
2. You can add moving average direction, angle and other determinations to avoid unnecessary trading during the platform period.
3. You can consider combining it with volatility indicators, such as Bollinger Bands, to suspend trading when volatility increases.
4. Position management rules can be set, such as opening a fixed quantity position, increasing positions incrementally, fund management, etc.
5. You can set a stop-loss and take-profit line, or suspend new orders at a fixed proportion of stop-loss to control single risk.
#### Summarize
This article provides a detailed analysis of the tracking moving average gap strategy written by Noro. This strategy takes advantage of the characteristics of the price gap moving average, and designs the indicator axis and color drawing to determine the timing of entry. At the same time, the position closing sequence logic is optimized and the trading time range is set. However, this strategy has the inherent shortcoming of tracking the moving average, and it is necessary to further optimize parameter settings, stop loss rules, and combination with other indicators to improve stability.
||


This article provides an in-depth analysis of the moving average gap trading strategy coded by Noro. The strategy identifies trend reversals by calculating the deviation between closing price and simple moving average, and achieves buy low and sell high.

#### Strategy Logic

The strategy first calculates the 3-day simple moving average (SMA). Then it computes the ratio of closing price (close) to SMA minus one as an indicator (ind). When ind crosses above the preset parameter limit, it means the closing price has surpassed SMA significantly and long position is considered. When ind crosses below -limit, it means the closing price has fallen far below SMA and short position is considered.

The strategy also plots the 0 axis, limit axis and -limit axis. The ind indicator is colored differently in separate areas to assist judgement. When ind crosses over limit or -limit, it signals long or short entry.

Upon long/short signal, the strategy will close opposite position first, then open long/short position. When ind returns between 0 axes, all positions will be closed.

#### Advantages

1. Adopting gap trading principle to catch trend reversals, unlike trend following strategies.

2. Plotting indicator axes for intuitive judgment of indicator position and crossover. 

3. Optimized close logic, closing existing position before reversing direction. Avoid unnecessary opposite positions.

4. Defined trading time range to avoid unnecessary overnight positions.

5. Flexibility to enable/disable long/short trading.

#### Risks

1. Moving average strategies tend to generate multiple losing trades, requiring patience in holding.

2. Moving averages lack flexibility in capturing real-time price changes. 

3. Preset limit parameter is static, requiring adjustments for different products and market environments.

4. Unable to identify fluctuations within trends, requiring combining with volatility indicators.

5. Need to optimize holding rules e.g. stop loss, take profit; or only catch initial gaps.

#### Enhancement Directions

1. Test different parameter settings e.g. SMA period, or adaptive moving averages like EMA.

2. Add moving average direction and slope validation to avoid meaningless trades.

3. Consider combining with volatility indicators like Bollinger Bands to pause trading when volatility rises.

4. Implement position sizing rules e.g. fixed quantity, incremental pyramiding, money management. 

5. Set stop loss/take profit lines, or pause new orders when fixed percentage stop loss triggered, to control per trade risk.

#### Summary

This article comprehensively analyzed Noro's moving average gap trading strategy. It utilizes the price gap from moving average feature and implements indicator axes and colors for entry timing. It also optimizes the close logic and defines trading time range. However, inherent weaknesses of moving average tracking remains, requiring further optimizations in parameters, stop loss rules, combining indicators etc. to improve robustness.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|100|Lot, %|
|v_input_4|10|limit|
|v_input_5|1900|From Year|
|v_input_6|2100|To Year|
|v_input_7|true|From Month|
|v_input_8|12|To Month|
|v_input_9|true|From Day|
|v_input_10|31|To Day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-19 00:00:00
end: 2023-10-25 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro
//2018

//@version=3
strategy(title = "Noro's Shift Close Strategy v1.0", shorttitle = "Shift Close 1.0", default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 5)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(true, defval = true, title = "Short")
capital = input(100, defval = 100, minval = 1, maxval = 10000, title = "Lot, %")
limit = input(10)
fromyear = input(1900, defval = 1900, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From Day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To Day")

//Shift MA
sma = sma(ohlc4, 3)
ind = ((close / sma) - 1) * 100

//Oscilator
plot(3 * limit, color = na, transp = 0)
plot(limit, color = black, transp = 0)
plot(0, color = black, transp = 0)
plot(-1 * limit, color = black, transp = 0)
plot(-3 * limit, color = na, transp = 0)
plot(ind, linewidth = 3, transp = 0)
col = ind > limit ? red : ind < -1 * limit ? lime : na
bgcolor(col, transp = 0)

//Signals
size = strategy.position_size
up = ind < -1 * limit
dn = ind > limit
exit = ind > -1 * limit and ind < limit

//Trading
lot = 0.0 
lot := size == 0 ? strategy.equity / close * capital / 100 : lot[1]

if up
    if strategy.position_size < 0
        strategy.close_all()
        
    strategy.entry("Long", strategy.long, needlong == false ? 0 : lot, when=(time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))

if dn
    if strategy.position_size > 0
        strategy.close_all()
        
    strategy.entry("Short", strategy.short, needshort == false ? 0 : lot, when=(time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))
    
if exit
    strategy.close_all()
```

> Detail

https://www.fmz.com/strategy/430259

> Last Modified

2023-10-26 16:05:01
