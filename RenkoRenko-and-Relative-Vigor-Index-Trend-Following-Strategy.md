
> Name

Trend following strategy based on Renko and Relative Vigor Index Renko-and-Relative-Vigor-Index-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/9f9b347ecbb86630734cb18eef618a26d933c60e9374becc0bf9ea5a899a057f.png)
[trans]

## Overview
This strategy combines two indicators, the Renko chart and the Relative Vitality Index (RVI), with the goal of capturing most of the market's main trends. Applicable to mainstream products such as Bitcoin and Hang Seng Index.
## Strategy Principle
The strategy uses 9-period ATR to construct a Renko brick. When the closing price exceeds the high point of the previous Renko brick, a new brick is constructed, and the color is green; when the closing price is lower than the low point of the previous Renko brick, a new brick is constructed, and the color is red. Combined with the RVI indicator to determine the trend direction.
The RVI indicator is used to determine the relative strength of bullish and bearish power. The RVI value fluctuates between 0 and 1. If it is higher than 0.5, it means that the bulls are stronger than the bears; if it is lower than 0.5, it means that the bears are stronger than the bulls. When RVI crosses its smooth moving average, it means that the power of shorts weakens and the power of bulls increases, giving a long signal; when RVI crosses below its smooth moving average, it means that the power of bulls weakens and the power of shorts strengthens, giving a short signal.
Based on the long and short signals of the Renko brick direction and the RVI indicator, enter the corresponding long or short position.
## Strategic Advantages
1. Renko brick isolates normal market fluctuations and only focuses on larger price changes to avoid being trapped.
2. The RVI indicator determines the timing of trend reversal and further locks in trading signals.
3. Combining two indicators for filtering can effectively capture the main market trends and filter out some noise.
## Risk Analysis
1. The size of the Renko brick directly affects the transaction frequency. If the brick is too large, opportunities will be missed, and if the brick is too small, the transaction frequency and handling fees will increase.
2. Improper setting of RVI indicator parameters will also lead to missed signals or an increase in false signals.
3. Dual indicator filtering will miss certain signals and fail to capture all market trends.
## Optimization direction
1. Dynamically optimize the Renko brick size to adapt to market volatility.
2. Optimize RVI indicator parameters and find the best balance point.
3. Try different varieties and cycle parameter combinations to evaluate stability.
## Summarize
This strategy combines the advantages of two different types of indicators and aims to capture the mainstream trend of the market. By optimizing the Renko and RVI parameters, higher stability can be achieved. However, no model can be perfect, and it is inevitable to miss certain signals. The key is to grasp the main direction. Users need to clearly evaluate their own risk preferences and choose the varieties and parameters that suit them.
||

## Overview

This strategy combines the Renko charts and Relative Vigor Index (RVI) to capture most of the major market trends. It works well on major symbols like BTCUSD, HSI etc.

## Strategy Logic  

The strategy constructs Renko bricks based on 9 period ATR. A new green brick is constructed when close price exceeds the previous brick's high. A new red brick is constructed when close price falls below the previous brick's low. The trend direction is determined by RVI indicator.

RVI oscillates between 0-1 to measure the relative strength between buying and selling pressure. Above 0.5 represents stronger buying pressure while below 0.5 represents stronger selling pressure. RVI crossing above its smooth moving average gives buy signal as selling pressure eases. RVI crossing below gives sell signal as buying pressure eases.

Combine the Renko brick direction and RVI signals to enter long or short positions accordingly.

## Advantages

1. Renko bricks filter out normal market noise and only react to significant price movement, avoiding whipsaws.  
2. RVI helps identifying trend reversal, further confirming trading signals.
3. Combining two indicators filters out some noise and enables capturing major trends.

## Risks

1. Brick size directly affects trading frequency. Bricks too large may miss opportunity while too small increases costs.
2. Improper RVI parameters may cause missing signals or more false signals.  
3. Double filtering misses some trading opportunity.  

## Enhancement  

1. Dynamic brick size to adapt changing volatility.
2. Optimize RVI parameters to find best balance.
3. Test stability across different symbols and timeframes.  

## Conclusion  

This strategy combines two different types of indicators to capture major trends. Further optimization on Renko and RVI parameters can improve stability. No model is perfect and missing some trades is inevitable. Users need to assess their own risk preference and choose proper symbol/parameter combo.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|D|TimeFrame|
|v_input_2|9|ATR length|
|v_input_3|5|SMA length|
|v_input_4|20|SMA CurTF length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-28 00:00:00
end: 2024-02-03 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Lancelot RR Strategy", overlay=false)
p=9
CO=close-open
HL=high-low
value1 = (CO + 2*CO[1] + 2*CO[2] + CO[3])/6
value2 = (HL + 2*HL[1] + 2*HL[2] + HL[3])/6
num=sum(value1,p)
denom=sum(value2,p)
RVI=denom!=0?num/denom:0
RVIsig=(RVI+ 2*RVI[1] + 2*RVI[2] + RVI[3])/6

rvicloselongcondition = crossunder(RVI, RVIsig)
rvicloseshortcondition = crossover(RVI, RVIsig)

plot(RVI,color=green,style=line,linewidth=1)
plot(RVIsig,color=red,style=line,linewidth=1)
bgcolor(rvicloseshortcondition ? green : na, transp = 75)
bgcolor(rvicloselongcondition ? red : na, transp = 75)

///Renko///
TF = input(title='TimeFrame', defval="D")
ATRlength = input(title="ATR length",  defval=9, minval=2, maxval=100)
SMAlength = input(title="SMA length",  defval=5, minval=2, maxval=100)
SMACurTFlength = input(title="SMA CurTF length",  defval=20, minval=2, maxval=100)

HIGH = request.security(syminfo.tickerid, TF, high)
LOW = request.security(syminfo.tickerid, TF, low)
CLOSE = request.security(syminfo.tickerid, TF, close)
ATR = request.security(syminfo.tickerid, TF, atr(ATRlength))
SMA = request.security(syminfo.tickerid, TF, sma(close, SMAlength))
SMACurTF = sma(close, SMACurTFlength)

RENKOUP = na
RENKODN = na
H = na
COLOR = na
BUY = na
SELL = na
UP = na
DN = na
CHANGE = na

RENKOUP := na(RENKOUP[1]) ? ((HIGH+LOW)/2)+(ATR/2) : RENKOUP[1]
RENKODN := na(RENKOUP[1]) ? ((HIGH+LOW)/2)-(ATR/2) : RENKODN[1]
H := na(RENKOUP[1]) or na(RENKODN[1]) ? RENKOUP-RENKODN : RENKOUP[1]-RENKODN[1]
COLOR := na(COLOR[1]) ? white : COLOR[1]
BUY := na(BUY[1]) ? 0 : BUY[1]
SELL := na(SELL[1]) ? 0 : SELL[1]
UP := false
DN := false
CHANGE := false

if(not CHANGE and close >= RENKOUP[1]+H*3)
    CHANGE := true
    UP := true
    RENKOUP := RENKOUP[1]+ATR*3
    RENKODN := RENKOUP[1]+ATR*2
    COLOR := lime
    SELL := 0
    BUY := BUY+3

if(not CHANGE and close >= RENKOUP[1]+H*2)
    CHANGE := true
    UP := true
    RENKOUP := RENKOUP[1]+ATR*2
    RENKODN := RENKOUP[1]+ATR
    COLOR := lime
    SELL := 0
    BUY := BUY+2

if(not CHANGE and close >= RENKOUP[1]+H)
    CHANGE := true
    UP := true
    RENKOUP := RENKOUP[1]+ATR
    RENKODN := RENKOUP[1]
    COLOR := lime
    SELL := 0
    BUY := BUY+1

if(not CHANGE and close <= RENKODN[1]-H*3)
    CHANGE := true
    DN := true
    RENKODN := RENKODN[1]-ATR*3
    RENKOUP := RENKODN[1]-ATR*2
    COLOR := red
    BUY := 0
    SELL := SELL+3

if(not CHANGE and close <= RENKODN[1]-H*2)
    CHANGE := true
    DN := true
    RENKODN := RENKODN[1]-ATR*2
    RENKOUP := RENKODN[1]-ATR
    COLOR := red
    BUY := 0
    SELL := SELL+2

if(not CHANGE and close <= RENKODN[1]-H)
    CHANGE := true
    DN := true
    RENKODN := RENKODN[1]-ATR
    RENKOUP := RENKODN[1]
    COLOR := red
    BUY := 0
    SELL := SELL+1
    
plotshape(UP, style=shape.arrowup, location=location.bottom, size=size.normal)

renkolongcondition = UP
renkoshortcondition = DN

///Long Entry///
longcondition = UP
if (longcondition)
    strategy.entry("Long", strategy.long)
    
///Long exit///
closeconditionlong = rvicloselongcondition
if (closeconditionlong)
    strategy.close("Long")
```

> Detail

https://www.fmz.com/strategy/440997

> Last Modified

2024-02-04 15:49:19
