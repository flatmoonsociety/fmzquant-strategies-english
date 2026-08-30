
> Name

Bollinger Band Channel Breakout Trading Strategy Bollinger-Band-Channel-Breakout-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

This strategy trades by watching for a price breakout of the Bollinger Bands channel. Bollinger Bands can effectively define the range of price shocks, and their breakthroughs can serve as signals for trend transitions.
Strategy principle:
1. Calculate the middle line, upper band and lower band of Bollinger Bands. The midline is the n-day simple moving average, and the bandwidth is several times the n-day standard deviation.
2. When the price crosses the upper band and the lower band, go long; when the price crosses the lower band, go short.
3. Set the stop loss on the Bollinger Bands line in the opposite direction for risk control.
4. Use trend following stop loss to lock in more profits, or you can choose fixed stop loss.
5. Mutual exclusion can be set for long and short orders to avoid the existence of long and short orders at the same time.
Advantages of this strategy:
1. Breaking through the Bollinger Bands can effectively identify trend change points.
2. Stop loss set on Bollinger Bands is helpful for timely exit from the trend.
3. Mutually exclusive orders can avoid hedging in the same direction.
Risks of this strategy:
1. There is a lag between the Bollinger Bands moving average and standard deviation, and the best entry point may be missed.
2. Frequent false breakthroughs may occur in a volatile trend.
3. Standard parameters cannot adapt to changes in market volatility.
In short, this strategy trades by judging the breakthrough of Bollinger Bands, which is a typical channel breakthrough strategy. There is still room for improvement in parameter optimization and risk control, but the overall idea is simple and reliable.
||

This strategy trades the price breakout of Bollinger Bands. The bands effectively define price oscillation range, with breakouts signaling potential trend turns. 

Strategy Logic:

1. Calculate BB midline, upper and lower bands. Midline is n-period SMA, band width is n-period standard deviation multiple.

2. Go long on lower band breakout, and short on upper band breakout.

3. Set stop loss on opposite band for risk control.

4. Trailing stop to lock in more profits, or fixed stop.

5. Apply mutually exclusive orders to avoid simultaneous long/short.

Advantages:

1. BB breakout accurately identifies trend changes.

2. Stops on bands allow timely trend exit. 

3. Mutual exclusion avoids same-direction hedging.

Risks:

1. BB mean and deviation lag, missing best entries.

2. Whipsaws common in ranging markets.

3. Static parameters Unable to adapt changing volatility.

In summary, this strategy trades BB breakouts as a typical channel system. There is room for improvement in tuning and risk management but the overall concept is simple and robust.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|45|length|
|v_input_2|2.5|mult|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-05 00:00:00
end: 2023-09-11 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Kozlod - BB Strategy - 1 minute", overlay=true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100)

// 
// author: Kozlod
// date: 2019-05-27
// RSI - BTCUSDT - 1m
// https://www.tradingview.com/u/Kozlod/
// https://t.me/quantnomad
//

source = close
length = input(45, minval=1)
mult = input(2.5, minval=0.001, maxval=50)

basis = sma(source, length)
dev = mult * stdev(source, length)

upper = basis + dev
lower = basis - dev

plot(upper)
plot(lower)

buyEntry  = crossover(source, lower)
sellEntry = crossunder(source, upper)

if (crossover(source, lower))
    strategy.entry("BBandLE", strategy.long, stop=lower, oca_name="BollingerBands",  comment="BBandLE")
else
    strategy.cancel(id="BBandLE")

if (crossunder(source, upper))
    strategy.entry("BBandSE", strategy.short, stop=upper, oca_name="BollingerBands",  comment="BBandSE")
else
    strategy.cancel(id="BBandSE")
```

> Detail

https://www.fmz.com/strategy/426514

> Last Modified

2023-09-12 17:05:56
