
> Name

Quantitative-Strategy-of-Negative-Volume-Index-Reversal Quantitative-Strategy-of-Negative-Volume-Index-Reversal
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/41994621706cf2bae461772ba3325b0cc7eefc1504799267d59522552c2da276.png)
[trans]

## Overview
The name of this strategy is Negative Volume Index Reversal Strategy. This strategy uses the Negative Volume Index (NVI) and its moving average to construct long and short signals, and performs reversal transactions when conditions are met. It is a reversal strategy.
## Strategy Principle
The core indicator of the negative volume indicator reversal strategy is the negative volume indicator (NVI). The calculation formula for NVI is:
When the trading volume of the day < the trading volume of the previous day: NVI = NVI of the previous day + price change rate of the day
When the trading volume of the current day >= the trading volume of the previous day: NVI = NVI of the previous day
In other words, NVI is only updated on days when trading volume shrinks, and reflects price trends through the addition and subtraction of the price change rate. 과NVI’s logic for constructing long and short signals is:
- Go long when NVI is above its N-day moving average
- Go short when NVI is below its N-day moving average
In this way, reversal trades are carried out when the volume shrinks.
## Strategic Advantages
The main advantages of the negative volume indicator reversal strategy are:
1. Using trading volume signals, you can find reversal points, which has a certain timing advantage.
2. The strategy logic is simple and easy to understand and implement.
3. It can be optimized by adjusting parameters to adapt to different market environments.
## Strategy Risk
The negative volume indicator reversal strategy also has some risks:
1. The accuracy of trading volume signals cannot be guaranteed, and there is a certain probability of wrong transactions.
2. Improper parameter settings may lead to too frequent transactions or unclear signals.
3. It is necessary to ensure that the data source is reliable to avoid risks caused by errors in trading volume data.
These risks can be reduced through parameter optimization and stop-loss strategies.
## Optimization direction
The negative volume indicator reversal strategy can be optimized from the following aspects:
1. Optimize the moving average parameters and find parameters that better describe the market characteristics.
2. Add other indicator filters to avoid unnecessary wrong transactions. For example, increase the level of trend judgment.
3. Combine with powerful stop loss methods to limit single losses.
4. Test the differences in parameter settings of different varieties and set adaptive parameters.
## Summarize
The negative volume indicator reversal strategy performs reversal operations when trading volume shrinks, with the goal of capturing potential trend reversal points. This strategy has the advantages of being simple and easy to understand, but it also has certain risks of wrong transactions. Strategy stability and profitability can be improved through parameter optimization and adding auxiliary indicators. Overall, the negative indicator reversal strategy has good development and application prospects.
||

## Overview

The name of this strategy is Negative Volume Index Reversal Strategy. This strategy uses Negative Volume Index (NVI) and its moving average to construct long and short signals and make reversal trades when conditions are met. It belongs to the reversal strategy category.  

## Strategy Principle

The core indicator of the Negative Volume Index reversal strategy is Negative Volume Index (NVI). The calculation formula of NVI is:

If today's volume < previous day's volume: NVI = previous day's NVI + today's price change rate  

If today's volume >= previous day's volume: NVI = previous day's NVI

That is to say, NVI is only updated on the day when the trading volume shrinks, and the trend of the price is reflected through the addition and subtraction of the price change rate. The logic of constructing long and short signals with NVI and its moving average is:  

- When NVI is above its N-day moving average, go long.  

- When NVI is below its N-day moving average, go short.   

So it makes reversal trades when the volume shrinks.

## Advantages of the Strategy  

The main advantages of the Negative Volume Index reversal strategy are:  

1. Using volume signals can find reversal points and has certain timing advantages.  

2. The strategy logic is simple, easy to understand and implement.

3. Parameters can be optimized to adapt to different market environments.

## Risks of the Strategy

The Negative Volume Index reversal strategy also has some risks:   

1. The accuracy of volume signals cannot be guaranteed, and there is a certain probability of erroneous trades.  

2. Improper parameter settings may lead to over-frequent trading or unclear signals.

3. Ensure reliable data sources to avoid risks from erroneous volume data.

These risks can be reduced through parameter optimization, stop loss strategies, etc.  

## Optimization Directions  

The Negative Volume Index reversal strategy can be optimized in the following aspects:

1. Optimize the moving average parameters to find parameters that better describe market characteristics.  

2. Add other indicators for filtering to avoid unnecessary erroneous trades. For example, add larger timeframe trend judgments.

3. Combine with strong stop loss methods to limit single loss.

4. Test differences in parameter settings for different varieties, and set adaptive parameters.   

## Conclusion  

The Negative Volume Index reversal strategy makes reversal operations when the trading volume shrinks, aiming to capture potential trend reversal points. This strategy has the advantages of simplicity and easy understanding, and also has certain risks of erroneous trades. The stability and profitability of the strategy can be improved through parameter optimization, adding auxiliary indicators, etc. In general, the Negative Volume Index reversal strategy has good prospects for development and application.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|255|EMA_Len|
|v_input_2|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-13 00:00:00
end: 2023-12-20 00:00:00
period: 30m
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter 11/08/2017
// The theory behind the indexes is as follows: On days of increasing 
// volume, you can expect prices to increase, and on days of decreasing 
// volume, you can expect prices to decrease. This goes with the idea of 
// the market being in-gear and out-of-gear. Both PVI and NVI work in similar 
// fashions: Both are a running cumulative of values, which means you either 
// keep adding or subtracting price rate of change each day to the previous day`s 
// sum. In the case of PVI, if today`s volume is less than yesterday`s, don`t add 
// anything; if today`s volume is greater, then add today`s price rate of change. 
// For NVI, add today`s price rate of change only if today`s volume is less than 
// yesterday`s.
//
// You can change long to short in the Input Settings
// Please, use it only for learning or paper trading. Do not for real trading.
////////////////////////////////////////////////////////////
strategy(title="Negative Volume Index Backtest", shorttitle="NVI Str")
EMA_Len = input(255, minval=1)
reverse = input(false, title="Trade reverse")
xROC = roc(close, 1)
nRes = iff(volume < volume[1], nz(nRes[1], 0) + xROC, nz(nRes[1], 0))
nResEMA = ema(nRes, EMA_Len)
pos = iff(nRes > nResEMA, 1,
	     iff(nRes < nResEMA, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue ) 
plot(nRes, color=red, title="NVI")
plot(nResEMA, color=blue, title="EMA")
```

> Detail

https://www.fmz.com/strategy/436111

> Last Modified

2023-12-21 12:12:04
