
> Name

The-Double-EMA-Strategy-Analysis based on double EMA strategy analysis
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/194a4748bdee0f685c8.png)
[trans]

## Overview
The double EMA strategy is a trend following strategy that determines whether to open or close a position by calculating the EMA of different periods and identifying the trend direction of the price. This strategy is simple and practical and suitable for markets with strong trends.
## Strategy Principle
This strategy is mainly based on two EMA indicators, one is the short-period 9-day EMA, and the other is the longer-period 21-day EMA. Their crossover is a signal for opening and closing positions.
When the short-term EMA crosses the long-term EMA, it is considered that the price has entered an upward trend, and this strategy will open a long order at this time to track the price increase. When the short-term EMA crosses the long-term EMA, it is considered that the price has entered a downward trend, and this strategy will open a short order at this time to track the price decline.
The EMA indicator can effectively filter the noise in price data and identify the main direction of the price trend. Therefore, this strategy uses the double EMA indicator as the basis for opening and closing positions in the hope of capturing a longer price trend cycle.
## Strategic Advantages
This strategy has the following advantages:
1. The strategic ideas are simple and clear, easy to understand and implement.
2. Ability to effectively identify price trends and establish positions in a timely manner to track trends.
3. Use the EMA indicator to filter noise and avoid being disturbed by short-term price fluctuations.
4. EMA parameters can be configured to adjust the sensitivity of the strategy.
## Strategy Risk
There are also some risks with this strategy:
1. When the trend reverses, the lagging characteristic of the EMA indicator may lead to increased losses.
2. Improper setting of EMA parameters will increase the false signal rate.
3. This strategy is more suitable for strong trending markets and is prone to losses during consolidation.
## Strategy optimization
This strategy can be optimized from the following aspects:
1. Combine with other indicators to determine trend reversal and reduce losses. For example, MACD, KDJ, etc.
2. Add stop loss logic. A good stop loss strategy can significantly reduce the maximum drawdown of the strategy.
3. Optimize EMA parameters to make them more suitable for the price characteristics of different varieties.
4. Combined with machine learning algorithms to achieve automatic optimization of EMA parameters.
## Summarize
Overall, the double EMA strategy is a very practical trend following strategy. It is simple to operate, easy to understand, and performs well in strong trending markets. At the same time, this strategy also has some risks, and it can be optimized from multiple dimensions to improve the stability of the strategy. In general, the double EMA strategy is an important reference template for quantitative trading.
||

## Overview

The double EMA strategy is a trend following strategy that identifies the trend direction of prices by calculating EMAs of different cycles and uses that to determine entries and exits. This simple and practical strategy works well in trending markets.   

## Strategy Logic  

The strategy is mainly based on two EMA indicators, a short-term 9-day EMA and a longer 21-day EMA. Their crossovers generate entry and exit signals.  

When the short EMA crosses above the long EMA, it is viewed as prices entering an uptrend. The strategy will go long to follow the rising trend. When the short EMA crosses below the long EMA, it is viewed as prices entering a downtrend. The strategy will go short to follow the falling trend.
  
The EMA indicators can effectively filter out noise from price data and identify the main direction of the trend. Therefore, the strategy uses dual EMAs as the basis for entries and exits in order to capture longer price trends.   

## Advantages  

The strategy has the following advantages:

1. The strategy idea is simple and easy to understand and implement.  
2. It can effectively identify price trends and timely enter positions to follow trends.   
3. Using EMAs filters noise and avoids interference from short-term price fluctuations.
4. The EMA parameters can be configured to adjust the sensitivity of the strategy.   

## Risks  

There are also some risks with this strategy:   

1. The lagging characteristic of EMAs may increase losses when trends reverse.  
2. Improper EMA parameter settings increase false signal rates.  
3. The strategy is more suitable for strong trending markets and vulnerable in range-bound periods.  

## Enhancement  

The strategy can be optimized in the following aspects:  

1. Incorporate other indicators to identify trend reversals and reduce losses, e.g. MACD, KDJ, etc.  
2. Add stop loss logic. Good stop loss strategies can greatly reduce maximum drawdown.   
3. Optimize the EMA parameters to make them fit better with the price characteristics of different products. 
4. Use machine learning algorithms to automate EMA parameter optimization.   

## Summary   

In summary, the double EMA strategy is a very useful trend following strategy. It is easy to operate, understand, and performs excellently in strong trending markets. The strategy also has some risks that can be mitigated through various enhancements to improve its stability. Overall, double EMAs serve as an important reference template for quantitative trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|9|Short EMA Length|
|v_input_2|21|Long EMA Length|
|v_input_color_1|close[1]>openLPrice?LongWColor:LongLColor,.rgb(0,255,0,0)|(?Strategy Lines)Long Win Color|
|v_input_color_2|close[1]>openLPrice?LongWColor:LongLColor,.rgb(0,0,255,0)|Long Loss Color|
|v_input_color_3|close[1]>openLPrice?LongWColor:LongLColor,.rgb(255,255,0,0)|Short Win Color|
|v_input_color_4|close[1]>openLPrice?LongWColor:LongLColor,.rgb(255,0,0,0)|Short Loss Color|
|v_input_color_5|close[1]>openLPrice?LongWColor:LongLColor,.rgb(0,0,0,0)|Win Font Color|
|v_input_color_6|close[1]>openLPrice?LongWColor:LongLColor,.rgb(255,255,255,0)|Loss Font Color|
|v_input_3|false|Show Labels?|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-02-21 00:00:00
end: 2024-02-27 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
// This can only draw so many lines. Use bar replay to go back further
strategy("Strategy Lines", shorttitle="Strategy Lines", overlay=true, max_lines_count=500)

//###########################################################################################################################################
// Replace your strategy here
//###########################################################################################################################################

shortEMA = ta.ema(close, input(9, title="Short EMA Length"))
longEMA = ta.ema(close, input(21, title="Long EMA Length"))

// Entry conditions for long and short positions
longCondition = ta.crossover(shortEMA, longEMA)
shortCondition = ta.crossunder(shortEMA, longEMA)

//###########################################################################################################################################
// Strategy Lines
//###########################################################################################################################################

var timeLow = bar_index
var line li = na
var openLPrice = 0.0000
var openSPrice = 0.0000

LongWColor = input.color(color.rgb(0,255,0,0),"Long Win Color", group="Strategy Lines")
LongLColor = input.color(color.rgb(0,0,255,0),"Long Loss Color", group="Strategy Lines")
ShortWColor = input.color(color.rgb(255,255,0,0),"Short Win Color", group="Strategy Lines")
ShortLColor = input.color(color.rgb(255,0,0,0),"Short Loss Color", group="Strategy Lines")
WinFontColor = input.color(color.rgb(0,0,0,0),"Win Font Color", group="Strategy Lines")
LossFontColor = input.color(color.rgb(255,255,255,0),"Loss Font Color", group="Strategy Lines")
LinesShowLabel = input(false,"Show Labels?",group = "Strategy Lines")

// // Start new line when we go long
// if strategy.position_size >0
//     line.delete(li)
//     li := line.new(timeLow, close[bar_index-timeLow], bar_index, close, width=2, color=close>openLPrice?LongWColor:LongLColor)

// // Start new line when we go short
// if strategy.position_size <0
//     line.delete(li)
//     li := line.new(timeLow, close[bar_index-timeLow], bar_index, close, width=2, color=close<openSPrice?ShortWColor:ShortLColor)

// //Delete Lines if we don't have a position open
// if strategy.position_size ==0
//     li := line.new(timeLow, close[bar_index-timeLow], bar_index, close, width=2, color=color.rgb(0,0,0,100))
//     line.delete(li)

if LinesShowLabel
    // Short Label
    if strategy.position_size>=0 and strategy.position_size[1] <0
        label.new(
             timeLow, na, 
             text=str.tostring((openSPrice-close[1])/(syminfo.mintick*10)), 
             color=close[1]<openSPrice?ShortWColor:ShortLColor, 
             textcolor=close[1]<openSPrice?WinFontColor:LossFontColor,
             size=size.small, 
             style=label.style_label_down, yloc=yloc.abovebar)
    // Long Label
    if strategy.position_size<=0 and strategy.position_size[1] >0
        label.new(
             timeLow, na,
             text=str.tostring((close[1]-openLPrice)/(syminfo.mintick*10)), 
             color=close[1]>openLPrice?LongWColor:LongLColor, 
             textcolor=close[1]>openLPrice?WinFontColor:LossFontColor,
             size=size.small, 
             style=label.style_label_down, yloc=yloc.abovebar)

// Open long position and draw line
if (longCondition)
    //strategy.entry("Long", strategy.long)
    // timeLow := bar_index
    // li := line.new(timeLow, close[bar_index-timeLow], bar_index, close, width=2, color=close>openLPrice?LongWColor:LongLColor)
    openLPrice := close

// Open short position and draw line
if (shortCondition)
    //strategy.entry("Short", strategy.short)
    // timeLow := bar_index
    // li := line.new(timeLow, close[bar_index-timeLow], bar_index, close, width=2, color=close<openSPrice?ShortWColor:ShortLColor)
    openSPrice := close

//###########################################################################################################################################
// Strategy Execution (Replace this as well)
//###########################################################################################################################################

if (longCondition)
    strategy.entry("Long", strategy.long)

if (shortCondition)
    strategy.entry("Short", strategy.short)
```

> Detail

https://www.fmz.com/strategy/443043

> Last Modified

2024-02-28 18:07:59
