
> Name

Vegas-Trend-Wave-Strategy

> Author

ChaoZhang

> Strategy Description


[trans]
Furgan Trend Wave Strategy
This strategy determines the price trend direction by calculating the price difference percentage of multiple groups of EMA moving averages, and trades with Furgan trend waves.
Specifically, it calculates the percentage price difference between the 144-period, 169-period, and 233-period EMA and the price itself respectively. When all three meet the preset positive difference, a long signal is generated. When the price is below three EMAs and the 144-period EMA has crossed below the 233-period EMA, a short signal is generated.
This method based on EMA moving average combination can filter out more false breakthroughs than a single moving average. At the same time, the Furgan wave itself contains multiple sets of EMA, which can effectively determine the trend direction.
However, the EMA moving average itself has hysteresis and cannot grasp the best entry point. The wave theory also has a certain degree of subjectivity, and the effect of real trading is highly related to parameter optimization. The actual effect of this strategy needs to be carefully evaluated.
Generally speaking, Furgan's trend wave strategy, combined with moving average analysis and wave theory, can achieve better results in trend markets. However, you still need to pay attention to risk management before you can use it in the long term.
||

This strategy calculates percentage price difference between multiple EMA pairs to determine trend direction, and trades based on the Vegas wave.

Specifically, it computes percentage price differences between current price, 144-period EMA, 169-period EMA and 233-period EMA. Long signals are generated when all three meet the preset positive difference threshold. Shorts are triggered when price falls below all three EMAs and 144-period EMA crosses below 233-period EMA.

The EMA combo filters more false breaks compared to single EMA. Also, the Vegas wave itself contains multiple EMAs for robust trend analysis.

However, EMAs have inherent lag and cannot identify optimal entries. And there is subjectivity in wave theory, with performance relying largely on parameter optimization. Prudent assessment of live results is required.

Overall, the Vegas trend wave strategy synergizes EMA analysis and wave theory for good results in trending markets. But risk management remains crucial for long-term application.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0.1|EMA144 percent difference from EMA233|
|v_input_2|0.1|EMA169 percent difference from EMA233|
|v_input_3|0.1|Current price percent difference from EMA233|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-03 00:00:00
end: 2023-09-10 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Vegas Wave Strategy", overlay=true)

ema144 = ema(close, 144)
ema169 = ema(close, 169)
ema233 = ema(close, 233)

current = close

upd144 = input(title="EMA144 percent difference from EMA233", type=float, defval=0.1)
upd169 = input(title="EMA169 percent difference from EMA233", type=float, defval=0.1)
upd_current = input(title="Current price percent difference from EMA233", type=float, defval=0.1)

//pDiff - Percentage Difference
pDiff(x, y) =>
    ((x-y)/x)*100

gtDiff(x, y) =>
    x > y


pd144 = pDiff(ema144, ema233)
pd169 = pDiff(ema169, ema233)
pd_current = pDiff(current,ema233)

plot(ema144,color=orange, linewidth=2, transp=0, title="144 EMA")
plot(ema169,color=blue,linewidth=2, transp=0, title="169 EMA")
plot(ema233,color=red,linewidth=2, transp=0, title="233 EMA")


//plot(current, color=white, title="Current Candle")


if (gtDiff(pd_current, upd_current) and gtDiff(pd144, upd144) and gtDiff(pd169, upd169))
    strategy.entry("buy", strategy.long, when=strategy.position_size <=0)

// if (ema8 > ema55 and ema13 > ema55 and ema21 > ema55 and current > ema55 and pd_current > upd_current)
//     strategy.entry("buy", strategy.long, 10000, when=strategy.position_size <=0)
    
if (current < ema144 and current < ema169 and current < ema233 and ema144 <= ema233)
    strategy.entry("sell", strategy.short, when=strategy.position_size > 0)
```

> Detail

https://www.fmz.com/strategy/426367

> Last Modified

2023-09-11 15:23:35
