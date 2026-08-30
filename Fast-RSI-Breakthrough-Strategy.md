
> Name

Powell Index Fast-RSI-Breakthrough-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/b50f1ccc86b7d3ba7e.png)

[trans]

## Overview
This strategy is based on the RSI indicator and the EMA of the candle body to achieve rapid breakout operations. It utilizes RSI's fast patterns and large candle bodies to identify reversal signals.
## Strategy Principle
1. Calculate the RSI indicator, period 7, and use RMA to achieve acceleration patterns.
2. Calculate the EMA of the candle's real body size, period 30, as the real body size benchmark.
3. If RSI crosses the limit line (default 30), and the current K-line real body is greater than 1/4 of the average real body size, go long.
4. If the RSI falls below the limit line (default 70), and the current K-line entity is greater than 1/4 of the average entity size, go short.
5. If you have already held a position, close the position when RSI returns to the limit line again.
6. You can set RSI length, limit, reference price and other parameters.
7. You can set parameters such as entity size, EMA period, position opening chroot multiple, etc.
8. You can set the number of RSI golden crosses/dead crosses.
## Advantage Analysis
1. Utilize the reversal attribute of RSI indicator to capture reversal signals in time.
2. RMA realizes the acceleration form of RSI, making reversals more sensitive.
3. Combined with large K-line entity filtering to avoid arbitrage caused by small-scale shocks.
4. The backtest data is sufficient and the reliability is high.
5. Customizable parameters to adapt to different market environments.
6. The transaction logic is clear and simple.
## Risk Analysis
1. The RSI indicator has backtest deviation, and the actual effect needs to be verified.
2. Large K-line entities cannot completely filter out and fully shock the market.
3. The default parameters may not be suitable for all varieties and need to be optimized.
4. The winning rate may not be high, and you need to bear the psychological pressure of continuous stop losses.
5. The risk of failure to break through requires timely stop loss.
## Optimization direction
1. Optimize RSI parameters to adapt to different cycles and varieties.
2. Optimize the K-line entity EMA period and smooth the entity size.
3. Optimize the physical multiple of opening a position and control the frequency of entry.
4. Add moving stop loss to ensure winning rate.
5. Add trend filtering to avoid counter-trend trading.
6. Optimize fund management strategies and control single transaction risks.
## Summarize
This strategy is overall a very simple and straightforward reversal strategy. It simultaneously uses the reversal properties of the RSI indicator and the destructive power of large K-line entities to quickly enter the market when the market breaks through. Although the backtest effect is good, the actual effect has yet to be verified. When using it, you need to pay attention to optimizing parameters and controlling risks. Overall, this strategy has very high value and is one of the very good strategies that can be applied and continuously optimized in real trading.
|| 

## Overview

This strategy implements fast breakthrough operations based on RSI indicator and EMA of candlestick bodies. It identifies reversal signals using the fast formation of RSI and large candlestick bodies.  

## Strategy Logic

1. Calculate RSI indicator with period 7 and use RMA for acceleration.

2. Calculate EMA of candlestick body size with period 30 as benchmark for body size.

3. If RSI crosses above the limit line (default 30) and current candle body is larger than 1/4 of average body size, go long.

4. If RSI crosses below the limit line (default 70) and current candle body is larger than 1/4 of average body size, go short.

5. If already in position, close when RSI crosses back the limit line.

6. Parameters like RSI length, limit, reference price can be configured. 

7. Parameters like body EMA period, open position chroot multiplier can be configured.

8. The number of RSI crossings can be configured.

## Advantage Analysis  

1. Utilize the reversal attribute of RSI to capture reversals timely.

2. RMA accelerates RSI formation for more sensitive reversals. 

3. Filter small range consolidations with large candlestick bodies.

4. Sufficient backtest data ensures reliability.  

5. Customizable parameters adapt to different market environments.

6. Simple and clear logic.

## Risk Analysis

1. RSI has backtest bias, actual performance to be validated.

2. Large bodies cannot fully filter choppy markets.

3. Default parameters may not suit all products, optimization needed.

4. Win rate may not be high, need to endure consecutive losses mentally.

5. Risk of failed breakthrough, need timely stop loss.

## Optimization Directions

1. Optimize RSI parameters for different periods and products.

2. Optimize body EMA period to smooth body size.

3. Optimize body multiplier for open positions to control entry frequency. 

4. Add moving stop loss to ensure win rate.

5. Add trend filter to avoid counter trend trading.

6. Optimize money management for risk control.

## Conclusion

In summary, this is a very simple and direct reversal strategy. It utilizes both the reversal attribute of RSI and the momentum of large candlestick bodies to get in fast during market reversals. Although backtest results look good, actual performance is yet to be validated. Parameter optimization and risk control are needed when applying it. Overall it is a strategy with great value and is worth applying and constantly improving in live trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|7|RSI Period|
|v_input_4|30|RSI limit|
|v_input_5_close|0|RSI Price: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_6|true|RSI Bars|
|v_input_7|2018|From Year|
|v_input_8|2100|To Year|
|v_input_9|true|From Month|
|v_input_10|12|To Month|
|v_input_11|true|From day|
|v_input_12|31|To day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-23 00:00:00
end: 2023-10-23 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy(title = "Noro's Fast RSI Strategy v1.2", shorttitle = "Fast RSI str 1.2", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 5)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(true, defval = true, title = "Short")
rsiperiod = input(7, defval = 7, minval = 2, maxval = 50, title = "RSI Period")
limit = input(30, defval = 30, minval = 1, maxval = 100, title = "RSI limit")
rsisrc = input(close, defval = close, title = "RSI Price")
rb = input(1, defval = 1, minval = 1, maxval = 5, title = "RSI Bars")
fromyear = input(2018, defval = 2018, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To day")

//Fast RSI
fastup = rma(max(change(rsisrc), 0), rsiperiod)
fastdown = rma(-min(change(rsisrc), 0), rsiperiod)
fastrsi = fastdown == 0 ? 100 : fastup == 0 ? 0 : 100 - (100 / (1 + fastup / fastdown))
uplimit = 100 - limit
dnlimit = limit

//RSI Bars
ur = fastrsi > uplimit
dr = fastrsi < dnlimit
uprsi = rb == 1 and ur ? 1 : rb == 2 and ur and ur[1] ? 1 : rb == 3 and ur and ur[1] and ur[2] ? 1 : rb == 4 and ur and ur[1] and ur[2] and ur[3] ? 1 : rb == 5 and ur and ur[1] and ur[2] and ur[3] and ur[4] ? 1 : 0
dnrsi = rb == 1 and dr ? 1 : rb == 2 and dr and dr[1] ? 1 : rb == 3 and dr and dr[1] and dr[2] ? 1 : rb == 4 and dr and dr[1] and dr[2] and dr[3] ? 1 : rb == 5 and dr and dr[1] and dr[2] and dr[3] and dr[4] ? 1 : 0

//Body
body = abs(close - open)
emabody = ema(body, 30)

//Signals
bar = close > open ? 1 : close < open ? -1 : 0
up = bar == -1 and (strategy.position_size == 0 or close < strategy.position_avg_price) and dnrsi and body > emabody / 4
dn = bar == 1 and (strategy.position_size == 0 or close > strategy.position_avg_price) and uprsi and body > emabody / 4
exit = ((strategy.position_size > 0 and fastrsi > dnlimit and bar == 1) or (strategy.position_size < 0 and fastrsi < uplimit and bar == -1)) and body > emabody / 2

//Trading
if up
    strategy.entry("Long", strategy.long, needlong == false ? 0 : na, when=(time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 00, 00)))

if dn
    strategy.entry("Short", strategy.short, needshort == false ? 0 : na, when=(time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 00, 00)))
    
if time > timestamp(toyear, tomonth, today, 00, 00) or exit
    strategy.close_all()
```

> Detail

https://www.fmz.com/strategy/430017

> Last Modified

2023-10-24 11:51:56
