
> Name

Market reversal key point strategy WMX-Williams-Fractals-Reversal-Pivot-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/16a61b1fbe58739b0e1.png)
 [trans]

## Overview
This strategy uses the breakthrough principle of the William indicator and combines it with a specific form of K-line to design an efficient long-short position opening and closing model, so that it can accurately do long and short positions at key points of market reversal, capture short- and medium-term trends, and obtain excess returns.
## Strategy Principle
This strategy uses fractal points in the William indicator to identify reversal signals. When an upper or lower fractal appears, if the direction is consistent with the K-line entity, a trading signal will be generated.

Specifically, a custom indicator WMX Williams Fractals is defined in the strategy. The factor function is used in this indicator to determine the upper fractal (upFractal) and lower fractal (dnFractal).
The judgment logic of the upper parting type is: the highest price of the current K line is higher than the highest price of the previous n K lines (n is an adjustable parameter), thus forming a parting type that breaks through the upper part.
The judgment logic of the downward classification is: the lowest price of the current K-line is lower than the lowest price of the previous n K-lines, thus forming a breakthrough below the classification.
After obtaining the upper and lower types, determine whether they have changed, that is, from nothing to something or from something to nothing. At this time, the parting pattern has just formed, indicating a greater possibility of reversal.
Then combine the direction of the K-line entity to determine the specific trading signal. When the upper parting pattern is formed and Close is higher than Open, go long; when the lower parting pattern is formed and Close is lower than Open, go short.

## Strategic Advantages
1. Use the parting point of William indicator to determine the reversal time point. This is a mature and reliable technical indicator.
2. Confirm trading signals based on the physical direction of the K-line to avoid random chops in non-trend areas.
3. Few parameters, only need to adjust the parting cycle n, easy to test and optimize
4. Position opening rules can be flexibly set, such as position size, position closing conditions, etc., making it easy to apply in real transactions

## Strategy Risk
1. After the pattern is formed, the market may not completely reverse, and it needs to be judged based on the trend.
2. The stop loss position needs to be set carefully to prevent the loss from being stopped by noisy and huge market prices.
3. The parameter n needs to be adjusted according to different varieties. If the cycle is too large or too small, the effect will be affected.

Solution:
1. Indicators such as moving averages can be added to determine the general trend and avoid opening positions against the trend.
2. Dynamically trail the stop loss or set a reasonable retracement limit stop loss
3. Use the Walk Forward Analysis method to optimize parameters and find the best parameters

## Strategy optimization direction
1. The reversal strategy based on segmentation can easily result in multiple profits and then reversal leading to losses. You can consider adding trend filtering to further limit the trading range and reduce unnecessary reversal transactions.
2. The current stop loss method is relatively simple and cannot effectively track the market. You can try to add stop loss methods such as trailing stop loss, time stop loss, and dynamic stop loss.
3. Currently only the physical direction of the K line is judged. If more K-line information such as shadow lines and closing positions are taken into account, more accurate trading signals can be designed.

## Summarize
This strategy is a reversal strategy based on technical indicators. It uses the classification of the William indicator to capture the changing trend of the underlying stock at key points, and combines it with the K-line entity to form a trading signal, in order to achieve excess returns.
Compared with other reversal strategies, this strategy is designed through parametric design, with clear logic and easy to understand. Parameter adjustment is convenient and easy to test, and it can be directly put into real operation. In the next step, through further optimization of trend judgment and stop loss methods, it is expected to achieve better strategic effects.
||


## Overview  

This strategy adopts the Williams indicator fractal breakout principle and combines specific K-line patterns to design an efficient long and short opening and closing model. It can accurately go long and short at the key reversal points of market movements to capture medium and short term trends and obtain excess returns.

## Strategy Principle

This strategy uses the fractal points in the Williams indicator to determine reversal signals. When a top or bottom fractal appears and it is consistent with the K-line entity direction, a trading signal is generated.   

Specifically, a custom indicator called WMX Williams Fractals is defined in the strategy. It uses factor functions to determine the top fractal (upFractal) and bottom fractal (dnFractal).  

The top fractal logic is: the highest price of the current K-line is higher than the highest price of the previous n K-lines (n is an adjustable parameter), thus forming a top side breakout fractal.

The bottom fractal logic is: the lowest price of the current K-line is lower than the lowest price of the previous n K-lines, thus forming an bottom side breakout fractal.   

After getting the top and bottom fractals, determine whether they change, that is, from none to exist or vice versa. At this time, the fractal has just formed, indicating a greater possibility of reversal.

Then, combined with the K-line entity direction to determine specific trading signals. When the top fractal is formed and Close is higher than Open, go long. When the bottom fractal is formed and Close is lower than Open, go short.

## Strategy Advantages  

1. Use the Williams indicator fractal points to determine the reversal timing. It is a mature and reliable technical indicator.  

2. Combine the K-line entity direction to confirm trading signals and avoid choppy non-trend regions.   

3. Few parameters that only need to adjust the fractal period n, easy to test and optimize.  

4. Flexible settings for opening positions rules like position sizing, closing conditions, etc., easy to apply in live trading.

## Strategy Risks  

1. After the fractal forms, the market may not completely reverse, need to combine with trend judgment.  

2. Stop loss position setting needs to be cautious to prevent being knocked out by noisy huge volatility moves.

3. The n parameter needs to adjust for different products. If the period is too large or too small it will affect the results.  

Solutions:  

1. Can add indicators like moving average to judge major trend, avoid trading against trends.  

2. Use dynamic trailing stop loss or set reasonable drawdown based stop loss.  

3. Utilize Walk Forward Analysis to optimize parameters and find the optimal values.   

## Strategy Optimization Directions   

1. Fractal reversal strategies tend to form multiple profits then reverse again to form losses. Can consider adding trend filters to further limit trading range and reduce unnecessary reversal trades.   

2. Current simple stop loss method cannot effectively track market moves. Can try more advanced stop loss techniques like moving stop loss, time based stop loss, dynamic stop loss etc.   

3. Currently only use K-line entity direction. If considering more K-line information like wicks and close location, can design even more precise trade signals.  

## Conclusion  

This is a reversal strategy based on technical indicators. It utilizes the Williams indicator fractals to capture changes in the trend of the underlying at key pivot points, combined with K-line entity direction to form trade signals, aiming to achieve excess returns.   

Compared to other reversal strategies, this strategy features parameterized design for clear logic and easy understanding. It has flexible parameter adjustments for convenient testing, and can directly be applied in live trading. Next step further optimizations on trend filtering, stop loss methods etc. can improve strategy performance.  
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2|Periods|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-14 00:00:00
end: 2023-12-14 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © WMX_Q_System_Trading

//@version=4
SystemName="WMX Williams Fractals strategy V4"
InitCapital = 1000000
InitPosition = 100
InitCommission = 0.075
InitPyramidMax = 10
strategy(title=SystemName, shorttitle=SystemName, overlay=true, initial_capital=InitCapital, default_qty_type=strategy.percent_of_equity, default_qty_value=InitPosition, commission_type=strategy.commission.percent, commission_value=InitCommission)


//study("WMX Williams Fractals", shorttitle="WMX Fractals", format=format.price, precision=0, overlay=true)
// Define "n" as the number of periods and keep a minimum value of 2 for error handling.
n = input(title="Periods", defval=2, minval=2, type=input.integer)
h=close
l=close

factorh(High)=>
    upFractal = (                                                                                                          (High[n+2]  < High[n]) and (High[n+1]  < High[n]) and (High[n-1] < High[n]) and (High[n-2] < High[n]))
             or (                                                                               (High[n+3]  < High[n]) and (High[n+2]  < High[n]) and (High[n+1] == High[n]) and (High[n-1] < High[n]) and (High[n-2] < High[n]))
             or (                                                    (High[n+4]  < High[n]) and (High[n+3]  < High[n]) and (High[n+2] == High[n]) and (High[n+1] <= High[n]) and (High[n-1] < High[n]) and (High[n-2] < High[n]))
             or (                          (High[n+5] < High[n]) and (High[n+4]  < High[n]) and (High[n+3] == High[n]) and (High[n+2] == High[n]) and (High[n+1] <= High[n]) and (High[n-1] < High[n]) and (High[n-2] < High[n]))
             or ((High[n+6] < High[n]) and (High[n+5] < High[n]) and (High[n+4] == High[n]) and (High[n+3] <= High[n]) and (High[n+2] == High[n]) and (High[n+1] <= High[n]) and (High[n-1] < High[n]) and (High[n-2] < High[n]))
    upFractal
upFractal=factorh(h)
factorl(Low)=>
    dnFractal = (                                                                                                  (Low[n+2]  > Low[n]) and (Low[n+1]  > Low[n]) and (Low[n-1] > Low[n]) and (Low[n-2] > Low[n]))
             or (                                                                         (Low[n+3]  > Low[n]) and (Low[n+2]  > Low[n]) and (Low[n+1] == Low[n]) and (Low[n-1] > Low[n]) and (Low[n-2] > Low[n]))
             or (                                                (Low[n+4]  > Low[n]) and (Low[n+3]  > Low[n]) and (Low[n+2] == Low[n]) and (Low[n+1] >= Low[n]) and (Low[n-1] > Low[n]) and (Low[n-2] > Low[n]))
             or (                        (Low[n+5] > Low[n]) and (Low[n+4]  > Low[n]) and (Low[n+3] == Low[n]) and (Low[n+2] == Low[n]) and (Low[n+1] >= Low[n]) and (Low[n-1] > Low[n]) and (Low[n-2] > Low[n]))
             or ((Low[n+6] > Low[n]) and (Low[n+5] > Low[n]) and (Low[n+4] == Low[n]) and (Low[n+3] >= Low[n]) and (Low[n+2] == Low[n]) and (Low[n+1] >= Low[n]) and (Low[n-1] > Low[n]) and (Low[n-2] > Low[n]))
    
dnFractal=factorl(l)

U=valuewhen(upFractal[0]!= upFractal[1],l[0],3)
L=valuewhen(dnFractal[0]!=dnFractal[1],h[0],3)

longcon=crossover(close ,L) and close>open
shortcon=crossunder(close ,U) and close<open

if longcon
    
    strategy.entry("Long", strategy.long,   when = strategy.position_size <= 0 )
    
if  shortcon
    strategy.entry("Short", strategy.short,  when = strategy.position_size >= 0 )
        





```

> Detail

https://www.fmz.com/strategy/435469

> Last Modified

2023-12-15 10:37:01
