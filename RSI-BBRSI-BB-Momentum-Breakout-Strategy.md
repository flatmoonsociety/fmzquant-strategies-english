
> Name

RSI-BB Momentum Breakout Strategy RSI-BB-Momentum-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/16aac6830cf06137396.png)
[trans]


## Overview
The RSI-BB momentum breakout strategy is a breakout strategy that combines the Relative Strength Index (RSI) and the Bollinger Bands indicator (BB). This strategy uses RSI to determine the market trend and overbought and oversold phenomena, and uses BB to determine the breakthrough point. When the RSI and BB indicators send out buy or sell signals at the same time, the corresponding buy or sell operation is performed.
## Strategy Principle
The code first calculates the two indicators RSI and BB.
The calculation method of RSI is:
```pine
up = rma(max(change(close), 0), 30) 
down = rma(-min(change(close), 0), 30)
rsi = down == 0 ? 100 : up == 0 ? 0 : 100 - (100 / (1 + up / down))
```

Among them, up counts the increase in the closing price in the past 30 days, down counts the decrease in the closing price in the past 30 days, and rsi is calculated based on the ratio of the increase and the decrease.
The calculation method of BB is:
```pine
basis = sma(close, 50)
dev = 0.2 * stdev(close, 50) 
upper = basis + dev
lower = basis - dev
```

Among them, basis is the 50-day moving average, dev is 0.2 times the standard deviation, and upper and lower are the midline and lower rails respectively.
bbi is the Bollinger Band width index, the calculation method is:
```pine 
bbr = close>upper? 1 : close<lower? -1 : 0
bbi = bbr - bbr[1]
```

bbr determines whether the current close breaks through the upper and lower rails. If it breaks through, it will be 1, if it falls below, it will be -1, otherwise it will be 0. bbi is the current bbr minus the bbr of the previous period. If it is greater than 0, it means an upward breakthrough, and if it is less than 0, it means a downward breakthrough.
After calculating RSI and BBI, the strategy’s trading signal judgment logic is:
```
long = rsi>52 and rsi<65 and bbi>0.11 and bbi<0.7 
short = rsi<48 and rsi>35 and bbi<-0.11 and bbi>-0.7
```

That is, when the RSI is in the range of 52-65, and the BBI is greater than 0.11 and less than 0.7, go long; when the RSI is in the range of 35-48, and the BBI is less than -0.11 and greater than -0.7, go short.
## Strategic Advantages
1. Combining the two indicators RSI and BB can more accurately determine the buying and selling point. RSI determines overbought and oversold, and BB determines the breakthrough point. The combination of the two is more reliable.
2. The RSI parameter is set to the 30-day line, which can filter out some noise in the market and identify the main trend.
3. The BB parameters are set to the 50-day line and 0.2 times the standard deviation, which can filter out shocks.
4. BBI adds filter conditions of 0.11 and 0.7 to filter out false breakthroughs.
5. The long and short range of RSI is set to 52-65 and 35-48. Increase the buffer to avoid missing buying and selling points.
## Strategy Risk
1. Breakthrough trading strategies are easy to be trapped, and stop loss needs to be set to control risks.
2. The backtest data may be overfitted, and the actual results may be different.
3. The market may undergo drastic changes, causing the stop loss to be broken down and resulting in large losses.
4. It is necessary to optimize the parameters of RSI and BB, including cycle parameters and buying and selling interval parameters.
5. The price setting of the order will also have a great impact on the effect of the firm offer.
## Strategy optimization direction
1. Test different RSI and BB parameter combinations to find the best parameters.
2. Add other indicators to judge filter signals, such as MACD, KD, etc.
3. Optimize and adjust the RSI interval parameters for buying and selling, and reduce the interval range to filter out more noise.
4. Optimize the filtering parameters of BBI and set up dynamic interval filtering for false breakthroughs.
5. Add trend judgment indicators to avoid counter-trend operations.
6. Test different stop loss methods and find the stop loss plan with the maximum retracement acceptable.
7. Test different ordering methods and find the ordering plan with the smallest impact on slippage.
## Summarize
The RSI-BB momentum breakout strategy combines the advantages of trend judgment and breakthrough judgment and performed well in backtesting. However, the effect of real offer may be affected by slippage and stop loss. It is necessary to optimize the parameters based on the backtest results and test different stop loss and order plans to find settings more suitable for real trading. In addition, parameters and filtering conditions need to be dynamically adjusted to respond to market changes. Overall, this strategy has certain practical value, but it requires continuous optimization and verification to produce stable results.
||


## Overview

The RSI-BB momentum breakout strategy combines the Relative Strength Index (RSI) and Bollinger Bands (BB) indicators for breakout trading. It uses RSI to determine market trends and overbought/oversold levels, and BB to identify breakout points. When both RSI and BB signals align, the strategy will enter long or short trades accordingly.

## Strategy Logic

The code first computes the RSI and BB indicators. 

The RSI is calculated as:

```pine
up = rma(max(change(close), 0), 30)
down = rma(-min(change(close), 0), 30) 
rsi = down == 0 ? 100 : up == 0 ? 0 : 100 - (100 / (1 + up / down))
```

Where up measures the upward price movement over 30 periods, down measures the downward price movement, and rsi is computed based on the ratio of up to down.

The BB is calculated as:

```pine 
basis = sma(close, 50)
dev = 0.2 * stdev(close, 50)
upper = basis + dev
lower = basis - dev
```

Where basis is the 50-period moving average, dev is 0.2 times the standard deviation, upper and lower are the bands.

bbi is the bollinger bandwidth index, computed as:

```pine
bbr = close>upper? 1 : close<lower? -1 : 0 
bbi = bbr - bbr[1]
```

bbr checks if close breaks upper or lower band. Breakout is 1, breakdown is -1, otherwise 0. bbi is the difference between current and previous bbr. Positive bbi indicates upward breakout, negative indicates downward.

The strategy signals are determined as: 

```
long = rsi>52 and rsi<65 and bbi>0.11 and bbi<0.7
short = rsi<48 and rsi>35 and bbi<-0.11 and bbi>-0.7 
```

Go long when RSI is between 52-65 and BBI is between 0.11 and 0.7. Go short when RSI is between 35-48 and BBI is between -0.11 and -0.7.

## Advantages

1. Combining RSI and BB provides more reliable signals. RSI gauges trend and overbought/oversold levels, BB identifies breakout.

2. 30-period RSI filters out some market noise and focuses on major trends. 

3. 50-period BB with 0.2 standard deviation helps filter out whipsaws.

4. BBI thresholds filter fake breakouts. 

5. RSI long/short zones of 52-65 and 35-48 provide some buffer to avoid missed trades.

## Risks

1. Breakout strategies are prone to being caught in whipsaws, need to manage risk with stop loss.

2. Backtest results may be overfitted, live performance may vary.

3. Extreme market moves may hit stop loss resulting in large losses.

4. RSI and BB parameters including periods and thresholds need to be optimized. 

5. Order price can significantly impact live performance.

## Enhancement Opportunities 

1. Test different combinations of RSI and BB parameters to find optimal settings.

2. Add other indicators like MACD, KD for signal filtration. 

3. Optimize RSI long/short zones to filter out more noise.

4. Optimize dynamic BBI thresholds to better filter fakeouts.

5. Add trend filter to avoid trading against major trend.

6. Test different stop loss techniques to find optimal risk control.

7. Test different order types to minimize slippage impact.

## Conclusion

The RSI-BB strategy combines the advantages of using trend and momentum indicators. Backtest results are promising but live performance may vary due to real-world factors like slippage and stop loss. Parameters and filters need to be optimized based on backtest results. Stop loss and order placement should also be evaluated for real-world effectiveness. The strategy has merit but requires ongoing enhancements and robustness testing to generate consistent results.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|50|length|
|v_input_2|0.2|Mult Factor|
|v_input_3|0.1|alertLevel|
|v_input_4|0.75|impulseLevel|
|v_input_5|false|showRange|
|v_input_6|250|TP|
|v_input_7|20|SL|
|v_input_8|false|TS|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-03 00:00:00
end: 2023-11-02 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
//Based on Larry Connors RSI-2 Strategy - Lower RSI
strategy(title="Spyfrat Strat", shorttitle="SpyfratStrat", overlay=true)
src = close, 
// BB Init
source = close
length = input(50, minval=1)
mult = input(0.2, title="Mult Factor", minval=0.001, maxval=50)
alertLevel=input(0.1)
impulseLevel=input(0.75)
showRange = input(false, type=bool)
//RSI CODE
up = rma(max(change(src), 0), 30)
down = rma(-min(change(src), 0), 30)
rsi = down == 0 ? 100 : up == 0 ? 0 : 100 - (100 / (1 + up / down))
//BB CODE
basis = sma(source, length)
dev = mult * stdev(source, length)
upper = basis + dev
lower = basis - dev
bbr = source>upper?(((source-upper)/(upper-lower))/10): source<lower?(((source-lower)/(upper-lower))/10) : 0.1
bbi = bbr - nz(bbr[1]) 
//Rule
long = rsi>52 and rsi<65 and  bbi>0.11 and bbi<0.7
short = rsi<48 and rsi>35 and  bbi<-0.11 and bbi>-0.7
//Trade Entry
strategy.entry("long", strategy.long, when=long)
strategy.entry("short", strategy.short, when=short)
//Trade Exit
TP = input(250) * 10
SL = input(20) * 10
TS = input(0) * 10
CQ = 100

TPP = (TP > 0) ? TP : na
SLP = (SL > 0) ? SL : na
TSP = (TS > 0) ? TS : na

strategy.exit("Close Long", "long", qty_percent=CQ, profit=TPP, loss=SLP, trail_points=TSP)
strategy.exit("Close Short", "short", qty_percent=CQ, profit=TPP, loss=SLP, trail_points=TSP)
```

> Detail

https://www.fmz.com/strategy/430977

> Last Modified

2023-11-03 15:02:19
