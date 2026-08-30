
> Name

Zigzag-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/d71e0122301b7eb791.png)

[trans]


## Overview
This strategy uses the ZigZag indicator to draw support and resistance lines, and takes corresponding long or short operations when the price breaks through the support or resistance lines.
## Strategy Principle
This strategy begins by using the ZigZag indicator to draw a Zigzag line under specific parameters. Then draw a green support line when the ZigZag indicator bottoms and a red resistance line when it tops. Go long when the price crosses above the green line and go short when it crosses below the red line.
Specifically, the core logic of this strategy is:
1. Use EMA to perform three exponential moving averages on the close price to obtain the smooth curve _hls.
2. Determine whether the smooth curve is rising. If it is rising and the previous K line does not rise, record it as the bottom and take the lowest value of this K line. If it falls and the previous K line rises, it is recorded as the top, and the highest value of this K line is taken. Otherwise NaN.
3. Repeat this process to get the ZigZag line zigzag.
4. When zigzag rises, it is recorded as the current top point dot; when it falls, it is recorded as the current bottom point dot.
5. When dot rises, draw the green support line uplevel; when dot falls, draw the red resistance line dnlevel.
6. Go long when the price crosses above the green line, and go short when it crosses below the red line.
## Advantage Analysis
This strategy has the following advantages:
1. Use the ZigZag indicator to identify key support and resistance levels, which are often of great significance.
2. ZigZag eliminates some of the noise in the market and makes trading signals clearer.
3. Use the breakthrough method to enter the market, which can capture the turning point of the trend in time.
4. The method of drawing support and resistance lines is simple and effective.
5. The strategy logic is clear and easy to understand, and there is plenty of room for parameter optimization.
6. Flexible selection of trading varieties and time periods, with strong adaptability.
## Risk Analysis
There are also some risks with this strategy:
1. Improper setting of ZigZag indicator parameters may result in missed trading opportunities.
2. A retest may occur after the support and resistance levels are broken, and a stop loss should be set to control the risk.
3. Breakthrough signals may be misleading and should be verified based on trends and patterns.
4. The market may fluctuate sideways for a long time, and the strategy will produce too many invalid transactions at this time.
5. It is necessary to consider the impact of transaction costs and avoid too frequent transactions.
Corresponding measures include:
1. Optimize ZigZag parameters and find the best parameter combination.
2. Set a stop loss promptly after a breakthrough to control single losses.
3. Combine with trend indicators and other filtering signals to improve accuracy.
4. Add conditions to identify consolidation markets and do not trade during this period.
5. Appropriately relax the breakthrough range and reduce invalid transactions.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize ZigZag parameters and find the best parameter combination. You can find the best parameters by iterating through backtests.
2. After breaking through the market, consider the possibility of testing the support and resistance levels again, and set the exit logic for retesting.
3. Combine with trend indicators such as MA to filter out low-probability trading signals.
4. Add volume and energy indicators to confirm breakthrough signals and avoid false signals.
5. Set up the "dual technique" mentioned by Lachenbruch (simultaneously long and short) to filter out false signals and profit.
6. Consider using algorithms such as machine learning to dynamically optimize parameters.
7. Introduce stop-loss strategies and set stop-loss points to control risks.
## Summarize
This strategy is generally a simple and practical shock breakthrough strategy. It utilizes the ZigZag indicator to draw support and resistance lines and take action when price breaks through these lines. The strategy has strong adaptability, but there are also certain risks. The strategy can be improved through parameter optimization, signal filtering, risk control and other means. This type of breakout strategy is suitable for active traders who have a pulse on the market.

|| 



## Overview

This strategy uses the Zigzag indicator to draw support and resistance lines and takes long or short positions when the price breaks through the support or resistance lines.

## Strategy Logic

The strategy first uses the Zigzag indicator to draw Zigzag lines under certain parameters. Green support lines are drawn when the Zigzag indicator bottoms out. Red resistance lines are drawn when the Zigzag tops out. Long positions are taken when the price breaks above the green line. Short positions are taken when the price breaks below the red line. 

Specifically, the core logic is:

1. Use ema to smooth the close price with triple exponential moving averages, obtaining the smoothed curve _hls.

2. Judge if the smoothed curve is rising. If rising and the previous bar was not rising, it is considered a bottom. Take the lowest price of this bar. If falling and the previous bar was rising, it is considered a top. Take the highest price of this bar. Otherwise NaN.

3. Repeat this process to obtain the Zigzag line zigzag. 

4. When zigzag rises, record the current peak dot. When falling, record the current trough dot.

5. Draw the green support line uplevel when dot rises. Draw the red resistance line dnlevel when dot falls.

6. Take long position when price breaks above green line. Take short position when price breaks below red line.

## Advantage Analysis

The advantages of this strategy include:

1. Identify key support/resistance levels using Zigzag indicator. These levels are often significant.

2. Zigzag filters out some market noise, generating clearer trading signals. 

3. Enter positions by breakout, which can timely capture trend reversals.

4. Simple and effective way to draw support/resistance lines. 

5. Clear logic and large parameter optimization space.

6. Flexibility in choosing products and timeframes. Strong adaptability.

## Risk Analysis

Risks of this strategy:

1. Improper Zigzag parameters may miss trading opportunities. 

2. Prices may retest support/resistance after breakout. Use stop loss to control risks.

3. Breakout signals may be misleading. Need validation with trends and patterns.

4. Prolonged sideways may generate excessive ineffective trades.

5. Consider transaction costs. Avoid overly frequent trading.

Solutions:

1. Optimize Zigzag parameters to find best combination.

2. Set timely stop loss after breakout to limit losses.

3. Add filters like trend indicators to improve accuracy. 

4. Identify sideways and avoid trading during these periods.

5. Relax breakout range to reduce ineffective trades.

## Optimization Directions

The strategy can be optimized in the following aspects:

1. Optimize Zigzag parameters by backtesting to find optimum. 

2. Consider the possibility of retesting support/resistance after breakout. Add exit logic for retest scenarios.

3. Add filters like MA to screen out low probability signals.

4. Incorporate volume indicators to confirm breakout signals.

5. Implement Lachenbruch's dual methodology (long and short) to filter incorrect signals and profit.

6. Use machine learning to dynamically optimize parameters. 

7. Introduce stop loss strategy to limit risks.

## Conclusion

In summary, this is a simple and practical oscillation breakout strategy. It draws support/resistance using Zigzag and trades breakouts. The strategy is adaptive but with some risks. Optimization on parameters, signal filters and risk control can improve it. Such breakout strategies suit active traders who can grasp market rhythm.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|100|Capital, %|
|v_input_4|4|ZigZag length|
|v_input_5|4|ZigZag extreme|
|v_input_6_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_7|false|Show ZigZag|
|v_input_8|1900|From Year|
|v_input_9|2100|To Year|
|v_input_10|true|From Month|
|v_input_11|12|To Month|
|v_input_12|true|From day|
|v_input_13|31|To day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-13 00:00:00
end: 2023-10-19 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro
//2018

//@version=3
// strategy(title = "Noro's ZZ-2 Strategy", shorttitle = "Noro's ZZ-2 Strategy", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 0)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(true, defval = true, title = "Short")
capital = input(100, defval = 100, minval = 1, maxval = 10000, title = "Capital, %")
length = input(4, title = "ZigZag length")
Extreme = input(4, title = "ZigZag extreme")
src = input(close, title = "Source")
showzz = input(false, defval = false, title = "Show ZigZag")
fromyear = input(1900, defval = 1900, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To day")

//ZigZag
f_zz(_length, _detection)=>
    _hls = ema(ema(ema(src, _length), round(_length*0.66)), round(_length*0.33))
    _isRising = _hls >= _hls[1]
    _zigzag = _isRising and not _isRising[1] ? lowest(_detection) :  not _isRising and _isRising[1] ? highest(_detection) : na
zigzag = f_zz(length, Extreme)
zzcol = showzz ? black : na
plot(zigzag, color = zzcol, linewidth = 2)

//Levels
dot = 0.0
dot := zigzag > 0 ? zigzag : dot[1]
uplevel = 0.0
uplevel := dot > dot[1] ? zigzag : uplevel[1]
dnlevel = 0.0
dnlevel := dot < dot[1] ? zigzag : dnlevel[1]
upcol = na
upcol := dot > dot[1] ? na : lime
plot(uplevel, color = upcol, linewidth = 2)
dncol = na
dncol := dot < dot[1] ? na : red
plot(dnlevel, color = dncol, linewidth = 2)

//Trading
lot = 0.0
lot := strategy.position_size != strategy.position_size[1] ? strategy.equity / close * capital / 100 : lot[1]
if dot > 0
    strategy.entry("Long", strategy.long, needlong == false ? 0 : lot, stop = uplevel)
    strategy.entry("Short", strategy.short, needshort == false ? 0 : lot, stop = dnlevel)

```

> Detail

https://www.fmz.com/strategy/429776

> Last Modified

2023-10-20 16:37:28
