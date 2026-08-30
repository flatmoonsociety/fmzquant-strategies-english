
> Name

Trend-Following-Strategy-Based-on-Moving-Average-Crossover
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/800faa158942e669027db553d04de81dd3d2af16d67933c79d99eb2b9e391522.png)

[trans]

## Overview
This strategy mainly uses the golden cross of the moving average and the K-line to break through the moving average to make long and short decisions. Go long when the short-term moving average crosses above the longer-term moving average, and go short when the short-term moving average crosses below the longer-term moving average. At the same time, the closing price of the K line breaks through the moving average as an entry signal.
## Strategy Principle
1. Calculate two moving averages EMA1 and EMA2 with different periods. EMA1 has a short period and EMA2 has a long period.
2. Determine whether EMA1 crosses EMA2. If so, go long.
3. Determine whether EMA1 crosses EMA2. If so, go short.
4. Determine whether the closing price breaks through EMA1 as an entry signal.
5. Stop loss exit mechanism: Set a fixed stop loss point or set a stop loss through the Donchian channel.
The following functions are mainly used:
- ema(): Calculate exponential moving average
- crossover(): Determine whether EMA1 crosses EMA2
- crossunder(): Determine whether EMA1 undercuts EMA2
- rising()/falling(): Determine whether the price is rising/falling
- valuewhen(): returns different values based on conditions
## Advantage Analysis
1. The strategy is simple and easy to understand and implement.
2. Utilize the trend tracking characteristics of the moving average system to effectively track the trend.
3. Combined with the breakthrough of the K-line closing price as the entry opportunity, false breakthroughs can be avoided.
4. The moving average combination of different parameters can be flexibly used to adapt to different cycles.
5. A stop-loss mechanism can be set up to control risks.
## Risk Analysis
1. When the market is in a volatile market, the moving average will produce frequent golden cross and dead cross signals, making it easy to stop losses.
2. Fixed stop loss points may be too rigid and cannot be adjusted according to market changes.
3. The moving average system lags behind, and it is easy to miss reversal signals at trend turning points.
4. It is necessary to accurately judge the slope of the moving average to filter out false breakthroughs.
5. Parameters need to be selected carefully. Parameter combinations that are too frequent or lagging will affect the effect of the strategy.
## Optimization direction
1. The zero-axis crossing of the MACD indicator can be used to determine the trend and filter out shocks.
2. Donchian channel can be added to set dynamic stop loss lines to improve fixed stop loss problems.
3. Bollinger Bands indicators can be added to determine the strength and weakness of trends to avoid invalid transactions in volatile markets.
4. Optimize the combination of moving average parameters and test the actual effects of different period strategies.
5. Consider adding anchored moving averages to avoid lagging.
## Summarize
The overall idea of ​​this strategy is simple and clear. It uses the routine moving average golden cross trading strategy and combines K-line breakthroughs to enter the market, which can effectively filter out false signals. The room for optimization lies in using other indicators to judge the strength of the trend, setting dynamic stop losses, etc. Overall, the trend following strategy based on moving averages is classic and easy to understand, and it is worth exploring its optimization space.
|| 

## Overview

This strategy mainly uses the golden cross and dead cross of moving averages and candlestick breakthrough of moving averages to make long and short decisions. It goes long when the short period moving average crosses over the longer period moving average, and goes short when the short period moving average crosses below the longer period moving average. Candlestick close price breaking through the moving average is also used as the entry signal.

## Principles

1. Calculate two moving averages, EMA1 and EMA2, with different periods. EMA1 has a shorter period and EMA2 has a longer period.

2. Determine if EMA1 crosses over EMA2, if yes, go long.  

3. Determine if EMA1 crosses below EMA2, if yes, go short.

4. Determine if the closing price breaks through EMA1 as the entry signal.

5. Exit mechanism: set fixed stop loss or use Donchian Channel to set stop loss.

Main functions used:

- ema(): calculate exponential moving average
- crossover(): determine if EMA1 crosses over EMA2
- crossunder(): determine if EMA1 crosses below EMA2  
- rising()/falling(): determine if price is rising or falling
- valuewhen(): return different values based on condition

## Advantages

1. Simple logic, easy to understand and implement.

2. Utilize the trend following trait of moving averages to effectively track trends.

3. Combining candlestick close price breakthrough helps avoid false breakthroughs.

4. Flexible usage of different moving average combinations adaptable to different periods. 

5. Stop loss mechanism controls risk.

## Risks

1. Frequent golden crosses and dead crosses during market consolidation cause whipsaws.

2. Fixed stop loss points may be too rigid to adjust based on market changes.

3. Moving averages lag and may miss reversal signals at turning points. 

4. Precise judgment of moving average slope needed to filter false breakthroughs.

5. Parameter selection needs caution, inappropriate frequency or lagging may affect strategy performance.

## Optimization

1. MACD zero line crossover can help determine trends and filter consolidations.

2. Add Donchian Channel for dynamic stop loss line to improve fixed stop loss.

3. Add Bollinger Bands to judge strong or weak trends, avoiding ineffective trading during market consolidations.

4. Optimize moving average parameter combinations and test actual performance of different period strategies.

5. Consider adding anchored moving averages to reduce lag.

## Conclusion

The overall logic of this strategy is simple and clear, utilizing classic moving average crossover trading techniques, and combining candlestick breakout for entry to effectively filter false signals. Optimization spaces include using other indicators for trend strength, dynamic stops etc. In general, trend following strategies based on moving averages are classic and intuitive, with valuable exploration spaces for optimization.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|Candle body resistance Channel: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|false|Bar Channel On/Off|
|v_input_3|10|Support / Resistance length:|
|v_input_4|13|EMA 1|
|v_input_5|21|EMA 2|
|v_input_6|false|Display Hull MA Set:|
|v_input_7_close|0|Hull MA's Source:: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_8|8|Hull MA's Base Length:|
|v_input_9|5|Hull MA's Length Scalar:|
|v_input_10|720|period|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-01 00:00:00
end: 2023-10-23 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy(title='Mega crypto bot strategy', shorttitle='megacryptobot_Strategy', overlay=true, pyramiding=0, initial_capital=10000, currency=currency.USD)

//Candle body resistance Channel-----------------------------//
len = 34
src = input(close, title="Candle body resistance Channel")
out = sma(src, len)
last8h = highest(close, 13)
lastl8 = lowest(close, 13)
bearish = cross(close,out) == 1 and falling(close, 1)
bullish = cross(close,out) == 1 and rising(close, 1)
channel2=input(false, title="Bar Channel On/Off")
ul2=plot(channel2?last8h:last8h==nz(last8h[1])?last8h:na, color=black, linewidth=1, style=linebr, title="Candle body resistance level top", offset=0)
ll2=plot(channel2?lastl8:lastl8==nz(lastl8[1])?lastl8:na, color=black, linewidth=1, style=linebr, title="Candle body resistance level bottom", offset=0)
//fill(ul2, ll2, color=black, transp=95, title="Candle body resistance Channel")

//-----------------Support and Resistance 
RST = input(title='Support / Resistance length:',  defval=10) 
RSTT = valuewhen(high >= highest(high, RST), high, 0)
RSTB = valuewhen(low <= lowest(low, RST), low, 0)
RT2 = plot(RSTT, color=RSTT != RSTT[1] ? na : red, linewidth=1, offset=+0)
RB2 = plot(RSTB, color=RSTB != RSTB[1] ? na : green, linewidth=1, offset=0)

//--------------------Trend colour ema------------------------------------------------// 
src0 = close, len0 = input(13, minval=1, title="EMA 1")
ema0 = ema(src0, len0)
direction = rising(ema0, 2) ? +1 : falling(ema0, 2) ? -1 : 0
plot_color = direction > 0  ? lime: direction < 0 ? red : na
plot(ema0, title="EMA", style=line, linewidth=1, color = plot_color)

//-------------------- ema 2------------------------------------------------//
src02 = close, len02 = input(21, minval=1, title="EMA 2")
ema02 = ema(src02, len02)
direction2 = rising(ema02, 2) ? +1 : falling(ema02, 2) ? -1 : 0
plot_color2 = direction2 > 0  ? lime: direction2 < 0 ? red : na
plot(ema02, title="EMA Signal 2", style=line, linewidth=1, color = plot_color2)

//=============Hull MA//
show_hma = input(false, title="Display Hull MA Set:")
hma_src = input(close, title="Hull MA's Source:")
hma_base_length = input(8, minval=1, title="Hull MA's Base Length:")
hma_length_scalar = input(5, minval=0, title="Hull MA's Length Scalar:")
hullma(src, length)=>wma(2*wma(src, length/2)-wma(src, length), round(sqrt(length)))
plot(not show_hma ? na : hullma(hma_src, hma_base_length+hma_length_scalar*6), color=black, linewidth=2, title="Hull MA")

//============ signal Generator ==================================//
period = input('720')
ch1 = request.security(syminfo.tickerid, period, open)
ch2 = request.security(syminfo.tickerid, period, close)
longCondition = crossover(request.security(syminfo.tickerid, period, close),request.security(syminfo.tickerid, period, open))
if (longCondition)
    strategy.entry("BUY", strategy.long)
shortCondition = crossunder(request.security(syminfo.tickerid, period, close),request.security(syminfo.tickerid, period, open))
if (shortCondition)
    strategy.entry("SELL", strategy.short)

///////////////////////////////////////////////////////////////////////////////////////////
```

> Detail

https://www.fmz.com/strategy/430011

> Last Modified

2023-10-24 11:02:52
