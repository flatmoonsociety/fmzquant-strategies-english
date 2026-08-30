
> Name

Bollinger-Breakout-Strategy near the Bohr belt
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
This strategy is based on the design of the Bohr Band indicator. When the price breaks through the upper and lower rails of the Bohr Band, corresponding long or short operations will be taken. Strategies profit by capturing breakouts.
### Strategy Principles
1. Calculate the middle orbit, upper orbit and lower orbit of the Bohr band
2. Go long when it breaks through the lower rail; go short when it breaks through the upper rail.
3. Set the start and end time and limit the trading range
4. Set the position holding time and close the position on the same day by default
Specifically, the strategy first calculates the middle rail SMA with length length, and the upper and lower rails calculated with mult times the standard deviation. When the closing price breaks through the lower rail from bottom to top, enter the market long; when the closing price breaks through the upper rail from top to bottom, enter the market short. At the same time, set the start and end time to limit the trading range. Forced liquidation before opening every day.
This strategy attempts to capture the expansion after price breaks out of the upper and lower bands. When it breaks through the lower track, the strength of the bullish side increases, and when it breaks through the upper track, the strength of the short side increases. At this time, trading in the same direction is beneficial.
### Advantage Analysis
1. Simple and intuitive, easy to understand and implement
2. Use Bohr band indicators to judge market breakthroughs and have certain trend following capabilities
3. Parameters can be flexibly adjusted, suitable for different cycles and varieties
4. Daily position closing can control overnight risks
5. Long or short transactions can be opened individually
### Risk Analysis
1. Risk of false breakthrough. After the breakout, the price may retrace again.
2. Parameters need to be adjusted in a timely manner. Parameters need to be adjusted for different periods.
3. Risk of potential loss expansion. Expanding the breakthrough range may expand a single loss.
4. Risks of increased transaction costs. Frequent transactions may increase transaction costs.
The above risks can be reduced by optimizing entry conditions, adding stop loss strategies, and introducing trend filters.
### Optimization direction
1. Optimize parameters to adapt to different cycles
2. Add re-entry and re-opening conditions to track trends
3. Add stop-loss strategies to control risks
4. Set trading time periods to avoid important news events
5. Evaluate trend filters to filter out twists and turns
6. Test different holding times and compare results
### Summarize
This strategy is a breakthrough strategy based on the Bohr band, which makes profits by capturing the market as the breakthrough unfolds. The advantage is that the idea is simple and easy to implement; the disadvantage is that it is easily misled by tortuous market conditions. The strategy effect can be improved and risks controlled through parameter optimization, stop loss strategies, trading time control, etc. This strategy allows traders to understand the basic methods of indicator application and breakout trading.
|| 


### Overview

This strategy is based on Bollinger Bands indicator, taking long or short positions when price breaks out of Bollinger Bands upper or lower lines. It aims to profit from catching breakout moves.

### Strategy Logic

1. Calculate Bollinger midline, upper and lower lines
2. Go long on lower line breakout; go short on upper line breakout
3. Set start and end time to define trading hours 
4. Set holding time, default to intraday exit  

Specifically, it first calculates the midline SMA of length length, and upper/lower lines of mult times standard deviation. When close breaks out upward from the lower line, go long. When close breaks down from the upper line, go short. Also set start and end time to limit trading hours. Exit before daily open.

The strategy attempts to capture expanding moves after price breaks out of bands. Breaking lower band indicates strengthening bullish forces, while breaking upper band means strengthening bearish forces, so trading in line with breakout is favorable.

### Advantage Analysis

1. Simple and intuitive, easy to understand and implement
2. Utilize Bollinger Bands to judge trend breakouts, has some trend following capacity 
3. Flexible parameter adjustment for different cycles and products
4. Intraday exit controls overnight risk
5. Can enable only long or short trading

### Risk Analysis 

1. False breakout risk. Price may retrace after initial breakout.
2. Need timely parameter tuning. Parameters need adjustments for different cycles.
3. Potential loss enlargement risk. Larger breakout range may expand losses.
4. Increased transaction costs. Frequent trading may increase transaction costs.

Risks can be reduced by optimizing entry rules, adding stop loss, introducing trend filter etc.

### Optimization Directions

1. Optimize parameters for different cycles
2. Add re-entry and pyramiding rules to follow trends
3. Introduce stop loss to control risks
4. Set trading hours to avoid significant news events
5. Test trend filters to avoid choppy price action
6. Evaluate different holding periods and compare results

### Summary

This is a breakout strategy based on Bollinger Bands. It profits from breakout moves. Pros are simple logic and easy implementation; Cons are susceptibility to false breakouts. Risks can be managed through parameter optimization, stop loss, trading hours control etc. It allows traders to understand basics of using indicators and trading breakouts.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|20|length|
|v_input_4|true|mult|
|v_input_5|1900|From Year|
|v_input_6|2100|To Year|
|v_input_7|true|From Month|
|v_input_8|12|To Month|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-21 00:00:00
end: 2023-09-20 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro
//2018

//@version=2
strategy("Noro's Bollinger Strategy v1.0", shorttitle = "Bollinger str 1.0", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100.0, pyramiding = 5)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(true, defval = true, title = "Short")

length = input(20, minval=1)
mult = input(1.0, minval=0.001, maxval=50)

fromyear = input(1900, defval = 1900, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")

source = close
basis = sma(source, length)
dev = mult * stdev(source, length)

upper = basis + dev
lower = basis - dev

up = close < lower
dn = close > upper
exit = (strategy.position_size > 0 and close > open) or (strategy.position_size < 0 and close < open)

if up
    strategy.entry("Long", strategy.long, needlong == false ? 0 : na, when=(time > timestamp(fromyear, frommonth, 01, 00, 00) and time < timestamp(toyear, tomonth, 31, 00, 00)))

if dn
    strategy.entry("Short", strategy.short, needshort == false ? 0 : na, when=(time > timestamp(fromyear, frommonth, 01, 00, 00) and time < timestamp(toyear, tomonth, 31, 00, 00)))
    
if time > timestamp(toyear, tomonth, 31, 00, 00) or exit
    strategy.close_all()
```

> Detail

https://www.fmz.com/strategy/427440

> Last Modified

2023-09-21 10:38:13
