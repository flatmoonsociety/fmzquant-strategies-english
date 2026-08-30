
> Name

Reversal-Trading-Strategy-Based-on-Multi-Period-RSI
> Author

ChaoZhang

> Strategy Description


[trans]

This article will introduce in detail a quantitative trading strategy that uses the multi-period RSI indicator to determine reversal points. This strategy analyzes multiple RSI indicators simultaneously to identify the formation of market turning points.
1. Strategy Principle
This strategy uses 3 sets of RSI indicators with different parameter settings. The specific logic is as follows:
1. Calculate the RSI values ​​of 2 periods, 7 periods and 14 periods respectively;
2. When RSI-2 is less than 10, RSI-7 is less than 20, and RSI-14 is less than 30, it is judged that a bottom is formed;
3. When RSI-2 is greater than 90, RSI-7 is greater than 80, and RSI-14 is greater than 70, it is judged that a top is formed.
4. Generate buy and sell signals based on the consistency of the RSI indicator.
5. Parameters required for indicator consistency can be preset to control signal frequency.
In this way, the collective analysis of multi-period RSI indicators can improve the accuracy of judgment of reversal points.
2. Strategic advantages
The biggest advantage of this strategy is the use of multi-period RSI indicators for collective analysis, which can improve the accuracy of judgment on key points and filter out false signals.
Another advantage is that you can adjust the consistency parameters to control the trading frequency and adapt to different market environments.
Finally, the combination of RSI with different periods also provides more parameter space for optimization.
3. Potential risks
But this strategy also has the following risks:
First of all, the RSI indicator itself has a lag problem in its judgment of price reversal.
Secondly, the signal judgment caused by the combination of multiple indicators is difficult, and clear filtering rules need to be set.
Finally, reversal trading itself has a certain failure rate, which requires psychological preparation.
4. Content summary
This article introduces in detail a quantitative trading strategy based on the multi-period RSI indicator to identify reversal points. It improves the ability to identify market turning points by judging the consistency of the RSI indicator. But it is also necessary to prevent and control lag problems and signal judgment errors. Overall, it provides an RSI strategy optimization idea with flexible parameters.
||

This article explains in detail a quantitative trading strategy that utilizes multi-period RSI indicators to identify reversal points. It analyzes multiple RSI indicators simultaneously to spot market turning points.

I. Strategy Logic

The strategy employs 3 groups of RSI indicators with different parameters:

1. Calculate RSI values for period 2, 7, and 14 respectively.

2. When RSI-2 is below 10, RSI-7 below 20, and RSI-14 below 30, a bottom is identified.

3. When RSI-2 is above 90, RSI-7 above 80, and RSI-14 above 70, a top is identified. 

4. Generate buy/sell signals based on RSI unanimity. 

5. Preset adjustable parameters for indicator consensus, controlling signal frequency.

By analyzing RSI indicators across periods collectively, reversal point accuracy can be improved.

II. Advantages of the Strategy

The biggest advantage is using multiple timeframe RSI analysis improves identification of key points and filters out false signals.

Another advantage is the flexibility to adjust consensus parameters and adapt to different market environments.

Lastly, the RSI combinations also provide more tuning options.

III. Potential Risks

However, the following risks exist:

Firstly, RSI itself has inherent lag in identifying reversals.

Secondly, multiple indicators introduce signal ambiguity requiring clear rules.

Finally, reversal trades have a failure rate requiring psychological preparation. 

IV. Summary

In summary, this article has explained a quantitative strategy of identifying reversals based on multi-period RSI analysis. It improves recognition of market turning points by judging RSI unanimity. But risks like lagging and wrong signals need to be managed. Overall it provides a flexible RSI strategy optimization approach.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|true|leverage|
|v_input_4|3|Indicators|
|v_input_5|3|accuracy|
|v_input_6|1900|From Year|
|v_input_7|2100|To Year|
|v_input_8|true|From Month|
|v_input_9|12|To Month|
|v_input_10|true|From day|
|v_input_11|31|To day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-06 00:00:00
end: 2023-09-13 00:00:00
period: 45m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro
//2018

//@version=2
strategy(title = "Noro's Triple RSI Top/Bottom v1.1", shorttitle = "3RSI Top/Bottom 1.1", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 0)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(true, defval = true, title = "Short")
leverage = input(1, defval = 1, minval = 1, maxval = 100, title = "leverage")
indi = input(3, defval = 3, minval = 1, maxval = 3, title = "Indicators")
accuracy = input(3, defval = 3, minval = 1, maxval = 10, title = "accuracy")
fromyear = input(1900, defval = 1900, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To day")

//RSI-2
fastup = rma(max(change(close), 0), 2)
fastdown = rma(-min(change(close), 0), 2)
fastrsi = fastdown == 0 ? 100 : fastup == 0 ? 0 : 100 - (100 / (1 + fastup / fastdown))

//RSI-7
middleup = rma(max(change(close), 0), 7)
middledown = rma(-min(change(close), 0), 7)
middlersi = middledown == 0 ? 100 : middleup == 0 ? 0 : 100 - (100 / (1 + middleup / middledown))

//RSI-14
slowup = rma(max(change(close), 0), 14)
slowdown = rma(-min(change(close), 0), 14)
slowrsi = slowdown == 0 ? 100 : slowup == 0 ? 0 : 100 - (100 / (1 + slowup / slowdown))

//Body
body = abs(close - open)
abody = sma(body, 10)

//Signals
acc = 10 - accuracy
signalup1 = fastrsi < (5 + acc) ? 1 : 0
signalup2 = middlersi < (10 + acc * 2) ? 1 : 0
signalup3 = slowrsi < (15 + acc * 3) ? 1 : 0

signaldn1 = fastrsi > (95 - acc) ? 1 : 0
signaldn2 = middlersi > (90 - acc * 2) ? 1 : 0
signaldn3 = slowrsi > (85 - acc * 3) ? 1 : 0

up = signalup1 + signalup2 + signalup3 >= indi
dn = signaldn1 + signaldn2 + signaldn3 >= indi
exit = ((strategy.position_size > 0 and close > open) or (strategy.position_size < 0 and close < open)) and body > abody / 3

//Trading
lot = strategy.position_size == 0 ? strategy.equity / close * leverage : lot[1]

if up
    if strategy.position_size < 0
        strategy.close_all()
        
    strategy.entry("Bottom", strategy.long, needlong == false ? 0 : lot)

if dn
    if strategy.position_size > 0
        strategy.close_all()
        
    strategy.entry("Top", strategy.short, needshort == false ? 0 : lot)
    
if time > timestamp(toyear, tomonth, today, 23, 59) or exit
    strategy.close_all()
```

> Detail

https://www.fmz.com/strategy/426855

> Last Modified

2023-09-14 20:42:55
