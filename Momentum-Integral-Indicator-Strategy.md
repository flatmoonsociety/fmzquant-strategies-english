
> Name

Indicator integration strategy Momentum-Integral-Indicator-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/b48141d6010819465656de479a6cfe5d53e7fe1a3eb2462391de1848c8957d09.png)

[trans]


## Overview
This strategy calculates the difference k between the two indicators ROC and SMA, then sums k over a certain length, and uses the positive or negative sum of the sum as the basis for judging long and short positions. This strategy is a short-term trading strategy.
## Strategy Principle
This strategy first calculates the SMA moving average and ROC indicator of length l, and then calculates the difference k between the current closing price and the SMA. Then calculate the s-day cumulative sum sum of k. Go long when sum>0, go short when sum<0.
Specifically, in the code:
1. Calculate the SMA moving average a of length l
2. Calculate the ROC index r of length l
3. Calculate the difference between the current closing price and the SMA moving average k = close - a
4. Perform s-day cumulative sum on k to get sum
5. If sum>0, go long; if sum<0, go short
6. Conditions for closing a position: sum<0 when closing a long position; sum>0 when closing a short position
The key to this strategy is to calculate the cumulative sum sum of k, and use the positive or negative sum as a trading signal. When k>0 in the recent period, it means that the price is rising, then go long; when k<0 in the recent period, it means the price is falling, then go short.
## Advantage Analysis
This is a relatively simple and practical short-term trading strategy with the following advantages:
1. The indicator combination used is relatively simple and easy to understand and implement.
2. By filtering through the difference in indicators, you can find more accurate trading opportunities.
3. Accumulating and summing the differences can capture short-term trends more accurately.
4. The parameters l and s can be adjusted according to the market to adapt to different cycles.
5. The strategy is clear, the program is concise, and it is easy to modify and optimize.
6. High capital utilization efficiency, enabling frequent short-term transactions.
## Risk Analysis
This strategy also has certain risks, mainly including:
1. Short-term trading is risky and there is a possibility of loss.
2. Improper parameter settings may lead to too frequent transactions or missed opportunities.
3. Unable to effectively respond to trend reversal, skipping stop loss may cause large losses.
4. Frequent monitoring and adjustment of parameters is required, and it relies heavily on trader experience.
5. Frequent transactions can easily increase transaction costs and slippage, affecting profits.
Risk-based solutions include:
1. Adjust parameters appropriately to reduce transaction frequency.
2. Combine with trend indicators to identify trend reversals.
3. Optimize the stop loss strategy and control single losses.
4. Add an automated parameter optimization module to reduce reliance on trader experience.
5. Optimize the order module and reduce transaction costs.
## Optimization direction
This strategy can be further optimized from the following aspects:
1. Optimize the parameter calculation method to make the parameters more adaptive. You can consider using genetic algorithms, Markov chains and other methods to dynamically optimize parameters.
2. Combine more indicators and filter conditions to improve the quality of trading signals. For example, combine trend indicators to avoid contrarian trading, etc.
3. Improve stop loss strategies, such as introducing trailing stop loss, average stop loss, etc., to control single losses.
4. Optimize fund management strategies, such as risk point management, fixed proportion allocation of funds, etc., to control overall risks.
5. Optimize the order module and use algorithms such as trend tracking and slippage control to reduce transaction costs.
6. Add an automated backtest optimization module to quickly evaluate the impact of different parameters on the strategy.
7. Add a quantitative indicator evaluation module to evaluate the quality of trading signals and improve strategy stability.
Through the above optimization, this strategy can be built into a more comprehensive, intelligent, stable and controllable short-term trading system.
## Summarize
Generally speaking, this strategy generates trading signals through simple indicator calculations, has clear ideas and is easy to implement, and is a typical short-term trading strategy. Through further optimization of parameters, stop losses, fund management, etc., risks can be reduced and stability improved, making it one of the quantitative trading strategies worth using. However, no strategy can be perfect. Traders also need to remain rational and make adjustments based on their own risk preferences.
|| 

## Overview

This strategy generates trading signals by calculating the sum of differences between ROC and SMA. It belongs to short-term trading strategies.   

## Strategy Logic

The strategy first calculates SMA with length l and ROC. Then it calculates the difference k between close price and SMA. Next it sums up k for s days and gets sum. When sum>0, it goes long. When sum<0, it goes short.  

Specifically, in the code:

1. Calculate SMA with length l, get a.

2. Calculate ROC with length l, get r.

3. Calculate difference between close price and SMA: k = close - a.

4. Sum up k for s days, get sum.

5. If sum>0, long position; if sum<0, short position.  

6. Exit when sum<0 for long, and sum>0 for short.

The key is to sum up the difference k and use the sign of sum for trading signals. When k>0 for recent days, price is increasing, so go long. When k<0, price is decreasing, so go short.

## Advantage Analysis 

This simple short-term trading strategy has the following advantages:

1. The indicators used are simple and easy to understand. 

2. Filtering by the difference of indicators can find more accurate trading opportunities.

3. Summing up the difference can better capture short-term trends.  

4. The parameters l and s can be adjusted for different cycle.

5. The logic is clear and easy to modify and optimize.

6. High capital utilization efficiency for frequent short-term trading.

## Risk Analysis

There are also some risks:

1. Higher risks in short-term trading, losses are possible.

2. Improper parameters may lead to over-trading or missing opportunities.

3. Hard to adapt to trend reversal, no stop loss may lead to big losses.

4. Frequent adjustment of parameters relies heavily on trader's experience. 

5. High trading frequency may increase transaction costs and slippage.

Solutions:

1. Adjust parameters properly to lower trading frequency.

2. Add trend indicators to identify reversals. 

3. Optimize stop loss to control single trade loss.

4. Add auto parameter optimization to lower dependence on experience.

5. Optimize order execution model to lower transaction costs.

## Optimization Directions

The strategy can be further optimized in the following aspects:

1. Optimize parameter calculation methods, like genetic algorithms, to make parameters adaptive.

2. Add more indicators and filters to improve signal quality.

3. Improve stop loss strategy, like trailing stop loss. 

4. Optimize money management strategies like risk point control.

5. Optimize order execution model with trend following, slippage control etc.

6. Add backtesting and auto optimization modules. 

7. Add quantitative evaluation of signal quality.

With these optimizations, this strategy can become a more comprehensive, intelligent, stable and controllable short-term trading system.

## Summary

In summary, this strategy generates simple signals from indicators, with clear logic and easy implementation. With further optimizations in parameters, stop loss, money management etc., it can become a worthwhile quantitative trading strategy. But no strategy is perfect. Traders still need to apply it rationally based on personal risk preference.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|170|Length for indicator|
|v_input_2|18|Length of summation|
|v_input_3|false|Take Profit|
|v_input_4|false|Stop Loss|
|v_input_5|false|Trailing Stop Loss|
|v_input_6|false|Trailing Stop Loss Offset|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-06 00:00:00
end: 2023-11-05 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("Indicator Integrator Strat",default_qty_type = strategy.percent_of_equity, default_qty_value = 100,currency="USD",initial_capital=662, overlay=false)

l = input(defval=170,title="Length for indicator")
s = input(title="Length of summation",defval=18)
a= sma(close,l)
r=roc(close,l)
k=close-a
sum = 0
for i = 0 to s
    sum := sum + k[i]
//plot(a,color=yellow,linewidth=2,transp=0)
//bc =  iff( sum > 0, white, teal)
//plot(sum,color=bc, transp=20, linewidth=3,style=columns)
//plot(sma(sum,3),color=white)
//hline(0)

inpTakeProfit = input(defval = 0, title = "Take Profit", minval = 0)
inpStopLoss = input(defval = 0, title = "Stop Loss", minval = 0)
inpTrailStop = input(defval = 0, title = "Trailing Stop Loss", minval = 0)
inpTrailOffset = input(defval = 0, title = "Trailing Stop Loss Offset", minval = 0)
useTakeProfit = inpTakeProfit >= 1 ? inpTakeProfit : na
useStopLoss = inpStopLoss >= 1 ? inpStopLoss : na
useTrailStop = inpTrailStop >= 1 ? inpTrailStop : na
useTrailOffset = inpTrailOffset >= 1 ? inpTrailOffset : na

////buyEntry = crossover(source, lower)
////sellEntry = crossunder(source, upper)
if sum>0
    strategy.entry("Long", strategy.long, oca_name="Long",  comment="Long")
else
    strategy.cancel(id="Long")
if sum<0
    strategy.entry("Short", strategy.short, oca_name="Short", comment="Short")
else
    strategy.cancel(id="Short")
strategy.initial_capital = 50000
plot(strategy.equity-strategy.initial_capital-strategy.closedtrades*.25/2, title="equity", color=red, linewidth=2)
hline(0)
//longCondition = sum>0
//exitlong = sum<0

//shortCondition = sum<0
//exitshort = sum>0

//strategy.entry(id = "Long", long=true, when = longCondition)
//strategy.close(id = "Long", when = exitlong)
//strategy.exit("Exit Long", from_entry = "Long", profit = useTakeProfit, loss = useStopLoss, trail_points = useTrailStop, trail_offset = useTrailOffset, when=exitlong)

//strategy.entry(id = "Short", long=false, when = shortCondition)
//strategy.close(id = "Short", when = exitshort)
//strategy.exit("Exit Short", from_entry = "Short", profit = useTakeProfit, loss = useStopLoss, trail_points = useTrailStop, trail_offset = useTrailOffset, when=exitshort)
```

> Detail

https://www.fmz.com/strategy/431249

> Last Modified

2023-11-06 14:40:26
