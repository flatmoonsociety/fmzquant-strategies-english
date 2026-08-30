
> Name

Breakthrough-Fair-Value-Gap-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/30a3685aa74450a34769d48956a6c18d53a8488f83fc714538a133b1fe448ca9.png)
[trans]
## Overview
This is a very simple trend following strategy. It will go long when a long fair price difference occurs, and close or go short when a short fair price difference occurs. It does not perform well in consolidation conditions, but can make very generous profits in trending conditions.
## Strategy Principle
The core logic of this strategy is to identify fair spread patterns. The so-called "fair price difference" means that the highest price of the day is lower than the lowest price of the previous day, or the lowest price of the day is higher than the highest price of the previous day, which will form a "breakthrough gap". This often signals a possible trend turn. Specifically, the policy rules are:
1. If the highest price of the day is lower than the lowest price of the previous two days, and the closing price is lower than the lowest price of the previous two days, it is considered that a short fair price difference is formed, and a short position is made.
2. If the lowest price of the day is higher than the highest price of the previous two days, and the closing price is higher than the highest price of the previous two days, it is considered that a fair price difference is formed and a long position is formed.
Two lags are used here, that is, the high and low prices of the first two K lines to determine the fair price difference. This avoids being affected by false breakthroughs or short-term corrections and improves the reliability of form judgment and signal quality.
## Strategic Advantages
1. Identifying appropriate fair spread patterns can well predict possible future trend reversals.
2. The strategy logic and rules are simple, clear and easy to understand and implement.
3. Can quickly capture new trend opportunities.
## Strategy Risk
1. Judgment of the fair spread pattern is not completely accurate, and it will also produce wrong signals if there is a correction in the short term.
2. This strategy will cause losses when the trend reverses, and it is necessary to stop losses in time to prevent risks. 
3. Poor performance in consolidation market, there will be more false signals and small losses.
## Optimization direction
1. Optimize the stop loss mechanism. Dynamic risk control can be achieved in combination with dynamic ATR.
2. Optimize filtering conditions. The reliability of fair spread breakthroughs can be judged based on trading volume, moving average indicators, etc. 
3. Combine with multi-factor model to predict future trend probability.
## Summary
This strategy identifies the formation of fair spreads to determine whether the trend may reverse, and is a basic trend following strategy. The advantage is that it is more accurate to capture the timing of trend reversal, but there is also a certain false alarm rate. Risks can be controlled through stop loss and filtering, and more factors can be combined to improve the accuracy of judgment. Overall, this is a very simple and practical trend trading strategy that is worthy of expansion and optimization.
||

## Overview  
This is a very simple trend following strategy. It will go long when a bullish FVG appears and close or go short when a bearish FVG appears. It does not perform well in range-bound markets, but can be very profitable in trending markets.

## Strategy Logic
The core logic of the strategy is to identify the fair value gap pattern. The so-called "fair value gap" refers to when the highest price today is lower than the lowest price the day before, or when the lowest price today is higher than the highest price the day before, a "breakthrough gap" will be formed. This usually signals a possible trend reversal ahead. Specifically, the rules of the strategy are:  

1. If today's highest price is lower than the lowest price 2 days ago, and the close is lower than the lowest price 2 days ago, a bearish fair value gap is considered to be formed, go short.

2. If today's lowest price is higher than the highest price 2 days ago, and the close is higher than the highest price 2 days ago, a bullish fair value gap is considered to be formed, go long.  

Here 2 lags are used, which is the highest and lowest price of the previous 2 bars to judge the fair value gap. This avoids being affected by false breakouts or short-term pullbacks and improves the reliability and quality of pattern recognition.

## Advantages
1. Identifying proper fair value gap patterns can well predict possible future trend reversals.  
2. The strategy logic and rules are simple, clear and easy to understand and implement.
3. Can quickly capture new trend opportunities.

## Risks 
1. Fair value gap pattern recognition is not completely accurate. False signals may also occur if there is a callback in the short term.  
2. The strategy will incur losses when the trend is reversed, so timely stop losses are needed to hedge risks.
3. It performs poorly in range-bound markets, with more false signals and small losses.

## Optimization Directions 
1. Optimize the stop loss mechanism. Dynamic ATR can be used to achieve dynamic risk control.
2. Optimize filtering conditions. The reliability of fair value gap breaks can be judged based on factors like volume and moving averages.   
3. Incorporate multifactor models to predict future trend probabilities.

## Conclusion
This strategy identifies the formation of fair value gaps to determine if trends may reverse. It belongs to the basic trend-following strategy. The advantage is that it can capture the timing of trend reversals more precisely. But there are also certain false signals. Risks can be controlled through stop losses and filtering. More factors can also be incorporated to improve judgment accuracy. Overall, this is a very simple and practical trend trading strategy that is worth expanding and optimizing.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_bool_1|false|Take only long trades?|
|v_input_bool_2|false|(?REMINDERS)Since this can generate a lot of trades, make sure to fill in the commission (if applicable) for a realistic ROI.|
|v_input_bool_3|false|Modify pyramiding orders to increase the amount of trades.|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Greg_007

//@version=5
strategy("Fair Value Gap Strategy", "FVG Strategy", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=100, pyramiding = 1)

var longOnly = input.bool(false, "Take only long trades?")
var pyramid = input.bool(false, "Since this can generate a lot of trades, make sure to fill in the commission (if applicable) for a realistic ROI.", group = "REMINDERS")
var pyramid2 = input.bool(false, "Modify pyramiding orders to increase the amount of trades.", group = "REMINDERS")
var bearFVG = false
var bullFVG = false
var plotBull = false
var plotBear = false
var bearTrend = false
var bullTrend = false

//BEARISH FVG
if high < low[2] and close[1] < low[2]
    bullFVG := false
    bearFVG := true
    plotBear := true
    if not longOnly
        strategy.entry("Short", strategy.short)
    else
        strategy.close_all()
else
    //BULLISH FVG 
    if low > high[2] and close[1] > high[2]
        bullFVG := true
        bearFVG := false
        plotBull := true
        strategy.entry("Long", strategy.long)
        
// plotshape(plotBull, style=shape.labeldown, location=location.abovebar, color=color.green, text="FVG",textcolor=color.white, size=size.tiny, title="Bull FVG", display=display.all - display.status_line)
// plotshape(plotBear, style=shape.labelup, location=location.belowbar, color=color.red, text="FVG",textcolor=color.white, size=size.tiny, title="Bear FVG", display=display.all - display.status_line)

// //reset the status
// plotBull := false
// plotBear := false


```

> Detail

https://www.fmz.com/strategy/442257

> Last Modified

2024-02-20 15:47:05
