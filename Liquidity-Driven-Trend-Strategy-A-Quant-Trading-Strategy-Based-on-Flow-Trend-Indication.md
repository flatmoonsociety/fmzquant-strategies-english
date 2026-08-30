
> Name

Liquidity-Driven-Trend-Strategy-A-Quant-Trading-Strategy-Based-on-Flow-Trend-Indication
> Author

ChaoZhang

> Strategy Description


![IMG](assets/images/4cd26810491da6f6f7a364eee4de6cf9193ceb560b94a340a6478f454a4b39de.png)

[trans]

## Overview
This strategy is called "Liquidity Driven Trend Strategy" and its purpose is to identify the price trend direction in different time periods and make buying or selling decisions accordingly. This strategy uses a dual moving average system to determine the trend, and uses the spread relative strength index (RSI) on multiple time frames to respond promptly when the trend changes.
## Strategy Principle
The core logic of this strategy is based on the CHOP indicator, in which the moving average system determines the direction of the general trend. Specifically, the strategy calculates the RSI values ​​of the fast line (Length=20) and the slow line (Length=50) on the high cycle time frame, and calculates the difference between the two. When the fast RSI crosses above the slow RSI, it is judged to be bullish, forming a long signal; conversely, when the fast RSI crosses below the slow RSI, it is bearish, forming a short signal. According to the RSI difference that changes when the price rises and falls, the trend change point can be determined sensitively.
This strategy also introduces multi-time frame judgment: calculate the RSI difference in a higher-level period (such as the daily line) to determine the overall trend direction; based on the judgment results of the higher-level period, perform specific buy and sell executions in a lower-level period (such as the 5-minute line). This combination of multiple time frames takes into account both high-cycle trend judgment and the flexibility of low-cycle operations.
## Strategic Advantages
- Use the RSI difference to determine potential trend reversals, react in advance, and be sensitive
- Apply multi-time frame ideas, judge trends in high cycles, and execute operations in low cycles
- The RSI indicator reflects changes in price and trading volume, reflecting market liquidity and participation enthusiasm.
- Simple parameter settings, easy to understand, explain and adjust
## Strategic risks and solutions
- False breakthroughs may occur when judging double moving averages
- Failure to break through may cause unnecessary losses
Solution:
1. Adjust moving average parameters to reduce the probability of false breakthroughs
2. Add filter conditions to avoid unnecessary admissions
## Strategy optimization direction
- Optimize RSI parameters using Kalman Filter algorithm
- Add indicators such as MACD to assist judgment
- Set dynamic exit positions based on changes in trading volume
## Summarize
This strategy uses the RSI difference to determine potential trend changes and capture turning points sensitively. The use of multiple time frames not only ensures the judgment of the general trend, but also makes specific trading operations more flexible. Compared with other trend following strategies, this strategy is simpler and more direct, with intuitive parameter settings and easy to adjust and optimize. Overall, this strategy forms an efficient and practical trend trading system, which is worthy of further exploration and application.

||

## Overview

The strategy is named "Liquidity Driven Trend Strategy". It aims to identify the price trend direction across different time frames and make corresponding long or short decisions. The strategy employs a dual moving average system to determine the trend and uses the difference between Relative Strength Index (RSI) values across multiple time frames to respond timely to trend changes.  

## Strategy Logic   

The core logic of this strategy is based on the CHOP indicator, where the moving average system judges the overall trend direction. Specifically, the strategy calculates the RSI values of a fast line (Length = 20) and a slow line (Length = 50) on higher time frames, and computes the difference between the two RSI lines. When the fast line RSI crosses above the slow line RSI, it signals an upward trend and triggers long signals. On the contrary, if the fast line RSI crosses below the slow line RSI, it indicates a downward trend and generates short signals. The varying RSI difference driven by price rises and falls can sensitively identify trend changing points.   

The strategy also introduces a multi-timeframe mechanism: it computes the RSI difference on higher time frames (e.g. daily) to determine the overall trend direction, and then executes actual buy and sell orders on lower time frames (e.g. 5 mins) based on the higher timeframe trend judgment. Such combination of multiple time frames takes into account both high-timeframe trend decisions and the flexibility of low-timeframe execution.  

## Advantages of the Strategy  

- Sensitively capture potential trend reversals ahead of time using RSI divergence 
- Apply multi-timeframe concept to determine trend on higher TF and execute orders on lower TF
- RSI reflects price and volume changes, indicating market liquidity and participation  
- Simple parameter settings, easy to understand, explain and tune  

## Risks & Solutions

- False breakout may happen with dual MA system  
- Failed breakout can cause unnecessary losses

Solutions:

1. Adjust MA parameters to reduce false breakout probability  
2. Add filters to avoid unnecessary entry  

## Optimization Directions 

- Optimize RSI parameters using Kalman Filter algorithms
- Add MACD and other indicators to assist judgement 
- Set dynamic exit positions based on trading volume changes  

## Conclusion

This strategy leverages RSI divergence to sensitively capture potential turning points of the trend. The multi-timeframe application ensures judging the overall trend while keeping specific trade execution flexible. Compared to other trend following strategies, this strategy is more straightforward, intuitive in parameter adjustments and easy to optimize. In conclusion, the strategy forms an efficient and practical trend trading system worth further exploration and application.  

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-19 00:00:00
end: 2023-12-19 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Flow Trend Indicator Strategy", "FlowTI", overlay=true, calc_on_every_tick=true)

isTimeFrame(timeFrame) =>
    timeFrame == timeframe.period ? true : false

Htf() =>
    isTimeFrame("12") ? "60" : isTimeFrame("60") ? "300" : isTimeFrame("300") ? "D" : isTimeFrame("D") ? "W" : isTimeFrame("W") ? "M" : isTimeFrame("M") ? "5M" : "D"

TrendIndication() =>
    trendFastLength = 20
    trendSlowLength = 50
    upFastHtf = request.security(syminfo.tickerid, Htf(), rma(max(change(close), 0), trendFastLength), barmerge.gaps_off, barmerge.lookahead_on)
    downFastHtf = request.security(syminfo.tickerid, Htf(), rma(-min(change(close), 0), trendFastLength), barmerge.gaps_off, barmerge.lookahead_on)
    rsiFastHtf = downFastHtf == 0 ? 100 : upFastHtf == 0 ? 0 : 100 - (100 / (1 + upFastHtf / downFastHtf))
    upSlowHtf = request.security(syminfo.tickerid, Htf(), rma(max(change(close), 0), trendSlowLength), barmerge.gaps_off, barmerge.lookahead_on)
    downSlowHtf = request.security(syminfo.tickerid, Htf(), rma(-min(change(close), 0), trendSlowLength), barmerge.gaps_off, barmerge.lookahead_on)
    rsiSlowHtf = downSlowHtf == 0 ? 100 : upSlowHtf == 0 ? 0 : 100 - (100 / (1 + upSlowHtf / downSlowHtf))
    rsiDiff = rsiFastHtf - rsiSlowHtf
    crossover(rsiDiff, 0) ? true : crossunder(rsiDiff, 0) ? false : na

if (TrendIndication() == true)
    strategy.entry("Long", strategy.long)

if (TrendIndication() == false)
    strategy.entry("Short", strategy.short)
```

> Detail

https://www.fmz.com/strategy/436089

> Last Modified

2023-12-21 10:19:52
