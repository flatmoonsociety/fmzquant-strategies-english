
> Name

Bollinger Bands Backtest Strategy Based on Trend Trader Average Trend-Trader-Bands-Backtest-Strategy-Based-on-Trend-Trader-Moving-Average
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/152ae6aaf78c490087c.png)
[trans]

## Overview
The main idea of ​​this strategy is to use moving averages and Bollinger Bands to judge price trends and generate trading signals. Specifically, the average true fluctuation range ATR of a certain period is first calculated, and then the limit channel is obtained by combining the highest price and the lowest price. If the price breaks out of the channel, let the close price equal the channel price. Then find the moving average of the closed price after the limit, and then draw the banding above and below it to form a trading signal. Go long when the price breaks through the upper band of Bollinger Bands, and go short when it breaks through the lower band of Bollinger Bands.
## Strategy Principle
This strategy first calculates the ATR fluctuation range, and then combines it with the highest price and lowest price to obtain the limit channel. Only when the price breaks through the channel, the close price will be limited to the channel price. Then find the moving average of the closed price after the limit. This moving average is called the Trend Trade AVR. This moving average reflects the mid- to long-term trend direction of prices. Finally, draw a parallel line above and below the Trend Trader Average as the upper and lower Bollinger Bands. When the price breaks through the upper Bollinger Band, a long signal is generated, and when the price breaks through the lower Bollinger Band, a short signal is generated.
The core of this strategy to judge the trend is the trend trader average line, which reflects the medium and long-term trend direction. The function of Bollinger Bands is to filter out some false breakthroughs and make trading signals more reliable. The entire strategy combines trend tracking and breakthrough judgment to form a strong trend system.
## Strategic Advantages
1. Use ATR combined with the highest and lowest prices to form a channel, which can effectively track market fluctuations
2. Trend traders use the average line to clearly determine the mid- and long-term trends.
3. Bollinger Bands filter false breakthroughs and improve signal quality
4. The system as a whole reflects a strong trend, and long-term holding can obtain good returns.
## Strategy Risk
1. When holding in the medium to long term, you may suffer large losses due to emergencies.
2. Improper parameter settings may lead to frequent transactions, increased transaction fees and slippage losses.
3. The effect is highly related to parameter settings, and it needs to be tuned to find the best parameters.
Countermeasures:
1. The position holding period can be shortened appropriately and losses should be stopped in time.
2. Optimize parameters so that the signal has a certain buffer
3. Use historical data and real offer to optimize parameters
## Strategy optimization direction
1. Study in more detail the parameter settings of different cycles in different markets
2. Test whether other indicators can be added to filter out false breakthroughs
3. Try to combine stop-loss strategies to control single losses
## Summarize
This strategy overall is a strong trend following system. It can judge market trends in the medium and long term and combine with Bollinger Bands to generate trading signals. Through parameter optimization, stable excess returns can be obtained. However, you also need to pay attention to risk control to avoid losses caused by major events during long-term holdings. Overall, this strategy deserves further study and optimization to achieve long-term sustained alpha.
||

## Overview

The main idea of this strategy is to judge price trends and generate trading signals using moving averages and Bollinger bands. Specifically, it first calculates the average true range (ATR) over a certain period to get volatility range, then combines highest and lowest prices to form a limiting channel. If price breaks through this channel, the close price is set to be the channel price. After that, it calculates moving average of the limited close prices, which is called Trend Trader moving average (AVR). Finally, draw Bollinger bands above and below Trend Trader moving average to form trading signals. Go long when price breaks through upper band, and go short when breaking through lower band.


## Strategy Logic

The strategy first calculates ATR range and forms a limiting channel combined with highest and lowest prices. The close price will be limited to the channel price only when it breaks through the channel. After that, it calculates Trend Trader moving average of the limited close prices, which reflects mid-long term trend direction. At last, draw a upper band and a lower band parallel to the Trend Trader moving average as Bollinger bands. Breaking through upper band generates long signal and breaking through lower band generates short signal.

The core of judging trend lies in Trend Trader moving average, which embodies mid-long term trend direction. The role of Bollinger bands is to filter some false breakouts and make trading signals more reliable. The whole strategy combines trend following and breakout, forming a strong trend system.

## Advantages

1. ATR and price range build an adaptive channel to track market volatility
2. Trend Trade AVR clearly judges mid-long term trend 
3. Bollinger Bands filter false breakouts and improve signal quality
4. The system reflects strong trend, long holding can obtain good returns

## Risks

1. Long holding may suffer huge loss due to some sudden events
2. Improper parameter setting may lead to over-trading, increasing transaction costs and slippage 
3. Performance relies heavily on parameter tuning

Solutions:
1. Properly reduce holding period and set stop loss
2. Optimize parameters to give signals enough buffer
3. Utilize historical data and live trading for parameter tuning

## Optimization Directions 

1. Research parameters settings on different markets and timeframes
2. Test whether other indicators can filter false breakouts  
3. Try to incorporate stop loss to limit per trade loss

## Conclusion

The strategy is overall a strong trend following system. It can judge mid-long term trend and generate trading signals combined with Bollinger bands. Through parameter optimization, it can obtain stable alpha. But risk control is also important to avoid huge losses due to some sudden events when holding for long term. Generally speaking, the strategy deserves further research and optimization for long term sustainable alpha.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|21|Length|
|v_input_2|21|LengthMA|
|v_input_3|20|BandStep|
|v_input_4|3|Multiplier|
|v_input_5|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-04 00:00:00
end: 2023-12-10 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 16/10/2018
// This is plots the indicator developed by Andrew Abraham 
// in the Trading the Trend article of TASC September 1998  
// It was modified, result values wass averages.
// And draw two bands above and below TT line.
////////////////////////////////////////////////////////////
strategy(title="Trend Trader Bands Backtest", overlay = true)
Length = input(21, minval=1),
LengthMA = input(21, minval=1),
BandStep = input(20),
Multiplier = input(3, minval=1)
reverse = input(false, title="Trade reverse")
avgTR      = wma(atr(1), Length)
highestC   = highest(Length)
lowestC    = lowest(Length)
hiLimit = highestC[1]-(avgTR[1] * Multiplier)
loLimit = lowestC[1]+(avgTR[1] * Multiplier)
ret = 0.0
ret :=  iff(close > hiLimit and close > loLimit, hiLimit,
         iff(close < loLimit and close < hiLimit, loLimit, nz(ret[1], 0)))
nResMA = ema(ret, LengthMA)        
pos = 0.0
pos := iff(close < nResMA - BandStep , -1,
       iff(close > nResMA + BandStep, 1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue ) 
barcolor(pos == -1 ? red: pos == 1 ? green : blue )
plot(nResMA, color= blue , title="Trend Trader AVR")
plot(nResMA+BandStep, color= red , title="Trend Trader UpBand")
plot(nResMA-BandStep, color= green, title="Trend Trader DnBand")
```

> Detail

https://www.fmz.com/strategy/434966

> Last Modified

2023-12-11 13:12:44
