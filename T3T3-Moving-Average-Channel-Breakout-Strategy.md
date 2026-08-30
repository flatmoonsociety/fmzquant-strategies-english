
> Name

T3 Moving Average Channel Breakout Strategy T3-Moving-Average-Channel-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description


[trans]

## Strategy Principle
This strategy uses T3 moving averages and their channels to identify trend direction and generate trading signals when price breaks out of the channels.
Specific transaction logic:
1. Calculate a T3 moving average to represent the midline
2. Calculate the channel range of the moving average. The upper track is the moving average plus the range, and the lower track is the moving average minus the range.
3. When the price reaches the upper limit, go long
4. When the price falls below the lower band, go short
5. Changes in background color represent trend transitions and assist judgment.
The T3 moving average is a moving average with a small delay. It responds quickly when the channel breaks through, which is conducive to capturing turning points. This strategy also uses background color to assist in judging long-term trends and combines multiple factors to determine trading opportunities.
## Strategic Advantages
- T3 moving average delay is small and responsive
- Channel breakouts send clear trading signals
- Judge based on background color to avoid wrong trades
## Strategy Risk
- Repeated testing is required to determine appropriate parameters
- Breakthrough trading is easy to get trapped, so you need to be cautious
- If the signals are frequent, the breakthrough amplitude can be appropriately increased.
## Summarize
This strategy takes advantage of the sensitivity of the T3 moving average to trade at channel breakouts. Use the background color to determine the long-term trend. Through parameter optimization, a balance between efficiency and stability can be achieved. But be careful to prevent over-trading.
[trans]

||

## Strategy Logic

This strategy uses a T3 moving average and its channels to identify trend direction, generating signals when price breaks the channel lines. 

The trading logic is:

1. Plot a T3 MA as the middle line 

2. Calculate the channel range around the MA as upper and lower bands

3. Go long when price breaks above the upper band 

4. Go short when price breaks below the lower band

5. Background color changes indicate trend shifts

The T3 MA has less lag and reacts faster to breakouts. The strategy also uses background color to aid long term trend judgement, combining factors for robust signals.

## Advantages

- T3 MA has less lag and faster reaction

- Clear trade signals from channel breakouts

- Background color avoids bad trades against the trend

## Risks

- Requires iterative testing to find optimal parameters

- Breakout trades prone to traps need caution 

- Frequent signals, consider wider breakouts

## Summary

This strategy capitalizes on the T3 MA's sensitivity by trading channel breakouts, with background color indicating the long-term trend. Parameter optimization can achieve a balance between efficiency and stability. But over-trading risks require prudence.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|24|DTMA Lenth|
|v_input_2_close|0|DTMA Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-07 00:00:00
end: 2023-04-15 00:00:00
period: 4d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Trader_7ye

//@version=4

strategy(title="T3MA_KC_7ye  Strategy", shorttitle="T3MA_KC_7ye  Strategy",max_bars_back=500,overlay=true,default_qty_type=strategy.percent_of_equity,default_qty_value=100,initial_capital=5000,currency=currency.USD)

t3(src,len)=>
    xe1 = ema(src, len)
    xe2 = ema(xe1, len)
    xe3 = ema(xe2, len)
    xe4 = ema(xe3, len)
    xe5 = ema(xe4, len)
    xe6 = ema(xe5, len)
    b = 0.7
    c1 = -b*b*b
    c2 = 3*b*b+3*b*b*b
    c3 = -6*b*b-3*b-3*b*b*b
    c4 = 1+3*b+b*b*b+3*b*b
    c1 * xe6 + c2 * xe5 + c3 * xe4 + c4 * xe3
    
 
Length = input(title="DTMA Lenth", type=input.integer, defval=24, minval=1)
xPrice = input(title="DTMA Source", type=input.source, defval=close)
T3ma=t3(xPrice,Length)

upCol = T3ma > T3ma[1] 
downCol = T3ma < T3ma[1]


range= high - low
rangema=t3(range,Length)

upper = T3ma + rangema
lower = T3ma - rangema

myColor = upCol ? color.lime : downCol ? color.red : na
plot(T3ma, color=myColor, title="T3 Slow")

c = color.blue
u = plot(upper, color=#0094FF, title="Upper")
l = plot(lower, color=#0094FF, title="Lower")
fill(u, l, color=#0094FF, transp=95, title="Background")
buySignal = upCol and ohlc4>upper
sellSignal= downCol and ohlc4<lower

//=======输出======= 
//多空颜色判断
direction=0
direction:=buySignal?1:sellSignal?-1:direction[1]
macolor=direction==1?color.green:color.red

//多信号处理为一个信号
alertlong = direction!=direction[1] and direction== 1
alertshort= direction!=direction[1] and direction==-1
bgcolor(alertshort ? color.red : alertlong?color.lime:na, transp=20)

if (alertlong)
    strategy.entry("Long", strategy.long)
if (alertshort)
    strategy.entry("Short",strategy.short)
```

> Detail

https://www.fmz.com/strategy/426786

> Last Modified

2023-09-14 15:51:25
