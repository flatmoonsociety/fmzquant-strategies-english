
> Name

Crossing-Strategy-Between-Bollinger-Bands-and-Hull-Indicator
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/fc5cfeabbb7b754b78.png)
[trans]

## Overview
This strategy is based on the intersection of the Bollinger Bands and the Hull indicator to generate trading signals. Go long when the Hull indicator crosses the lower track of the Bollinger Bands, and go short when the Hull indicator crosses the upper track of the Bollinger Bands. This strategy combines the Bollinger Bands breakout strategy with the Hull Indicator's trend following strategy, thus taking advantage of the best of both worlds.
## Strategy Principle
This strategy is primarily based on the intersection of the Bollinger Bands and the Hull indicator to generate trading signals.
First of all, Bollinger Bands contains three lines: the middle track, the upper track, and the lower track. The middle rail is the n-day moving average, and the upper and lower rails are the upper and lower rails plus one standard deviation respectively. If the price breaks through the upper track, it means there is an opportunity for a breakthrough; if the price falls below the lower track, it means there is an opportunity for a correction.
Secondly, the Hull indicator is a trend following indicator. It uses the difference between the weighted moving averages of two different periods to determine the current trend. If the short-term average is higher than the long-term average, it is bullish; otherwise, it is bearish.
This strategy combines the best of both indicators. When the Hull indicator crosses the lower track of the Bollinger Bands, it is believed that the stock price may enter the upward trend stage, then go long; when the Hull indicator crosses the upper track of the Bollinger Bands, it is believed that the stock price may enter the downward stage of correction, then go short.
## Strategic Advantages
1. Combine the advantages of Bollinger Bands and Hull indicators to make trading signals more reliable.
2. Use the Hull indicator to determine the trend direction and the Bollinger Bands to determine the support and resistance positions to form cross signals, which can increase the probability of profit.
3. By adjusting the parameters of Bollinger Bands and Hull indicators, it can be optimized for stocks in different cycles, and has a wider application.
## Risks and Solutions
1. When the stock price is trading sideways, this strategy may produce more false signals and bring losses. False signals can be reduced by optimizing parameters or adding filtering conditions.
2. When the stock price fluctuates violently, the Bollinger Bands and Hull indicators may issue trading signals at the same time. It is necessary to ensure the order of the signals and avoid misjudgment of cross signals. Consider adding a stop loss to control losses.
3. The opening quantity is directly set to 100% in the code. During actual deployment, position management needs to be adjusted, and full positions cannot be opened, which may lead to expanded losses.
## Optimization direction
1. You can test and optimize the parameters of Bollinger Bands and Hull indicators to adapt to stocks with more cycles.
2. Add volume or volatility filters to avoid false signals during consolidation.
3. Optimize the stop loss strategy and set a trailing stop loss or a pending order stop loss.
4. Adjust the position management rules and add conditions for re-entering the market to avoid expanding losses.
## Summarize
This strategy comprehensively utilizes the Bollinger Bands' breakthrough strategy and the Hull indicator's trend following strategy to form a trading signal through the intersection of the two, achieving the dual effects of trend following and breakthrough. This strategy has strong adaptability to short- and medium-term stocks on the premise that the fundamentals do not change significantly. However, in actual deployment, it is still necessary to optimize parameters according to the characteristics of individual stocks, and appropriately adjust position management, stop loss strategies, etc., so as to make the strategy more robust.
||

## Summary  

This strategy generates trading signals based on the crossover between Bollinger Bands and the Hull indicator. It goes long when the Hull indicator crosses above the lower band of Bollinger Bands, and goes short when the Hull indicator crosses below the upper band of Bollinger Bands. The strategy combines the breakout strategy of Bollinger Bands and the trend-following strategy of the Hull indicator to utilize the advantages of both.  

## Principles  

The strategy mainly uses the crossover between Bollinger Bands and the Hull indicator to generate trading signals. 

Bollinger Bands contain three lines: middle line, upper line and lower line. The middle line is the N-day moving average, while the upper and lower lines are middle line ± standard deviation. If price breaks through the upper line, it indicates a breakthrough opportunity; if price breaks through the lower line, it indicates a callback opportunity.

The Hull indicator is a trend-following indicator. It uses the difference between two weighted moving averages of different periods to determine the current trend. If the short period moving average is above the long period one, it indicates an uptrend, and vice versa.  

The strategy combines the strengths of both indicators. When the Hull indicator crosses above the lower band of Bollinger Bands, it is considered that stock price may enter an uptrend, so go long. When the Hull indicator crosses below the upper band, it is considered that stock price may enter a downward callback, so go short.

## Advantages  

1. Combines the strengths of Bollinger Bands and Hull indicator to make trading signals more reliable. 

2. Uses Hull indicator to determine trend direction and Bollinger Bands to determine support/resistance levels, generating crossover signals to improve profitability.

3. Parameters of both indicators can be optimized for stocks of different cycles to expand applicability.  

## Risks and Solutions

1. The strategy may generate more false signals during range-bound movements, causing losses. Parameters can be optimized or filters can be added to reduce false signals.  

2. Prices may fluctuate violently, causing both indicators to issue signals simultaneously. Ensure signal sequencing to avoid erroneous crossover signal judgment. Consider adding stop loss to control losses.

3. Strategy sets position size to 100% directly. In actual deployment, position sizing needs to be adjusted to avoid magnified losses due to full position opening.

## Optimization Directions   

1. Test and optimize parameters of both indicators to adapt to more stock cycles.  

2. Add filters like trading volume or volatility to avoid wrong signals during consolidation.  

3. Optimize stop loss strategies by setting trailing stop loss or stop limit orders.

4. Adjust position sizing rules by adding re-entry conditions to avoid loss magnification.   

## Conclusion

This strategy combines the breakout strategy of Bollinger Bands and trend-following strategy of the Hull indicator by using crossover signals between them to achieve both trend-following and breakout effects. The strategy has strong adaptability to medium- and short-term stocks given no major fundamental changes. But parameters, position sizing, stop loss strategies still need optimization during actual deployment to make the strategy more robust.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|3|period|
|v_input_2|true|i|
|v_input_3|20|length1|
|v_input_4_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_5|2|mult|
|v_input_6|500|TP|
|v_input_7|500|SL|
|v_input_8|20|TS|
|v_input_9|10|TO|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-30 00:00:00
end: 2023-12-07 00:00:00
period: 30m
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/


//@version=3
strategy(title="Strategy Hull Bollinger", shorttitle="Hull bollinger",overlay=true, calc_on_order_fills=true, default_qty_type=strategy.percent_of_equity, default_qty_value=100, overlay=false)

n=input(title="period",defval=3)


n2ma=2*wma(close,round(n/2))
nma=wma(close,n)
diff=n2ma-nma
sqn=round(sqrt(n))


n2ma1=2*wma(close[1],round(n/2))
nma1=wma(close[1],n)
diff1=n2ma1-nma1
sqn1=round(sqrt(n))


n1=wma(diff,sqn)
n2=wma(diff1,sqn)
c=n1>n2?green:red

i = input(1)
PP = close[i]

length1 = input(20, minval=1)
src = input(close, title="Source")
mult = input(2.0, minval=0.001, maxval=10, step=0.2)
basis = sma(src, length1)
dev = mult * stdev(src, length1)
upper = basis + dev
lower = basis - dev


TP = input(500) * 10
SL = input(500) * 10
TS = input(20) * 10
TO = input(10) * 10
CQ = 100

TPP = (TP > 0) ? TP : na
SLP = (SL > 0) ? SL : na
TSP = (TS > 0) ? TS : na
TOP = (TO > 0) ? TO : na

longCondition = crossover(n1,lower)
if (longCondition)
    strategy.entry("Long", strategy.long)


shortCondition = crossunder(n1,upper)
if (shortCondition)
    strategy.entry("Short", strategy.short)

strategy.exit("Close Short", "Short", qty_percent=CQ, profit=TPP, loss=SLP, trail_points=TSP, trail_offset=TOP)
strategy.exit("Close Long", "Long", qty_percent=CQ, profit=TPP, loss=SLP, trail_points=TSP, trail_offset=TOP)
```

> Detail

https://www.fmz.com/strategy/434681

> Last Modified

2023-12-08 11:58:07
