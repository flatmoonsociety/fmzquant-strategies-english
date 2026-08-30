
> Name

Smooth moving average and moving average trading strategy EMA-and-Heikin-Ashi-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/3f3fffdd2f031be83d255a32ff51a302f2ff60342e8b93515f04065e979f26b5.png)

Here is an article about EMA and Heikin Ashi trading strategy:
[trans]


## Overview
This strategy uses smoothed moving averages and moving averages to determine trends, and generates trading signals based on price breakthroughs of moving averages of different periods.
## Strategy Principle
This strategy uses 15-period and 50-period exponential moving average EMAs. Calculate the current Heikin Ashi closing price and compare it with the EMA. If the closing price is higher than the two EMAs, and the 15EMA is higher than the 50EMA, a buy signal is generated; if the closing price is lower than the two EMAs, and the 15EMA is lower than the 50EMA, a sell signal is generated.
When the price breaks above the 15EMA again, perform a reverse trade.
## Advantage Analysis
1. Using EMA can effectively filter market noise and determine the trend direction.
2. Combined with EMA of different periods, short-term and medium-term trends can be captured at the same time.
3. Heikin Ashi can filter out false breakthroughs and verify trading signals.
4. The strategy is simple, clear and easy to implement.
## Risk Analysis
1. EMA has hysteresis and may miss the trend turning point.
2. Fixed parameters cannot adapt to market changes and require dynamic optimization.
3. Transactions are frequent and transaction costs may be high.
4. Breakout trading is susceptible to false breakthroughs and should be verified in conjunction with other indicators.
Risks can be reduced through parameter optimization and integration of other indicators.
## Optimization direction
1. Dynamically optimize EMA parameters and adjust the cycle according to market changes.
2. Optimize breakthrough filtering to avoid false breakthroughs. For example, increase transaction volume verification.
3. Combine with other indicators such as MACD to verify trading signals.
4. Use lagging EMA according to the trend and leading EMA according to the shock.
## Summarize
This strategy uses EMA to determine the trend direction and Heikin Ashi to verify the signal, which is simple and direct. However, attention should be paid to the lag of EMA and the risk of false breakthrough. It can be improved through parameter optimization, indicator integration, etc. to reduce risks while improving strategy effects.

||

## Overview

This strategy uses exponential moving averages (EMA) and Heikin Ashi to determine trends and generate trading signals when prices break through EMAs of different periods.

## Trading Logic

The strategy uses 15-period and 50-period EMAs. It calculates the current Heikin Ashi closing price and compares it to the EMAs. If the closing price is above both EMAs and the 15-period EMA is above the 50-period EMA, a long signal is generated. If the closing price is below both EMAs and the 15-period EMA is below the 50-period EMA, a short signal is generated.

When the price breaks back above the 15-period EMA, a reverse trade is made.

## Advantage Analysis  

1. Using EMAs helps filter out market noise and determine trend direction.

2. Combining EMAs of different periods captures both short-term and mid-term trends.

3. Heikin Ashi filters out false breakouts and confirms trading signals.

4. The strategy is simple and easy to implement.

## Risk Analysis

1. EMAs have lag and may miss trend turning points. 

2. Fixed parameters fail to adapt to changing markets, requiring dynamic optimization.

3. Frequent trading leads to potentially high transaction costs. 

4. Breakout trading is susceptible to false breakouts, requiring additional indicator confirmation.

Risks can be reduced through parameter optimization, integrating other indicators, etc.

## Optimization Directions

1. Dynamically optimize EMA periods based on market changes.

2. Optimize breakout filters to avoid false breakouts, e.g. add volume confirmation.

3. Incorporate other indicators like MACD to confirm signals.  

4. Use lagging EMA for trends and leading EMA for ranges.

## Summary

This strategy uses EMAs to determine trend direction and Heikin Ashi to verify signals. It is simple and straightforward but EMA lag and false breakout risks need to be addressed. Improvements can be made via parameter optimization, indicator integration to reduce risk and improve strategy performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|price: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|15|MA1_Length|
|v_input_3|50|MA2_Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-09 00:00:00
end: 2023-10-12 02:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("EMA & Heikin Ashi", shorttitle="EMA & Heikin Ashi", overlay=true, initial_capital=1)


// squaa's Strategy
//
// Idea by Thw on March 10, 2018.
//
//
// The strategy should be used with high leverages,
// never stop running,
// and is always long or short.

// Input
price = input(close)
MA1_Length = input(15)
MA2_Length = input(50)


haclose = request.security(heikinashi(syminfo.tickerid), timeframe.period, close)

// === FUNCTION EXAMPLE ===
start     = timestamp(2018, 01, 01, 20, 00)  // backtest start window
window()  => time >= start ? true : false // create function "within window of time"


// Calculation
MA1 = ema(price, MA1_Length)
MA2 = ema(price, MA2_Length)

// Strategy
long = haclose > MA1 and haclose > MA2 and MA1 > MA2 and window()
short = haclose < MA1 and haclose < MA2 and MA1 < MA2 and window()

// MA trend output color
MA2_color = long?lime:short?red:blue

strategy.entry("Long", strategy.long, when=long)
strategy.entry("Short", strategy.short, when=short)
strategy.close("Long", when=haclose < MA1)
strategy.close("Short", when=haclose > MA1)


// MA output
EMA1 = plot(MA1, title="EMA 1", style=linebr, linewidth=1, color=MA2_color)
EMA2 = plot(MA2, title="EMA 2", style=linebr, linewidth=3, color=MA2_color)
fill(EMA1, EMA2, color=silver, transp=50)

//plot(strategy.equity, title="equity", color=red, linewidth=2, style=areabr)
```

> Detail

https://www.fmz.com/strategy/429493

> Last Modified

2023-10-17 16:11:19
