
> Name

Reverse-Trading-Strategy-Based-on-Overlapping-Price-Differentials
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1d6be9527270f6e75f0.png)
[trans]

## Overview
The main idea of ​​this strategy is to use the overlapping difference in prices to determine the market trend. When the difference reverses from a negative number to a positive number, go long and when the difference reverses from a positive number to a negative number, go short. It is a reversal trading strategy.
## Principle
The strategy first calculates the price overlap difference (Close-Close[1]), which is today's closing price minus yesterday's closing price, and then calculates the sum of the differences in the last 30 days. A long signal is generated when the sum reverses from a negative number to a positive number, and a short signal is generated when the sum reverses from a positive number to a negative number, which is a typical reversal trading strategy.
Specifically, the strategy maintains three indicators:
1. ff: The sum of the differences in the last 30 days
2. dd1: 15-day weighted moving average of ff
3. dd2: 30-day weighted moving average of ff
When ff reverses from a negative number to a positive number, that is, from less than 0 to greater than 0, and dd1 also reverses from a negative number to a positive number, a long signal is generated.
When ff reverses from a positive number to a negative number, that is, from greater than 0 to less than 0, and dd1 also reverses from a positive number to a negative number, a short signal is generated.
Take-profit and stop-loss lines will be set after going long or short.
## Advantages
This strategy has the following advantages:
1. The ideas are clear and easy to understand and implement.
2. Use the price reversal characteristics to obtain better entry opportunities at market turning points.
3. Combined with the double confirmation mechanism, false breakthroughs can be filtered out.
4. Parameters can be customized to adapt to different market environments.
## Risk
There are also some risks with this strategy:
1. The probability of reversal failure is high, and it is easy to stop losses in a range-bound market.
2. Improper parameter settings may lead to frequent transactions and increase transaction costs.
3. It is necessary to combine other indicators for filtering entry to avoid chasing tops and bottoms.
The corresponding solutions are as follows:
1. Set a reasonable stop loss ratio to control single loss.
2. Optimize parameters and find the best parameter combination.
3. Add filter conditions to avoid unnecessary admissions.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Increase the filtering of trading volume, for example, when a breakthrough occurs, the trading volume needs to be enlarged.
2. Combine with trend indicator filtering to avoid counter-trend operations.
3. Dynamically adjust parameters so that they can change according to market conditions.
4. Optimize the stop loss mechanism, such as moving the stop loss with the price.
## Summarize
This strategy determines the market turning point by calculating the reversal of the price difference. It is a typical reversal trading strategy. The strategic ideas are clear, easy to implement, and have certain practical value. But there are also some risks that require further optimization to adapt to market changes. In general, this strategy provides a basic framework for quantitative trading and can be expanded on this basis.
||

## Overview

The main idea of this strategy is to use the overlapping price differentials to judge market trends. It goes long when the differential reverses from negative to positive, and goes short when the differential reverses from positive to negative. It belongs to reverse trading strategies.

## Principle 

The strategy first calculates the overlapping price differential (Close-Close[1]), which is today's close price minus yesterday's close price, and then calculates the sum of the differentials over the past 30 days. It generates a long signal when the sum reverses from negative to positive, and generates a short signal when the sum reverses from positive to negative. It is a typical reverse trading strategy.

Specifically, the strategy maintains three indicators:

1. ff: Sum of price differentials over the past 30 days  
2. dd1: 15-day weighted moving average of ff
3. dd2: 30-day weighted moving average of ff

It generates a long signal when ff changes from negative to positive, i.e. from less than 0 to greater than 0, and dd1 also changes from negative to positive.  

It generates a short signal when ff changes from positive to negative, i.e. from greater than 0 to less than 0, and dd1 also changes from positive to negative.

After going long or short, take profit and stop loss lines will be set.

## Advantages

The strategy has the following advantages:

1. The logic is clear and easy to understand and implement.
2. It captures good entry timing at market turning points by utilizing price reversal features.  
3. False breakouts can be filtered out with the dual confirmation mechanism. 
4. Customizable parameters adapt to different market environments.

## Risks

There are also some risks for the strategy:

1. High probability of reversal failure, likely to be stopped out in range-bound markets.
2. Improper parameter settings may lead to frequent trading and increased transaction costs.
3. Other indicators should be incorporated to filter entries, avoiding chasing tops and bottoms.

The corresponding solutions are:

1. Set proper stop loss percentage to control single loss.
2. Optimize parameters to find the best combination.
3. Add filtering conditions to avoid unnecessary entries.

## Optimization Directions  

The strategy can be optimized in the following aspects:

1. Add volume filter, requiring enlarged volume on breakouts.
2. Incorporate trend indicators to avoid countertrend operations.
3. Dynamically adjust parameters to adapt to changing market conditions.
4. Optimize stop loss mechanism, such as trailing stop loss.


## Summary

The strategy judges market turning points by calculating price differential reversals. It is a typical reverse trading strategy. The logic is clear and easy to implement with some practical value. But there are also risks that need to be further optimized to adapt to market changes. Overall, the strategy provides a basic framework for quantitative trading, which can be built upon and extended.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|30|SUMM|
|v_input_2|15|Signalperiod|
|v_input_3|30|Info|
|v_input_4|95|profit|
|v_input_5|95|loss|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-07 00:00:00
end: 2023-12-14 00:00:00
period: 10m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy(title="Fst",currency="USD",initial_capital=100000)

//Length0 = input(30, title="fastperiod", minval=1)
Length = input(30, title="SUMM")
Length1 = input(15, title="Signalperiod", minval=1)
Length2= input(30, title="Info", minval=1)
profit=input(95, title="profit", minval=1)
loss=input(95, title="loss", minval=1)
//f=iff(close>open,close-open,iff(close>open[1],close[1]-open[1],0))
f=0.0
dd1=0.0
dd2=0.0
ff=0.0
ff0=0.0
f:=close-close[1]
ff:=sum(f,Length)
//ff0:=sum(f,Length0)
dd1:=wma(ff,Length1)
dd2:=wma(ff,Length2)

bull=ff<0 and dd1<0 and ff[1]<dd1 and ff>dd1 and abs(ff)>20
bear=ff>0 and dd1>0 and ff[1]>dd1 and ff<dd1 and abs(ff)>20
if(bull)
    
    strategy.entry("long", strategy.long)
strategy.exit("exit", "long", profit = close*profit/1000, loss=close*loss/1000) 

strategy.close("long", when = bear)




plotchar(bull,size=size.small,location=location.bottom)
plot(ff,color=black,linewidth=2)
plot(ff0,color=green,linewidth=2)
plot(wma(ff,Length1),color=red,linewidth=2)
plot(wma(ff,Length2),color=blue,linewidth=2)
plot(wma(ff,Length1)-wma(ff,Length2),color=green,style=columns)

plot(0,linewidth=1,color=black)
plot(500,linewidth=1,color=red)
plot(-500,linewidth=1,color=red)

```

> Detail

https://www.fmz.com/strategy/435506

> Last Modified

2023-12-15 15:47:23
