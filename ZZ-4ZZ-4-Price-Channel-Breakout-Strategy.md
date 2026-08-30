
> Name

ZZ-4 Price Channel Breakout StrategyZZ-4-Price-Channel-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
This strategy trades based on the price channel of the ZZ indicator, and uses the signal that the price breaks through the upper limit of the channel upwards or falls below the lower limit of the channel to establish a long or short position. This strategy attempts to capture trend bursts outside of the price channel range.
### Strategy Principles
1. Calculate the upper and lower limits of the price channel
2. Go long when the price rises above the upper limit
3. Go short when the price falls and breaks through the lower limit
4. Set the start and end transaction time
5. Clear positions before the market closes every day
Specifically, the strategy calculates the upper and lower limits of the price channel through the ZZ indicator. When the price breaks through the upper limit from below, enter the market long; when it breaks through the lower limit from above, enter the market short. Stop-loss orders are used after long and short positions, and the upper and lower limits of the price channel are used as stop-loss levels. At the same time, set a date and time range, trade within this range, and clear positions before the market closes every day to avoid overnight risks.
### Advantage Analysis
1. Use price channels to determine potential trend breakthrough points, and have certain trend identification capabilities
2. Trading signals are simple, intuitive and easy to judge.
3. Channel cycle parameters can be customized to adapt to different varieties and cycles
4. Setting date range and daily clearance helps risk control
5. Use stop-loss orders to limit single losses
### Risk Analysis
1. Fluctuations within the price channel range may result in multiple stop losses
2. Parameters need to be adjusted in a timely manner, otherwise the channel range may be inaccurate
3. The breakthrough may be a false breakthrough, and there is a risk of being trapped.
4. Potential profits are limited by the price channel range
5. Failure to fully utilize the profit margins of trending markets
The above risks can be reduced by relaxing the channel range, optimizing the stop loss strategy, and judging the strength of the trend.
### Optimization direction
1. Test different parameters to find the best combination
2. Broaden the price channel range to capture larger market trends
3. Introduce trend judgment indicators to avoid false breakthroughs
4. Optimize the stop loss strategy to prevent being trapped
5. Increase the proportion of positions to maximize profits from breakthroughs
6. Evaluate returns on different date ranges
### Summarize
This strategy is based on the price channel to determine the trend breaking point for trading. The advantage is that the trading signal is simple, the stop loss is clear, and it is easy to operate; the disadvantage is that there are frequent gaps and underutilization of trends. Through parameter optimization, strategy combination and other methods, the above shortcomings can be overcome while maintaining the advantages. This strategy can help traders master the application skills of price channels.
|| 

### Overview

This strategy trades based on the price channel of the ZZ indicator, taking long/short positions when price breaks out above/below the channel bands. It aims to capture trend outbreak moves outside the channel range.

### Strategy Logic

1. Calculate price channel upper/lower bands
2. Go long when price breaks out above upper band 
3. Go short when price breaks down below lower band
4. Set trading time range
5. Clear positions before daily close 

Specifically, it uses the ZZ indicator to calculate the price channel bands. When price breaks out upward from the lower band, go long. When price breaks down from the upper band, go short. Stop loss orders are used with the channel bands as stop loss levels. Trading hours are also defined to avoid overnight risks.

### Advantage Analysis

1. Price channel identifies potential trend breakouts
2. Simple and clear trading signals  
3. Customizable channel period fits different products and cycles
4. Trading hours and daily exit manage risks
5. Stop loss limits single trade loss

### Risk Analysis

1. Whipsaws inside channel may repeatedly hit stop loss
2. Requires timely parameter tuning, otherwise channel range may be inaccurate
3. Breakouts can be false, risks of being trapped
4. Profit potential is limited by channel range
5. Fails to fully capitalize on trend moves

Risks can be reduced by widening channel range, optimizing stop loss, gauging trend strength etc.

### Optimization Directions 

1. Test different parameter combinations for best setup
2. Widen price channel to capture larger moves
3. Add trend indicator to avoid false breakouts
4. Optimize stop loss to prevent being trapped
5. Increase position size to maximize breakout profits 
6. Evaluate profitability across different date ranges

### Summary

This strategy trades price channel breakouts to identify trend outbreaks. Pros are simple clear signals and easy operation; Cons are whipsaws and failure to ride trends. Parameter optimization and strategy combination can overcome the cons while retaining pros. It helps traders master applying price channel techniques.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|100|Capital, %|
|v_input_4|7|Length|
|v_input_5|true|Show Levels|
|v_input_6|false|Show Background|
|v_input_7|false|Show Price Channel|
|v_input_8|1900|From Year|
|v_input_9|2100|To Year|
|v_input_10|true|From Month|
|v_input_11|12|To Month|
|v_input_12|true|From day|
|v_input_13|31|To day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-14 00:00:00
end: 2023-09-20 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro
//2019

//@version=4
strategy(title = "Noro's ZZ-4 Strategy", shorttitle = "Noro's ZZ-4 Strategy", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 0)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(true, defval = true, title = "Short")
capital = input(100, defval = 100, minval = 1, maxval = 10000, title = "Capital, %")
len = input(7, minval = 1, title = "Length")
showll = input(true, defval = true, title = "Show Levels")
showbg = input(false, defval = false, title = "Show Background")
showpc = input(false, defval = false, title = "Show Price Channel")
fromyear = input(1900, defval = 1900, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To day")

//Price channel
h = highest(ohlc4, len)
l = lowest(ohlc4, len)
pccol = showpc ? color.blue : na
plot(h, color = pccol, transp = 0)
plot(l, color = pccol, transp = 0)

//Levels
ml = 0
ml := l > l[1] ? 1 : l < l[1] ? -1 : ml[1]
ll = 0.0
ll := ml == 1 and ml[1] == -1 ? l[1] : ll[1]
mh = 0
mh := h > h[1] ? 1 : h < h[1] ? -1 : mh[1]
hl = 0.0
hl := mh == -1 and mh[1] == 1 ? h[1] : hl[1]

//Lines
colorh = showll and hl == hl[1] ? color.lime : na
colorl = showll and ll == ll[1] ? color.red : na
plot(hl, color = colorh, linewidth = 2, transp = 0, title = "Long")
plot(ll, color = colorl, linewidth = 2, transp = 0, title = "Short")

//Background
size = strategy.position_size
trend = 0
trend := size > 0 ? 1 : size < 0 ? -1 : high >= hl ? 1 : low <= ll ? -1 : trend[1]
bgcol = showbg == false ? na : trend == 1 ? color.lime : trend == -1 ? color.red : na
bgcolor(bgcol, transp = 80)

//Trading
truetime = time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)
lot = 0.0
lot := size != size[1] ? strategy.equity / close * capital / 100 : lot[1]
if ll > 0 and hl > 0
    strategy.entry("Long", strategy.long, needlong == false ? 0 : lot, stop = hl, when=(truetime))
    strategy.entry("Short", strategy.short, needshort == false ? 0 : lot, stop = ll, when=(truetime))
if time > timestamp(toyear, tomonth, today, 23, 59)
    strategy.close_all()
    strategy.cancel("Long")
    strategy.cancel("Short")
```

> Detail

https://www.fmz.com/strategy/427450

> Last Modified

2023-09-21 10:59:55
