
> Name

Trend-Following-Strategy-Based-on-MBO-Indicator
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy implements a simple trend following trading system based on the MBO indicator. The MBO indicator is similar to the MACD indicator, using the difference between the fast moving average and the slow moving average as a trading signal. Go long when the fast moving average crosses the slow moving average and go short when it crosses below. This strategy trades by following the trend of the MBO indicator.
## Strategy Principle
This strategy is mainly based on the construction of the MBO indicator to generate trading signals. The MBO indicator was developed by Bryan Strain and Mark Whitley. The indicator calculation method is:
MBO = 25-day simple moving average – 200-day simple moving average
Then smooth the MBO index acceleration line and calculate the MBO's 18-day simple moving average SMAMBO.
When MBO crosses SMAMBO above, go long; when MBO crosses SMAMBO below, go short.
From the code logic point of view, the main steps are:
1. Calculate the 25-day and 200-day simple moving averages and assign values ​​to xFastAvg and xSlowAvg
2. Calculate the value of MBO: MFBO = xFastAvg - xSlowAvg
3. Calculate MBO’s 18-day simple moving average SMAMBO
4. Compare MBO and SMAMBO to generate trading signal pos
If MBO > SMAMBO, pos = 1, go long
If MBO < SMAMBO, pos = -1, short
5. Determine entry and exit based on the value of pos
This strategy trades by following the trend shown by the MBO indicator, which is a typical trend following strategy.
## Advantage Analysis
This strategy has the following advantages:
1. By following the mid- to long-term trend, you can reduce the frequency of transactions and avoid unnecessary stop losses.
2. The MBO indicator parameters are adjustable and can be adjusted to adapt to different market environments.
3. The strategy logic is simple and clear, easy to understand and implement, and is suitable for beginners to learn.
4. Visual indicators clearly show changes in trends and support strategic decisions.
5. It has strong scalability, can be optimized based on this strategy, and can add stop loss mechanism, etc.
## Risk Analysis
There are also some risks with this strategy:
1. Trading following the trend is prone to vertical rises and falls, which may result in larger losses.
2. Failure to stop the loss and exit in time when the trend reverses may lead to larger losses.
3. Improper parameter settings may lead to excessive trading frequency or inaccurate signals.
4. It is easy to generate false breakthrough signals and a filtering mechanism needs to be added.
5. The strategy itself does not set a stop loss point, and there is a risk of unlimited losses.
Corresponding solutions:
1. Set the moving average parameters reasonably and not be too sensitive.
2. Add indicators for trend reversal and stop losses promptly when a reversal is found.
3. Optimize parameter settings and adjust to generate accurate signals.
4. Add a filtering mechanism to avoid false breakthroughs.
5. Set a stop loss point to control single loss.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Add the trend reversal signal indicator to stop losses in time when the trend reverses.
2. Optimize the moving average parameter settings to balance trading frequency and signal quality.
3. Add ATR stop loss, set a reasonable stop loss point, and control single loss.
4. Combine with other indicators to filter out false breakthrough signals.
5. Add position management and adjust positions according to the strength of the trend.
6. You can consider entering the market after forming a three-push structure before the breakthrough.
7. Establish a parameter optimization mechanism and adjust parameters according to different markets.
## Summarize
This strategy captures trends through a simple MBO indicator and conducts trend following transactions. The advantages are simple and practical, clear visual indicators, and suitable for beginners to learn. However, there is also the risk of only chasing the rise and killing the fall, and being unable to stop the loss. We can optimize the strategy by adding reversal signals, optimized parameter settings, stop loss mechanisms, etc., to make it a stable and reliable trend following strategy. Overall, this strategy is very good as an entry-level trend following strategy and can become a powerful tool for daily trading through optimization.
||

## Overview

This strategy implements a simple trend following trading system based on the MBO indicator. The MBO indicator is similar to the MACD indicator, using the difference between fast and slow moving averages as trading signals. It goes long when the fast moving average crosses above the slow one, and goes short when the fast crosses below the slow one. The strategy follows the trend of the MBO indicator to trade.

## Strategy Logic

The strategy generates trading signals primarily based on the MBO indicator. The MBO indicator was developed by Bryan Strain and Mark Whitley. The indicator is calculated as:

MBO = 25-day Simple Moving Average - 200-day Simple Moving Average

The MBO line is then smoothed by calculating the 18-day Simple Moving Average of MBO, called SMAMBO.

When MBO crosses above SMAMBO, go long. When MBO crosses below SMAMBO, go short.

The key steps in the strategy logic are:

1. Calculate the 25-day and 200-day SMA, assigned to xFastAvg and xSlowAvg. 

2. Calculate the MBO value: MBO = xFastAvg - xSlowAvg

3. Calculate the 18-day SMA of MBO, called SMAMBO.

4. Compare MBO and SMAMBO to generate trading signals pos:

    If MBO > SMAMBO, pos = 1, go long
    
    If MBO < SMAMBO, pos = -1, go short

5. Enter and exit trades based on the value of pos.

The strategy follows the trend exhibited by the MBO indicator. It is a typical trend following strategy.

## Advantage Analysis 

The advantages of this strategy include:

1. Lower trading frequency and avoid unnecessary stops by following medium/long term trends.

2. Flexible MBO parameters adaptable to different market conditions. 

3. Simple and clear logic, easy to understand and implement, good for beginners.

4. Visual indicator clearly shows trend changes to support decisions. 

5. High extensibility to optimize with stops, etc.

## Risk Analysis

The risks of the strategy:

1. Trend following tends to vertical rallies/selloffs that can produce large losses.

2. Fails to exit in a timely manner when trend reverses, potentially increasing losses.

3. Inappropriate parameters may cause too frequent trading or inaccurate signals. 

4. Susceptible to false breakout signals, needs filter mechanisms.

5. No stop loss mechanism results in unlimited loss potential.

Solutions:

1. Use reasonable SMA parameters, not too sensitive.

2. Add trend reversal indicator, exit quickly after reversal signaled.

3. Optimize parameters for accurate signals.  

4. Add filters to avoid false breakouts.

5. Implement stop loss to control loss per trade.

## Optimization Directions

The strategy can be improved in the following ways:

1. Add trend reversal indicator, implement timely stop loss after reversal.

2. Optimize SMA parameters to balance trade frequency and signal quality.

3. Add ATR stop loss to set reasonable stop levels to control loss.

4. Incorporate other indicators to filter false breakouts. 

5. Implement position sizing based on trend strength.

6. Consider requiring triple confirmation before entry.

7. Build parameter optimization mechanism to adjust to different markets.

## Summary

The strategy captures trends using a simple MBO indicator for trend following trading. The advantages are being simple, intuitive visuals, and beginner friendly. But risks like chasing rallies and inability to stop loss exist. We can optimize it by adding reversal signals, optimizing parameters, implementing stops etc, to build a robust trend following system. Overall it is a great introductory trend following strategy, and can become a practical daily trading tool after optimization.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|25|Fastavg|
|v_input_2|200|Slowavg|
|v_input_3|18|Length|
|v_input_4|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-08 00:00:00
end: 2023-10-08 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 16/08/2018
// MBO indicator is the third component of TFS trading system. This indicator
// was developed by Bryan Strain and Mark Whitley.
// The idea of MBO is similar to moving average convergence/divergence (MACD)
// indicator. It is calculated by subtracting the 200-day moving average from
// the 25-day moving average.
//
// You can change long to short in the Input Settings
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="TFS: MBO Backtest", shorttitle="TFS: MBO indicator")
Fastavg = input(25, minval=1)
Slowavg = input(200, minval=1)
Length = input(18, minval=1)
reverse = input(false, title="Trade reverse")
hline(0, color=blue, linestyle=line)
xFastAvg = sma(close, Fastavg)
xSlowAvg = sma(close, Slowavg)        
nMBO = xFastAvg - xSlowAvg
xSMAMBO = sma(nMBO, Length)
pos = iff(nMBO > xSMAMBO, 1,
       iff(nMBO < xSMAMBO, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue ) 
plot(nMBO, color=red, style = histogram, title="TFS: MBO indicator")
plot(xSMAMBO, color=blue, title="SMA")
```

> Detail

https://www.fmz.com/strategy/428793

> Last Modified

2023-10-09 15:22:04
