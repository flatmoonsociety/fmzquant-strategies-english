
> Name

Slow-Heiken-Ashi-Exponential-Moving-Average-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/79a72c72545c0710ab9519c2266440dc6d567ac3e56d468d83a440e633f14b76.png)

[trans]

## Overview
This strategy uses a combination of slow Heiken Ashi and exponential moving averages to identify trends and conduct long and short two-way trades in trending markets. Go long when the price exceeds the 100-day EMA, go short when the price is below the 100-day EMA, and close the position under certain conditions.
## Strategy Principle
This strategy uses a combination of the following indicators:
1. Slow Heiken Ashi: A special type of K-line chart, drawn using the average price of the previous K-line, which can filter market noise and identify trends. This is achieved through the adaptive Kama filter.
2. Exponential moving average: an average that is exponentially smoothed on the price. This includes EMAs for multiple periods from 5 to 100 days.
The specific transaction logic is:
1. When the price goes above the 100-day EMA, go long; when the price goes below the 100-day EMA, go short.
2. Position closing conditions: When the opening price of Heiken Ashi crosses its closing price (potential reversal signal), the corresponding long position will be closed through the reverse cross, and the same applies to the short position.
## Advantage Analysis
This strategy combines trend judgment and reversal signals, which can capture larger price fluctuations in the trend market, and at the same time avoid expansion of losses through reversal signals.
1. Use EMA to determine the global trend direction and avoid being misled by local shocks.
2. Heiken Ashi’s crossover signal can detect reversal opportunities early.
3. Adaptive Kama filter reduces the probability of false signals.
## Risk Analysis
1. A significant breakthrough of EMA may cause losses to expand. You can appropriately shorten the position period or set a stop loss.
2. The reversal signal may be delayed, so consider reducing the position size to control risks.
3. Improper setting of EMA parameters will also affect strategy performance and should be adjusted according to different varieties and market environments.
## Optimization direction
1. It can be judged by combining multiple indicators to avoid the probability of both EMA and Heiken Ashi sending wrong signals. For example, add MACD, Bollinger Bands, etc.
2. The EMA parameters can be optimized in real time based on market volatility, tightening the stop loss when volatility is high and relaxing slippage when volatility is low.
3. Automatically optimize each parameter setting and filtering rules based on machine learning algorithms to make the strategy more robust.
## Summarize
Overall, this strategy is relatively simple and practical, and it combines trends and reversals. With parameter optimization and risk control in place, there is still good room for profit. In the future, we can start from the optimization direction to make the strategy more adaptable to changes in the market environment.
||

## Overview 

This strategy combines slow Heiken Ashi and exponential moving averages to identify trends and make long/short trades during trending markets. It goes long when price is above 100-day EMA and goes short when price is below 100-day EMA, closing positions on specific reversal signals.  

## Strategy Logic

The strategy employs the following indicators:

1. Slow Heiken Ashi: A special type of candlestick calculated using the previous bar's average price, filtering out market noise and identifying trends. Implemented here using adaptive KAMA filter.

2. Exponential Moving Average: Smoothed price averages with exponential weighting applied. Contains EMAs from 5-day to 100-day periods.  

The specific trading logic is:

1. Go long when price crosses above 100-day EMA, go short when price crosses below 100-day EMA.  

2. Exit positions when Heiken Ashi's open price crosses its close price (potential reversal signal). Long positions are closed on reverse crossovers and short positions likewise.

## Advantage Analysis 

The strategy combines trend-following and reversal signals, capturing large price swings during trending markets while avoiding excessive losses when trends reverse.

1. EMA determines overall market trend direction, preventing distraction from localized fluctuations. 

2. Heiken Ashi crossovers provide early detection of potential reversals.  

3. Adaptive KAMA filter reduces false signals.

## Risk Analysis

1. Sudden, large EMA breaks can lead to amplified losses. Consider tighter holding periods or stop losses.  

2. Reversal signals may lag. Lower position sizes to control risk.

3. Inadequate EMA parameterization negatively impacts performance. Parameters should adapt to different products and market environments. 

## Optimization Directions

1. Incorporate additional indicators like MACD and Bollinger Bands to avoid simultaneous EMA/Heiken Ashi errors.  

2. Dynamically optimize EMA parameters based on market volatility, tightening stops/increasing slippage tolerance accordingly.

3. Utilize machine learning to automatically tune parameters, filter rules and improve robustness.

## Conclusion

The strategy is relatively simple and practical overall, combining both trend and reversal elements. With well-tuned parameters and risk controls, it retains decent profit potential. Further improvements can build on the optimization directions to make the strategy more adaptive.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|6|Period|
|v_input_2|0.666|fastend|
|v_input_3|0.0645|slowend|
|v_input_4|true|Exponential MA|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-14 00:00:00
end: 2023-12-19 10:00:00
period: 15m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("NoScoobies Slow Heiken Ashi and Exponential Moving average Strategy 2.2", overlay=true)

//SHA
p=input(6,title='Period')
fastend=input(0.666,step=0.001)
slowend=input(0.0645,step=0.0001)
kama(close,amaLength)=>
    diff=abs(close[0]-close[1])
    signal=abs(close-close[amaLength])
    noise=sum(diff, amaLength)
    efratio=noise!=0 ? signal/noise : 1
    smooth=pow(efratio*(fastend-slowend)+slowend,2)
    kama=nz(kama[1], close)+smooth*(close-nz(kama[1], close))
    kama
hakamaper=1
Om=sma(open,p)
Hm=sma(high,p)
Lm=sma(low,p)
Cm=sma(close,p)
vClose=(Om+Hm+Lm+Cm)/4
vOpen= kama(vClose[1],hakamaper)
vHigh= max(Hm,max(vClose, vOpen))
vLow=  min(Lm,min(vClose, vOpen))
asize=vOpen-vClose
size=abs(asize)

//MMAR
exponential = input(true, title="Exponential MA")
src = close
ma05 = exponential ? ema(src, 05) : sma(src, 05)
ma10 = exponential ? ema(src, 10) : sma(src, 10)
ma15 = exponential ? ema(src, 15) : sma(src, 15)
ma20 = exponential ? ema(src, 20) : sma(src, 20)
ma25 = exponential ? ema(src, 25) : sma(src, 25)
ma30 = exponential ? ema(src, 30) : sma(src, 30)
ma35 = exponential ? ema(src, 35) : sma(src, 35)
ma40 = exponential ? ema(src, 40) : sma(src, 40)
ma45 = exponential ? ema(src, 45) : sma(src, 45)
ma50 = exponential ? ema(src, 50) : sma(src, 50)
ma55 = exponential ? ema(src, 55) : sma(src, 55)
ma60 = exponential ? ema(src, 60) : sma(src, 60)
ma65 = exponential ? ema(src, 65) : sma(src, 65)
ma70 = exponential ? ema(src, 70) : sma(src, 70)
ma75 = exponential ? ema(src, 75) : sma(src, 75)
ma80 = exponential ? ema(src, 80) : sma(src, 80)
ma85 = exponential ? ema(src, 85) : sma(src, 85)
ma90 = exponential ? ema(src, 90) : sma(src, 90)
ma95 = exponential ? ema(src, 95) : sma(src, 95)
ma100 = exponential ? ema(src, 100) : sma(src, 100)

longcondition=src>ma100
shortcondition=src<ma100
long=longcondition and size<size[1] and (vOpen<vClose or vOpen>vClose)
short=shortcondition and size<size[1] and (vOpen>vClose or vOpen<vClose)
close_long=longcondition and crossunder(open, vClose)
close_short=shortcondition and crossover(open, vClose)
_close=close_long[2] or close_short[2]

if long
    strategy.entry("LONG", strategy.long)
    strategy.close("LONG", when = _close)
if short
    strategy.entry("SHORT", strategy.short)
    strategy.close("SHORT", when = _close)
    

```

> Detail

https://www.fmz.com/strategy/436228

> Last Modified

2023-12-22 13:18:34
