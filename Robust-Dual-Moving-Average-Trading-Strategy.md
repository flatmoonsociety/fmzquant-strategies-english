
> Name

Robust-Dual-Moving-Average-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/6d11bbe4e33a9d6334.png)
[trans]
## Overview
The dual moving average robust trading strategy combines the dual power of the relative strength index (RSI) and the rate of change indicator (ROC) to identify the direction of medium and long-term trends. This strategy sets filter conditions and stop-loss conditions at the same time, enabling entry based on confirmation of the trend direction, which can effectively reduce the risk caused by false breakthroughs.
## Strategy Principle
This strategy is based on a combination of the RSI indicator and the ROC indicator to determine when to enter. When the price approaches the relatively oversold area, it is considered a structural turning point, forming a reversal signal; when the price fluctuates in the relatively oversold area, it indicates that the current trend will continue for a period of time. The ROC indicator judges the trend and intensity of price changes from the perspective of rate of change. The combination of the two can form complementarity in judging market structure.
In addition, this strategy adds two filtering conditions: SMA and short-term stop loss line for medium and long-term trend judgment, which allows the strategy to enter the market only when the direction of the medium- and long-term trend is confirmed and there is no stop loss risk in the short term. This configuration method can reduce the chance of being caught in volatile market conditions, making the risk controllable for traders.
The flexible input settings of this strategy also allow traders to freely choose to use only one of the RSI or ROC indicators as the entry basis, or use a combination of the two, which can be optimized for different varieties and market types, which further expands the scope of application of the strategy.
## Advantage Analysis
The biggest advantage of this strategy is that it combines trend and reversal signals to make entry judgments, taking into account both trend factors and structural opportunities, and is based on changes in market structure, thus ensuring accurate entry timing. Compared with a single indicator, the combined use of RSI and ROC also makes the strategy more resistant to random noise in the market.
Another advantage is the strategy's built-in trend filter (SMA) and short-term stop loss, which can effectively reduce the probability of being trapped in volatile market conditions. The setting of two lines of defense, trend judgment and short-term stop loss, makes this a sound strategy with controllable risks.
Finally, the strategy has a variety of built-in parameter setting combinations, and traders can optimize for different varieties and market types, which makes the strategy very widely applicable. Whether it is a trending market or a consolidation market, this strategy can adapt to market changes through parameter adjustment.
## Risk Analysis
The biggest risk with this strategy is that there is some lag in reversal signal indicators such as RSI and ROC. When the trend changes, these indicators often have a certain lag before the parameters reach the set threshold level. This lag will cause the strategy to enter the market late and fail to capture the initial start-up stage of the trend.
Another potential risk is that in an oscillatory trend, the parameter settings of RSI and ROC may be too sensitive, resulting in certain false signals. If the short-term stop loss is triggered, these false signals will directly cause actual losses.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Add more indicators to the combination, such as KDJ, MACD, etc., use more dimensions to judge the market structure and improve the accuracy of signals
2. Add an adaptive optimization mechanism to the parameter settings of RSI and ROC so that the indicator parameters can be dynamically adjusted according to real-time volatility.
3. Optimize the entry logic and set up a certain confirmation mechanism when the trend indicator and reversal indicator meet the conditions to avoid false signals during shocks.
4. Expand the stop loss range or set a free stop loss to give more room for reversal to reduce missed profits caused by too dense a stop loss.
## Summarize
The double moving average robust trading strategy successfully combines trend judgment and reversal indicators to capture structural opportunities based on the confirmation of medium and long-term trends. This strategy also has strong configurability, and traders can optimize parameters for individual stocks and market types. The built-in dual protection mechanism also makes it a risk-controllable choice. By further integrating more indicators or establishing an adaptive parameter adjustment mechanism, the performance of this strategy still has room to expand.
||

## Overview

The Robust Dual Moving Average Trading Strategy combines the power of both Relative Strength Index (RSI) and Rate of Change (ROC) indicators to identify the direction of intermediate-to-long-term trends. With built-in filters and stop loss conditions, this strategy enters the market only after the trend direction is confirmed, which effectively reduces the risk of false breakouts.

## Strategy Logic

This strategy uses a combination of RSI and ROC indicators to determine entry signals. When prices approach the overbought/oversold areas, it indicates potential reversal points and formation of reversal signals. When prices oscillate within these areas, it suggests the current trend may persist for some time. The ROC indicator judges price trend and momentum from the perspective of rate of change. The two indicators complement each other in assessing market structure.

In addition, the strategy incorporates intermediate-to-long-term trend filters (SMA) and short-term stop loss lines before entering any trades. This ensures that entries only occur in confirmed trend direction and without imminent stop loss risks in oscillating markets. Such configurations reduce the likelihood of being whipsawed in range-bound environments, making the strategy risk-manageable for traders.  

The flexible input settings also allow traders to choose between RSI only, ROC only or a combination of both as the entry trigger. This expands the adaptability of the strategy across different products and market conditions.

## Advantage Analysis 

The biggest advantage of this strategy lies in combining both trend and reversal signals for entry decisions, taking into consideration both trend and structural factors to ensure precise timing. Compared to single-indicator strategies, the RSI+ROC combo also makes the strategy more robust against market noise and randomness.

Another advantage is the built-in trend filters (SMA) and short-term stop loss, which reduce the probability of being trapped in oscillating markets. The two lines of defense via trend diagnosis and short-term stop loss make this a risk-controllable robust strategy.

Lastly, the multiple parameter setting combinations allow traders to optimize the strategy for different products and market environments. Whether in trending or range-bound markets, the strategy can be adaptive through parameter tuning.

## Risk Analysis

The biggest risk of the strategy comes from the lagging nature of reversal signal indicators like RSI and ROC. When trends start to shift, these indicators often lag behind before reaching the threshold levels set in the parameters. Such lag may delay the strategy’s entry and cause it to miss the initial stage of trend launches.  

Another potential risk is that in oscillating markets, the RSI and ROC parameter settings may become too sensitive and generate certain false signals. If triggered concurrently with short-term stop loss, such false signals can lead to actual losses.

## Optimization Directions  

The strategy can be optimized in the following aspects:

1. Incorporate more indicators for combo usage like KDJ, MACD to improve signal accuracy with multi-dimensional assessments of market structure

2. Introduce adaptive optimization mechanisms into RSI and ROC parameters so the settings can dynamically adjust based on real-time volatility

3. Refine entry logic by adding confirmation mechanisms when trend tools and reversal tools concurrently meet conditions, avoiding acting on false signals in oscillations  

4. Expand stop loss range or set trailing stop loss to provide reversals more room, reducing missed profits due to stop loss clustering

## Conclusion

The Robust Dual Moving Average Trading Strategy successfully combines trend diagnosis and reversal indicators to capture structural opportunities upon intermediate-to-long-term trend confirmation. With robust configurability, traders can optimize parameters for individual stocks and market conditions. The dual line of defense also makes it a risk-controllable choice. Further performance improvements can be achieved by incorporating more indicators or establishing adaptive parameter tuning mechanisms.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0|Long Only or Short Only or Both?: Both|Long Only|Short Only|
|v_input_2|0|RSI Only, ROC Only, Both?: Both|RSI Only|ROC Only|
|v_input_3|14|RSI Length|
|v_input_4|70|RSI Upper Threshold|
|v_input_5|30|RSI Lower Threshold|
|v_input_6|14|ROC Length|
|v_input_7|0.01|ROC Upper Threshold|
|v_input_8|-0.01|ROC Lower Threshold|
|v_input_9|5|Long Exit SMA Length|
|v_input_10|5|Short Exit SMA Length|
|v_input_11|0|Trend SMA Filter?: Above|Below|Don't Include|
|v_input_12|200|Trend SMA Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-05 00:00:00
end: 2024-02-04 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © GlobalMarketSignals

//@version=4
strategy("GMS: RSI & ROC Strategy", overlay=true)

LongShort = input(title="Long Only or Short Only or Both?", type=input.string, defval="Both", options=["Both", "Long Only", "Short Only"])
RSIroc = input(title="RSI Only, ROC Only, Both?", type=input.string, defval="Both", options=["Both", "RSI Only", "ROC Only"])
RSILength = input(title="RSI Length", type = input.integer ,defval=14)
RSIUpper = input(title="RSI Upper Threshold", type = input.float ,defval=70)
RSILower = input(title="RSI Lower Threshold", type = input.float ,defval=30)
ROCLength = input(title="ROC Length", type = input.integer ,defval=14)
ROCUpper = input(title="ROC Upper Threshold", type = input.float ,defval=0.01)
ROCLower = input(title="ROC Lower Threshold", type = input.float ,defval=-0.01)
LongExit = input(title="Long Exit SMA Length", type = input.integer ,defval=5)
ShortExit = input(title="Short Exit SMA Length", type = input.integer ,defval=5)
AboveBelow = input(title="Trend SMA Filter?", type=input.string, defval="Above", options=["Above", "Below", "Don't Include"])
TrendLength = input(title="Trend SMA Length", type = input.integer ,defval=200)

//RSI ONLY
 //Long Side

if LongShort =="Long Only" and AboveBelow == "Above" and RSIroc == "RSI Only"
    strategy.entry("LONG", true, when = rsi(close,RSILength)<RSILower and close< sma(close,LongExit) and close>sma(close,TrendLength))
    strategy.close("LONG", when = close>sma(close,LongExit))
    
if LongShort =="Long Only" and AboveBelow == "Below" and RSIroc == "RSI Only"
    strategy.entry("LONG", true, when = rsi(close,RSILength)<RSILower and close< sma(close,LongExit) and close<sma(close,TrendLength))
    strategy.close("LONG", when = close>sma(close,LongExit))
    
if LongShort =="Long Only" and AboveBelow == "Don't Include" and RSIroc == "RSI Only"
    strategy.entry("LONG", true, when = rsi(close,RSILength)<RSILower and close< sma(close,LongExit))
    strategy.close("LONG", when = close>sma(close,LongExit))
    
if LongShort =="Both" and AboveBelow == "Above" and RSIroc == "RSI Only"
    strategy.entry("LONG", true, when = rsi(close,RSILength)<RSILower and close< sma(close,LongExit) and close>sma(close,TrendLength))
    strategy.close("LONG", when = close>sma(close,LongExit))
    
if LongShort =="Both" and AboveBelow == "Below" and RSIroc == "RSI Only"
    strategy.entry("LONG", true, when = rsi(close,RSILength)<RSILower and close< sma(close,LongExit) and close<sma(close,TrendLength))
    strategy.close("LONG", when = close>sma(close,LongExit))
    
if LongShort =="Both" and AboveBelow == "Don't Include" and RSIroc == "RSI Only"
    strategy.entry("LONG", true, when = rsi(close,RSILength)<RSILower and close< sma(close,LongExit))
    strategy.close("LONG", when = close>sma(close,LongExit))
    
//RSI ONLY
 //SHORT SIDE

if LongShort =="Short Only" and AboveBelow == "Above" and RSIroc == "RSI Only"
    strategy.entry("SHORT", false, when = rsi(close,RSILength)>RSIUpper and close> sma(close,ShortExit) and close>sma(close,TrendLength))
    strategy.close("SHORT", when = close<sma(close,ShortExit))
    
if LongShort =="Short Only" and AboveBelow == "Below" and RSIroc == "RSI Only"
    strategy.entry("SHORT", false, when = rsi(close,RSILength)>RSIUpper and close> sma(close,ShortExit) and close<sma(close,TrendLength))
    strategy.close("SHORT", when = close<sma(close,ShortExit))
    
if LongShort =="Short Only" and AboveBelow == "Don't Include" and RSIroc == "RSI Only"
    strategy.entry("SHORT", false, when = rsi(close,RSILength)>RSIUpper and close> sma(close,ShortExit))
    strategy.close("SHORT", when = close<sma(close,ShortExit))
    
if LongShort =="Both" and AboveBelow == "Above" and RSIroc == "RSI Only"
    strategy.entry("SHORT", false, when = rsi(close,RSILength)>RSIUpper and close> sma(close,ShortExit) and close>sma(close,TrendLength))
    strategy.close("SHORT", when = close<sma(close,ShortExit))
    
if LongShort =="Both" and AboveBelow == "Below" and RSIroc == "RSI Only"
    strategy.entry("SHORT", false, when = rsi(close,RSILength)>RSIUpper and close> sma(close,ShortExit) and close<sma(close,TrendLength))
    strategy.close("SHORT", when = close<sma(close,ShortExit))
    
if LongShort =="Both" and AboveBelow == "Don't Include" and RSIroc == "RSI Only"
    strategy.entry("SHORT", false, when = rsi(close,RSILength)>RSIUpper and close> sma(close,ShortExit))
    strategy.close("SHORT", when = close<sma(close,ShortExit))
    
///////-----------------/////////////
///////-----------------/////////////
///////-----------------/////////////
    
    
//ROC ONLY
 //Long Side

if LongShort =="Long Only" and AboveBelow == "Above" and RSIroc == "ROC Only"
    strategy.entry("LONG", true, when = roc(close,ROCLength)<ROCLower and close< sma(close,LongExit) and close>sma(close,TrendLength))
    strategy.close("LONG", when = close>sma(close,LongExit))
    
if LongShort =="Long Only" and AboveBelow == "Below" and RSIroc == "ROC Only"
    strategy.entry("LONG", true, when = roc(close,ROCLength)<ROCLower and close< sma(close,LongExit) and close<sma(close,TrendLength))
    strategy.close("LONG", when = close>sma(close,LongExit))
    
if LongShort =="Long Only" and AboveBelow == "Don't Include" and RSIroc == "ROC Only"
    strategy.entry("LONG", true, when = roc(close,ROCLength)<ROCLower and close< sma(close,LongExit))
    strategy.close("LONG", when = close>sma(close,LongExit))
    
if LongShort =="Both" and AboveBelow == "Above" and RSIroc == "ROC Only"
    strategy.entry("LONG", true, when = roc(close,ROCLength)<ROCLower and close< sma(close,LongExit) and close>sma(close,TrendLength))
    strategy.close("LONG", when = close>sma(close,LongExit))
    
if LongShort =="Both" and AboveBelow == "Below" and RSIroc == "ROC Only"
    strategy.entry("LONG", true, when = roc(close,ROCLength)<ROCLower and close< sma(close,LongExit) and close<sma(close,TrendLength))
    strategy.close("LONG", when = close>sma(close,LongExit))
    
if LongShort =="Both" and AboveBelow == "Don't Include" and RSIroc == "ROC Only"
    strategy.entry("LONG", true, when = rsi(close,ROCLength)<ROCLower and close< sma(close,LongExit))
    strategy.close("LONG", when = close>sma(close,LongExit))
    
//ROC ONLY
 //SHORT SIDE

if LongShort =="Short Only" and AboveBelow == "Above" and RSIroc == "ROC Only"
    strategy.entry("SHORT", false, when = roc(close,ROCLength)>ROCUpper and close> sma(close,ShortExit) and close>sma(close,TrendLength))
    strategy.close("SHORT", when = close<sma(close,ShortExit))
    
if LongShort =="Short Only" and AboveBelow == "Below" and RSIroc == "ROC Only"
    strategy.entry("SHORT", false, when = roc(close,ROCLength)>ROCUpper and close> sma(close,ShortExit) and close<sma(close,TrendLength))
    strategy.close("SHORT", when = close<sma(close,ShortExit))
    
if LongShort =="Short Only" and AboveBelow == "Don't Include" and RSIroc == "ROC Only"
    strategy.entry("SHORT", false, when = roc(close,ROCLength)>ROCUpper and close> sma(close,ShortExit))
    strategy.close("SHORT", when = close<sma(close,ShortExit))
    
if LongShort =="Both" and AboveBelow == "Above" and RSIroc == "ROC Only"
    strategy.entry("SHORT", false, when = roc(close,ROCLength)>ROCUpper and close> sma(close,ShortExit) and close>sma(close,TrendLength))
    strategy.close("SHORT", when = close<sma(close,ShortExit))
    
if LongShort =="Both" and AboveBelow == "Below" and RSIroc == "ROC Only"
    strategy.entry("SHORT", false, when = roc(close,ROCLength)>ROCUpper and close> sma(close,ShortExit) and close<sma(close,TrendLength))
    strategy.close("SHORT", when = close<sma(close,ShortExit))
    
if LongShort =="Both" and AboveBelow == "Don't Include" and RSIroc == "ROC Only"
    strategy.entry("SHORT", false, when = roc(close,ROCLength)>ROCUpper and close> sma(close,ShortExit))
    strategy.close("SHORT", when = close<sma(close,ShortExit))
   
    
///////-----------------/////////////
///////-----------------/////////////
///////-----------------/////////////   

    
//BOTH
 //Long Side

if LongShort =="Long Only" and AboveBelow == "Above" and RSIroc == "Both"
    strategy.entry("LONG", true, when = rsi(close,RSILength)<RSILower and roc(close,ROCLength)<ROCLower and close< sma(close,LongExit) and close>sma(close,TrendLength))
    strategy.close("LONG", when = close>sma(close,LongExit))
    
if LongShort =="Long Only" and AboveBelow == "Below" and RSIroc == "Both"
    strategy.entry("LONG", true, when = rsi(close,RSILength)<RSILower and roc(close,ROCLength)<ROCLower and close< sma(close,LongExit) and close<sma(close,TrendLength))
    strategy.close("LONG", when = close>sma(close,LongExit))
    
if LongShort =="Long Only" and AboveBelow == "Don't Include" and RSIroc == "Both"
    strategy.entry("LONG", true, when = rsi(close,RSILength)<RSILower and roc(close,ROCLength)<ROCLower  and close< sma(close,LongExit))
    strategy.close("LONG", when = close>sma(close,LongExit))
    
if LongShort =="Both" and AboveBelow == "Above" and RSIroc == "Both"
    strategy.entry("LONG", true, when = rsi(close,RSILength)<RSILower and roc(close,ROCLength)<ROCLower  and close< sma(close,LongExit) and close>sma(close,TrendLength))
    strategy.close("LONG", when = close>sma(close,LongExit))
    
if LongShort =="Both" and AboveBelow == "Below" and RSIroc == "Both"
    strategy.entry("LONG", true, when = rsi(close,RSILength)<RSILower and roc(close,ROCLength)<ROCLower  and close< sma(close,LongExit) and close<sma(close,TrendLength))
    strategy.close("LONG", when = close>sma(close,LongExit))
    
if LongShort =="Both" and AboveBelow == "Don't Include" and RSIroc == "Both"
    strategy.entry("LONG", true, when = rsi(close,RSILength)<RSILower and roc(close,ROCLength)<ROCLower  and close< sma(close,LongExit))
    strategy.close("LONG", when = close>sma(close,LongExit))
    
//BOTH
 //SHORT SIDE

if LongShort =="Short Only" and AboveBelow == "Above" and RSIroc == "Both"
    strategy.entry("SHORT", false, when = rsi(close,RSILength)>RSIUpper and roc(close,ROCLength)>ROCUpper and close> sma(close,ShortExit) and close>sma(close,TrendLength))
    strategy.close("SHORT", when = close<sma(close,ShortExit))
    
if LongShort =="Short Only" and AboveBelow == "Below" and RSIroc == "Both"
    strategy.entry("SHORT", false, when = rsi(close,RSILength)>RSIUpper and roc(close,ROCLength)>ROCUpper and close> sma(close,ShortExit) and close<sma(close,TrendLength))
    strategy.close("SHORT", when = close<sma(close,ShortExit))
    
if LongShort =="Short Only" and AboveBelow == "Don't Include" and RSIroc == "Both"
    strategy.entry("SHORT", false, when = rsi(close,RSILength)>RSIUpper and roc(close,ROCLength)>ROCUpper and close> sma(close,ShortExit))
    strategy.close("SHORT", when = close<sma(close,ShortExit))
    
if LongShort =="Both" and AboveBelow == "Above" and RSIroc == "Both"
    strategy.entry("SHORT", false, when = rsi(close,RSILength)>RSIUpper and roc(close,ROCLength)>ROCUpper and close> sma(close,ShortExit) and close>sma(close,TrendLength))
    strategy.close("SHORT", when = close<sma(close,ShortExit))
    
if LongShort =="Both" and AboveBelow == "Below" and RSIroc == "Both"
    strategy.entry("SHORT", false, when = rsi(close,RSILength)>RSIUpper and roc(close,ROCLength)>ROCUpper and close> sma(close,ShortExit) and close<sma(close,TrendLength))
    strategy.close("SHORT", when = close<sma(close,ShortExit))
    
if LongShort =="Both" and AboveBelow == "Don't Include" and RSIroc == "Both"
    strategy.entry("SHORT", false, when = rsi(close,RSILength)>RSIUpper and roc(close,ROCLength)>ROCUpper and close> sma(close,ShortExit))
    strategy.close("SHORT", when = close<sma(close,ShortExit))
    
    
```

> Detail

https://www.fmz.com/strategy/441055

> Last Modified

2024-02-05 10:57:28
