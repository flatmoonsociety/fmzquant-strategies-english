
> Name

Dynamic-Support-Resistance-Breakout-Trend-Strategy Dynamic-Support-Resistance-Breakout-Trend-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/5d2296c9e095a86b13.png)
[trans]

## Overview
This strategy determines the trend direction based on the breakthrough of long-term support and resistance, and uses the breakthrough of support and resistance as the entry opportunity. It uses polylines to define highs and lows, and 2 K-lines to confirm highs/lows, so there is a lag of 2 K-lines. It calculates the SMA difference between the high and low points within a certain period (default 21) as an auxiliary support and resistance level. This idea comes from synapticEx's Nebula-Advanced-Dynamic-Support-Resistance indicator. When the price breaks through the dynamic support resistance, go long and short.
## Strategy Principle
This strategy uses the following logic to determine trends and trading signals:
1. Use broken lines to determine the high and low points: Among the current five K lines, if the low point of the fifth K line is lower than the fourth K line, the fourth K line is lower than the third K line, the third K line is higher than the second K line, and the second K line is higher than the first K line, confirm that the low point of the third K line is the lowest low point. The same goes for judging high points.
2. Calculate the number of high points hn and the number of low points ln within a certain period (default 21). If hn>0 and ln>0, calculate the average value of high points hsum/hn and the average value of low points lsum/ln within a certain period. The difference r between them serves as an auxiliary support and resistance level.
3. Compare the closing price with the dynamic resistance lvalr and support level hvalr to determine the trend direction. A breakout is valid if the closing price exceeds one of the two.
4. When it effectively breaks through the dynamic resistance line, go long; when it effectively breaks through the dynamic support line, go short.
## Advantage Analysis
This strategy has the following advantages:
1. Using broken lines to judge support and resistance is more accurate and can avoid false breakthroughs.
2. Support and resistance based on long-term statistics have more reference value and can reduce position risks.
3. Introduce auxiliary support and resistance to improve the effectiveness of breakthroughs.
4. The strategy logic is simple and clear, easy to understand and implement, and is suitable for quantitative trading.
5. The resistance statistical period can be customized to adapt to different periods and varieties.
## Risk Analysis
There are also some risks with this strategy:
1. The broken line determines the support and resistance point with a lag of 2 K lines, and the best entry point may be missed.
2. The predicted support and resistance are for reference only, and the price may still experience unexplained breakthroughs.
3. Improper statistical period length may cause support and resistance to fail.
4. Price adjustments after a breakout may trigger stop losses.
5. After entering into long or short positions, the price may fluctuate violently, resulting in greater losses.
Corresponding risk control and optimization methods include:
1. Appropriately shorten the statistical period and reduce lag.
2. Combine more factors to predict support and resistance levels.
3. Test the stability of different cycle parameters.
4. Set a reasonable stop loss level.
5. Use position control methods to limit single losses.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Use machine learning methods to predict support and resistance. Can increase the success rate of support resistance breakouts.
2. Combine the trading volume CONF indicator to determine the effectiveness of the breakthrough. A large amount of open interest participating in a breakout is more convincing.
3. Statistically classify support and resistance according to different periods. For example, separate statistics based on daily lines, weekly lines, etc. can improve the effectiveness of support and resistance levels.
4. Add positions to profitable positions and set free stops to balance profits and losses. This can ensure greater profits while ensuring profits.
5. Use moving average indicators to determine the trend and avoid blindly going long or short when there is no clear trend.
## Summarize
Overall, this strategy is a relatively robust and reliable trend following strategy. It has a higher probability of correctly judging the trend direction and has certain risk control measures. However, due to a certain lag, there is no 100% guarantee that every long and short sale will be profitable. Therefore, it is more suitable for experienced quantitative traders to apply with their own strategies. By optimizing statistical period parameters and combining with other indicators or models, this strategy can become an efficient trend following strategy.
||

## Overview

This strategy judges the trend direction based on the long-term support/resistance breakout and enters the position when the support/resistance is broken. It uses zigzag to define peaks and valleys, confirming peaks/valleys with 2 bars, so there is 2 bars lag. It calculates the difference between SMA of peaks and valleys in a defined period (21 by default) as alternative SR level. This idea is from synapticEx's Nebula-Advanced-Dynamic-Support-Resistance indicator. It goes long when resistance broken and goes short when support broken.

## Strategy Logic

The strategy uses the following logic to determine trends and trading signals:

1. Confirm peaks/valleys with zigzag: when in last 5 bars, bar 5 peak < bar 4 peak < bar 3 peak > bar 2 peak > bar 1 peak, bar 3 valley is confirmed as lowest valley. Confirm highest peak similarly.  

2. Calculate number of peaks hn and valleys ln in defined period (default 21). If hn>0 and ln>0, calculate average level of peaks hsum/hn and average level of valleys lsum/ln. Their difference r is used as alternative SR level.

3. Compare close price with dynamic resistance lvalr and support hvalr to determine trend direction. Breakout of either resistance or support is regarded as valid breakout.  

4. Go long when valid breakout of resistance happen. Go short when valid breakout of support happen.

## Advantage Analysis   

The advantages of this strategy:

1. Using zigzag to confirm SR provides accuracy, avoiding false breakout. 

2. SR based on long term statistics is more valuable to reduce risk.

3. Alternative SR improves validity of breakout signals.  

4. The logic is simple and easy to understand, suitable for quant trading.

5. Customizable statistic period fits different cycles and products.

## Risk Analysis

Risks of this strategy:

1. 2 bars lag with zigzag may miss best entry point.  

2. Predicted SR is just for reference, abnormal breakout can still happen.

3. Improper statistic period leads to invalid SR.

4. Price pullback after breakout may trigger stop loss. 

5. Violent price swing after entry brings larger loss.

The solutions are:

1. Shorten statistic period properly to reduce lag.

2. Combine more factors to predict SR.  

3. Test stability of different periods.

4. Set reasonable stop loss level.

5. Use position sizing to limit single loss.

## Optimization Directions   

The strategy can be optimized from aspects below:

1. Use machine learning to predict SR, improving success rate of breakout signals.  

2. Combine CONF volume to confirm validity of breakout signals. High open interests makes breakout more convincing.   

3. Classify statistic of SR based on different cycles, improving efficiency of SR.

4. Add position on profit, set trail stop to balance profit/loss. Earns more profit while locking gain.

5. Combine MA to determine trend, avoiding blindly long/short without trend.  

## Conclusion

In conclusion, this is a robust trend following strategy. It has high accuracy in determining trend direction and proper risk control. But the lag makes it impossible to profit from every long/short signal. So it fits experienced quant traders to combine with their own strategies. By optimizing statistic periods and integrating other indicators or models, it can become an efficient trend following strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|21|SR lookbak length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-25 00:00:00
end: 2023-12-25 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("SR TREND STRATEGY", shorttitle="SR TREND", overlay=true, calc_on_order_fills=true)
//based on by synapticEx SR indicator https://www.tradingview.com/script/O0F675Kv-Nebula-Advanced-Dynamic-Support-Resistance/
length = input(title="SR lookbak length", type=input.integer, defval=21)
h = bar_index>5 and high[5]<high[4] and high[4]<high[3] and high[3]>high[2] and high[2]>high[1] ? 1 : 0
l = bar_index>5 and low[5]>low[4]   and low[4]>low[3]   and low[3]<low[2]   and low[2]<low[1]   ? 1 : 0
ln = sum(l, length)
hn = sum(h, length)
hval =  h>0 ? high[3] : 0
lval =  l>0 ? low[3]  : 0
lsum = sum(lval, length)
hsum = sum(hval, length)
r = ln>0 and hn>0 ? abs((hsum/hn) - (lsum/ln)): 0
float lvalc = na
float lvalr = na
float hvalc = na
float hvalr = na
lvalc := lval and r>0 ? lval   : lvalc[1]
lvalr := lval and r>0 ? lval+r : lvalr[1]
hvalc := hval and r>0 ? hval   : hvalc[1]
hvalr := hval and r>0 ? hval-r : hvalr[1]
int trend=0
trend:=close > lvalr and close > hvalr ? 1 : close < lvalr and close < hvalr ? -1 : trend[1]
strategy.close("Long", when=trend==-1)
strategy.close("Short", when=trend==1)
strategy.entry("Long", strategy.long, when=trend==1 and close>hvalc)
strategy.entry("Short", strategy.short, when=trend==-1 and close<lvalc)
int long=0
int short=0
long:= trend==1 and close>hvalc ? 1 : trend==-1 ? -1 : long[1]
short:= trend==-1 and close<lvalc ? 1 : trend==1 ? -1 : short[1]
barcolor(long>0? color.green : short>0? color.red : trend>0? color.white: trend<0 ? color.orange : color.blue)
```

> Detail

https://www.fmz.com/strategy/436641

> Last Modified

2023-12-26 15:21:45
