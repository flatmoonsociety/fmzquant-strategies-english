
> Name

Multi-Timeframe-Diagonally-Layered-RSI-Strategy Multi-Timeframe-Diagonally-Layered-RSI-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy is a multi-time frame non-repaint RSI strategy that only goes long when the two higher time frames are oversold. I wrote it on the 1 minute line of BTC/USD, but the logic can be applied to other assets. Aims to profit when an asset is in a downward trend.
## Principle
Diagonal cascading means that entry and exit conditions are spread over different time frames. Often, the indicator can become unprofitable because in a downtrend, the overbought zone of the current time frame is not touched, but the overbought zone of the higher time frame is hit first, and then a pullback occurs. The diagonal cascading strategy mitigates this problem by selling diagonally when the faster time frames are overbought and buying when the slower time frames are oversold.
Therefore, this strategy is stacked diagonally. I might create a separate script that switches between diagonal up and diagonal down depending on the overall trend, as the indicator may not flash as frequently during an extended uptrend. This can be seen as an "X" shape on time series and time frame charts. It’s worth considering…
## Advantages
- Utilize multiple time frame RSI indicators to improve the reliability of trading signals
- Diagonal cascading entries for more opportunities in downtrends
- Non-redrawing indicator, reliable signal
- Configurable RSI parameters and overbought and oversold limits to adapt to different markets
- Consider transaction costs and pursue stable profits rather than high-frequency trading
## Risks and Solutions
- RSI is prone to produce false signals, so parameters can be adjusted appropriately or filter conditions added.
- Diagonal stacking increases entry difficulty and can reduce the number of stacking time frames
- If you only go long, you need to bear directional risks. You can consider going long and short in a balanced way.
- Use fixed stop loss to control single losses
## Optimization direction
- Add trend judgment, use diagonal stacking when the trend is falling, and use diagonal upwards when the trend is rising.
- Optimize RSI parameters and find the best parameter combination
- Add Volume, MA and other indicator filters to improve signal quality
- Add short selling strategy to make the strategy profitable in all markets
- Optimize stop loss strategy and reduce retracement
## Summarize
This strategy overall is a very effective downtrend trading strategy. Using the multi-time frame RSI indicator and the diagonal cascading entry method, you can capture rebound opportunities during the decline stage. At the same time, the non-redrawing feature also improves the reliability of the signal. By optimizing parameters, adding filters and shorting strategies, it can be made into a powerful strategy suitable for any market.
||

## Overview

This strategy is a multi-timeframe non-repainting RSI strategy that goes long only when two higher timeframes are oversold. I wrote it on BTC/USD 1-min, but the logic should work on other assets as well. It is designed to be profitable when the asset is in a downtrend.  

## Principle 

Diagonal layering refers to entry and exit conditions spread across different timeframes. Normally, indicators can become unprofitable because in downtrends, the overbought zones of the current timeframe are not reached. Rather, the overbought zones of the higher timeframes are reached first, followed by a pullback. Diagonally layered strategies mitigate this by selling diagonally, that is, selling once the faster timeframe reaches overbought and buying once the slower timeframe reaches oversold.

Thus this strategy is diagonally layered. I may create a separate script that toggles between diagonal-up and diagonal-down based on overall trend, as in extended uptrend periods this indicator may not flash as frequently. This can be visualized on a time series x timeframe chart as an "X" shape. Something to consider...

## Advantages

- Utilizes RSI indicators across multiple timeframes, improving signal reliability
- Diagonal layering provides more opportunities in downtrends 
- Non-repainting indicators give reliable signals
- Configurable RSI parameters and overbought/oversold levels adapt to different markets
- Considers trading costs, targets steady profits over high-frequency trading

## Risks and Solutions

- RSI prone to false signals, tweak parameters or add filters 
- Diagonal layering increases entry difficulty, reduce layered timeframes
- Long only, exposed to directional risk, consider balancing long/short
- Use fixed stop loss to control loss per trade

## Optimization Directions

- Add trend detection, use diagonal layering in downtrends, diagonal-up in uptrends
- Optimize RSI parameters to find best combo
- Add Volume, MA etc. filters to improve signal quality
- Add short strategy so strategy can profit in all markets
- Optimize stop loss to reduce drawdown

## Summary

Overall this is a very effective downtrend trading strategy. Using multi-timeframe RSIs and diagonal layering provides opportunities to catch bounces in downtrends. Non-repainting also improves signal reliability. With parameter optimization, adding filters and a short strategy, it can be made into a robust strategy for any market.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|7|RSI Length|
|v_input_timeframe_1|3|HT 1|
|v_input_timeframe_2|5|HT 2|
|v_input_int_2|80|Overbought Level|
|v_input_int_3|20|Oversold Level|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-21 00:00:00
end: 2023-06-24 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © wbburgin

//@version=5
strategy("MTF Layered RSI - Bitcoin Bot [wbburgin]",overlay=false, pyramiding = 20, initial_capital=10000)

length = input.int(7,"RSI Length")
tf2 = input.timeframe("3",title="HT 1")
tf3 = input.timeframe("5",title="HT 2")
ob = input.int(80,"Overbought Level")
os = input.int(20,"Oversold Level")

rsi = ta.rsi(close,length)
rsi2 = request.security(syminfo.tickerid, tf2, rsi[1], barmerge.gaps_off, lookahead=barmerge.lookahead_on)
rsi3 = request.security(syminfo.tickerid, tf3, rsi[1], barmerge.gaps_off, lookahead=barmerge.lookahead_on)

plot(rsi,color=color.yellow,title="RSI Current TF")
plot(rsi2,color=color.new(color.yellow,50),title="RSI HT1")
plot(rsi3,color=color.new(color.yellow,75),title="RSI HT2")

lm=hline(os,title="Oversold")
hm=hline(ob,title="Overbought")

fill(hm,lm,color=color.new(color.blue,95))

htCross = (ta.crossover(rsi2,os) and rsi3>os and rsi>os) or (ta.crossover(rsi3,os) and rsi2>os and rsi>os)
buySig = (ta.crossover(rsi,os) and rsi2 < os and rsi3 < os) or htCross
sellSig = ta.crossunder(rsi,ob)

if buySig
    strategy.entry("Long",strategy.long)
if sellSig
    strategy.close("Long")

plotshape(buySig,title="Buysig",style=shape.triangleup,location=location.bottom,color=color.green,size=size.tiny)
plotshape(sellSig,title="Sellsig",style=shape.triangledown,location=location.top,color=color.red,size=size.tiny)
```

> Detail

https://www.fmz.com/strategy/428102

> Last Modified

2023-09-28 16:12:25
