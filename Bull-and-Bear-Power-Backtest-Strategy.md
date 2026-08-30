
> Name

Bull-and-Bear-Power-Backtest-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/2a771ab098af50e3e3dd95e522118552a944b65379cc6178f94392c2b26c8f94.png)

[trans]

## Overview
The long-short power strategy was developed by Dr. Alexander Elder and uses the Elder-ray indicator to measure buying and selling pressure in the market. Elder-ray indicators are typically used in conjunction with three-screen trading systems, but can also be used independently.
Dr. Alexander Elder uses the 13-day exponential moving average (EMA) to represent consensus on market value. Bull power reflects the ability of buyers to push prices above consensus on value. Short power reflects the ability of sellers to push prices below the average value consensus.
Bull power is calculated by subtracting the 13-day EMA from the high. Bear power is calculated by subtracting the 13-day EMA from the low.
## Strategy Principle
This strategy determines the long and short situation of the market by calculating the long and short power indicators.
1. Calculate the 13-day EMA as the market value consensus
2. Calculate bull power: the highest price of the day minus the 13-day EMA
3. Calculate short power: the lowest price of the day minus the 13-day EMA
4. Compare the relationship between bull power and short power and the threshold, and determine the long and short signals
5. You can choose reverse transaction
When the bullish power is greater than the threshold, it is a long signal, and when the bearish power is greater than the threshold, it is a short signal. And you can choose to reverse the transaction.
## Advantage Analysis
1. Use the long and short power indicator to judge the long and short situation of the market, which is simple and easy to understand.
2. Flexible configurable parameters, adjustable thresholds and cycles
3. Optional reverse trading to adapt to different market environments
4. Using exponential moving average, it is less sensitive to emergencies
## Risk Analysis
1. The long and short power indicators are prone to produce false signals and need to be filtered in combination with trends and other indicators.
2. The fixed cycle cannot adapt to market changes, so adaptive cycle optimization can be used
3. There is no stop loss, and it is easy to follow the market and cause excessive losses.
4. Only judging long and short, lack of timing to enter the market
Stop loss can be set, moving average cycles can be optimized, and trend indicators can be combined for optimization.
## Optimization direction
1. Optimize the moving average period parameters and use adaptive period EMA
2. Add trend indicator filtering to avoid counter-trend trading
3. Add stop loss strategy to control single loss
4. Combine with other indicators to choose a better time to enter the market
5. Use machine learning technology to optimize parameter settings
## Summarize
The long-short power strategy uses the Elder-ray indicator to judge the market's long-short situation, which is simple and intuitive, with configurable parameters. However, it is easy to generate false signals, and further optimization is required to include trend judgment and stop loss. This strategic idea is worth learning from, but caution needs to be applied directly.
||

## Overview

The Bull and Bear Power strategy was developed by Dr. Alexander Elder using the Elder-ray indicator to measure buying and selling pressure in the market. The Elder-ray is often used with the Triple Screen system but can also be used on its own. 

Dr. Elder uses a 13-period exponential moving average (EMA) to indicate the market consensus of value. Bull power measures the ability of buyers to drive prices above the consensus of value. Bear power reflects the ability of sellers to drive prices below the average consensus of value.

Bull power is calculated by subtracting the 13-period EMA from the high. Bear power subtracts the 13-period EMA from the low.

## Strategy Logic

The strategy judges market sentiment through calculating bull and bear power indicators.

1. Calculate 13-period EMA as market value consensus  
2. Calculate bull power: High minus 13-period EMA
3. Calculate bear power: Low minus 13-period EMA
4. Compare bull power and bear power with threshold to determine long and short signals
5. Option to trade reverse signals

When bull power is greater than threshold, it's long signal. When bear power is greater than threshold, it's short signal. Reverse trading can be selected.

## Advantage Analysis 

1. Simple and intuitive using bull and bear power indicators to judge market sentiment
2. Flexible configuration of parameters, adjustable threshold and period
3. Option for reverse trading adapts to different market environments
4. Uses exponential moving average, less sensitive to outliers

## Risk Analysis

1. Prone to false signals, needs combining with trend and other filters  
2. Fixed period cannot adapt to market changes, adaptive period can optimize
3. No stop loss, easily chasing market with huge losses
4. Only judges long or short, lacks timing selection

Can add stop loss, optimize moving average period, combine with trend filter etc.

## Optimization Directions

1. Optimize moving average period, use adaptive period EMA
2. Add trend filter to avoid counter trend trading
3. Add stop loss to control single trade loss
4. Combine other indicators to select better entry timing
5. Utilize machine learning to optimize parameters

## Conclusion

The Bull and Bear Power strategy judges market sentiment simply and intuitively with configurable parameters. But it's prone to false signals and needs further optimization with trend and stop loss. The logic is worth learning but direct application needs caution.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|13|Length|
|v_input_2|false|Trigger|
|v_input_3|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-23 00:00:00
end: 2023-10-23 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version = 2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 08/12/2016
// Developed by Dr Alexander Elder, the Elder-ray indicator measures buying 
// and selling pressure in the market. The Elder-ray is often used as part 
// of the Triple Screen trading system but may also be used on its own.
// Dr Elder uses a 13-day exponential moving average (EMA) to indicate the 
// market consensus of value. Bull Power measures the ability of buyers to 
// drive prices above the consensus of value. Bear Power reflects the ability 
// of sellers to drive prices below the average consensus of value.
// Bull Power is calculated by subtracting the 13-day EMA from the day's High. 
// Bear power subtracts the 13-day EMA from the day's Low.
//
// You can use in the xPrice any series: Open, High, Low, Close, HL2, HLC3, OHLC4 and ect...
// You can change long to short in the Input Settings
// Please, use it only for learning or paper trading. Do not for real trading.
////////////////////////////////////////////////////////////
strategy(title="Elder Ray (Bull Power) Strategy Backtest")
Length = input(13, minval=1)
Trigger = input(0)
reverse = input(false, title="Trade reverse")
hline(0, color=purple, linestyle=line)
xPrice = close
xMA = ema(xPrice,Length)
DayHigh = iff(dayofmonth != dayofmonth[1], high, max(high, nz(DayHigh[1])))
nRes = DayHigh - xMA
pos = iff(nRes > Trigger, 1,
	   iff(nRes < Trigger, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
         iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue )
plot(nRes, color=blue, title="Bull Power", style = histogram)
```

> Detail

https://www.fmz.com/strategy/430065

> Last Modified

2023-10-24 16:43:52
