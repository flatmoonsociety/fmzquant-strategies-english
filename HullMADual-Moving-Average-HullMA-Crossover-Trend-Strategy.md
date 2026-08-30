
> Name

Dual-Moving-Average-HullMA-Crossover-Trend-Strategy Dual-Moving-Average-HullMA-Crossover-Trend-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/4295afe8c289b1f282ec578e5fb602c1b0cde66b4ad2762ccb02d27a096341b4.png)
[trans]
## Overview
The Double Moving Average HullMA crossover trend strategy is a trend following strategy based on double moving average crossovers. It uses weighted moving averages (WMA) to build a dual moving average system and generates trading signals when they cross. This strategy also combines price breakthrough judgment to further filter signals.
## Strategy Principle
The double moving average HullMA cross trend strategy uses three WMA lines with different periods, including wma1, wma2 and wma3. Wma2 and wma3 construct a double moving average system. When wma2 crosses wma3 above, it is a bullish signal, and when wma2 crosses below wma3, it is a bearish signal. wma1 is the auxiliary judgment line.
This strategy additionally uses Hull moving average to enhance signal judgment. Specifically, it calculates the difference between twice the 2-day weighted moving average n2ma and the n-day weighted moving average nma, and measures the change in the difference value. A bullish signal is confirmed only when the difference rises, and a bearish signal is confirmed when the difference falls.
This strategy also incorporates price determination. Only when the price is higher than the previous day's price will the bullish signal be confirmed and a long order will be generated. Only when the price is lower than the previous day's price will the bearish signal be confirmed and a short order will be generated.
## Advantage Analysis
The double moving average HullMA crossover trend strategy combines double moving average crossover and price determination, which can effectively filter out false signals, which is its biggest advantage. In addition, this strategy uses three moving averages of different periods to capture trends at different levels and can enter the market at the early stage of the trend. Its stop-loss liquidation method is also relatively stable and reliable.
## Risk Analysis
As a trend following strategy, the double moving average HullMA cross trend strategy is prone to higher number of transactions and slippage losses in the consolidation market. Additionally, the double moving average crossover system is too sensitive and may send false signals on the sideways. It is recommended to adjust the moving average parameters appropriately or add additional filtering conditions.
## Optimization direction
The double moving average HullMA cross trend strategy can be optimized from the following aspects:
1. Optimize moving average parameters and find the optimal parameter combination
2. Add filters such as trading volume or volatility to eliminate false breakthroughs
3. Combine with other indicators as auxiliary judgment to improve signal quality
4. Dynamically optimize moving average cycle parameters
## Summarize
The double moving average HullMA cross trend strategy is overall a stable and reliable trend following strategy. It combines double moving average crossovers and price determination to produce high-quality signals. By optimizing parameters and adding filters, false signals can be further reduced, resulting in better strategy performance. This strategy is suitable for capturing medium and long-term trends and is a good choice for quantitative trading.
||

## Overview

The Dual Moving Average HullMA Crossover Trend strategy is a trend-following strategy based on the crossover of dual moving averages. It builds a dual moving average system using Weighted Moving Average (WMA) lines and generates trading signals when they cross over. The strategy also incorporates price breakout validation to further filter the signals.

## Strategy Logic

The Dual Moving Average HullMA Crossover Trend strategy employs three WMA lines with different periods, including wma1, wma2, and wma3. The wma2 and wma3 construct the dual moving average system. The wma2 crossing above wma3 gives bullish signals, while the wma2 crossing below wma3 gives bearish signals. The wma1 serves as an auxiliary reference line.

Additionally, the strategy utilizes the Hull Moving Average to strengthen signal validation. Specifically, it calculates the difference between 2-period WMA doubled (n2ma) and n-period WMA (nma). Only when the difference rises will bull signals be confirmed valid. Only when the difference falls will bear signals be confirmed valid. 

The strategy also incorporates price validation. Only when the price is higher than the previous day will bull signals be confirmed valid for long orders. Only when the price is lower than the previous day will bear signals be confirmed valid for short orders.

## Advantage Analysis 

The Dual Moving Average HullMA Crossover Trend strategy combines dual moving average crossover and price validation, which allows it to effectively filter out false signals. This is its biggest strength. Also, with three moving average lines of various periods, the strategy can capture trends of different levels early on. Its stop loss mechanism is quite stable and reliable as well.

## Risk Analysis

As a trend-following strategy, the Dual Moving Average HullMA Crossover Trend strategy can generate relatively more trades and slippage costs during range-bound markets. Additionally, dual moving average crossover systems tend to be too sensitive and may emit incorrect signals during sideways trends. It is advisable to tune the moving average parameters or impose additional filters accordingly. 

## Optimization Directions

The Dual Moving Average HullMA Crossover Trend strategy can be improved in the following aspects:

1. Optimize the moving average parameters to find the best parameter combination

2. Add filters like volume or volatility to eliminate false breakouts 

3. Incorporate other indicators as supplementary validation to improve signal quality

4. Dynamically optimize moving average period parameters

## Summary 

In summary, the Dual Moving Average HullMA Crossover Trend strategy is a stable and reliable trend-following strategy. It produces high-quality signals by combining dual moving average crossover and price validation. Through parameter tuning and adding filters, it can further reduce incorrect signals and achieve better performance. It is suitable for catching medium- to long-term trends and a solid choice for quantitative trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0.001|Decision Threshold|
|v_input_2|7|Double HullMA Cross|
|v_input_3|34|MA 1|
|v_input_4|144|MA 2|
|v_input_5|377|MA 3|
|v_input_6|4200|TP ($)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-02-25 00:00:00
end: 2024-02-25 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("ZendicatoR", overlay=true)
dt = input(defval=0.0010, title="Decision Threshold", type=float, step=0.0001)
keh=input(title="Double HullMA Cross",defval=7, minval=1)
che1=input(title="MA 1",defval=34,minval=1)
che2=input(title="MA 2",defval=144,minval=1)
che3=input(title="MA 3",defval=377,minval=1)
amnt=input(title="TP ($)",defval=4200,minval=1)
wma1=wma(close,che1)
wma2=wma(close,che2)
wma3=wma(close,che3)
tms=10000000000000
A=request.security(syminfo.tickerid, 'D', close)*tms
B=request.security(syminfo.tickerid, 'D', close[1])*tms
C=A>B?green:red
D=wma2>wma3?green:red
plot(wma1,style=line,color=C,linewidth=4)
p1=plot(wma2,style=line,color=D)
p2=plot(wma3,style=line,color=D)
fill(p1, p2, color=D, transp=75)
n2ma=2*wma(close,round(keh/2))
nma=wma(close,keh)
diff=n2ma-nma,sqn=round(sqrt(keh))
n2ma1=2*wma(close[2],round(keh/2))
nma1=wma(close[2],keh)
diff1=n2ma1-nma1,sqn1=round(sqrt(keh))
n1=wma(diff,sqn)*tms
n2=wma(diff1,sqn)*tms
closelong = A*tms<B*tms and n2*tms>n1*tms and strategy.openprofit>amnt
if (closelong)
    strategy.close("Long")
closeshort = A*tms>B*tms and n1*tms>n2*tms and strategy.openprofit>amnt
if (closeshort)
    strategy.close("Short") 
longCondition = A*tms>B*tms and n1*tms>n2*tms
if (longCondition)
    strategy.entry("Long",strategy.long)
shortCondition = A*tms<B*tms and n1*tms<n2*tms
if (shortCondition)
    strategy.entry("Short",strategy.short)
```

> Detail

https://www.fmz.com/strategy/442817

> Last Modified

2024-02-26 11:21:45
