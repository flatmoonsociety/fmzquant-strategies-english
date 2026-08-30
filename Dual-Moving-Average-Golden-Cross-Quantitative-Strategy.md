
> Name

Dual-Moving-Average-Golden-Cross-Quantitative-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/18baf10de60f52273b4.png)
[trans]

## Overview
This strategy determines price trends and trading opportunities by calculating the intersection of double moving averages. When the fast line crosses the slow line, it is considered a golden cross, and you go long; when the fast line crosses the slow line, it is considered a death cross, and you go short. At the same time, combine the volume and energy indicators to determine the true crossover and avoid false signals.
## Strategy Principle
This strategy is mainly based on the following principles:
1. Calculate two sets of moving averages with different parameters, one group responds quickly to price changes, and the other group is relatively slow. When the fast line crosses the slow line, it indicates that the price has started an upward trend; when the fast line crosses the slow line, it indicates that the price has started to fall.
2. When the moving average crosses, then detect changes in the energy indicator. If the volume and energy indicators break through simultaneously, it means that the cross signal is credible; if the volume and energy indicators do not break through correspondingly, it may be a false signal.
3. Enter a long or short position based on the cross direction and volume judgment. And set profit-taking conditions to stop profit when the profit reaches a certain proportion.
Specifically, the strategy determines the price trend by calculating the crossover of the 7-day double moving average; calculates the volume change indicator to determine the reliability of the crossover signal; when the reliable signal is determined, press SIGNAL to go long or short; set profit conditions to achieve take-profit.
## Advantage Analysis
The main advantages of this strategy are:
1. Combine the double moving average to determine the trend direction, and combine the volume and energy indicators to filter out false signals to avoid being trapped.
2. Only enter the market when the energy indicator is confirmed to increase the success rate.
3. Set profit-taking conditions and stop profits in time to avoid losing money after making money.
## Risk Analysis
The main risks of this strategy are:
1. The moving average crossover is delayed and it is easy to miss the best opportunity for price changes. Parameters can be optimized appropriately to make the moving average more sensitive.
2. It is difficult to judge when there are differences in quantity and energy indicators. More auxiliary indicators can be introduced for confirmation.
3. Unreasonable setting of the profit stop point may lead to ultra-short-term or ultra-long-term operations. Take profit parameters should be tested and optimized.
## Optimization direction
This strategy can be optimized in the following directions:
1. Optimize the moving average cycle parameters to make it more sensitive and capture price changes in a timely manner.
2. Add more indicators for signal confirmation, such as MACD, KD, etc., to avoid misjudgments in energy indicators. 
3. Combine with more take-profit strategies, such as moving take-profit, percentage take-profit, shock take-profit, etc., to achieve dynamic take-profit.
4. Add automatic stop loss strategy to control single loss.
5. Optimize position management and adjust strategic positions under different market environments.
## Summarize
Overall, the core idea of ​​this strategy is to determine the trend when the two moving averages cross, and the volume and energy indicators filter the signals. The effect is relatively stable and easy to implement. By further optimizing parameters, adding signal filtering and take-profit/stop-loss strategies, the strategy can be made more reliable and intelligent, with high practical value.
||

## Overview

This strategy judges price trends and trading opportunities by calculating dual moving average crossovers. When the fast MA crosses above the slow MA, it is considered a golden cross to go long. When the fast MA crosses below the slow MA, it is considered a death cross to go short. At the same time, combine the Volume Indicator to judge the reliability of crossovers to avoid false signals.

## Strategy Principle  

The core principles of this strategy are:

1. Calculate two groups of moving averages with different parameters, one group responds quickly to price changes and the other reacts relatively slowly. When the fast MA crosses above the slow MA, it signals an upward price trend. When the fast MA crosses below the slow MA, it signals a downward price trend.

2. When the MAs cross, check the change of the Volume Indicator. If the Volume Indicator also breaks through significantly, the crossover signal is reliable. If there is no corresponding breakout in Volume, it may be a false signal.

3. Enter long or short positions based on the crossover direction and volume judgment. Set take profit criteria to close positions when reaching a certain profit level.

Specifically, the strategy judges price trends using 7-period dual MAs crossover. It uses Volume indicators to check signal reliability. When getting reliable signals, it goes long or short per the SIGNAL. It sets profit targets to take profits.

## Advantage Analysis

The main advantages of this strategy are:

1. Combining dual MAs to determine trend direction and Volume filter to avoid false signals and being trapped.

2. Only taking positions when Volume confirms, increasing success rate.  

3. Having profit taking mechanism to take profits in time and avoid giving back profits.

## Risk Analysis

The main risks of this strategy are: 

1. MA crossover delay may miss best opportunity. Can optimize parameters to make MAs more sensitive.

2. Hard to judge when Volume diverges. Can add more indicators for confirmation. 

3. Improper stop profit setting may lead to over trading or holding winners too long. Need to test and optimize stop profit parameters.

## Optimization Directions

The strategy can be optimized from the following aspects:

1. Optimize MA periods to make it more responsive to catch price changes in time.

2. Add more indicators such as MACD, KD for signal confirmation to avoid Volume false signals.

3. Incorporate more profit taking mechanics like trail stop, percentage stop, volatility stop for dynamic profit taking.

4. Add stop loss mechanism to control single trade loss amount. 

5. Optimize position sizing adaptable to different market environments.

## Conclusion

In conclusion, the core idea of this strategy is using dual MA crossover for trend and Volume filter for signal reliability. It is stable and easy to implement. Further optimizations on parameters, signal filtering, profit taking and stop loss can make it more reliable and intelligent for practical trading.

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
start: 2022-12-19 00:00:00
end: 2023-12-25 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("ZendicatoR", overlay=true, calc_on_order_fills= true, calc_on_every_tick=true, default_qty_type=strategy.percent_of_equity, default_qty_value=15, pyramiding=0)
dt = input(defval=0.0010, title="Decision Threshold", type=float, step=0.0001)
keh=input(title="Double HullMA Cross",defval=7, minval=1)
che1=input(title="MA 1",defval=34,minval=1)
che2=input(title="MA 2",defval=144,minval=1)
che3=input(title="MA 3",defval=377,minval=1)
amnt=input(title="TP ($)",defval=4200,minval=1)
wma1=wma(close,che1)
wma2=wma(close,che2)
wma3=wma(close,che3)
sma1=sma(close,11)
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
Q=n1>n2?blue:yellow
plot(sma1,style=line,color=Q,linewidth=4)
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

https://www.fmz.com/strategy/436646

> Last Modified

2023-12-26 15:52:13
