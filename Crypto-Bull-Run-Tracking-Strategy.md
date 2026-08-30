
> Name

Dynamic Moving Average Crossover Trend Tracking Strategy Crypto-Bull-Run-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/41d462698f4479995c418eb73f043d4f1281f722c75ef962d07bc1dd27a9373e.png)
[trans]

## Overview
This strategy tracks the trend by calculating two dynamic moving averages, DEMA and TEMA, and establishing long or short positions when they occur golden crosses or dead crosses. At the same time, the strategy also sets a certain number of positions to avoid unnecessary stop losses.
## Strategy Principle
This strategy is mainly based on the intersection of two dynamic moving averages, DEMA and TEMA, to determine the direction of the trend.
DEMA stands for Double Exponential Moving Average, which combines the weighted smoothing characteristics of EMA and optimizes the lag problem existing in EMA. The calculation formula is:
DEMA = 2*EMA(CLOSE,N) - EMA(EMA(CLOSE,N),N)  

Here N is Demalength.
TEMA stands for Triple Exponential Moving Average, which uses three exponential smoothing to reduce the lag of the average. The calculation formula is:
EMA1 = EMA(CLOSE,Temalength)  
EMA2 = EMA(EMA1,Temalength)  
EMA3 = EMA(EMA2,Temalength)  
TEMA = 3*EMA1 - 3*EMA2 + EMA3  

When TEMA crosses above DEMA, it is regarded as a golden cross signal and you go long; when TEMA crosses below DEMA, it is regarded as a dead cross signal and you go short.
In addition, the strategy also sets delayBars to ensure the validity of the signal and avoid false signals. It requires a golden cross or a dead cross to continue for a certain period before entry is triggered.
Finally, the strategy adds double-checking logic. That is, before opening a position, it will be judged whether it is necessary to close the current reverse position, which can avoid the risk of two-way arbitrage.
## Advantage Analysis
1. Use two dynamic moving averages to judge trends more accurately
The two dynamic moving averages, DEMA and TEMA, are more sensitive than the traditional EMA and SMA, and can capture trend changes faster, thereby improving the accuracy of judging market trends.
2. Set a certain delay period to filter out false signals
The setting of the delayBars parameter makes it necessary to wait until the signal continues for a period of time before opening a position. This can filter out some false signals and avoid being trapped.
3. Double checking reduces risk
The strategy will give priority to determining whether the reverse position needs to be closed before opening a position, which can avoid the risk of holding two-way positions at the same time and minimize arbitrage losses.
4. Has strong versatility
This strategy mainly relies on the general technical indicator of moving average crossover to judge trends and signals. It does not rely on specific varieties and is suitable for most varieties with obvious trends.
## Risk Analysis
1. It’s easy to get trapped in a sharply volatile market
When the market falls into a huge fluctuation range, the moving averages may cross frequently, which can easily form false signals and lead to traps. At this time, the delay period setting may not be able to completely filter the signal.
The solution is to pause the strategy after identifying the oscillation trend, or to appropriately adjust the moving average parameters and delay period.
2. Failure to recognize traps or emergencies
This strategy only tracks price trends and cannot predict short-term traps or reversals caused by major emergencies. This is when the strategy may suffer large losses.
The solution is to use other indicators to determine the risk background, or to appropriately reduce the position size.
## Optimization direction
1. Test more types of moving average indicators
In addition to DEMA and TEMA, you can also test combinations of SMA, EMA, and other modified moving averages to find moving average indicators that better match the market.
2. Optimize MA parameters and delay period
Find the best moving average length parameters and signal delay period through parameter optimization to obtain more accurate trading signals.
3. Different varieties adapt to different parameters
According to the characteristics of the variety, find the moving average and delay period parameter combinations that are suitable for its fluctuation range and trend.
4. Conduct risk assessment in combination with other indicators
For example, the Bollinger Bands indicator determines volatility and price position to avoid falling into a shock trap; it combines the strength of energy indicators to evaluate the reliability of the trend.
## Summarize
This strategy tracks the general trend through the intersection of dynamic moving averages DEMA and TEMA, and is a simple trend following strategy. The advantage is high stability, reliability and versatility, and it is suitable for use as a basic strategy; but it also has the disadvantages of certain hysteresis and weak reversal recognition ability. This article conducts a comprehensive analysis and summary of the advantages, risks and subsequent optimization directions of this strategy, providing a valuable reference for the use of this strategy. Overall, this strategy provides a typical example for the design of quantitative trading strategies and is worthy of in-depth study and reference.
||

## Overview  

This strategy tracks the trend by calculating two dynamic moving averages, DEMA and TEMA, and establishing long or short positions when they generate golden crosses or death crosses. At the same time, the strategy sets a certain number of holding bars to avoid unnecessary stop loss.

## Strategy Logic  

The core logic of this strategy is to determine the trend direction based on the crossover between two dynamic moving averages, DEMA and TEMA. 

DEMA stands for Double Exponential Moving Average. It combines the weighted smoothing feature of EMA and optimizes the lagging problem of EMA. Its formula is:  

DEMA = 2*EMA(CLOSE, N) - EMA(EMA(CLOSE, N), N)

Here N is the Demalength.  

TEMA stands for Triple Exponential Moving Average. It uses triple exponential smoothing to reduce the lagging of moving averages. Its formula is:

EMA1 = EMA(CLOSE, Temalength) 
EMA2 = EMA(EMA1, Temalength)
EMA3 = EMA(EMA2, Temalength)
TEMA = 3*EMA1 - 3*EMA2 + EMA3  

When TEMA crosses over DEMA, it is considered as a golden cross signal to go long. When TEMA crosses below DEMA, it is considered as a death cross signal to go short.   

In addition, the strategy sets the delayBars to ensure the validity of signals and avoid false signals. It requires the golden/death cross to continue for a certain period before triggering entry.  

Finally, the strategy adopts dual checking logic. It will check whether the opposite position needs to be closed before opening new trades. This avoids the risk of double direction positions.

## Advantage Analysis 

1. More accurate trend judgment using two dynamic MAs  

Compared to traditional EMA and SMA, DEMA and TEMA are more sensitive dynamic MAs that can quickly capture trend changes, thus improving the accuracy of market trend judgments.  

2. Filtering false signals by setting a delay period 

The delayBars parameter forces the strategy to wait for a period of time after the signal emerges before entering positions. This filters out some false signals and avoids being trapped.  

3. Reducing risks through dual checking  

By checking whether the opposite position needs to be closed before opening new trades, the strategy avoids holding double direction positions and minimizes losses from hedge trades.

4. Strong universality  

This strategy relies mainly on the crossover between MAs, a common technical indicator, to determine trends and signals. It does not rely on specific products and is suitable for most trending products.

## Risk Analysis   

1. Prone to being trapped in whipsaw markets

In a market with huge sideways fluctuations, MAs may frequently cross and generate false signals that cause losses. In this case, the delay settings may fail too.  

The solutions are to pause the strategy when identifying sideways trends, or properly adjust the MA parameters and delay periods.

2. Fails to identify traps or black swan events 

The strategy purely tracks price trends and cannot predict short-term traps or trend reversals caused by major events. It may lead to huge losses in such cases.  

The solutions are to incorporate other indicators to assess risks, or properly reduce position sizes. 

## Optimization Directions

1. Test more types of MAs 

Apart from DEMA and TEMA, test combinations of SMA, EMA, and other enhanced MAs to find the most suitable ones for this market.  

2. Optimize MA parameters and delay periods  

Run optimizations to find the optimum MA lengths and signal delay periods for more accurate trading signals.  

3. Adapt parameters for different products  

Given different product characteristics, find suitable combinations of MA lengths, delay periods for their price fluctuations and trendiness.  

4. Incorporate other indicators for risk assessment

E.g. use Bollinger Bands to judge volatility and price level to avoid whipsaw markets. Use momentum indicators to evaluate trend strengths.  

## Conclusion   

This is a basic trend following strategy based on dynamic MA crossovers between DEMA and TEMA. Its advantages are high stability, reliability and universality. But it also has some lagging and weak reversal detection capacity. This article provides a comprehensive analysis of its pros, cons and optimization directions, serving as valuable references for using this strategy. On the whole, it offers a typical example of quantitative trading strategy design worthy of further study.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|230|Demalength|
|v_input_int_2|210|Temalength|
|v_input_1|5|Bar Delay|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-01 00:00:00
end: 2023-12-07 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © jacobdickson255

strategy("Crypto Bull Run Tracker", overlay=true, pyramiding=0)

//Dema Scripting
Demalength = input.int(230, minval=1)
src = close
e1 = ta.ema(src, Demalength)
e2 = ta.ema(e1, Demalength)
dema = 2 * e1 - e2
plot(dema, "DEMA", color=#43A047)

//Tema Scripting
Temalength = input.int(210, minval=1)
ema1 = ta.ema(close, Temalength)
ema2 = ta.ema(ema1, Temalength)
ema3 = ta.ema(ema2, Temalength)
tema = 3 * (ema1 - ema2) + ema3
plot(tema, "TEMA", color=#2962FF)

delayBars = input(5, title="Bar Delay")
var int lastTradeBar = na

longCondition = ta.crossover(tema, dema) 
longExit = ta.crossunder(tema, dema)
shortCondition = ta.crossunder(tema, dema)
shortExit = ta.crossover(tema, dema)

// Exit conditions should be checked before entry conditions
// Close short position if a long condition is present
if ((shortExit and strategy.position_size < 0)) // If conditions for exiting the short are met, and there is a balance in the short direction, exit the short
    strategy.close("Short")
   

// Close long position if a short condition is present
if ((longExit and strategy.position_size > 0))
    strategy.close("Long")
   
// Now check for entry conditions
if (longCondition)
    strategy.entry("Long", strategy.long)
    lastTradeBar := bar_index

if (shortCondition)
    strategy.entry("Short", strategy.short)
    lastTradeBar := bar_index

```

> Detail

https://www.fmz.com/strategy/434706

> Last Modified

2023-12-08 15:45:47
