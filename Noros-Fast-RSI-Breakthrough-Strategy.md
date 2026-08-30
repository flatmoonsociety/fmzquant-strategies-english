
> Name

Noros-Fast-RSI-Breakthrough-Strategy

> Author

ChaoZhang

> Strategy Description

[trans]
Noro’s Rapid RSI Breakout Strategy Explained
This article will analyze the principle of Noro's rapid RSI breakout strategy in detail, explain its trading signal formation mechanism, and analyze the advantages and potential risks of this strategy.
1. Strategy Overview
This strategy uses the RSI indicator as the main trading signal, combined with K-line entity filtering and minimum price/maximum price breakthrough auxiliary judgment to form a complete long and short decision-making system. The strategy name is "Noro Rapid RSI Breakout Strategy".
2. Detailed analysis of strategy
1. RSI Quick Line Setup
This strategy uses the RSI fast line with a length of 7 to capture signs of market trends through the rapid shocks of RSI. At the same time, the RSI upper limit is set to 70 and the lower limit is 30. When the RSI exceeds the upper and lower limits, a trading signal is generated.
2. K-line entity filtering
The strategy uses the K-line entity size SMA to filter RSI signals, and only considers RSI signals on bars whose entities are larger than the 5-day average entity size to avoid being hit by shock market adjustments.
3. Minimum price/maximum price breakthrough
The strategy determines whether there is a minimum price breakthrough or a maximum price breakthrough within the recent mmbars, and combines the RSI position to determine the bottom rebound and head sinking opportunities.
4. Summary of trading signals
Long signals: RSI breaks below the 30 limit, the real body is larger than the average real body size, and the minimum price breaks through the bottom support.
Short signal: RSI crosses the 70 limit, the real body is larger than the average real body size, and the maximum price breaks through the head pressure.
Position closing signal: When the position direction is opposite to the direction of the K-line entity, the position will be closed when RSI breaks through the limit again.
3. Strategic advantages
1. RSI indicator parameters are optimized to quickly capture trend transitions.
2. Combine K-line and minimum price and maximum price breakthrough to avoid unnecessary switching in the volatile market.
3. There is a stop loss mechanism, stop loss and exit when RSI breaks through the limit again.
4. Strategic risks
1. RSI can easily produce illusory signals and needs to be combined with auxiliary judgment.
2. Backtest data fitting risks, too strict parameter optimization may only be suitable for specific market cycles.
3. The stop loss mechanism may be too mechanical and unable to control the risk of too large a single stop loss.
5. Summary
This strategy integrates multiple technical indicator signals to form a more robust trend tracking system. However, you still need to pay attention to backtesting hyper-optimization and stop-loss risks, and carefully evaluate the actual effect of the strategy. When used for real trading, it is recommended to adjust the parameters appropriately and control the size of a single position.
||

This article will detail the logic behind Noro's Fast RSI Breakthrough Strategy, explain how trading signals are generated, and analyze the advantages and potential risks of this strategy. 

I. Strategy Overview

This strategy mainly uses the RSI indicator to generate trading signals, combined with candlestick filtering and min/max breakthroughs as auxiliary judgements, forming a complete long/short decision system. The strategy name is "Noro's Fast RSI Breakthrough Strategy".

II. Strategy Details 

1. Fast RSI Setting

The strategy uses a length 7 fast RSI to capture signs of market trends through fast RSI oscillations. Upper and lower limits of 70 and 30 are also set for the RSI to trigger signals when breached.

2. Candlestick Filtering 

The strategy filters RSI signals using the candlestick body size sma, only considering RSI signals on candlesticks with body size larger than 5-day average body size, avoiding whipsaws.

3. Min/Max Breakthroughs

The strategy checks if min/max breakthroughs happened in recent mmbars, combined with RSI level to determine bottom reversals and top breakdowns.

4. Trading Signal Summary

Long signal: RSI crosses below 30, body size exceeds average body size, and min breaks supports. 

Short signal: RSI crosses above 70, body size exceeds average body size, and max breaks resistances.

Exit signal: When RSI recrosses limits in opposite direction of position.

III. Advantages of the Strategy

1. Optimized RSI parameters capture trend change quickly.

2. Combining with candlesticks and min/max prevents unnecessary whipsaws. 

3. Stop loss mechanism exits when RSI recrosses limits.

IV. Risks of the Strategy

1. RSI prone to false signals, needs auxiliary confirmation.

2. Backtest overfitting risks. Optimized parameters may only fit specific market periods.

3. Stop loss mechanism may be too mechanical, unable to control large loss on single stop loss.

V. Conclusion

This strategy integrates multiple technical indicators for robust trend following. But risks of backtest overfitting and stop loss should be noted, and live performance should be evaluated cautiously. Fine tune of parameters and control of position sizing recommended for live trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|true|Use Fast RSI Strategy|
|v_input_4|true|Use Min/Max Strategy|
|v_input_5|true|Use BarColor Strategy|
|v_input_6|false|Use SMA Filter|
|v_input_7|20|SMA Filter Period|
|v_input_8|7|Fast RSI Period|
|v_input_9|30|RSI limit|
|v_input_10_close|0|RSI Price: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_11|true|RSI Bars|
|v_input_12|true|Min/Max Bars|
|v_input_13|false|Show SMA Filter|
|v_input_14|false|Show Arrows|
|v_input_15|2018|From Year|
|v_input_16|2100|To Year|
|v_input_17|true|From Month|
|v_input_18|12|To Month|
|v_input_19|true|From day|
|v_input_20|31|To day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-11 00:00:00
end: 2023-01-11 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro
//2018

//@version=3
strategy(title = "Noro's Fast RSI Strategy v1.6", shorttitle = "Fast RSI str 1.6", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 10)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(true, defval = true, title = "Short")
usersi = input(true, defval = true, title = "Use Fast RSI Strategy")
usemm = input(true, defval = true, title = "Use Min/Max Strategy")
usebc = input(true, defval = true, title = "Use BarColor Strategy")
usesma = input(false, defval = false, title = "Use SMA Filter")
smaperiod = input(20, defval = 20, minval = 2, maxval = 1000, title = "SMA Filter Period")
fast = input(7, defval = 7, minval = 2, maxval = 50, title = "Fast RSI Period")
limit = input(30, defval = 30, minval = 1, maxval = 100, title = "RSI limit")
rsisrc = input(close, defval = close, title = "RSI Price")
rsibars = input(1, defval = 1, minval = 1, maxval = 20, title = "RSI Bars")
mmbars = input(1, defval = 1, minval = 1, maxval = 5, title = "Min/Max Bars")
showsma = input(false, defval = false, title = "Show SMA Filter")
showarr = input(false, defval = false, title = "Show Arrows")
fromyear = input(2018, defval = 2018, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To day")

//Fast RSI
fastup = rma(max(change(rsisrc), 0), fast)
fastdown = rma(-min(change(rsisrc), 0), fast)
fastrsi = fastdown == 0 ? 100 : fastup == 0 ? 0 : 100 - (100 / (1 + fastup / fastdown))

//Limits
bar = close > open ? 1 : close < open ? -1 : 0
uplimit = 100 - limit
dnlimit = limit

//RSI Bars
upsignal = fastrsi > uplimit ? 1 : 0
dnsignal = fastrsi < dnlimit ? 1 : 0
uprsi = sma(upsignal, rsibars) == 1
dnrsi = sma(dnsignal, rsibars) == 1

//Body
body = abs(close - open)
abody = sma(body, 10)

//MinMax Bars
min = min(close, open)
max = max(close, open)
minsignal = min < min[1] and bar == -1 and bar[1] == -1 ? 1 : 0
maxsignal = max > max[1] and bar == 1 and bar[1] == 1 ? 1 : 0
mins = sma(minsignal, mmbars) == 1
maxs = sma(maxsignal, mmbars) == 1

//SMA Filter
sma = sma(close, smaperiod)
colorsma = showsma ? blue : na
plot(sma, color = colorsma, linewidth = 3)

//Signals
up1 = bar == -1 and (strategy.position_size == 0 or close < strategy.position_avg_price) and dnrsi and body > abody / 5 and usersi
dn1 = bar == 1 and (strategy.position_size == 0 or close > strategy.position_avg_price) and uprsi and body > abody / 5 and usersi
up2 = mins and (close > sma or usesma == false) and fastrsi < 70 and usemm
dn2 = maxs and (close < sma or usesma == false) and fastrsi > 30 and usemm 
up3 = sma(bar, 2) == -1 and usebc
dn3 = sma(bar, 2) == 1 and usebc
exit = ((strategy.position_size > 0 and fastrsi > dnlimit and bar == 1) or (strategy.position_size < 0 and fastrsi < uplimit and bar == -1)) and body > abody / 2

//Arrows
col = exit ? black : up1 or dn1 ? blue : up2 or dn2 ? red : na
needup = up1 or up2
needdn = dn1 or dn2
needexitup = exit and strategy.position_size < 0
needexitdn = exit and strategy.position_size > 0
plotarrow(showarr and needup ? 1 : na, colorup = blue, colordown = blue, transp = 0)
plotarrow(showarr and needdn ? -1 : na, colorup = blue, colordown = blue, transp = 0)
plotarrow(showarr and needexitup ? 1 : na, colorup = black, colordown = black, transp = 0)
plotarrow(showarr and needexitdn ? -1 : na, colorup = black, colordown = black, transp = 0)

//Trading
if up1 or up2 or up3
    if strategy.position_size < 0
        strategy.close_all()
        
    strategy.entry("Long", strategy.long, needlong == false ? 0 : na, when=(time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))

if dn1 or dn2 or dn3
    if strategy.position_size > 0
        strategy.close_all()
        
    strategy.entry("Short", strategy.short, needshort == false ? 0 : na, when=(time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))
    
if time > timestamp(toyear, tomonth, today, 23, 59) or exit
    strategy.close_all()
```

> Detail

https://www.fmz.com/strategy/426461

> Last Modified

2023-09-12 11:40:44
