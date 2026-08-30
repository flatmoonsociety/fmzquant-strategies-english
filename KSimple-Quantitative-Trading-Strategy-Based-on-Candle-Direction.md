
> Name

Simple-Quantitative-Trading-Strategy-Based-on-Candle-Direction
> Author

ChaoZhang

> Strategy Description


[trans]  

This article will introduce in detail a simple quantitative trading strategy based on the K-line direction. This strategy generates long and short signals directly based on price closing relationships.
1. Strategy Principle
This strategy only determines the direction based on the closing price relationship of the K line. The specific trading logic is:
1. When the closing price is greater than the opening price, go long;
2. When the closing price is lower than the opening price, go short;
3. You can set the position size;
4. The backtest time range can be set.
The simplest tracking signal is formed by directly judging the closing Yin or closing Yang of the K line. Although it is very primitive, it has also formed a complete trading system.
2. Strategic advantages
The biggest advantage of this strategy is that it is very simple and intuitive. It only uses the K-line direction to judge and does not need to calculate indicators.
Another advantage is that risk can be controlled by adjusting position size.
Finally, you can set the backtest time range to conduct testing for different periods.
3. Potential risks
But this strategy also has the following problems:
First of all, it is impossible to make an accurate judgment on the market based on the K-line direction alone, and the signal quality is poor.
Secondly, without setting stop-loss and stop-profit conditions, trading risks cannot be controlled.
Finally, parameter optimization was not performed and it was not stable enough.
4. Content summary
This article introduces in detail a simple quantitative trading strategy based only on the K-line direction. It forms a complete trading system through the most basic judgment of price relationships. However, there are also some problems that need to be improved, such as optimizing parameters, adding stop loss and profit, etc. Overall, it provides a very simple and original strategy idea.
||

This article explains in detail a simple quantitative trading strategy based solely on candle direction. It generates long/short signals directly according to the closing price relationship.

I. Strategy Logic

The strategy purely judges direction based on candle close, with the logic being:

1. Go long when close is greater than open. 

2. Go short when close is less than open.

3. Position sizing can be configured. 

4. Backtest date range can be set.

By simply determining candle closes up or down, the most basic trend following signals are formed. Despite being very primitive, it constitutes a complete trading system.

II. Advantages of the Strategy

The biggest advantage is the extreme simplicity and intuition, solely judging based on candle direction without indicators. 

Another advantage is the ability to control risk through position sizing.

Lastly, backtest time ranges can be set to test different periods.

III. Potential Risks

However, some issues exist:

Firstly, just candle direction is insufficient for accurate market judgment, resulting in poor signal quality.

Secondly, the lack of stop loss and take profit fails to control trade risks.

Lastly, the absence of parameter tuning leads to instability. 

IV. Summary

In summary, this article has explained a simple quantitative trading strategy based purely on candle direction. It forms a complete system through the most basic price relationship analysis. But improvements are needed such as parameter optimization and adding stops. Overall it provides a very simple and primitive strategy concept.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2016|year|
|v_input_2|9|month|
|v_input_3|true|day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-15 00:00:00
end: 2023-09-02 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("BarUpDn time limited", overlay=true, pyramiding=1, default_qty_type = strategy.fixed, default_qty_value = 1 )

//input boxes for the limit date
yearLimit = input(2016,title="year") 
monthLimit = input(9, title="month")
dayLimit = input(1, title="day")

//function that checks if the current date is more recent than the limit
dateOk(yl,ml,dl) =>
    ok = timestamp(yl,ml,dl,0,1) < time
    
checkDate = dateOk(yearLimit,monthLimit,dayLimit)
conditionUp = close > open ? true : false
conditionDown = close < open ? true : false
if ( checkDate  )
    strategy.entry("BarUp", strategy.long, when = conditionUp)
    strategy.entry("BarDn", strategy.short, when = conditionDown)




```

> Detail

https://www.fmz.com/strategy/426884

> Last Modified

2023-09-15 11:45:01
