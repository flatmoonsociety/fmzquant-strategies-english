
> Name

Typical trend following strategy Dual-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1148a4aa63b71da3062.png)

[trans]

## Overview
The double moving average crossover strategy is a typical trend following strategy. It uses two EMA moving averages of different periods. When the short-period moving average crosses the long-period moving average, it goes long and when the short-period moving average crosses below the long-period moving average, it goes short to capture the turning point of the price trend.
## Strategy Principle
The core indicators of this strategy are two EMA moving averages, respectively 30-period and 60-period. In the code, two EMA moving averages are calculated through a custom function:
```
emaLen1 = emaFuncOne(close, lenMA1)  
emaLen2 = emaFuncTwo(close, lenMA2)
```

The trading signal for the strategy comes from the crossover of two EMAs:
```
currentState = if emaLen2 > emaLen1  
    0
else
    1

previousState = if emaLastLen2 > emaLastLen1
    0  
else
    1

convergence = if currentState != previousState
    1
else 
    0
```

When the short-term EMA crosses the long-term EMA, currentState and previousState are not equal, and a crossover signal appears. Go long at this time.
When the short-term EMA crosses the long-term EMA, currentState and previousState are not equal, and a crossover signal appears. Go short at this time.
## Advantage Analysis
This strategy has the following advantages:
1. The strategic ideas are simple and intuitive, easy to understand and implement
2. Use the smoothing characteristics of EMA to effectively filter market noise
3. Automatically track trends, making it less likely to miss a purchase or sale.
## Risk Analysis
There are also some risks with this strategy:
1. The double moving average crossover signal may be lagging behind and unable to capture the turning point in time.
2. Multiple false signals may appear in volatile market conditions
3. Improper parameter settings may lead to over sensitivity or lag.
It can be optimized by adjusting the EMA period or adding filter conditions.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Test EMA period combinations of different lengths
2. Add trading volume or volatility conditions to filter out false signals
3. Combine with other indicators to confirm the trend, such as MACD
4. Optimize fund management and set stop-loss and stop-profit
## Summarize
The double moving average crossover strategy is overall a simple and practical trend following strategy. It's straight-forward, easy to implement, and can automatically track trends. But there is also some lag and the risk of false signals. By optimizing parameters and adding filtering conditions, it can be further improved, making it one of the basic strategies for quantitative trading.
||

## Overview   

The Dual Moving Average Crossover strategy is a typical trend following strategy. It uses two EMA lines with different periods and goes long when the shorter period EMA crosses over the longer period EMA and goes short when the opposite crossing happens to capture trend reversals.  

## Principles  

The core indicators of this strategy are two EMA lines, one is 30-period and the other is 60-period. The two EMA lines are calculated by custom functions in the code:   

```
emaLen1 = emaFuncOne(close, lenMA1)
emaLen2 = emaFuncTwo(close, lenMA2)  
```

The trading signals are generated from the crossing of the two EMA lines:  

```  
currentState = if emaLen2 > emaLen1
    0
else 
    1

previousState = if emaLastLen2 > emaLastLen1 
    0
else
    1

convergence = if currentState != previousState
    1  
else
    0
```
  
When the shorter period EMA crosses over the longer period EMA, currentState is not equal to previousState, a crossover signal is triggered, go long. 
When the shorter period EMA crosses below the longer period EMA, currentState is not equal to previousState, a crossover signal is triggered, go short.

## Advantage Analysis   

The advantages of this strategy are:  

1. The logic is simple and intuitive, easy to understand and implement  
2. Smoothes price fluctuations with EMA and filters out market noise  
3. Automatically follows trends, avoids missing trades   

## Risk Analysis   

There are also some risks with this strategy:   

1. Crossover signals may lag and fail to capture reversals in a timely manner
2. Whipsaw signals may occur frequently during ranging markets  
3. Poor parameter tuning may cause oversensitivity or delays

Optimization can be done by adjusting EMA periods or adding filters.  

## Optimization Directions

This strategy can be optimized from the following aspects:  

1. Test different EMA period combinations  
2. Add volume or volatility filters to reduce false signals
3. Incorporate other indicators like MACD to confirm trends  
4. Optimize money management with stop loss and take profit

## Conclusion  

The Dual Moving Average Crossover strategy is a simple and practical trend following system overall. It is straight-forward, easy to implement and can automatically track trends. But some risks like lagging and false signals exist. With parameter tuning and adding filters, it can be further improved to become one of the fundamental algorithmic trading strategies.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|30|Length 1|
|v_input_2|60|Length 2|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-10 00:00:00
end: 2024-01-11 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("ParkerMAStrat", overlay=true)

lenMA1=input(title="Length 1", defval=30)
lenMA2=input(title="Length 2",  defval=60)

x = 0

checkLines(current, last) =>

    if current > last
        x = 1
    else
        x = 0
    x
    

//plot ema based on len1
emaFuncOne(src, time_period) =>

    alpha = 2 / (time_period + 1)
    // we have defined the alpha function above
    ema = 0.0
    // this is the initial declaration of ema, since we dont know the first ema we will declare it to 0.0 [as a decimal]
    ema := alpha * src + (1 - alpha) * nz(ema[1])
    // this returns the computed ema at the current time
    // notice the use of : (colon) symbol before =, it symbolises, that we are changing the value of ema,
    // since the ema was previously declared to 0
    // this is called mutable variale declaration in pine script
    ema
    // return ema from the function

emaLen1 = emaFuncOne(close, lenMA1)

    
plot(emaLen1, color=green, transp=0, linewidth=2)
// now we plot the _10_period_ema

//plot ema based on len2
emaFuncTwo(src, time_period) =>

    alpha = 2 / (time_period + 1)
    // we have defined the alpha function above
    ema = 0.0
    // this is the initial declaration of ema, since we dont know the first ema we will declare it to 0.0 [as a decimal]
    ema := alpha * src + (1 - alpha) * nz(ema[1])
    // this returns the computed ema at the current time
    // notice the use of : (colon) symbol before =, it symbolises, that we are changing the value of ema,
    // since the ema was previously declared to 0
    // this is called mutable variale declaration in pine script
    ema
    // return ema from the function

//plot ema based on len2
emaFuncOneLast(src, time_period) =>

    alpha = 2 / (time_period + 1)
    // we have defined the alpha function above
    ema = 0.0
    // this is the initial declaration of ema, since we dont know the first ema we will declare it to 0.0 [as a decimal]
    ema := alpha * src + (1 - alpha) * nz(ema[0])
    // this returns the computed ema at the current time
    // notice the use of : (colon) symbol before =, it symbolises, that we are changing the value of ema,
    // since the ema was previously declared to 0
    // this is called mutable variale declaration in pine script
    ema
    // return ema from the function

//plot ema based on len2
emaFuncTwoLast(src, time_period) =>

    alpha = 2 / (time_period + 1)
    // we have defined the alpha function above
    ema = 0.0
    // this is the initial declaration of ema, since we dont know the first ema we will declare it to 0.0 [as a decimal]
    ema := alpha * src + (1 - alpha) * nz(ema[0])
    // this returns the computed ema at the current time
    // notice the use of : (colon) symbol before =, it symbolises, that we are changing the value of ema,
    // since the ema was previously declared to 0
    // this is called mutable variale declaration in pine script
    ema
    // return ema from the function



emaLastLen1 = emaFuncOneLast(close, lenMA1)
emaLastLen2 = emaFuncTwoLast(close, lenMA2)
emaLen2 = emaFuncTwo(close, lenMA2)

    
plot(emaLen2, color=red, transp=30, linewidth=2)
// now we plot the _10_period_ema

//now we compare the two and when green crosses red we buy/sell (line1 vs line2)

previousState = if emaLastLen2 > emaLastLen1
    0
else
    1

currentState = if emaLen2 > emaLen1
    0
else
    1

convergence = if currentState != previousState
    1
else
    0

    
lineCheck = if convergence == 1 
    checkLines(currentState, previousState)
    
if lineCheck == 1
    strategy.entry("Long", strategy.long)
else
    strategy.entry("Short", strategy.short)

```

> Detail

https://www.fmz.com/strategy/438507

> Last Modified

2024-01-12 14:59:18
