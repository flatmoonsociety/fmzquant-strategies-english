
> Name

Short-Term-Medium-Term-and-Long-Term-EMA-Crossover-Trading-Strategy
> Author

ChaoZhang

> Strategy Description


![IMG](https://www.fmz.com/upload/asset/17173b7cc08054c20d6.png)
[trans]


This strategy generates trading signals based on three exponential moving averages (EMA) with different periods: short-term, medium-term and long-term. Among them, the short-term EMA period is 5 days, the medium-term EMA period is 8 days, and the long-term EMA period is 13 days. When the short-term EMA crosses above the medium-term and long-term EMA, go long; when the short-term EMA crosses below the medium-term and long-term EMA, go short.
#### Strategy Principle
This strategy determines market trends by calculating EMAs of different periods. The short-term EMA reflects the average price in recent days, and the medium- and long-term EMA reflects the average price over a longer period of time. If the short-term EMA crosses above the medium- and long-term EMA, it means that the price has begun to break upward, so go long; if the short-term EMA crosses below the medium- and long-term EMA, it means that the price has begun to break downward, so go short.
Specifically, this strategy calculates three EMAs of 5 days, 8 days and 13 days at the same time. A long signal is generated when the 5-day EMA crosses above the 8-day and 13-day EMA; a short signal is generated when the 5-day EMA crosses below the 8-day and 13-day EMA. After going long, if the 5-day EMA falls below the 13-day EMA again, the position will be closed. After shorting, if the 5-day EMA crosses the 13-day EMA again, the position will be closed.
#### Strategic Advantages
1. Use multi-period EMA to determine trends and avoid missing key trend turning points because a single EMA period is too short or too long.
2. Combined with the three period EMAs of medium, short and long periods, trading signals are more reliable and accurate
3. Smoothing prices through EMA can filter out some market noise and prevent unnecessary opening of positions.
#### Strategy Risk
1. The three EMAs are all delayed trend indicators. There must be a time difference before the actual price breaks through, which may cause the trading signal to lag.
2. EMA cannot distinguish between true trends and short-term adjustments and may produce false signals.
3. The fixed EMA period cannot adapt to the changing characteristics of the market in different periods.
It can be optimized by:
1. Combine with other indicators such as MACD to determine the true trend and avoid generating false signals.
2. The EMA cycle parameters can be flexibly adjusted according to different varieties and market environments.
3. Add a trailing stop to lock in profits and control risks
#### Summarize
This strategy determines the turning point of the market trend by calculating three period EMAs of short, medium and long periods and comparing their intersections. It is a typical breakthrough system. The advantage is that the trading signals are simple, clear and easy to operate; the disadvantage is that the EMA indicator itself lags behind and cannot distinguish between real trends and short-term adjustments. In the future, we can consider supplementing judgment with other technical indicators, or optimizing this strategy in combination with adaptive parameter adjustment.
||

This strategy generates trading signals based on three exponential moving average lines (EMA) with different periods: short-term EMA with 5-day period, medium-term EMA with 8-day period and long-term EMA with 13-day period. It goes long when the short-term EMA crosses over the medium-term and long-term EMAs, and goes short when the short-term EMA crosses under the medium-term and long-term EMAs.  

#### Strategy Logic

This strategy judges the market trend by calculating EMAs of different periods. The short-term EMA reflects the average price of the recent few days while the medium- and long-term EMAs reflect the average price over longer timeframes. The crossover of short-term EMA over medium- and long-term EMAs signals an upward breakout of the price, so a long position is taken. Conversely, when the short-term EMA crosses under the other two, it signals a downward price breakout so a short position is taken.  

Specifically, this strategy concurrently computes 5-day, 8-day and 13-day EMAs. It generates long signals when the 5-day EMA crosses over the 8-day and 13-day ones; it generates short signals when the 5-day EMA crosses under the other two. After going long, the position is closed once the 5-day EMA crosses back under the 13-day EMA. Likewise for the short position.

#### Advantages of the Strategy

1. Using multiple-period EMAs avoids missing key trend reversal points that could occur with overly short or long single EMA periods  
2. Combining three EMAs of short, medium and long terms enhances reliability of trading signals
3. Smoothed pricing via EMAs filters out some market noise and prevents unnecessary entries

#### Risks of the Strategy

1. All three EMAs are lagging trend indicators, inherently containing some time delays before actual price breakouts, risking late signals
2. EMAs cannot effectively distinguish real trends versus short-term corrections, apt to yield false signals  
3. Fixed EMA periods cannot adapt to varying market regimes across different timeframes

Improvement ideas:

1. Adding other indicators like MACD to better gauge real trend, avoiding false signals
2. Flexibly tuning EMA period parameters for different products and market environments 
3. Adding moving stop loss to lock in profits and control risks

#### Summary
This is a typical breakout system that judges trend reversals by comparing crossovers between short, medium and long-period EMAs. Its simplicity in signaling facilitates ease of trading, but also suffers from EMAs' inherent lagging and inability to filter real trends from temporary corrections. Future enhancements may integrate other technical indicators or adaptive parameter tuning to optimize it.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2020|Backtest Start Year|
|v_input_2|5|Length|
|v_input_3|8|Length|
|v_input_4|13|Length|
|v_input_5|false|Long Only|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-16 00:00:00
end: 2023-11-23 00:00:00
period: 30m
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
// 
// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © gregoirejohnb
// @It is modified by ttsaadet.
// Moving average crossover systems measure drift in the market. They are great strategies for time-limited people.
// So, why don't more people use them?
// 

//
strategy(title="EMA Crossover Strategy", shorttitle="EMA-5-8-13 COS by TTS", overlay=true, pyramiding=0, default_qty_type=strategy.percent_of_equity, default_qty_value=100, currency=currency.TRY,commission_type=strategy.commission.percent,commission_value=0.04, process_orders_on_close = true, initial_capital = 100000)

// === GENERAL INPUTS ===
//strategy start date
start_year = input(defval=2020, title="Backtest Start Year")

// === LOGIC ===
short_period = input(type=input.integer,defval=5,minval=1,title="Length")
mid_period = input(type=input.integer,defval=8,minval=1,title="Length")
long_period = input(type=input.integer,defval=13,minval=1,title="Length")

longOnly = input(type=input.bool,defval=false,title="Long Only")
shortEma = ema(hl2,short_period)
midEma = ema(hl2,mid_period)
longEma = ema(hl2,long_period)

plot(shortEma,linewidth=2,color=color.red,title="Fast")
plot(midEma,linewidth=2,color=color.orange,title="Fast")
plot(longEma,linewidth=2,color=color.blue,title="Slow")

longEntry = ((shortEma > midEma) and crossover(shortEma,longEma)) or ((shortEma > longEma) and crossover(shortEma,midEma))
shortEntry =((shortEma < midEma) and crossunder(shortEma,longEma)) or ((shortEma < longEma) and crossunder(shortEma,midEma))

plotshape(longEntry ? close : na,style=shape.triangleup,color=color.green,location=location.belowbar,size=size.small,title="Long Triangle")
plotshape(shortEntry and not longOnly ? close : na,style=shape.triangledown,color=color.red,location=location.abovebar,size=size.small,title="Short Triangle")
plotshape(shortEntry and longOnly ? close : na,style=shape.xcross,color=color.black,location=location.abovebar,size=size.small,title="Exit Sign")

// === STRATEGY - LONG POSITION EXECUTION ===
enterLong() =>
    longEntry 
exitLong() =>
    crossunder(shortEma,longEma)

strategy.entry(id="Long", long=strategy.long, when=enterLong())
strategy.close(id="Long", when=exitLong())


// === STRATEGY - SHORT POSITION EXECUTION ===

enterShort() =>
    not longOnly and shortEntry  
exitShort() =>
    crossover(shortEma,longEma)

strategy.entry(id="Short", long=strategy.short, when=enterShort())
strategy.close(id="Short", when=exitShort())
```

> Detail

https://www.fmz.com/strategy/433092

> Last Modified

2023-11-24 13:33:21
