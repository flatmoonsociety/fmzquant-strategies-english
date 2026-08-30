
> Name

Moving-Average-Trend-Following-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/5af453948c8ed3539af885ac7b35eda1ebb9a02939627cd124ad14ca5d6f09dc.png)
[trans]

## Overview
This strategy calculates the moving average and price change rate, combined with the K-line within a certain period, to determine whether it is in an upward trend or a downward trend, and go long or short accordingly.
## Strategy Principle
The strategy first calculates a simple moving average a of length l and a price change rate r of length l. Then calculate the difference k between the current K-line price and the moving average. Finally, calculate the sum of k's K lines in the past s.
When sum>0, it means that it is currently in an upward trend and this strategy will go long. When sum<0, it means that it is currently in a downward trend, and this strategy will go short.
After going long or short, the position will be held until the trend reverses (sum changes from positive to negative or from negative to positive), at which time the position will be closed.
## Advantage Analysis
The biggest advantage of this strategy is its ability to capture trends and is suitable for trend trading. Specifically, there are the following advantages:
1. Using moving averages to determine the overall trend direction can effectively filter market noise and lock in the main trend.
2. Use the Price Change Rate indicator to measure momentum strength to avoid missing out on strong moves.
3. By considering multiple K lines within a certain period, you can judge the trend more accurately and avoid being fooled.
4. As long as the trend remains unchanged, continue to hold positions and enjoy the profits brought by the trending market to the greatest extent.
## Risk Analysis
This strategy mainly involves the following risks:
1. Unable to accurately judge the end time of the trend, you may stop losses early or miss part of the profits.
2. The size of a single loss cannot be effectively controlled, and losses may be larger under extreme market conditions.
3. Improper strategy parameters may lead to too frequent trading or missing some trading opportunities.
4. Long-term positions may face overnight interest and margin risks.
To control risks, you can set stop loss points, trade only highly liquid commodities, optimize parameters, and use leverage appropriately.
## Optimization direction
This strategy can mainly be optimized from the following aspects:
1. Test moving averages and price change rates of different lengths to find the best parameter combination.
2. Try other indicators such as MACD to judge the trend to further improve the accuracy.
3. Add a position management mechanism, such as partial profit taking after profits are made, to control single losses.
4. Set dynamic stop loss combined with volatility indicators to reduce the risk of extreme market conditions.
5. Optimize the logic of opening and closing positions, filter out false breakthroughs and improve trading efficiency.
## Summarize
The overall idea of ​​this strategy is clear and easy to implement. By following the trend for long-term position trading, the drawdown control is relatively reasonable, and it is suitable for investors who pursue stable returns. If mechanisms such as stop loss and position management can be further optimized, better long-term stable returns can be expected.
||


## Overview

This strategy calculates the moving average and price change rate to determine whether the current state is in an uptrend or a downtrend combined with K-lines over a certain period, and accordingly goes long or short.

## Strategy Principle 

This strategy first calculates the simple moving average a of length l and the price change rate r of length l. Then it calculates the difference k between the current K-line price and the moving average. Finally, it calculates the sum sum of k over the past s K-lines.  

When sum>0, it indicates a current uptrend and the strategy will go long. When sum<0, it indicates a current downtrend and the strategy will go short.  

After going long or short, the position will be held until the trend reverses (sum changes from positive to negative or vice versa), then the position will be closed.

## Advantage Analysis

The biggest advantage of this strategy is that it can catch the trend and is suitable for trend trading. Specifically, it has the following advantages:

1. Using the moving average to determine the overall trend direction can effectively filter market noise and lock in the major trend.

2. Applying the price change rate indicator to measure momentum strength avoids missing strong momentum.

3. Taking into account multiple K-lines over a period can more accurately determine the trend and avoid being misled by einzelne Ausreißer. 

4. As long as the trend remains unchanged, continue holding the position to maximize profits from the trending market.

## Risk Analysis

The main risks of this strategy are:

1. Unable to accurately determine the end time of the trend, may stop loss prematurely or miss some profits.  

2. Unable to effectively control the size of single loss, losses may be large in extreme market conditions.

3. Improper strategy parameters may lead to over-frequent trading or missing some trading opportunities.  

4. Long-term holdings may face overnight interest and margin risks.

To control risks, we can set stop loss points, trade only highly liquid products, optimize parameters and reasonably use leverage.

## Optimization Directions

The main aspects to optimize this strategy include:

1. Test moving averages and price change rates of different lengths to find the best parameter combination.

2. Try other indicators such as MACD to better determine the trend and further improve accuracy. 

3. Add position management mechanisms, such as taking profit after making some profits, to control single loss.

4. Incorporate volatility indicators to set dynamic stops to reduce risks in extreme market conditions.

5. Optimize entry and exit logic to filter false breakouts and improve trading efficiency.  

## Conclusion

The overall logic of this strategy is clear and easy to implement. By tracking trends for long-term holding trading, drawdown control is relatively reasonable. It is suitable for investors seeking stable returns. Further optimizing the stop loss and position management can expect good long-term steady returns.

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
start: 2023-12-03 00:00:00
end: 2023-12-10 00:00:00
period: 1m
basePeriod: 1m
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
    strategy.entry("BBandLE", strategy.long, oca_name="BollingerBands",  comment="BBandLE")
else
    strategy.cancel(id="BBandLE")
if sum<0
    strategy.entry("BBandSE", strategy.short, oca_name="BollingerBands",  comment="BBandSE")
else
    strategy.cancel(id="BBandSE")

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

https://www.fmz.com/strategy/434986

> Last Modified

2023-12-11 15:05:31
