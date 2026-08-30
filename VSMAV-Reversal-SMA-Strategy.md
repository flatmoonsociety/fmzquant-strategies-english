
> Name

V-Reversal-SMA-Strategy based on V-shaped reversal indicator SMA strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/24111ab34412f504ca4efdb2ca0bf411f9769acdcd4f3f5c9be99fb529fc381d.png)
[trans]
## Overview
Based on the V-shaped reversal indicator, the SMA strategy calculates the absolute difference between the 14-day highest price of the stock price and the previous day's lowest price and the absolute difference between the 14-day lowest price and the previous day's highest price, and then calculates its 14-day simple moving average respectively to form VI+ and VI- curves. When VI+ crosses VI-, it is a bullish signal. When VI- crosses VI+, it is a short signal.
## Strategy Principle
The core indicators of this strategy are VI+ and VI-. Among them, VI+ reflects the power of bulls and VI- reflects the power of shorts. The specific calculation formula is as follows:
```
VMP = SUM(ABS(HIGH - LOW[1]),14)
VMM = SUM(ABS(LOW - HIGH[1]),14)  
STR = SUM(ATR(1),14)
VI+ = VMP/STR  
VI- = VMM/STR
```

In order to remove the shock of the curve, the 14-day simple moving average is calculated for VI+ and VI- respectively, and SMA (VI+) and SMA (VI-) are obtained. A long signal is generated when SMA(VI+) crosses above SMA(VI-); a short signal is generated when SMA(VI-) crosses below SMA(VI+).
In addition, the strategy will also combine the upward and downward states of VI+ and VI- to determine the trend, thereby filtering and only going long when the trend is downward and short when the trend is upward.
## Advantage Analysis
This strategy combines the trend status and the golden cross of the VI indicator, which can effectively filter out false signals and increase the probability of profit. Compared with the simple moving average strategy, its breakthrough signal is more reliable.
## Risk Analysis
This strategy mainly faces two risks:
1. The VI indicator can produce misleading signals in certain periods. At this time, it is necessary to combine trend filtering and stop loss to control risks.
2. Markets with high transaction fees and slippage costs are not suitable for this strategy and will significantly reduce profit margins.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize the period parameters of the VI indicator and find the best parameter combination.
2. Use machine learning methods to automatically identify misleading signals and improve signal quality.
3. Combine stop loss and capital management to optimize the exit mechanism and control the loss of a single transaction.
4. Optimize the selection of trading products and choose markets with lower transaction costs.
## Summarize
The SMA strategy based on the V-shaped reversal indicator is a relatively reliable trend following strategy by calculating the VI+ and VI- indicators and combining the trend status to determine the buying and selling timing. The advantage of this strategy is that the signal quality is good and it can effectively filter noise. However, there is also the risk of being trapped, and it needs to be constantly optimized to adapt to market changes.
||

## Overview

The V-Reversal SMA strategy calculates the 14-day absolute difference between the highest price and the previous day's lowest price, and the 14-day absolute difference between the lowest price and the previous day's highest price. Then it calculates their 14-day simple moving averages to form the VI+ and VI- curves. A buy signal is generated when VI+ crosses over VI-. A sell signal is generated when VI- crosses below VI+.

## Principle 

The core indicators of this strategy are VI+ and VI-. VI+ reflects bullish momentum while VI- reflects bearish momentum. The specific calculation formulas are as follows:

```
VMP = SUM(ABS(HIGH - LOW[1]),14)  
VMM = SUM(ABS(LOW - HIGH[1]),14)
STR = SUM(ATR(1),14)
VI+ = VMP/STR
VI- = VMM/STR
```

To remove oscillations in the curves, 14-day simple moving averages are calculated on VI+ and VI- to obtain SMA(VI+) and SMA(VI-). A bullish signal is generated when SMA(VI+) crosses over SMA(VI-). A bearish signal is generated when SMA(VI-) crosses below SMA(VI+).

In addition, the strategy also combines the upward and downward status of VI+ and VI- to judge the trend and filter out signals, going long only when the trend is down and going short only when the trend is up.

## Advantage Analysis

By combining trend status and golden/dead cross of the VI indicator, this strategy can effectively filter out false signals and improve profitability. Compared to simple moving average strategies, its breakout signals are more reliable.

## Risk Analysis

The main risks of this strategy are:

1. The VI indicator may generate misleading signals in certain periods. Trend filtering and stop loss should be used to control risks.

2. Markets with high trading costs and slippage are not suitable for this strategy as it would greatly reduce profit margin.

## Optimization Directions

The strategy can be optimized in the following aspects:

1. Optimize the parameters of the VI indicator to find the best parameter combination.

2. Use machine learning methods to automatically identify misleading signals and improve signal quality. 

3. Optimize exit mechanisms with stop loss and money management to control single trade loss.

4. Optimize trading products selection focusing on markets with lower trading costs.

## Conclusion

The V-Reversal SMA strategy determines trading signals by calculating the VI+ and VI- indicators and combining trend status. It is a relatively reliable trend following strategy. Its strength lies in high signal quality and ability to filter out noise. But it also faces risks of being trapped, requiring continuous optimizations to adapt to market changes.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Period|
|v_input_2|14|WMA Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
//@author=SIDD
//Sidd-Vortex strategy is using Vortex formula  to generate 4 signals Bullish1 Bullish2 and Bearish1 Bearish2.

//Bullish1 signal is getting generated when smooth ma of VIP is crossing over smooth ma of VIM and smooth VIM is falling from previous bar smooth VIM

//Bullish2 signal is getting generated when smooth ma of VIP is crossing over smooth ma of VIM and smooth VIP is rising from previous bar smooth VIP

//Bearish1 signal is getting generated when smooth ma of VIM is crossing over smooth ma of VIP and smooth VIP is falling from previous bar smooth VIP

//Bearish2 signal is getting generated when smooth ma of VIM is crossing over smooth ma of VIP and smooth VIM is rising from previous bar smooth VIM

//This strategy can be converted into study un-commenting the plotshape and 15th line strategy replace with study and overlay=false

strategy(title = "SIDD-Vortex", shorttitle="SIDD-VORTEX", format=format.price, precision=4,overlay=true)
period_ = input(14, title="Period", minval=2)
len = input(14, minval=1, title="WMA Length")

VMP = sum( abs( high - low[1]), period_ ) // sum of absolute current high and previous low with 14 period default
VMM = sum( abs( low - high[1]), period_ ) // sum of absolute current low and previous high with 14 period default
STR = sum( atr(1), period_ )  //sum of daily atr for 14 days
VIP = VMP / STR
VIM = VMM / STR

simpleMAVIP=wma(VIP, len) 
smmaVIP = 0.0
smmaVIP := na(smmaVIP[1]) ? simpleMAVIP : (smmaVIP[1] * (len - 1) + VIP) / len // finding the Smoothing average 

simpleMAVIM=wma(VIM, len) 
smmaVIM = 0.0
smmaVIM := na(smmaVIM[1]) ? simpleMAVIM : (smmaVIM[1] * (len - 1) + VIM) / len // finding the Smoothing average 


risingVIP = rising(smmaVIP, 1)
fallingVIP = falling(smmaVIP, 1)

lineColorVIP = smmaVIP > 0.95 and risingVIP  ? color.lime : smmaVIP > 0.95 ? #d65240 : smmaVIP < 0.95 and fallingVIP ? color.red : color.olive

risingVIM = rising(VIM, 1)
fallingVIM = falling(VIM, 1)

lineColorVIM = smmaVIM > 0.95 and risingVIM  ? color.red : smmaVIM > 0.95 ? color.olive : smmaVIM < 0.95 and fallingVIM ? color.lime : #d65240

plot(VIP, title="VI +", color=lineColorVIP)
plot(VIM, title="VI -", color=lineColorVIM) 

longCondition = crossover(smmaVIP,smmaVIM)
shortCondition = crossover(smmaVIM,smmaVIP)


if (longCondition and fallingVIM)
    strategy.entry("Bullish1", strategy.long)
if (shortCondition and fallingVIP)
    strategy.entry("Bearish1", strategy.short)

if (longCondition and risingVIP)
    strategy.entry("Bullish2", strategy.long)
if (shortCondition and risingVIM)
    strategy.entry("Bearish2", strategy.short)
    
//plotshape(longCondition and fallingVIM, color=color.lime, location=location.belowbar, style=shape.triangleup,size= size.large,text="Bullish",offset=0,textcolor=color.white)
//plotshape(longCondition and risingVIP, color=color.lime, location=location.belowbar, style=shape.labelup,size= size.large,text="Bullish",offset=0,textcolor=color.white)
//plotshape(Diff > 0 and direction>0, color=color.lime, location=location.belowbar, style=shape.arrowup,size= size.normal,offset=0)
    
//plotshape(shortCondition and fallingVIP  , color=color.red, location=location.abovebar, style=shape.triangledown, size= size.large,text="Bearish",offset=0,textcolor=color.white)
//plotshape( shortCondition and risingVIM  , color=color.red, location=location.abovebar, style=shape.labeldown, size= size.large,text="Bearish",offset=0,textcolor=color.white)



//band1 = hline(1.0  , title="Upper Line", linestyle=hline.style_dashed, linewidth=3, color=color.red)
//band0 = hline(0.5, title="Lower Line", linestyle=hline.style_dashed, linewidth=3, color=color.lime)
//fill(band1, band0, color=color.purple, transp=70)



```

> Detail

https://www.fmz.com/strategy/441997

> Last Modified

2024-02-18 15:04:34
