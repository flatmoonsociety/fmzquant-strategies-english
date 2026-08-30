
> Name

Advanced-Bollinger-Band-Moving-Average-Grid-Trend-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/14a590824a8071e89c9.png)
[trans]

## Overview
The strategy is called “Advanced Bollinger Bands Moving Average Grid Trend Following Strategy.” It is a strategy that uses Bollinger Bands and moving averages to judge trends and establish a grid position tracking in the direction of the trend.
## Strategy Principle
The main ideas of this strategy are:
1. Use Bollinger Bands to determine the current market fluctuation range. The middle track of the Bollinger Bands is the n-day simple moving average, and the bandwidth is the n-day ATR average.
2. The four outer lines of the Bollinger Bands are all abnormal average true fluctuation range lines. The strategy opens positions on breaks of different level lines.
3. EMA fast and slow moving averages determine the direction of the general cycle trend. When the big cycle is bullish, only go long, and vice versa.
4. Follow the trend direction to open a position, and close the position to take profit when a needle-shaped K-line appears.
Specifically, the strategy is mainly divided into the following parts:
1. Determine the parameters of Bollinger Bands. The middle track of Bollinger Bands is the n-day SMA moving average, and the width of Bollinger Bands is the n-day ATR. The Bollinger length n in the strategy is 20.
2. Set up four Bollinger expansion lines. The distances above and below the line from the mid-track are respectively 1.236 times, 2.382 times, 3.618 times and 4.236 times the average true fluctuation range.
3. Set fast and slow EMA moving averages to determine the general cycle trend. The length of the fast line is 25 days and the length of the slow line is 200 days.
4. During the long period, long positions are gradually established when the price breaks through the four moving averages below. Same goes for bears.
5. When a pin-shaped K-line appears or the price crosses the large period moving average again, it is regarded as a signal of the end of the pin-shaped K-line and the position is closed to take profit.

The above are the main technical principles of this strategy. Use Bollinger Bands to determine the current fluctuation range, track and open positions under the general cycle trend, and ultimately achieve the effect of holding a position with high probability.
## Strategic advantage analysis
This strategy mainly has the following advantages:
1. Make full use of trend characteristics, judge the direction of the trend in a large period, and build a position in the direction of the trend, which can reduce unnecessary reverse operations.
2. The use of multi-level Bollinger Bands can more clearly judge the current fluctuation area, which is helpful for grasping most of the market conditions.
3. The grid holding method can evenly distribute risks to each unit of funds, thereby obtaining stable returns.
4. Use the pin-shaped K-line as an efficient signal to close positions and take profits quickly.
5. The strategy as a whole realizes the trinity of trend judgment, grid position holding, and specific signal closing, and is a relatively mature and complete quantitative strategy.

## Strategy risk analysis
This strategy also has the following risks:
1. The probability of misjudgment of large cycle trends. There is a certain probability of error in the fast and slow moving averages, which may lead to unnecessary reverse operations.
2. Failure probability of Bollinger Band breakthrough. Bollinger Bands cannot predict the price path 100%.
3. The pin-shaped K-line signal is sent out late and the profit cannot be taken in time.
4. It is easy to form excessive overlapping positions during large-cycle shock adjustments.

The corresponding solutions are as follows:
1. Adjust the fast and slow moving average parameters to reduce the error probability.
2. Adjust the Bollinger Band parameters to make the Bollinger Band as close as possible to most fluctuations.
3. Test more sensitive take-profit signals for specific patterns.
4. Increase the distance and control the size of positions.
## Strategy optimization direction
This strategy can be optimized from the following directions:
1. Test different moving average parameters to optimize large-cycle trend judgment. For example, test EMA, RSI and other indicators.
2. Test different multiples of ATR parameters to optimize Bollinger Band width settings. Make Bollinger Bands closer to real fluctuations.
3. Test other efficient take-profit signals. For example, SAR, Kalman moving average, etc.
4. Optimize grid spacing. This makes the fluctuation range more evenly divided and reduces repeated opening of positions.
5. Add a stop loss mechanism. Avoid big losses in extreme market conditions.
## Summarize
This strategy comprehensively uses technical means such as Bollinger Bands Channel, moving average indicators, and specific K-line patterns. On the premise of judging the big cycle trend, a trend-following moving average Bollinger grid strategy was constructed. Compared with the traditional Bollinger Band breakthrough, this strategy adds trend characteristic judgment, which can reduce unnecessary reverse position building. At the same time, the grid position method diversifies the capital risk of each unit, thereby obtaining stable returns. This strategy can be optimized and adjusted from multiple perspectives such as trend judgment, Bollinger width, take-profit signals, stop-loss methods, etc. to obtain a more stable strategy effect.

|| 

## Overview  

The strategy is named "Advanced Bollinger Band Moving Average Grid Trend Tracking Strategy". It is a strategy that uses Bollinger Bands and moving averages for trend determination and establishes grid positions to track the trend direction.

## Principle  

The main idea of this strategy is:

1. Use Bollinger Bands to judge the current market volatility range. The middle rail of Bollinger Bands is the n-day simple moving average, and the width is the n-day ATR average amplitude.

2. The four lines outside the Bollinger Bands are abnormal multiples of the average true volatility amplitude lines. The strategy establishes positions when breaking through different levels of lines.

3. The EMA fast and slow moving averages determine the big cycle trend direction. Go long only in the big cycle uptrend and go short on the contrary.

4. Track and build positions in the trend direction, close positions for profit when seeing pin bars.


Specifically, the main parts of this strategy are:  

1. Determine Bollinger Band parameters. The middle rail of Bollinger Bands is the n-day SMA moving average, and the width of Bollinger Bands is the n-day ATR. The Bollinger length n in the strategy is 20.

2. Set four expanded lines outside Bollinger Bands. The distance between the lines and the middle rail is 1.236 times, 2.382 times, 3.618 times and 4.236 times the average true volatility amplitude.  

3. Set fast and slow EMA moving averages to determine the big cycle trend. The fast line length is 25 days and the slow line is 200 days.

4. Establish long positions gradually when breaking through the four lines below in a big cycle uptrend. The short side is the same.  

5. When a pin bar appears or the price crosses the big cycle moving average again, it is regarded as an pin bar ending signal to close positions for profit.


The above is the main technical principle of this strategy. By judging the current volatility range through Bollinger Bands and establishing positions under the big cycle trend, the final effect of high probability positions can be achieved.

## Advantage Analysis   

The main advantages of this strategy are:

1. Make full use of trend characteristics, determine trend direction in big cycles, build positions in trend direction to reduce unnecessary reverse operations.

2. The use of multiple Bollinger lines can more clearly judge the current volatility range, which is conducive to capturing most trends.

3. The grid position method can evenly distribute risks to each unit of funds to obtain stable returns.  

4. The use of pin bar high efficiency signals for position closing can quickly lock in profits. 

5. The overall strategy integrates trend determination, grid positions, and specific signal position closing. It is a relatively mature and complete quantitative strategy.


## Risk Analysis

There are also some risks in this strategy:

1. Probability of incorrectly determining the big cycle trend. There is some probability of error in fast and slow moving averages, which may lead to unnecessary reverse operations.

2. Probability of Bollinger line breakout failures. Bollinger lines cannot predict price paths 100% accurately. 

3. Pin bar signals may come out late and cannot lock in profits in time. 

4. It is easy to form too many overlapping positions during big cycle shock adjustments.


The corresponding solutions are:

1. Adjust fast and slow moving average parameters to reduce probability of errors.

2. Adjust Bollinger line parameters to make Bollinger lines stick to most fluctuations as much as possible.  

3. Test more sensitive specific patterns for profit taking signals.  

4. Increase interval distance to control position size.

## Optimization Directions   

The strategy can be optimized in the following directions:

1. Test different moving average parameters to optimize big cycle trend determinations. For example, test other indicators like EMA, RSI, etc.

2. Test different multiples ATR parameters to optimize Bollinger channel width settings. Make Bollinger Bands stick closer to actual fluctuations.   

3. Test other efficient profit taking signals. For example, SAR, Kalman Lines, etc. 

4. Optimize grid interval to make volatility intervals divided more evenly to reduce overlapping positions.  

5. Increase stop loss mechanisms. Avoid huge losses in extreme market conditions.  

## Summary   

The strategy integrates the use of Bollinger channel, moving average indicators, specific K-line patterns and other technical means. Under the premise of determining the big cycle trend, it constructs a trend tracking grid strategy based on moving averages and Bollinger Bands. Compared with traditional Bollinger band breakouts, this strategy adds trend characteristic judgment, which can reduce unnecessary reverse positions. At the same time, the grid position method diversifies risks for each unit of funds to obtain stable returns. The strategy can be optimized from multiple angles such as trend determination, Bollinger width, profit taking signals, stop loss methods, etc. to obtain more stable strategy effects.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_7|25|fastlength(fastlength)|
|v_input_8|200|Slow length (slowlength)|
|v_input_bool_1|true|(?Backtest range backtest) Enable backtest time range limit (backtest)|
|v_input_1|timestamp(1 Jan 2015)|Start time(Start)|
|v_input_2|timestamp(1 Jan 2040)|End time (finish)|
|v_input_int_1|20|(?entry)Bollinger length,(boll length)|
|v_input_3|1.236|Fib 1|
|v_input_4|2.382|Fib 2|
|v_input_5|3.618|fib 3|
|v_input_6|4.236|Fib 4|

> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-24 00:00:00
end: 2023-11-23 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Aayonga

//@version=5
strategy("fib trend grid@Aa", overlay=true)

//回测时间
useDateFilter=input.bool(true,title = "启用回测时间范围限定(backtest)", group = "回测范围(backtest)")
backtesStarDate=input(timestamp("1 Jan 2015"),title = "开始时间(Start)", group = "回测范围(backtest)")
backtestEndDate=input(timestamp("1 Jan 2040"),title = "结束时间(finish)",group = "回测范围(backtest)")
inTradeWindow=true


//入场位 entry
bolllen=input.int(defval=20,minval=1,title="布林长度,(boll length)",group = "入场位(entry)")
sma=ta.sma(close,bolllen)
avg=ta.atr(bolllen)
fib1=input(defval=1.236,title="Fib 1",group = "入场位(entry)")
fib2=input(defval=2.382,title="Fib 2",group = "入场位(entry)")
fib3=input(defval=3.618,title="fib 3",group = "入场位(entry)")
fib4=input(defval=4.236,title="Fib 4",group = "入场位(entry)")
r1=avg*fib1
r2=avg*fib2
r3=avg*fib3
r4=avg*fib4
top4=sma+r4
top3=sma+r3
top2=sma+r2
top1=sma+r1
bott1=sma-r1
bott2=sma-r2
bott3=sma-r3
bott4=sma-r4



//趋势 plot

t4=plot(top4,title="卖 (sell)4",color=color.rgb(244, 9, 9))
t3=plot(top3,title = "卖(sell) 3",color=color.rgb(211, 8, 8))
t2=plot(top2,title="卖 (sell)2",color=color.rgb(146, 13, 13))
t1=plot(top1,title="卖(sell) 1",color=color.rgb(100, 3, 3))

b1=plot(bott1,title="买(buy1)1",color=color.rgb(4, 81, 40))
b2=plot(bott2,title="买(buy)2",color=color.rgb(15, 117, 46))
b3=plot(bott3,title = "买(buy)3",color =color.rgb(8, 176, 42) )
b4=plot(bott4,title="买(buy)4",color=color.rgb(15, 226, 103))
plot(sma,style=plot.style_cross,title="SMA",color=color.rgb(47, 16, 225))

//趋势
LengthF=input(defval = 25,title = "快线长度(fastlength)")
LengthS=input(defval=200,title = "慢线长度(slowlength)")
emaF=ta.ema(close,LengthF)
smaS=ta.sma(close,LengthS)
longTrend=emaF>smaS
longb=ta.crossover(emaF,smaS)
bgcolor(longb ? color.new(color.green,40):na,title = "多头强势(bull trend)")
shortTrend=smaS>emaF
shortb=ta.crossunder(emaF,smaS)
bgcolor(shortb ? color.new(#951313, 40):na,title = "空头强势(bear trend)")

//pinbar
bullPinBar = ((close > open) and ((open - low) > 0.6* (high - low))) or ((close < open) and ((close - low) > 0.9 * (high - low)))
//plotshape(bullPinBar  , text ="pinbar", textcolor=color.rgb(9, 168, 144),location=location.belowbar, color=color.rgb(29, 103, 67), size=size.tiny)
bearPinBar = ((close > open) and ((high - close) > 0.7 * (high - low))) or ((close < open) and ((high - open) > 0.7 * (high - low)))
//plotshape(bearPinBar  , text ="pinbar", textcolor=color.rgb(219, 12, 12),location=location.abovebar, color=color.rgb(146, 7, 7), size=size.tiny)

buy1=ta.crossunder(close,bott1) and longTrend and close>ta.ema(close,100)
buy2=ta.crossunder(close,bott2) and longTrend 
buy3=ta.crossunder(close,bott3) and longTrend 
buy4=ta.crossunder(close,bott4) and longTrend 
buyclose=bearPinBar or ta.crossunder(close,smaS)




if buy2 or buy3 or buy4 or buy1 and inTradeWindow
    strategy.order("多(buy)",strategy.long)

if buyclose  and inTradeWindow
    strategy.close("多(buy)")

sell1=ta.crossover(close,top1) and shortTrend and close<ta.ema(close,200)
sell2=ta.crossover(close,top2) and shortTrend and close<ta.ema(close,200)
sell3=ta.crossover(close,top3) and shortTrend and close<ta.ema(close,200)
sell4=ta.crossover(close,top4) and shortTrend and close<ta.ema(close,200)
sellclose=bullPinBar or ta.crossover(close,ta.sma(close,220))

if  sell1 or sell2 or sell3 or sell4 and inTradeWindow
    strategy.order("空(sell)",strategy.short)

if sellclose  and inTradeWindow
    strategy.close("空(sell)")
     
```

> Detail

https://www.fmz.com/strategy/433108

> Last Modified

2023-11-24 14:48:28
