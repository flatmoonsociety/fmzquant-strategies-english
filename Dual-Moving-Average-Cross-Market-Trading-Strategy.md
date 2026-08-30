
> Name

Dual-Moving-Average-Cross-Market-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/cd5a026721f879a94b.png)

[trans]


## Overview
This strategy combines the advantages of Hull Moving Average and T3 Moving Average to design a cross-market trading strategy. This strategy can be used for both short-term trading and medium- and long-term trend tracking. By calculating the average value of the Hull moving average and the T3 moving average as the main trading signal line, the entry and exit timings are judged based on changes in their directions.
## Strategy Principle
This strategy is mainly based on the calculation of Hull Moving Average and T3 Moving Average.
Hull Moving Average (HMA) can effectively filter market noise and show a smooth curve of price trends through the iterative calculation method of weighted moving average. It is more sensitive to price changes than the simple moving average and the exponential moving average, and can also effectively suppress false breakthroughs.
While reducing the hysteresis effect, the T3 moving average can make the moving average closer to the price through certain hyperparameter adjustments. It can respond to price changes more quickly through multiple exponential smoothing calculations.
This strategy calculates the average of the two as the main trading indicator. Determine the timing of entry based on the direction of the average: if the average of the current period is higher than the previous period, it is a long entry signal; if the average of the current period is lower than the previous period, it is a short entry signal.
Regarding the exit rules, if the price breaks through the stop loss point or reaches the take profit point, the exit will be exited; if the direction of the average line changes, the exit action will also be executed.
## Advantage Analysis
This strategy combines the advantages of the Hull Moving Average and the T3 Moving Average, which can both smooth and denoise and respond quickly to price changes, thereby generating a comprehensive indicator. Secondly, this strategy is suitable for both short-term and medium- and long-term transactions. By adjusting the calculation cycle parameters, the applicable trading cycle can be flexibly adjusted. Furthermore, this strategy uses trailing stop loss and trailing take profit settings, which can lock in profits and control risks.
## Risk Analysis
This strategy mainly relies on moving average indicators, which may produce multiple false signals during a volatile trend. In addition, the moving average has a certain lag and may miss the best entry point for price changes. You need to be careful when setting stop loss and profit points to avoid being too loose or too tight. Finally, optimization parameters need to be tested for different currencies and transaction cycles and cannot be reused directly.
## Optimization direction
You can consider adding other auxiliary indicators, such as strength indicators, volatility indicators, etc., to verify moving average signals and filter out false signals. You can test different moving average combinations and weighting algorithms to optimize the effect of generating moving average signals. Adaptive stop loss and trailing take profit can be added to dynamically manage risk. Backtest optimization can be performed for different currencies and trading cycles to find the best parameter combination.
## Summarize
This strategy integrates the advantages of the Hull Moving Average and the T3 Moving Average to form a comprehensive indicator to determine the trend direction. Through parameter optimization, the strategy can be flexibly applied to different trading cycles. The strategy has certain advantages, but there are also problems such as following lag and generating false signals. By adding other auxiliary indicators, optimizing parameters and dynamic stop loss and profit, the strategy can be continuously optimized and improved to obtain better results.
||

## Overview

This strategy combines the advantages of Hull moving average and T3 moving average to design a cross-market trading strategy. It can be used for both short-term trading and long-term trend tracking. By calculating the mean value of Hull moving average and T3 moving average as the main trading signal line, it determines entry and exit points based on the directional changes.

## Strategy Logic

The strategy is mainly based on the calculation of Hull moving average and T3 moving average. 

The Hull Moving Average (HMA) uses a weighted moving average iterative calculation method to effectively filter out market noise and display a smooth price trend curve. It is more sensitive to price changes than simple moving averages and exponential moving averages, while also effectively suppressing false breakouts.

The T3 moving average responds faster to price changes while reducing lag by adjusting parameters. Through multiple exponential smoothing calculations, it can quickly respond to price changes.

This strategy takes the average of the two as the main trading indicator. It judges entry timing according to the direction of this average line: if the current period's average is higher than the previous period, it is a long entry signal; if lower, it is a short entry signal.

For exit rules, if the price breaks through the stop loss or take profit point, exit; also exit when the moving average direction changes.

## Advantage Analysis 

This strategy combines the advantages of Hull moving average and T3 moving average to generate a comprehensive indicator. Next, this strategy is suitable for both short-term and long-term trading by adjusting the cycle parameter. Also, it adopts dynamic stop loss and take profit to lock in profits and control risks.

## Risk Analysis

The strategy relies mainly on the moving average indicator, which may generate multiple false signals in ranging trends. In addition, the lagging of moving averages may miss the best entry timing. The stop loss and take profit points need careful setting to avoid being too loose or too tight. Finally, parameters need optimization for different currencies and timeframes.

## Optimization

Consider adding other indicators to verify the MA signal and filter out false signals. Test different MA combinations and weighting algorithms to optimize the MA signal. Add adaptive stop loss and trailing take profit to dynamically manage risks. Conduct backtesting optimization on different currencies and timeframes to find the optimal parameter sets.  

## Summary

This strategy integrates the strengths of Hull moving average and T3 moving average to form a comprehensive indicator for judging trend direction. Through parameter optimization, the strategy can be flexibly applied to different trading cycles. The strategy has certain advantages but also problems like lagging and false signals. By adding other indicators, optimizing parameters and dynamic stops, it can be continuously improved for better results.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|From Day|
|v_input_2|true|From Month|
|v_input_3|2000|From Year|
|v_input_4|31|To Day|
|v_input_5|12|To Month|
|v_input_6|2021|To Year|
|v_input_7|50|Length MAs|
|v_input_8|0.08|TP Long|
|v_input_9|true|SL Long|
|v_input_10|0.03|TP Short|
|v_input_11|0.06|SL Short|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-23 00:00:00
end: 2023-10-23 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © exlux99

//@version=4


strategy(title="Swing HULL + T3 avg", shorttitle="Swing HULL T3 AVG", overlay=true)

fromDay = input(defval = 1, title = "From Day", minval = 1, maxval = 31)
fromMonth = input(defval = 1, title = "From Month", minval = 1, maxval = 12)
fromYear = input(defval = 2000, title = "From Year", minval = 1970)
 //monday and session 
// To Date Inputs
toDay = input(defval = 31, title = "To Day", minval = 1, maxval = 31)
toMonth = input(defval = 12, title = "To Month", minval = 1, maxval = 12)
toYear = input(defval = 2021, title = "To Year", minval = 1970)

startDate = timestamp(fromYear, fromMonth, fromDay, 00, 00)
finishDate = timestamp(toYear, toMonth, toDay, 00, 00)
time_cond = true



////////////////////////////GENERAL INPUTS//////////////////////////////////////

length_Ma= input(defval=50, title="Length MAs", minval=1)

//==========HMA
getHULLMA(src, len) =>
    hullma = wma(2*wma(src, len/2)-wma(src, len), round(sqrt(len)))
    hullma

//==========T3
getT3(src, len, vFactor) =>
    ema1 = ema(src, len)
    ema2 = ema(ema1,len)
    ema3 = ema(ema2,len)
    ema4 = ema(ema3,len)
    ema5 = ema(ema4,len)
    ema6 = ema(ema5,len)
    c1 = -1 * pow(vFactor,3)
    c2 = 3*pow(vFactor,2) + 3*pow(vFactor,3)
    c3 = -6*pow(vFactor,2) - 3*vFactor - 3*pow(vFactor,3)
    c4 = 1 + 3*vFactor + pow(vFactor,3) + 3*pow(vFactor,2)
    T3 = c1*ema6 + c2*ema5 + c3*ema4 + c4*ema3
    T3





hullma = getHULLMA(close,length_Ma)

t3 = getT3(close,length_Ma,0.7)


avg = (hullma+t3) /2


////////////////////////////PLOTTING////////////////////////////////////////////


colorado = avg > avg[1]? color.green : color.red

plot(avg , title="avg", color=colorado, linewidth = 4)

long=avg>avg[1]
short=avg<avg[1]

tplong=input(0.08, title="TP Long", step=0.01)
sllong=input(1.0, title="SL Long", step=0.01)

tpshort=input(0.03, title="TP Short", step=0.01)
slshort=input(0.06, title="SL Short", step=0.01)


if(time_cond)
    strategy.entry("long",1,when=long)
    strategy.exit("closelong", "long" , profit = close * tplong / syminfo.mintick, loss = close * sllong / syminfo.mintick, alert_message = "closelong")
    
    strategy.entry("short",0,when=short)
    strategy.exit("closeshort", "short" , profit = close * tpshort / syminfo.mintick, loss = close * slshort / syminfo.mintick, alert_message = "closeshort")

```

> Detail

https://www.fmz.com/strategy/430067

> Last Modified

2023-10-24 16:55:38
