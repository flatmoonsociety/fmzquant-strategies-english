
> Name

Price-Volatility-Breakout-Strategy-Based-on-Double-Moving-Averages
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/72a02090ae2f96ebb1003b2379eb2311ac5ba258396f7dcdb1b8d2489d5295af.png)
[trans]


## Overview
The core idea of ​​this strategy is to use price volatility to judge the market trend. When the volatility rises, it means that the market is forming a new trend; when the volatility falls, it means that the current trend is ending. The strategy calculates the percentage change of the price and then performs double moving average filtering on it to obtain an indicator reflecting price volatility. A buy signal is generated when the indicator crosses above its signal line, and a sell signal is generated when it crosses below its signal line.
## Strategy Principle
The strategy first calculates the percentage change in price:
```
i=(src/nz(src[1], src))*100
```

Then through a moving average filter with a length of 35, the primary price volatility indicator pmol2 is obtained. Then perform secondary filtering on pmol2 through a moving average with a length of 20 to obtain the final price volatility index pmol. Finally, the pmol signal line pmols is obtained through a moving average with a length of 10. When pmol crosses pmols above, a buy signal is generated; when pmol crosses below pmols, a sell signal is generated.
## Advantage Analysis
- Using double moving average filtering, price volatility can be better extracted and noise filtered.
- Calculate the percentage change of price, which can amplify price changes and reflect trend changes more clearly.  
- The profit method is relatively clear: buy when the trend starts and sell when the trend ends.
## Risk Analysis
-Double moving average filtering will bring a certain degree of lag.
- The percentage change calculation method is sensitive to price range.
- When converting between bull and bear, positions must be closed promptly.
Optimization direction:
- Optimize the moving average parameters to improve the capture of trends.
- Try different ways of calculating price changes.
- Add filter conditions to avoid false signals.
## Summarize
This strategy extracts price volatility and determines changes in market trends by calculating percentage changes and double moving average filtering. It is a relatively mature technical indicator strategy. This strategy has a strong ability to capture trends, but its ability to identify transition points is average. It can be optimized by adjusting parameters and adding auxiliary conditions.
||


## Overview

The core idea of this strategy is to use price volatility to judge market trends. When volatility rises, it means the market is forming a new trend. And when volatility declines, it means the current trend is ending. The strategy calculates the percentage change of price and then filters it with double moving averages to get an indicator reflecting price volatility. It generates buy signals when the indicator crosses above its signal line, and sells signals when crossing below.

## Strategy Logic

The strategy first calculates the percentage change of price:

```
i=(src/nz(src[1], src))*100
```

Then it filters i with a 35-period moving average to get the preliminary volatility indicator pmol2. Pmol2 is filtered again with a 20-period moving average to get the final indicator pmol. Finally, a 10-period moving average of pmol is used as the signal line pmols. Buy when pmol crosses over pmols and sell when crossing below.

## Advantage Analysis  

- The double MA filtering extracts volatility well and filters out noise.
- Calculating percentage change amplifies price movements, making trend changes more visible.
- Profit model is clear: buy at trend start, sell at trend end.

## Risk Analysis

- Double filtering causes some lag. 
- Percentage change calculation is sensitive to price amplitude.
- Need timely exits at bull-bear transitions.

## Optimization Directions

- Optimize MA parameters to improve trend catching.
- Try different price change calculation methods. 
- Add filters to avoid wrong signals.

## Summary   

This strategy uses percentage change and double MA filtering to extract price volatility and judge trend changes. It belongs to the relatively mature technical indicator strategies. The strategy has good trend catching capability but medium turning point recognition capability. Can optimize via parameter tuning and adding auxiliary conditions.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|35|First Smoothing|
|v_input_3|20|Second Smoothing|
|v_input_4|10|Signal Smoothing|
|v_input_5|false|Enable Bar Colors|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-01 00:00:00
end: 2023-12-07 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("Strategy for DPMO", overlay=true)

src=input(close, title="Source")
length1=input(35, title="First Smoothing")
length2=input(20, title="Second Smoothing")
siglength=input(10, title="Signal Smoothing")
ebc=input(false, title="Enable Bar Colors")

upSign = '↑' // indicates the indicator shows uptrend
downSign = '↓' // incicates the indicator showing downtrend
exitSign ='x' //indicates the indicator uptrend/downtrend ending

calc_csf(src, length) => 
	sm = 2.0/length
	csf=(src - nz(csf[1])) * sm + nz(csf[1])
	csf
i=(src/nz(src[1], src))*100
pmol2=calc_csf(i-100, length1)
pmol=calc_csf( 10 * pmol2, length2)
pmols=ema(pmol, siglength)
d=pmol-pmols
hc=d>0?d>d[1]?lime:green:d<d[1]?red:orange

buyDPMO = hc==lime and hc[1]!=lime
closeBuyDPMO = hc==green and hc[1]!=green
sellDPMO = hc==red and hc[1]!=red
closeSellDPMO = hc==orange and hc[1]!=orange

plotshape(buyDPMO, color=lime, style=shape.labelup, textcolor=#000000, text="DPMO", location=location.belowbar, transp=0)
plotshape(closeBuyDPMO, color=green, style=shape.labelup, textcolor=#ffffff,  text="X", location=location.belowbar, transp=0)
plotshape(sellDPMO, color=red, style=shape.labeldown, textcolor=#000000, text="DPMO", location=location.abovebar, transp=0)
plotshape(closeSellDPMO, color=orange, style=shape.labeldown, textcolor=#ffffff,  text="X", location=location.abovebar, transp=0)
barcolor(ebc?hc:na)


strategy.entry("Long", strategy.long, when=buyDPMO)
strategy.close("Long", when=closeBuyDPMO or sellDPMO)   
strategy.entry("Short", strategy.short, when=sellDPMO)
strategy.close("Short", when=closeSellDPMO or buyDPMO)  

```

> Detail

https://www.fmz.com/strategy/434712

> Last Modified

2023-12-08 16:44:22
