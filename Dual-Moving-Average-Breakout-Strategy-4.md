
> Name

Quantitative trading strategy Dual-Moving-Average-Breakout-Strategy based on fast moving average and slow moving average
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/b8f982164bf7fb0a7e3e3ef03fdaedf6289930a9d68a79c582a42b56112303a3.png)
 [trans]
## Overview
The Dual Moving Average Breakout Strategy is a quantitative trading strategy based on fast moving averages and slow moving averages. It uses two exponential moving averages (EMA) with different periods as trading signals. When the fast moving average crosses the slow moving average, a buy signal is generated; when the fast moving average crosses below the slow moving average, a sell signal is generated.
## Strategy Principle
The core logic of this strategy is to use fast moving averages and slow moving averages to form trading signals. The strategy defines the fast moving average period as 12 days and the slow moving average period as 26 days. The calculation method is as follows:
1. Calculate the exponential moving average AP of the price array, with a period of 2 days
2. Calculate the fast moving average Fast based on AP, with a period of 12 days
3. Calculate the slow moving average Slow based on AP, with a period of 26 days
4. Compare fast moving averages and slow moving averages:
   1. When Fast crosses Slow, it is a bull signal
   2. When Fast crosses Slow, it is a short signal
5. Combine the relationship between price and moving average to determine specific trading signals:
   1. Bull signal: Fast>Slow && AP>Fast
   2. Short signal: Fast<Slow && AP<Fast
It is a typical double-moving average strategy to judge market trends and generate trading signals through the intersection of fast moving averages and slow moving averages.
## Advantage Analysis
The double moving average breakout strategy has the following advantages:
1. The strategy logic is simple and clear, easy to understand and implement
2. By adjusting the moving average cycle, you can adapt to different market environments
3. You can do both long and short positions at the same time to achieve higher returns.
4. Can combine the relationship between price and moving average to issue more accurate trading signals
5. The moving average has a certain hysteresis and can effectively filter out market noise.
## Risk Analysis
The double moving average breakout strategy also has certain risks:
1. When the market is in a volatile period, more false signals will appear.
2. The double moving average strategy is prone to curve fitting and ignores market structural changes.
3. Relying only on technical indicators is susceptible to false breakthroughs and carries the risk of loss.
Solution:
1. Optimize the moving average cycle to make it more consistent with the current market status
2. Combine with other indicators such as trading volume confirmation signals to avoid false breakthroughs
3. Use trend following strategies to control the profit and loss ratio and reduce risks.
## Optimization direction
The double moving average breakout strategy can be optimized from the following aspects:
1. Find a more suitable moving average cycle combination to adapt to market changes
2. Add trading volume and other indicators to filter signals to ensure the effectiveness of trading signals
3. Combine market structure indicators to identify trends and adjust moving average cycle parameters
4. Using dynamic moving averages can automatically adjust the cycle according to market changes.
5. Combined with stop-loss strategies, you can effectively control risks and protect funds.
## Summarize
The double moving average breakthrough strategy is a simple and practical quantitative trading strategy. It has the advantages of simple strategic logic and easy implementation, but it also has certain market adaptability problems. We can make it a stable and profitable trading system through parameter optimization, signal filtering, risk control and other methods. In general, the double moving average strategy is a very good strategy prototype and is worthy of in-depth study and application by quantitative traders.
||

## Overview

The Dual Moving Average Breakout Strategy is a quantitative trading strategy based on a fast moving average and a slow moving average. It uses two exponential moving averages (EMA) with different periods as trading signals. When the fast EMA crosses above the slow EMA, a buy signal is generated. When the fast EMA crosses below the slow EMA, a sell signal is generated.

## Strategy Logic  

The core logic of this strategy is to use a fast moving average and a slow moving average to form trading signals. The strategy defines the fast EMA period as 12 days and the slow EMA period as 26 days. The calculation method is as follows:  

1. Calculate the exponential moving average AP of the price array with a period of 2 days
2. Calculate the fast moving average Fast based on AP, with a period of 12 days
3. Calculate the slow moving average Slow based on AP, with a period of 26 days 
4. Compare the fast and slow moving averages:
   1. When Fast crosses above Slow, it is a bullish signal
   2. When Fast crosses below Slow, it is a bearish signal
5. Determine specific trading signals combining price and moving average relationship:
   1. Bullish signal: Fast>Slow && AP>Fast 
   2. Bearish signal: Fast<Slow && AP<Fast

Using the crossover of the fast and slow moving average to determine market trends and generate trading signals is a typical dual moving average strategy.  

## Advantage Analysis

The Dual Moving Average Breakout Strategy has the following advantages:

1. The strategy logic is simple and clear, easy to understand and implement
2. The moving average period can be adjusted to adapt to different market environments  
3. Allow both long and short positions to achieve higher returns
4. More precise trading signals can be generated combining price and moving averages
5. The lagging feature of moving averages can effectively filter out market noise

## Risk Analysis  

The Dual Moving Average Breakout Strategy also has some risks:  

1. More false signals may occur when the market is range-bound
2. The dual moving average strategy may cause curve fitting, ignoring structural market changes
3. Relying solely on technical indicators is vulnerable to fake breakouts, with the risk of losses

Solutions:

1. Optimize the moving average period to better adapt to current market conditions
2. Confirm signals with other indicators like volume to avoid fake breakouts 
3. Adopt trend following strategies to control profit/loss ratio and reduce risk

## Optimization Directions   

The Dual Moving Average Breakout Strategy can be optimized in the following aspects:  

1. Find more suitable moving average period combinations to adapt to market changes
2. Add indicators like volume for signal filtering to ensure validity
3. Incorporate market structure indicators to identify trends and adjust parameters  
4. Adopt dynamic moving averages which can automatically adjust periods based on market changes
5. Incorporate stop loss strategies to effectively control risk and protect capital

## Conclusion  

The Dual Moving Average Breakout Strategy is a simple and practical quantitative trading strategy. It has advantages like easy logic and implementation, and also has some market adaptability issues. We can make it a stable profitable trading system through parameter optimization, signal filtering, risk control etc. Overall, the dual moving average strategy is a great strategy prototype worth in-depth research and application for quantitative traders.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0|Long/Short: Long only|Short only|Both|
|v_input_2_ohlc4|0|Data Array: ohlc4|high|low|open|hl2|hlc3|hlcc4|close|
|v_input_3|12|Short MA period|
|v_input_4|26|Long MA period|
|v_input_5|2000|From Year|
|v_input_6|true|From Month|
|v_input_7|true|From Day|
|v_input_8|9999|To Year|
|v_input_9|12|To Month|
|v_input_10|31|To Day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-17 00:00:00
end: 2024-01-23 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("CDC Action Zone V.2", overlay=true)

// CDC ActionZone V2 29 Sep 2016
// CDC ActionZone is based on a simple 2MA and is most suitable for use with medium volatility market
// 11 Nov 2016 : Ported to Trading View with minor UI enhancement
LSB = input(title="Long/Short", defval="Long only", options=["Long only", "Short only" , "Both"])
src = input(title="Data Array",type=input.source,defval=ohlc4)
prd1=input(title="Short MA period", type=input.integer,defval=12)
prd2=input(title="Long MA period",type=input.integer,defval=26)
AP = ema(src,2)
Fast = ema(AP,prd1)
Slow = ema(AP,prd2)


Bullish = Fast>Slow
Bearish = Fast<Slow

Green = Bullish and AP>Fast
Red = Bearish and AP<Fast
Yellow = Bullish and AP<Fast
Blue = Bearish and AP>Fast

Buy = Bullish and Bearish[1]
Sell = Bearish and Bullish[1]


alertcondition(Buy,"Buy Signal","Buy")
alertcondition(Sell,"Sell Signal","Sell")


//Plot

l1=plot(Fast,"Fast", linewidth=1,color=color.red)
l2=plot(Slow,"Slow", linewidth=2,color=color.blue)
bcolor = Green ? color.lime : Red ? color.red : Yellow ? color.yellow : Blue ? color.blue : na
barcolor(color=bcolor)
fill(l1,l2,bcolor)

// === INPUT BACKTEST RANGE ===
FromYear  = input(defval = 2000, title = "From Year", minval = 1920)
FromMonth = input(defval = 1, title = "From Month", minval = 1, maxval = 12)
FromDay   = input(defval = 1, title = "From Day", minval = 1, maxval = 31)
ToYear    = input(defval = 9999, title = "To Year", minval = 1921)
ToMonth   = input(defval = 12, title = "To Month", minval = 1, maxval = 12)
ToDay     = input(defval = 31, title = "To Day", minval = 1, maxval = 31)

// === FUNCTION EXAMPLE ===
start     = timestamp(FromYear, FromMonth, FromDay, 00, 00)  // backtest start window
finish    = timestamp(ToYear, ToMonth, ToDay, 23, 59)        // backtest finish window
window()  => true // create function "within window of time"


if LSB == "Long only" and Buy and window()
    strategy.entry("L",true)
if LSB == "Long only" and Sell and window()
    strategy.close("L",qty_percent=100,comment="TP Long")
if LSB == "Both" and Buy and window()
    strategy.entry("L",true)
if LSB == "Both" and Sell and window()
    strategy.entry("S",false)
if LSB == "Short only" and Sell and window()
    strategy.entry("S",false)
if LSB == "Short only" and Buy and window()
    strategy.close("S",qty_percent=100,comment="TP Short")
```

> Detail

https://www.fmz.com/strategy/439862

> Last Modified

2024-01-24 14:49:29
