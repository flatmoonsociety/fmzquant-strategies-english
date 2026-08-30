
> Name

Weighted-Quantitative-Moving-Average-Crossover-Trading-Strategy Based on Weighted Moving Average Crossover
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/353fc28e7f642e129839165cfa35e1e4bd754127abc1de4d0242c9a7ebc5cf50.png)
[trans]


## Overview
This strategy is called **Weighted Quantitative Moving Average Crossover Strategy** (Weighted Quantitative Moving Average Crossover Strategy). Its basic idea is to combine multiple indicators such as price and trading volume to design fast lines and slow lines, and send out buy and sell signals when they occur golden crosses or dead crosses.
## Strategy Principle
The core indicator of this strategy is the Quantitative Moving Average (QMA). QMA measures trend direction by calculating a weighted average price over a period of time. It differs from an ordinary moving average in that the weight of price (weight = price * trading volume) will decay over time. This way, the most recent prices are given greater weight and can respond to market changes more quickly.
Specifically, this strategy constructs a fast QMA line and a slow QMA line. The fast line parameters are set to 25 days, and the slow line parameters are set to 29 days. When the fast line crosses the slow line from below, a buy signal is generated; when the fast line crosses the slow line from above, a sell signal is generated.
## Advantage Analysis
Compared with ordinary moving averages, this strategy has the following advantages:
1. Respond to the market more quickly and seize short-term opportunities in a timely manner
2. It combines multiple dimensions of price and trading volume and has stronger stability.
3. Flexible parameter settings can adapt to different market environments
## Risk Analysis
This strategy also has some risks:
1. Frequent short-term operations can easily increase transaction costs and slippage.
2. Over-optimization of PARAMETERS may lead to curve fitting
3. When the trading volume is insufficient, the indicator effect may be compromised.
The above risks can be mitigated by appropriately adjusting parameter frequencies, strict walk forward analysis, and combining with other indicators.
## Optimization direction
There is still room for further optimization of this strategy:
1. Dynamically adjust the parameters of QMA so that it can adapt according to the degree of market fluctuations.
2. Filter entry opportunities based on volatility, trading volume and other indicators
3. Add stop loss strategy to control single loss
## Summarize
Generally speaking, this strategy is a short-term trading strategy with good stability. Compared with a single price average, its indicator can better reflect the market supply and demand relationship. Through parameter adjustment and the introduction of risk control methods, this strategy can operate stably in the long term and obtain good returns.
||

## Overview

This strategy is named **Weighted Quantitative Moving Average Crossover Strategy**. The basic idea is to design fast and slow lines based on price, trading volume and other indicators, and generate buy and sell signals when golden cross and dead cross occur between them.

## Strategy Logic

The core indicator of this strategy is Quantitative Moving Average (QMA). QMA measures the trend direction by calculating the weighted average price over a period of time. Different from regular moving average, the weights (weight = price * trading volume) of prices in QMA will decay over time. Thus, the latest prices have bigger weights which can respond to the market change more rapidly.

Specifically, this strategy builds fast QMA line with 25 days and slow QMA line with 29 days. It will generate buy signal when fast line crosses above slow line, and sell signal when fast line crosses below slow line. 

## Advantage Analysis 

Compared with regular moving average, this strategy has the following advantages:

1. Respond to the market more promptly, which enables it to capture short-term opportunities.  
2. Combine multiple dimensions including price and trading volume, which makes it more stable.
3. Flexible parameter settings to adapt to different market environments.

## Risk Analysis

This strategy also has some risks:  

1. High trading frequency of short-term operations, which may lead to increased transaction costs and slippages.
2. Overfitting due to excessive parameter optimization.  
3. Indicator effect may be compromised when the trading volume is insufficient.

The above risks could be mitigated by appropriately adjusting the frequency, strictly walk forward analysis, and incorporating other indicators.

## Improvement Directions

There is still room for further optimization of this strategy:

1. Dynamically adjust the parameters of QMA to make it self-adaptive to market volatility.
2. Filter trading opportunities with indicators like volatility and trading volume. 
3. Add stop loss strategies to control single loss.

## Conclusion  

In general, this is a stable short-term trading strategy. Compared with single price average, its indicator can better reflect the supply-demand relationship in the market. With proper parameter tuning and risk management, this strategy can operate steadily for the long run and gain sound profit.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|9|From Month|
|v_input_2|true|From Day|
|v_input_3|2018|From Year|
|v_input_4|true|To Month|
|v_input_5|true|To Day|
|v_input_6|9999|To Year|
|v_input_7|25|FastMA|
|v_input_8|29|SlowMA|
|v_input_9|9|Smoothing_period|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-29 00:00:00
end: 2023-12-05 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Brad VWMACD Strategy 2233", overlay=false, max_bars_back=500,default_qty_type=strategy.percent_of_equity,commission_type=strategy.commission.percent, commission_value=0.18, default_qty_value=100)

// === INPUT BACKTEST RANGE === 
FromMonth = input(defval = 9, title = "From Month", minval = 1, maxval = 12)
FromDay   = input(defval = 1, title = "From Day", minval = 1, maxval = 31)
FromYear  = input(defval = 2018, title = "From Year", minval = 2017)
ToMonth   = input(defval = 1, title = "To Month", minval = 1, maxval = 12)
ToDay     = input(defval = 1, title = "To Day", minval = 1, maxval = 31)
ToYear    = input(defval = 9999, title = "To Year", minval = 2017)

// === FUNCTION EXAMPLE ===
start     = timestamp(FromYear, FromMonth, FromDay, 00, 00)  // backtest start window
finish    = timestamp(ToYear, ToMonth, ToDay, 23, 59)        // backtest finish window
window()  => time >= start and time <= finish ? true : false // create function "within window of time"

// === INPUT SMA === 
//fastMA    = input(defval = 16, type = integer, title = "FastMA", minval = 1 )
//slowMA    = input(defval = 23, type = integer, title = "SlowMA", minval = 1)

fastMA    = input(defval = 25, title = "FastMA", minval = 1 )
slowMA    = input(defval = 29,  title = "SlowMA", minval = 1)

Long_period = slowMA
Short_period = fastMA
Smoothing_period = input(9, minval=1)
xLongMAVolPrice = ema(volume * close, Long_period) 
xLongMAVol = ema(volume, Long_period) 
xResLong = (xLongMAVolPrice * Long_period) / (xLongMAVol * Long_period)
xShortMAVolPrice = ema(volume * close, Short_period) 
xShortMAVol = ema(volume, Short_period) 
xResShort = (xShortMAVolPrice * Short_period) / (xShortMAVol * Short_period)
xVMACD = xResShort - xResLong
xVMACDSignal = ema(xVMACD, Smoothing_period)
nRes = xVMACD - xVMACDSignal
//plot(nRes*20+slowMA, color=blue, style = line )
//plot(3000, color=red, style = line )


// === SERIES SETUP ===

buy  = crossover( xVMACD,xVMACDSignal)     // buy when fastMA crosses over slowMA
sell = crossunder( xVMACD,xVMACDSignal)  // sell when fastMA crosses under slowMA


// === SERIES SETUP === 

//buy  = crossover(vwma(close, fastMA),7+vwma(close, slowMA))     // buy when fastMA crosses over slowMA
//sell = crossunder(vwma(close, fastMA),vwma(close, slowMA)-7)    // sell when fastMA crosses under slowMA

// === EXECUTION ===
strategy.entry("L", strategy.long, when = window() and buy)  // buy long when "within window of time" AND crossover
strategy.close("L", when = window() and sell)                // sell long when "within window of time" AND crossunder         

// === EXECUTION ===
strategy.entry("S", strategy.short, when = window() and sell)  // buy long when "within window of time" AND crossover
strategy.close("S", when = window() and buy)                // sell long when "within window of time" AND crossunder         

plotshape(window() and buy, style=shape.triangleup, color=green, text="up")
plotshape(window() and sell, style=shape.triangledown, color=red, text="down")
plot(xVMACD*100, title = 'FastMA', color = orange, linewidth = 2, style = line)  // plot FastMA
plot(xVMACDSignal*100, title = 'SlowMA', color = aqua, linewidth = 2, style = line)    // plot SlowMA

```

> Detail

https://www.fmz.com/strategy/434436

> Last Modified

2023-12-06 12:05:01
