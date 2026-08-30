
> Name

Dual-Moving-Average-Stop-Loss-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/df890d70efbf0b2e2e.png)

[trans]

## Overview
This strategy is a stop-loss strategy based on dual moving averages. It uses two moving averages, one as the main average and one as the stop loss line. Go long when the price is above the main moving average, close the long position when the price is below the stop loss line; go short when the price is below the main moving average, and close the short position when the price is above the stop loss line. By dynamically adjusting the price of long and short positions, stop loss and stop profit are achieved.
## Strategy Principle
This strategy uses the sma function to calculate a simple moving average of length len as the main moving average ma. Then based on the long stop loss percentage elpercent and short stop loss percentage espercent input by the user, the long stop loss line el and the short stop loss line es are calculated. The specific calculation formula is:
el = ma + (ma * elpercent / 100)
es = ma + (ma * espercent / 100) 

Among them, elpercent and espercent respectively represent the percentage of deviation from the main moving average.
In this way, three lines are obtained: the main moving average ma, the long stop loss line el, and the short stop loss line es.
The trading logic of the strategy is:
If the closing price is higher than the long stop loss line el, open a long position; if the closing price is lower than the short stop loss line es, close the long position.
If the closing price is lower than the short stop loss line es, a short position will be opened; if the closing price is higher than the long stop loss line el, the short position will be closed.
## Strategic Advantages
1. Use double moving averages to set stop loss and profit points, which can effectively control risks.
2. The length of the main moving average len and the offset percentages elpercent and espercent can be customized. The parameters can be adjusted for different markets and are highly adaptable.
3. Use a stop-loss mechanism to stop losses in time and avoid further losses.
4. The strategic ideas are simple and clear, easy to understand and implement, and suitable for novices to learn.
5. You can go long and short at the same time and make full use of the two-way market.
## Risks and Solutions
1. Backtest data fitting risk. The moving average strategy has a strong fit to historical data, and the actual effect may be different. The solution is to verify the real offer in the complex and ever-changing market and adjust parameters according to the real offer situation.
2. The risk caused by the stop loss point being too close. If the stop loss point is set too close to the main moving average, the stop loss may be triggered by short-term price fluctuations. This can be avoided by appropriately increasing the stop loss distance.
3. Financial pressure caused by bilateral transactions. To carry out long and short positions at the same time, sufficient funds need to be prepared as margin. Positions can be appropriately reduced to control financial pressure.
4. Parameter optimization risks. Parameter settings will vary greatly under different market conditions, and it takes time to optimize the parameters. Technologies such as machine learning can be used to assist parameter optimization.
## Optimization direction
1. You can consider adding more indicators to judge market trends and improve decision-making effects. For example, add volume price indicators, volatility indicators, etc.
2. Research can be conducted on automatically optimizing the moving average length len and stop loss parameters so that they can be adjusted according to market changes.
3. You can add filters for trading varieties and only trade on varieties with obvious trends.
4. You can consider changing the stop loss method to trailing stop loss, and adjust the stop loss point in real time according to the price.
5. You can establish an evaluation system for parameter optimization and use backtest results to automatically find the optimal parameter combination.
## Summarize
The overall idea of ​​this strategy is clear and easy to understand. Using double moving averages to stop losses can effectively control risks. The strategy has the advantages of adjustable parameters and strong adaptability, but there are also issues such as backtest data fitting and stop loss distance setting that need attention. Through further optimization, this strategy can become an effective stop-loss strategy that is easy to implement. It is suitable as a starting point for novices to learn algorithmic trading. It can be continuously improved in practice and gradually form a unique trading system.
||


## Overview

This strategy is a stop loss strategy based on dual moving averages. It uses two moving averages, one as the main moving average, and one as the stop loss line. When the price is above the main moving average, go long. When the price is below the stop loss line, close the long position. When the price is below the main moving average, go short. When the price is above the stop loss line, close the short position. It achieves stop loss and take profit by dynamically adjusting the long and short prices.

## Strategy Logic

This strategy uses the sma function to calculate the simple moving average of length len as the main moving average line ma. Then according to the user input long stop loss percentage elpercent and short stop loss percentage espercent, it calculates the long stop loss line el and short stop loss line es. The specific formulas are:

el = ma + (ma * elpercent / 100)
es = ma + (ma * espercent / 100)

Where elpercent and espercent represent the percentage offset from the main moving average line. 

This gives us three lines: main moving average ma, long stop loss line el, and short stop loss line es.

The trading logic of the strategy is:

If the closing price is above the long stop loss line el, open a long position. If the closing price is below the short stop loss line es, close the long position. 

If the closing price is below the short stop loss line es, open a short position. If the closing price is above the long stop loss line el, close the short position.

## Advantages of the Strategy

1. Using dual moving averages to set stop loss and take profit points can effectively control risks.

2. The length of the main moving average len and the offset percentages elpercent and espercent are customizable, which can be adjusted for different markets and adapt well.

3. The stop loss mechanism can cut losses in time and avoid further losses.

4. The strategy logic is simple and clear, easy to understand and implement, suitable for beginners.

5. It can go both long and short to take advantage of two-way markets.

## Risks and Solutions

1. Backtest overfitting risk. Moving average strategies tend to overfit backtest data. Actual performance may differ. Solution is to verify in complex live markets and adjust parameters accordingly.

2. Risk of stop loss being too close. If the stop loss is too close to the main moving average, it may be triggered by short-term price fluctuations. Increase the stop loss distance to avoid this.

3. Capital pressure from dual direction trading. Going both long and short requires sufficient margin. Reduce position size to control capital pressure.

4. Parameter optimization risk. Optimal parameters vary greatly across different market conditions. Time is needed to optimize parameters. Can use machine learning to assist parameter optimization.

## Optimization Directions

1. Consider adding more indicators to determine market trend and improve decisions, e.g. volume price indicator, volatility indicator.

2. Research auto-optimization of moving average length and stop loss parameters based on market changes.

3. Add filtering on trading instruments, only trading obvious trends.

4. Consider trailing stop loss instead of fixed stop loss, adjusting stops based on real-time prices. 

5. Build evaluation system for parameter optimization to automatically find optimum parameter sets via backtest results.

## Conclusion

The overall logic of this strategy is clear and easy to understand. It uses dual moving averages for stop loss and can effectively control risks. The strategy has advantages like customizable parameters and adaptability but also has risks like backtest overfit and stop loss distance setting that need attention. With further optimization, this strategy can become an effective stop loss strategy viable for live trading. It is suitable as a starting point for algorithmic trading beginners, and can be continually improved upon through practice to eventually form a unique trading system.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|false|Short|
|v_input_3|50|len|
|v_input_4_ohlc4|0|src: ohlc4|high|low|open|hl2|hlc3|hlcc4|close|
|v_input_5|5|Shift long, %|
|v_input_6|-5|Shift short, %|
|v_input_7|true|Show lines|
|v_input_8|true|Show background|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-08 00:00:00
end: 2023-11-14 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro
//2019

//@version=4
strategy(title = "Robot WhiteBox StopMA", shorttitle = "Robot WhiteBox StopMA", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 0)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(false, defval = false, title = "Short")
len = input(50)
src = input(ohlc4)
elpercent = input(5.0, minval = 0, maxval = 100, title = "Shift long, %")
espercent = input(-5.0, minval = -100, maxval = 0, title = "Shift short, %")
showlines = input(true, defval = true, title = "Show lines")
showbg = input(true, defval = true, title = "Show background")

//Levels
ma = sma(src, len)
el = ma + ((ma / 100) * elpercent)
es = ma + ((ma / 100) * espercent)

//Lines
colel = showlines ? color.lime : na
colma = showlines ? color.blue : na
coles = showlines ? color.red : na
plot(el, color = colel, offset = 1)
plot(ma, color = colma, offset = 1)
plot(es, color = coles, offset = 1)

//Background
trend = 0
trend := high > el[1] ? 1 : low < es[1] ? -1 : trend[1]
colbg = showbg == false ? na : trend == 1 ? color.lime : trend == -1 ? color.red : na
bgcolor(colbg, transp = 80)

//Trading
if ma > 0
    strategy.entry("Long", strategy.long, needlong ? na : 0, stop = el)
    strategy.entry("Short", strategy.short, needshort ? na : 0, stop = es)
```

> Detail

https://www.fmz.com/strategy/432211

> Last Modified

2023-11-15 15:44:48
