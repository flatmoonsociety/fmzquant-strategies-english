
> Name

Short-term trading strategy RSI-Bollinger-Bands-Short-term-Trading-Strategy combining RSI and Bollinger Bands
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/60e8c84d0408737eb32a82a893b52dad7a301546cee08f83e26bd038b95220fd.png)
[trans]

## Overview
This strategy combines the Relative Strength Index (RSI) and Bollinger Bands to construct a short-term trading strategy. This strategy mainly uses the RSI indicator to conduct buying and selling operations when it breaks through the upper and lower Bollinger Bands. At the same time, the strategy also includes a stop-loss mechanism, which can effectively control risks.
## Strategy Principle
1. Calculate the RSI indicator value and set the parameters to 14 periods.
2. Calculate the middle line of Bollinger Bands. Here, the weighted moving average of RSI is used, and the period is set to 25.
3. Calculate the upper and lower rails of the Bollinger Bands. The upper rail is the midline plus amplitude, and the lower rail is the midline minus amplitude. The amplitude is set to 20 times the RSI standard deviation.   
4. When the RSI goes above the upper rail, go long; when the RSI goes below the upper rail, go short.
5. Set up a stop loss mechanism. If the price drops below 6% of the purchase price after going long, the loss will be stopped.
## Advantage Analysis
This strategy combines the RSI indicator and Bollinger Bands to effectively utilize the advantages of both for short-term trading. The main advantages are as follows:
1. RSI can effectively determine whether the market is overbought or oversold. Combined with the upper and lower Bollinger Bands, the accuracy of the signal can be improved.
2. Bollinger Bands upper and lower track Dynamic, which can automatically adjust the range according to the degree of market fluctuations.
3. The stop loss mechanism is reasonably set, with a stop loss range of 6%, which can not only tolerate normal fluctuations, but also effectively control losses.
## Risk Analysis
This strategy also has certain risks, mainly reflected in:
1. The RSI indicator has hysteresis and may miss the opportunity for rapid reversal. 
2. Improper Bollinger Band parameter settings, or severe market fluctuations, can also lead to signal errors.
3. The stop loss position setting is unreasonable and may be too broad or too aggressive, increasing unnecessary losses.
Countermeasures and solutions:
1. You can consider combining it with other indicators, such as KDJ, etc., to comprehensively judge the market situation.
2. Dynamically optimize Bollinger Band parameters and adjust parameters according to different markets.
3. Test and optimize the stop loss position and set the best parameters.
## Optimization direction
This strategy also has room for further optimization:
1. You can consider adjusting the stop loss from a fixed range to a stop loss with dynamic tracking. In this way, the stop loss position can be flexibly adjusted according to price fluctuations.
2. On the basis of Bollinger Bands, the judgment rule of Bollinger Band Width Index (BBW) can be added. When the Bollinger Bands expand or contract too much, you can pause trading to avoid false signals.
3. It can be combined with trading volume indicators, such as energy tide, to increase the conditions for volume and price confirmation. This can further avoid false breakthroughs.
## Summarize
Overall, this strategy is a relatively stable and reliable short-term trading strategy. It combines the advantages of RSI indicator to judge overbought and oversold, and the characteristics of Bollinger Bands to automatically track the fluctuation range, forming a short-term strategy with certain advantages. After parameter optimization and rule optimization, this strategy can obtain relatively stable returns.
||

## Overview

This strategy combines the Relative Strength Index (RSI) and Bollinger Bands to construct a short-term trading strategy. It mainly utilizes the buy and sell signals when RSI breaks through the upper or lower Bollinger Bands. Meanwhile, a stop loss mechanism is included to effectively control risks.

## Strategy Logic   

1. Calculate the RSI indicator with a 14-period parameter.  
2. Calculate the Bollinger Midband using the weighted moving average of RSI, with a period set to 25.
3. Calculate the Upper Band and Lower Band of Bollinger Bands. The Upper Band is the Midband plus the amplitude, while the Lower Band is the Midband minus the amplitude. The amplitude is set to 20 times the RSI standard deviation.    
4. Go long when RSI breaks through the Lower Band, and go short when RSI breaks through the Upper Band.  
5. Set a stop loss mechanism that if the price drops below 6% of the long entry price, close the long position.

## Advantage Analysis

This strategy combines the strengths of both RSI and Bollinger Bands for short-term trading. The main advantages are:  

1. RSI can effectively determine overbought and oversold scenarios. Combining Bollinger Bands adds accuracy to the trading signals. 
2. Bollinger Bands are dynamic to automatically adjust the range based on market volatility. 
3. The stop loss setting is reasonable with 6% tolerance for normal fluctuations while controlling losses.

## Risk Analysis   

Potential risks of this strategy includes:    

1. RSI has lagging characteristics and may miss fast reversal opportunities.  
2. Incorrect Bollinger Bands parameter or drastic market swings can cause bad signals.
3. Stop loss parameter set unwisely may lead to unnecessary losses. 

Solutions:  

1. Consider combining with other indicators like KDJ for comprehensive judgment.  
2. Dynamically optimize parameters for different markets.   
3. Backtest and optimize stop loss parameter for best setting.

## Optimization Directions   

There is room for further optimization:

1. Change fixed stop loss to dynamic trailing stop loss according to price fluctuation. 
2. Add Bollinger Band Width Index rules to pause trading when Bands expand or contract too much.  
3. Combine volume indicators like Chaikin Money Flow for better confirmation.

## Summary  

In summary, this is a relatively stable and reliable short-term trading strategy. By combining the strengths of overbought-oversold judgment of RSI and the adaptive range of Bollinger Bands, it forms an advantageous short-term system. With parameter tuning and logic refinement, this strategy can achieve consistent profits.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|len_rsi|
|v_input_2|25|len_bb|
|v_input_3|20|mul10|
|v_input_4|94|stop loss rate|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-12 00:00:00
end: 2023-10-13 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("rsi+bb st", shorttitle="rsibb st 0.3")

len_rsi=input(14)
len_bb = input(25)
mul10 = input(20.0)
mul=mul10/10
sl100 = input(94.0, title='stop loss rate')
sl=sl100/100

lw = 3

vwma_e(src, len) =>
    ema(src*volume, len)/ema(volume,len)

rsi = rsi(close, len_rsi)
plot(rsi, color=blue, title= 'rsi blue', linewidth=lw)
plot(70, color=gray, title='line 70', linewidth=lw)
plot(30, color=gray, title='line 30', linewidth=lw)

bbg = stdev(rsi, len_bb)*mul
bbc = vwma_e(rsi, len_bb)
//bbc=ema(rsi,len_bb)
ratio = 0.6
bbc := bbc*ratio + 50*(1-ratio)

bbu = bbc+bbg
bbl = bbc-bbg
plot(bbu, color=green, title='bb_up green', linewidth=lw)
plot(bbl, color=red, title='bb_low red', linewidth=lw)
plot(bbc, color=#808000ff, title='bb center', linewidth=lw)

plot(50, color=black)

lc = crossover(rsi, bbl) //or crossover(rsi, bbc)
sc = crossunder(rsi, bbu)

last_pos = 0*close
if lc
    last_pos := 1
else
    last_pos := last_pos[1]
if sc
    last_pos := 2

last_price = 0*close
if last_pos[1] !=1 and last_pos == 1
    last_price := close
else
    last_price := last_price[1]
    
if last_pos==1 and close < last_price*sl
    lc:=false
    sc:=true
    last_pos:=2

if (lc)
    strategy.entry("long", strategy.long)

if (sc)
    strategy.entry("short", strategy.short)
```

> Detail

https://www.fmz.com/strategy/435843

> Last Modified

2023-12-19 11:31:09
