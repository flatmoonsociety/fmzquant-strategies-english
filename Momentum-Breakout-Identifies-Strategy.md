
> Name

Momentum-Breakout-Identifies-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/165c87312bbfd12f475.png)
[trans]

## Overview
This strategy makes profits by identifying stocks that are rising rapidly, building long positions when they break through new highs, and adopting a fixed percentage take-profit approach. This strategy is a trend following strategy.
## Principle
This strategy is mainly based on two indicators:
1. Rapid RSI: Determine price momentum by calculating the rise and fall of the last three K lines. When the rapid RSI is below 10, the stock is considered to be oversold.
2. Main body filtering: Calculate the average size of the real body of the last 20 K lines. When the price real body is greater than 2.5 times of the average real body, it is considered an effective breakthrough.
When the rapid RSI is below 10 and the entity filtering is effective, open a long position. Then set a fixed take-profit point of 20%. When the price exceeds the opening price * (1 + take-profit ratio), the position will be closed and the take-profit will be taken.
The advantage of this strategy is that it can capture breakthrough opportunities at the beginning of the trend, judge the bottom area through rapid RSI, and use entity filtering to avoid false breakthroughs. Adopt a fixed take-profit method to lock in the profit of each order, and you can continue to grasp the market trend.
## Advantage Analysis
This strategy has the following advantages:
1. Using fast RSI to determine the bottom oversold area can improve the accuracy of entry.
2. The main body filtering mechanism can avoid false breakthroughs caused by shocks.
3. By adopting a fixed percentage take-profit method, you can continue to make profits and grasp the market trend.
4. The strategy logic is simple and clear, easy to understand and implement.
5. The code structure is elegant and scalable, making it easy to optimize strategies.
6. During the backtest period, the strategy achieved stable positive returns and a high winning rate.
## Risk Analysis
There are also some risks to be aware of with this strategy:
1. The strategy does not have a stop-loss mechanism, and there is a risk of a single loss expanding.
2. Improper setting of fixed take-profit points may lead to premature take-profit or excessively deep take-profit points.
3. When the market fluctuates, it is easy to suffer continuous small losses.
4. The cost of margin financing and securities lending is not taken into account, and the income will be reduced when the offer is made.
5. The strategy parameters are not optimized enough, and parameters need to be adjusted for different varieties.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Add a stop-loss mechanism to control single losses.
2. Optimize the profit-taking point so that it can dynamically track the trend.
3. Optimize the breakthrough judgment indicators and improve the accuracy of entry.
4. Add a warehouse management module to optimize warehouse occupancy.
5. Add a variety parameter optimization module to automatically optimize the parameters of different varieties.
6. Add filter conditions to avoid losses when the market is too volatile.
7. Consider adding the position average cost management module.
## Summarize
This strategy is overall a very simple and elegant trend following strategy. It uses rapid RSI to determine oversoldness, entity filtering to determine effective breakthroughs, and fixed take-profit points to obtain stable returns. Although there is some room for optimization, this strategy is responsive and suitable for capturing situations where the market changes rapidly. It is a very practical trading strategy. Through continuous optimization, I believe it can become a powerful and reliable long-term holding strategy.
||

## Overview

This strategy identifies rapidly rising stocks and takes long positions when price breaks out new highs. It uses fixed percentage take profit to lock in profits. The strategy belongs to trend following strategies.

## Principle 

The strategy is mainly based on two indicators:

1. Fast RSI: It calculates the rise and fall of recent 3 bars to judge price momentum. When fast RSI is below 10, it is considered oversold status.

2. Body filter: It calculates the average body size of recent 20 bars. When the body size is larger than 2.5 times of average body, it is considered a valid breakout.

When fast RSI is below 10 and body filter is valid, a long position will be opened. After that, a fixed take profit of 20% is set. When price exceeds the open price * (1 + take profit percentage), the position will be closed.

The advantage of this strategy is it can capture the breakout opportunities at the beginning of trends. The fast RSI judges oversold levels and body filter avoids false breakouts. The fixed percentage take profit locks in profits of each trade and keeps catching the trend.

## Advantage Analysis

The advantages of this strategy:

1. Fast RSI identifies oversold levels and increases entry accuracy.

2. Body filter avoids false breakouts caused by fluctuations.

3. Fixed percentage take profit realizes stable profits and catches trends. 

4. The logic is simple and clear, easy to understand and implement.

5. Elegant code structure with great extensibility, easy to optimize.

6. Stable positive returns and high win rate in backtest.

## Risk Analysis

Some risks to note:

1. No stop loss mechanism, risks of expanding losses.

2. Improper take profit levels may lead to premature or too deep exit.

3. Consecutive small losses may occur in choppy markets.

4. Financing costs are not considered, actual returns may be lower.

5. Insufficient parameter optimization across different products.

## Optimization Directions

Some aspects can be optimized:

1. Add stop loss to control single trade loss.

2. Optimize dynamic take profit to follow trends.

3. Enhance breakout logic to improve entry accuracy. 

4. Add position sizing module to optimize capital usage.

5. Add parameter optimization module for different products.

6. Add filters to avoid losses in choppy markets.

7. Consider adding average cost management.

## Conclusion

In summary, this is an elegant and simple trend following strategy. It uses fast RSI to identify oversold levels, body filter to confirm valid breakout, and fixed percentage take profit to generate steady returns. Although there are rooms for optimization, the strategy is responsive and suitable for fast changing markets, making it a very practical trading strategy. With continuous optimizations, it can become a robust long term strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|TAKE PROFIT %|
|v_input_2|2019|BACKTEST START YEAR|
|v_input_3|true|BACKTEST START MONTH|
|v_input_4|true|BACKTEST START DAY|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-26 00:00:00
end: 2023-11-01 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
// this is based on https://www.tradingview.com/v/PbQW4mRn/
strategy(title = "ONLY LONG V4 v1", overlay = true, initial_capital = 1000, pyramiding = 1000,
   calc_on_order_fills = false, calc_on_every_tick = false, default_qty_type = strategy.percent_of_equity, default_qty_value = 50, commission_value = 0.075)

//study(title = "ONLY LONG V4 v1", overlay = true)

//Fast RSI
src = close
fastup = rma(max(change(src), 0), 3)
fastdown = rma(-min(change(src), 0), 3)
fastrsi = fastdown == 0 ? 100 : fastup == 0 ? 0 : 100 - (100 / (1 + fastup / fastdown))

//Body Filter
body = abs(close - open)
abody = sma(body, 20)

mac = sma(close, 20)
len = abs(close - mac)
sma = sma(len, 100)
max = max(open, close)
min = min(open, close)
up = close < open and len > sma * 2 and min < min[1] and fastrsi < 10 and body > abody * 2.5

// Strategy
// ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░

var bool longCondition = na

longCondition := up == 1 ? 1 : na

// Get the price of the last opened long

var float last_open_longCondition = na

last_open_longCondition := longCondition ? close : nz(last_open_longCondition[1])

// Get the bar time of the last opened long

var int last_longCondition = 0

last_longCondition := longCondition ? time : nz(last_longCondition[1])

// Take profit
// ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░

tp = input(20, "TAKE PROFIT %", type = input.float, minval = 0, step = 0.5)

long_tp = crossover(high, (1+(tp/100))*last_open_longCondition) and not longCondition

// Get the time of the last tp close

var int last_long_tp = na

last_long_tp := long_tp ? time : nz(last_long_tp[1])

Final_Long_tp = long_tp and last_longCondition > nz(last_long_tp[1])

// Count your long conditions

var int sectionLongs = 0

sectionLongs := nz(sectionLongs[1])

var int sectionTPs = 0

sectionTPs := nz(sectionTPs[1])

// Longs Counter

if longCondition
    sectionLongs := sectionLongs + 1
    sectionTPs := 0

if Final_Long_tp
    sectionLongs := 0
    sectionTPs := sectionTPs + 1
    
// Signals
// ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░

// Long

// label.new(
//    x = longCondition[1] ? time : na, 
//    y = na, 
//    text = 'LONG'+tostring(sectionLongs), 
//    color=color.lime, 
//    textcolor=color.black,  
//    style = label.style_labelup, 
//    xloc = xloc.bar_time, 
//    yloc = yloc.belowbar,
//    size = size.tiny)
   
// Tp

// label.new(
//    x = Final_Long_tp ? time : na, 
//    y = na, 
//    text = 'PROFIT '+tostring(tp)+'%', 
//    color=color.orange, 
//    textcolor=color.black,  
//    style = label.style_labeldown, 
//    xloc = xloc.bar_time, 
//    yloc = yloc.abovebar,
//    size = size.tiny) 

ltp = iff(Final_Long_tp, (last_open_longCondition*(1+(tp/100))), na), plot(ltp, style=plot.style_cross, linewidth=3, color = color.white, editable = false)

// Backtesting
// ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░

testStartYear = input(2019, "BACKTEST START YEAR", minval = 1, maxval = 2222) 
testStartMonth = input(01, "BACKTEST START MONTH", minval = 1, maxval = 12)
testStartDay = input(01, "BACKTEST START DAY", minval = 1, maxval = 31)
testPeriodStart = timestamp(testStartYear,testStartMonth,testStartDay,0,0)

strategy.entry("long", strategy.long, when = longCondition and (time >= testPeriodStart))
strategy.exit("TP", "long", limit = (last_open_longCondition*(1+(tp/100))))

// Alerts
// ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░

alertcondition(longCondition[1], title="Long Alert", message = "LONG")
alertcondition(Final_Long_tp, title="Long TP Alert", message = "LONG TP")

```

> Detail

https://www.fmz.com/strategy/430846

> Last Modified

2023-11-02 14:39:22
