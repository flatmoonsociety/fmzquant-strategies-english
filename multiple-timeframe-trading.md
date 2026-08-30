
> Name

Cross-period moving average trading multiple-timeframe-trading
> Author

inventor quantification
> Strategy Description

[trans] Demonstrates how the Pine language uses multiple timeframes[/trans]


> Source (PineScript)

``` pinescript
/*backtest
start: 2021-05-04 00:00:00
end: 2022-05-03 23:59:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Bitfinex","currency":"BTC_USD"}]
*/
strategy("multiple timeframe trading")

expr = ta.ema(close, 5)
hVal = request.security(syminfo.tickerid, '60', expr)

plot(expr, timeframe.period)
plot(hVal, '1hour')

// 5 hour vs 5 days
if hVal > expr
    strategy.entry("long", strategy.long)
else
    strategy.entry("short", strategy.short)

```

> Detail

https://www.fmz.com/strategy/361360

> Last Modified

2022-05-06 16:47:08
