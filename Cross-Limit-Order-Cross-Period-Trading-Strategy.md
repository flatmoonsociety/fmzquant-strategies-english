
> Name

Cross-Limit-Order-Cross-Period-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/865a3b9a78772e5a04.png)

[trans]


### Overview
This strategy is a trend-following trading strategy that uses a simple moving average to determine the market trend direction, and places limit orders on the moving average in the direction of the trend to achieve trend-following trading.
### Strategy Principles
1. Calculate the simple moving average SMA, and calculate the trend direction.
2. If anti-aliasing filtering is enabled, lows above the SMA are used to determine an uptrend, and highs below the SMA are used to determine a downtrend. If anti-aliasing filtering is not enabled, a closing price above the SMA is used to determine an uptrend, and a closing price below the SMA is used to determine a downtrend.
3. According to the trend direction trend and the enabled trading direction parameters needlong and needshort, place a limit order on the SMA price. The specific logic is:
- If you need to go long (needlong is true) and it is in an upward trend, place a long limit order at the SMA price
- If you need to go short (needshort is true) and it is in a downtrend, place a short limit order at the SMA price
4. Set stop loss logic. If the position direction does not match the trend direction, stop loss and exit.
5. According to the date range parameter, only trade within the specified date range.
### Advantage Analysis
1. Using SMA to determine trends can effectively filter market noise and lock in longer-term trends.
2. Placing a limit order at the SMA price can obtain a better entry point at the beginning of the trend.
3. You can choose to only go long or only short, and flexibly adjust to your personal trading style.
4. A stop-loss exit mechanism can be set up to avoid losses from expanding.
5. Supports setting a trading time range to avoid violent fluctuations caused by major events.
### Risk Analysis
1. As a trend judgment indicator, SMA has a lag problem and may miss the turning point of the trend, resulting in losses.
2. Limit order entry is not flexible enough and may not be able to enter the market due to short-term trend adjustments.
3. It is necessary to set the SMA cycle parameters reasonably. If the settings are improper, wrong trend judgment will be obtained.
4. It is necessary to consider the rationality of the trading period parameters to avoid missing trading opportunities or risky periods.
### Optimization direction
1. You can consider adding other indicators to judge and conduct multi-indicator verification to avoid the SMA lag problem.
2. It can be set to limit order tracking mode. When the price breaks through SMA, it will be changed to market order tracking to improve tracking flexibility.
3. Dynamically optimize SMA cycle parameters to adapt to market environments of different cycles.
4. Set the stop loss position to the lowest/highest price within the trend instead of a strict SMA position to make the stop loss more flexible.
5. Add algorithmic trading elements to make the trading period more intelligent and flexible and avoid major risk periods.
### Summarize
This strategy is overall a relatively simple trend following strategy. The core idea is to use SMA to determine the trend direction and place a limit order at the SMA price for tracking transactions. The flexibility, adaptability and intelligence of the strategy can be improved through certain optimizations. This strategy is easy to understand and implement, and is suitable for introductory learning of algorithmic trading. However, in real trading, you need to pay attention to risks, carefully evaluate backtest results, and conduct strict monitoring and optimization.
||

### Summary

This strategy is a trend following trading strategy that uses simple moving average to determine market trend direction and place limit orders along the moving average line to follow the trend.

### Strategy Logic

1. Calculate the Simple Moving Average (SMA) and the trend direction trend.

2. If Anti-Saw filter is enabled, uptrend is identified when lows are above SMA, downtrend is identified when highs are below SMA. If Anti-Saw filter is disabled, uptrend is identified when close is above SMA, downtrend is identified when close is below SMA.

3. Place limit orders at SMA price according to the trend direction trend and enabled trading directions needlong and needshort:

   - If long trade is needed (needlong is true) and in uptrend, place long limit order at SMA price

   - If short trade is needed (needshort is true) and in downtrend, place short limit order at SMA price

4. Set stop loss logic to exit positions if position direction does not match trend direction.  

5. Only trade within specified date range based on date range parameters.

### Advantage Analysis

1. Using SMA to determine trend can effectively filter market noise and lock in longer term trend.

2. Placing limit orders at SMA price can get good entry points when trend starts. 

3. Flexibility to only go long or short according to personal trading style.

4. Stop loss in place to avoid enlarging losses.

5. Trading time range sets to avoid volatility around major events.

### Risk Analysis

1. SMA as trend indicator has lagging effect, may miss trend turning points and cause losses.

2. Limit orders lack flexibility, may not get into positions due to short term trend adjustments.

3. SMA period parameter needs proper configuration, improper settings lead to wrong trend determination.  

4. Trading session parameters need to be reasonable to avoid missing opportunities or trading in risky periods.

### Optimization Directions

1. Consider adding other indicators for multi-indicator confirmation, avoiding SMA lagging issues.

2. Switch to market order trailing when price breaks SMA, improving tracking flexibility.

3. Dynamically optimize SMA period to adapt to different market cycles. 

4. Set stop loss to swing low/high instead of strictly at SMA price for more flexible stops.

5. Increase algorithmic elements for smarter dynamic trading sessions avoiding major risk events.

### Summary

Overall this is a relatively simple trend following strategy, with the core idea of determining trend direction with SMA and placing limit orders at SMA price to follow the trend. With certain optimizations it can improve flexibility, adaptability and intelligence. The strategy is easy to understand and implement, suitable for algorithmic trading beginners, but requires risk awareness, cautious backtest evaluation, strict monitoring and optimization for live trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|long|
|v_input_2|true|short|
|v_input_3|100|Lot, %|
|v_input_4_close|0|MA Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_5|5|SMA length|
|v_input_6|false|SMA offset|
|v_input_7|true|Anti-saw filter|
|v_input_8|false|Reverse|
|v_input_9|true|Show MA|
|v_input_10|false|Show background|
|v_input_11|1900|From Year|
|v_input_12|2100|To Year|
|v_input_13|true|From Month|
|v_input_14|12|To Month|
|v_input_15|true|From day|
|v_input_16|31|To day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-27 00:00:00
end: 2023-03-12 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro
//2020

//@version=4
strategy(title = "Noro's CrossLimit", shorttitle = "CrossLimit", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100.0, pyramiding = 0, commission_value = 0.0)

needlong = input(true, "long")
needshort = input(true, "short")
lotsize = input(100, defval = 100, minval = 1, maxval = 10000, title = "Lot, %")
src = input(close, defval = close, title = "MA Source")
len = input(5, defval = 5, minval = 1, title = "SMA length")
off = input(0, defval = 0, minval = 0, title = "SMA offset")
anti = input(true, defval = true, title = "Anti-saw filter")
rev = input(false, defval = false, title = "Reverse")
showma = input(true, defval = true, title = "Show MA")
showbg = input(false, defval = false, title = "Show background")
fromyear = input(1900, defval = 1900, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To day")

//MA
ma = sma(src, len)[off]
macol = showma ? color.blue : na
plot(ma, color = macol, linewidth = 3, transp = 0)

//Background
trend = 0
trend := anti == false and close > ma ? 1 : anti == false and close < ma ? -1 : low > ma ? 1 : high < ma ? -1 : trend[1]
bgcol = showbg ? trend == 1 ? color.lime : trend == -1 ? color.red : na : na
bgcolor(bgcol, transp = 70)

//Signals
bar = close > open ? 1 : close < open ? -1 : 0
up = (trend == 1 and rev == false) or (trend == -1 and rev == true)
dn = (trend == -1 and rev == false) or (trend == 1 and rev == true)

//Trading
size = strategy.position_size
truetime = time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)
lot = 0.0
lot := size != size[1] ? strategy.equity / close * lotsize / 100 : lot[1]
if trend != 0
    strategy.entry("Long", strategy.long, lot, limit = ma, when = needlong and truetime and up)
    strategy.entry("Short", strategy.short, lot, limit = ma, when = needshort and truetime and dn)
if size > 0 and needshort == false and trend == -1
    strategy.exit("Stop Long", "Long", limit = ma)
if size < 0 and needlong == false and trend == 1
    strategy.exit("Stop Short", "Short", limit = ma)
if time > timestamp(toyear, tomonth, today, 23, 59)
    strategy.close_all()
    strategy.cancel("Long")
    strategy.cancel("Short")
```

> Detail

https://www.fmz.com/strategy/431009

> Last Modified

2023-11-03 17:11:34
