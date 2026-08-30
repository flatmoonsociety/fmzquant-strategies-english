
> Name

Parabolic-SAR sector trailing stop loss strategy Parabolic-SAR-Trailing-Stop-Loss-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
Parabolic SAR fan trailing stop loss strategy is a trading strategy based on the Parabolic SAR indicator. This strategy aims to identify trend reversal points and promptly stop losses and exit positions when the trend reverses.
## Strategy Principle
The Parabolic SAR indicator identifies price trends and signals potential reversals. When the SAR point crosses the K line, it represents a move from long to short; when the SAR point crosses below the K line, it represents a move from short to long.
This strategy is based on this characteristic of the Parabolic SAR indicator, which recognizes trend reversal when the SAR point crosses the K-line and performs long or short operations accordingly. Specifically, the strategy logic is as follows:
1. Calculate Parabolic SAR value.
2. Determine whether there is a trend reversal signal. If the SAR point crosses from above to below the K line, it represents a short signal, go short; if the SAR point crosses from below to above the K line, it represents a long signal, go long.
3. Open a position when the crossing occurs, and close the position with a stop loss when the reverse SAR point crosses the K line again.
## Strategic Advantages
- Use the Parabolic SAR indicator to identify trend reversal points and avoid operating in the opposite direction of the trend.
- Quickly open a position when a reversal signal is recognized and capture the change of trend.
- Set the stop loss point when SAR crosses the K line again, you can quickly stop the loss and control the loss in time.
- The strategic ideas are simple, clear and easy to implement.
## Risks and Responses
- The Parabolic SAR indicator may generate a large number of false signals, causing unnecessary transactions. The parameters of SAR can be adjusted appropriately to reduce the false signal rate.
- In a rapidly reversing market, it is easy to get trapped. You can consider adding filtering conditions to avoid periods of severe fluctuations.
- Placing your stop loss too close may result in you being stopped too frequently. The stop loss range can be appropriately relaxed to give the price a certain room for correction.
- Relying on only one indicator is susceptible to specific market restrictions. Consider adding other indicators or filtering conditions to improve the fit.
## Summarize
The Parabolic SAR fan trailing stop loss strategy uses the trend identification ability of the Parabolic SAR indicator to quickly stop the loss and switch directions when the trend reverses. The strategic ideas are simple, clear and easy to master. However, relying only on Parabolic SAR as an indicator also has certain limitations. In practical applications, it is necessary to comprehensively consider the market environment, adjust parameters appropriately, and cooperate with other technical indicators to achieve it.
||



## Overview

The Parabolic SAR trailing stop loss strategy is a trading strategy based on the Parabolic SAR indicator. It aims to identify trend reversal points and exit positions in a timely manner when the trend reverses.

## Strategy Logic

The Parabolic SAR indicator can identify price trends and give potential reversal signals. When the SAR dot crosses above the candlestick, it represents a change from bullish to bearish; when the SAR dot crosses below the candlestick, it represents a change from bearish to bullish.

Based on this feature of the Parabolic SAR indicator, this strategy identifies trend reversals when the SAR dot crosses the candlestick, and makes corresponding long or short entries. Specifically, the strategy logic is as follows:

1. Calculate the Parabolic SAR values. 

2. Determine if there is a trend reversal signal. If the SAR dot crosses from above to below the candlestick, it represents a bearish signal, go short; if the SAR dot crosses from below to above the candlestick, it represents a bullish signal, go long.

3. Enter a position when the crossover occurs, and exit the position with a stop loss when the SAR dot crosses the candlestick in the opposite direction again.

## Advantages

- Utilizes the Parabolic SAR indicator to identify trend reversal points, avoiding trading against the trend.

- Enters positions quickly when reversal signals are identified, capturing trend changes.

- Sets stop loss at the SAR crossover point for quick stops and timely loss control.

- Simple and clear strategy logic, easy to implement.

## Risks and Mitigation

- The Parabolic SAR indicator can generate many false signals, causing unnecessary trades. Fine tune SAR parameters to reduce false signals.

- Prone to being whipsawed in fast reversing markets. Consider adding filters to avoid high volatility periods.

- Stop loss too close may result in excessive stops. Allow some wiggle room in the stop loss range. 

- Reliance on a single indicator makes the strategy susceptible to market-specific limitations. Consider combining with other indicators or filters to improve robustness.

## Conclusion

The Parabolic SAR trailing stop loss strategy utilizes the trend identification capability of the Parabolic SAR indicator to quickly stop out and reverse direction when trends reverse. The strategy logic is simple and clear. However, reliance on only the Parabolic SAR indicator has limitations. In practice, market conditions should be considered, parameters tuned accordingly, and other technical indicators combined to improve performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0.02|start|
|v_input_2|0.02|increment|
|v_input_3|0.2|maximum|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-16 00:00:00
end: 2023-09-15 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy(title="Parabolic SAR Strategy (on close) [QuantNomad]", shorttitle="SAR Strategy [QN]", overlay=true)

start     = input(0.02)
increment = input(0.02)
maximum   = input(0.2)

psar      = 0.0 // PSAR
af        = 0.0 // Acceleration Factor
trend_dir = 0   // Current direction of PSAR
ep        = 0.0 // Extreme point

sar_long_to_short = trend_dir[1] == 1  and close <= psar[1] // PSAR switches from long to short
sar_short_to_long = trend_dir[1] == -1 and close >= psar[1] // PSAR switches from short to long

trend_change = barstate.isfirst[1] or sar_long_to_short or sar_short_to_long

// Calculate trend direction
trend_dir    := barstate.isfirst[1] and close[1] > open[1] ? 1 : 
   barstate.isfirst[1] and close[1] <= open[1] ? -1 : 
   sar_long_to_short ? -1 : 
   sar_short_to_long ?  1 : nz(trend_dir[1])

// Calculate  Acceleration Factor
af := trend_change ? start : 
   (trend_dir == 1 and high > ep[1]) or  
   (trend_dir == -1 and low < ep[1]) ? 
   min(maximum, af[1] + increment) : 
   af[1]

// Calculate extreme point
ep := trend_change and trend_dir == 1 ? high :  
   trend_change and trend_dir == -1 ? low : 
   trend_dir == 1 ? max(ep[1], high) : 
   min(ep[1], low)

// Calculate PSAR
psar := barstate.isfirst[1] and close[1] > open[1] ? low[1] : 
   barstate.isfirst[1] and close[1] <= open[1] ? high[1] : 
   trend_change ? ep[1] :    
   trend_dir == 1 ? psar[1] + af * (ep - psar[1]) : psar[1] - af * (psar[1] - ep) 

plot(psar, style=plot.style_cross, color=trend_dir == 1 ? color.green : color.red,  linewidth = 2)

// Strategy 
strategy.entry("Long",  true,  when = sar_short_to_long)
strategy.entry("Short", false, when = sar_long_to_short)
```

> Detail

https://www.fmz.com/strategy/426993

> Last Modified

2023-09-16 18:54:28
