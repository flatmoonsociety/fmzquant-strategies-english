
> Name

Adaptive-ATR-Trend-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/16bbc07bdeb375ea887.png)

[trans]

## Overview
This strategy is a trend breakout strategy based on the ATR indicator. Its main idea is to perform trend breakthrough operations when the price exceeds a certain multiple of ATR. The strategy also includes trend confirmation and the ability to limit trades using date ranges.
## Principle
The strategy uses the ATR indicator to determine the extent of price fluctuations. ATR stands for average true range, which measures the average price fluctuation within a certain time period. Set the length parameter in the strategy to calculate the ATR period, and the numATRs parameter represents the ATR multiple of the breakthrough.
When the price rises and exceeds numATRs times ATR above, perform long operations; when the price falls and exceeds numATRs times ATR below, perform short operations.
In addition, the strategy adds BOOL variables that require long positions (needlong) and short positions (needshort), which can control only long or short positions. The strategy also sets a date range and only trades between specified dates, thereby achieving time range restrictions.
The strategy uses the size variable to determine the position and calculates the number of lots based on the position. Lot size is calculated as a percentage of account equity.
## Advantages
- Use the ATR indicator to automatically adapt to market volatility, eliminating the need to manually set the stop-loss and take-profit distances
- Flexible choice to go long, short or only long/short
- You can set a date range for trading to avoid important time points
- Flexible lot setting, orders can be placed based on account equity percentage
## Risks and Solutions
- The ATR indicator only considers price fluctuations. If the market changes drastically, the stop loss distance may be too small, and other indicators need to be combined for optimization.
- When restricting transactions by a date range, if there are no suitable opportunities before or after an important time period, it may result in missed trading opportunities. The date range can be appropriately expanded.
- When placing orders using the account equity ratio, you need to set the ratio reasonably to avoid excessive losses in a single transaction.
## Optimization ideas
- Consider adding trend indicators such as moving averages to filter out noise trading caused by non-trend breakthroughs
- You can test different ATR cycle parameters and select the best parameter combination
- You can consider using it in combination with other strategies to give full play to their respective advantages and improve the stability of the strategy.
## Summarize
The overall idea of ​​this strategy is clear and easy to understand. It uses the ATR indicator to automatically adapt to market volatility. It is a general trend following strategy. Through parameter optimization and combination with other strategies, strategy performance and stability can be further improved. However, you need to pay attention to prevent excessive single losses, and pay attention to the problem of insufficient stop loss when the market changes drastically.
||


## Overview

This strategy is a trend breakout strategy based on the ATR indicator. Its main idea is to take trend breakout trades when the price exceeds a certain multiple of ATR. The strategy also includes trend confirmation and limiting trades within date ranges.

## Principle 

The strategy uses the ATR indicator to measure price volatility. ATR stands for Average True Range and it measures the average volatility over a period. The length parameter in the strategy calculates the ATR period and numATRs represents the ATR multiplier for breakout.

When the price breaks out above the upper numATRs multiple of ATR, a long position is taken. When the price breaks below the lower numATRs multiple of ATR, a short position is taken.

In addition, the strategy includes needlong and needshort bool variables to control only long or only short trades. It also sets date ranges to limit trading within specified dates. 

The strategy uses a size variable to determine position size and calculates order size based on percentage of account equity.

## Advantages

- Uses ATR to automatically adapt to market volatility without manual profit/loss settings.

- Flexible to choose long, short or long/short only. 

- Can set date ranges to avoid trading at important events.

- Flexible position sizing based on account equity percentage.

## Risks and Solutions

- ATR only considers price volatility. It may have insufficient stop loss during huge market swings. Other indicators can be combined.

- Date range limits may miss opportunities if no good setups before/after. Can expand date range slightly.  

- Equity percentage sizing risks large losses on single trades. Reasonable percentages needed.

## Optimization Ideas

- Add moving averages for trend filter to reduce false breakout noise trades.

- Test ATR periods to find optimal parameters.

- Combine with other strategies to utilize strengths and improve stability.

## Conclusion

This is an understandable trend following strategy using ATR to adapt to volatility. Parameter optimization and combining with other strategies can further improve performance and stability. But large single-trade losses should be avoided and insufficient stops during huge swings must be noted.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|false|Short|
|v_input_3|100|Lot, %|
|v_input_4|5|length|
|v_input_5|0.75|numATRs|
|v_input_6|1900|From Year|
|v_input_7|2100|To Year|
|v_input_8|true|From Month|
|v_input_9|12|To Month|
|v_input_10|true|From day|
|v_input_11|31|To day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-30 00:00:00
end: 2023-10-30 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro
//2018

//@version=3
strategy(title = "Noro's Volty Strategy v1.0", shorttitle = "Volty 1.0", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 100)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(false, defval = false, title = "Short")
capital = input(100, defval = 100, minval = 1, maxval = 10000, title = "Lot, %")
length = input(5)
numATRs = input(0.75)
fromyear = input(1900, defval = 1900, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To day")

//Indicator
atrs = sma(tr, length) * numATRs

//Trading
size = strategy.position_size
lot = 0.0
lot := size == 0 ? strategy.equity / close * capital / 100 : lot[1]
if (not na(close[length])) and needlong
    strategy.entry("L", strategy.long, lot, stop = close + atrs, when = (time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))
if (not na(close[length])) and needlong == false
    strategy.entry("L", strategy.long, 0, stop = close + atrs, when = (time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))
if (not na(close[length])) and needshort
    strategy.entry("S", strategy.short, lot, stop = close - atrs, when = (time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))
if (not na(close[length])) and needshort == false
    strategy.entry("S", strategy.short, 0, stop = close - atrs, when = (time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))
```

> Detail

https://www.fmz.com/strategy/430681

> Last Modified

2023-10-31 15:58:46
