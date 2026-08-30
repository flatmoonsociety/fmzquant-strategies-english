
> Name

Aggregated Momentum Indicator StrategyChaikin-Oscillator-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
The aggregated momentum indicator strategy uses aggregated momentum indicators to judge the market's capital flow to capture market trend changes. This strategy combines the fast moving average and the slow moving average to form an indicator curve. The curve crosses the trend to buy and the curve crosses the trend to sell below to track the market trend.
## Strategy Principle
This strategy is based on the Aggregated Momentum indicator, which improves the William indicator by replacing the opening price with the average of the day's highest and lowest prices to solve the problem of missing opening prices. The indicator formula is:
Converging Momentum Line = Fast Converging Momentum Exponential Moving Average - Slow Converging Momentum Exponential Moving Average
Among them, the calculation formula of the aggregate momentum index is:
Aggregated Momentum Index = (Closing Price - Opening Price) / (Highest Price - Lowest Price) * Trading Volume
Since the opening price is missing, here is the following:
Aggregated Momentum Index = (Closing Price - (Highest Price + Lowest Price)/2) / (Highest Price - Lowest Price) * Trading Volume
The indicator uses the difference between the fast moving average and the slow moving average as the converged momentum line. When the fast line crosses the slow line, it is a buy signal, and when it crosses below, it is a sell signal.
The specific operations are:
1. Calculate the aggregate momentum index
2. Calculate fast EMA and slow EMA
3. Calculate the difference between the two as the aggregate momentum line
4. Buy when the line crosses the 0 axis, sell when the line crosses the 0 axis.
## Advantage Analysis
This strategy has the following advantages:
1. Capture market capital flows and determine market trends
2. Combine fast and slow moving averages to filter out false breakthroughs
3. The rules are clear, simple and easy to implement
## Risk Analysis
There are also some risks with this strategy:
1. The converged momentum indicator lags and may miss trend turning points
2. Parameters need to be adjusted appropriately to avoid generating too many trading signals
3. Stop loss needs to be considered to control single loss
Risks can be controlled through parameter optimization and combination with other indicators.
## Optimization direction
This strategy can consider the following directions for optimization:
1. Optimize fast and slow moving average parameters to balance trading frequency and stability
2. Add exit conditions, such as trend reversal and other signals
3. Filter in combination with other indicators, such as RSI, MACD, etc.
4. Add a stop-loss strategy to control single losses
5. Adjustable parameters for different varieties to generate customized strategies
## Summarize
The aggregated momentum indicator strategy is generally relatively stable and reliable, and can balance returns and risks through parameter adjustment. Adding filters and stops can further improve strategy stability. This strategy is suitable for tracking trending markets and can achieve satisfactory strategic effects through customized optimization.

||


## Overview

The Chaikin Oscillator strategy uses the Chaikin Oscillator indicator to judge capital flow in the market and capture trend changes. This strategy combines fast and slow moving averages to form an indicator curve, buying when the curve crosses above the trendline and selling when the curve crosses below to track market trends.

## Strategy Logic

This strategy is based on the Chaikin Oscillator indicator, which improves on the Williams Accumulation/Distribution indicator by using the average of the high and low prices instead of the opening price to address the missing opening price problem. The indicator formula is:

Chaikin Oscillator = Fast EMA of Accumulation/Distribution Index - Slow EMA of Accumulation/Distribution Index

Where the Accumulation/Distribution Index is calculated as: 

Accumulation/Distribution Index = (Close - Open) / (High - Low) * Volume

Since the opening price is missing, it is calculated here as:

Accumulation/Distribution Index = (Close - (High + Low)/2) / (High - Low) * Volume

The indicator takes the difference between fast and slow EMAs of the index as the Chaikin Oscillator. A crossing above 0 indicates a buy signal, while a crossing below 0 indicates a sell signal. 

The specific logic is:

1. Calculate the Accumulation/Distribution Index 
2. Calculate fast and slow EMAs
3. Take the difference as the Chaikin Oscillator
4. Buy when the oscillator crosses above 0, sell when it crosses below 0

## Advantage Analysis 

The advantages of this strategy are:

1. Captures capital flow to determine market trend
2. Combines fast and slow moving averages to filter false breaks  
3. Simple and clear rules easy to implement

## Risk Analysis

Some risks of this strategy are:

1. The Chaikin Oscillator lags, potentially missing trend turning points
2. Requires tuning parameters to avoid excessive trades  
3. Needs stop loss to control single losing trades

Risks can be managed through parameter optimization, combining with other indicators, etc.

## Improvement Directions

Some ways to improve this strategy:

1. Optimize fast and slow EMA periods to balance frequency and stability
2. Add exit conditions like trend reversal signals 
3. Add filters like RSI, MACD to confirm signals
4. Incorporate stop loss strategy to control losses
5. Adjust parameters for different products to create customized strategies

## Conclusion

Overall the Chaikin Oscillator strategy is relatively stable and reliable. Fine tuning parameters can balance profitability and risk. Adding filters and stop loss can further improve robustness. This trend following strategy can achieve satisfactory results through customized optimizations.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|3|Fast|
|v_input_2|10|Slow|
|v_input_3|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-11 00:00:00
end: 2023-10-11 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 18/09/2017
//    Indicator plots Money Flow Indicator (Chaikin). This indicator looks 
//    to improve on Larry William's Accumulation Distribution formula that 
//    compared the closing price with the opening price. In the early 1970's, 
//    opening prices for stocks stopped being transmitted by the exchanges. 
//    This made it difficult to calculate Williams' formula. The Chaikin 
//    Oscillator uses the average price of the bar calculated as follows 
//    (High + Low) /2 instead of the Open.
//    The indicator subtracts a 10 period exponential moving average of the 
//    AccumDist function from a 3 period exponential moving average of the 
//    AccumDist function.    
//
// You can change long to short in the Input Settings
// WARNING:
//  - For purpose educate only
//  - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="Money Flow Indicator (Chaikin Oscillator)", shorttitle="MFI")
Fast = input(3, minval=1)
Slow = input(10, minval=1)
reverse = input(false, title="Trade reverse")
hline(0, color=gray, linestyle=hline.style_dashed)
lenMax = max(Fast, Slow)
lenMin = min(Fast, Slow)
xDiv = (high - low) * volume
SumMax = sum(iff(xDiv > 0, (close - open) / (high - low) * volume , 0) , lenMax)
SumMin = sum(iff(xDiv > 0, (close - open) / (high - low) * volume , 0) , lenMin)
emaMax = ema(SumMax, lenMax)
emaMin = ema(SumMin, lenMin)
nRes = emaMax - emaMin
pos = iff(nRes > 0, 1,
	   iff(nRes < 0, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue ) 
plot(nRes, color=blue, title="RMI")
```

> Detail

https://www.fmz.com/strategy/429077

> Last Modified

2023-10-12 16:41:54
