
> Name

Ichimoku-Kinko-Hyo Trend Following Strategy Ichimoku-Kinko-Hyo-indicator-Balancing-Trend-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/756f14bd74da3fbb39ae0f69ad97fd1379f6d790e162f5241577a35602d525c5.png)
[trans]

## Overview
The Ichimoku strategy is a trend following strategy implemented using the Ichimoku Kinko Hyo indicator. This strategy combines multiple indicators to identify the trend direction, go long in the bull market and short in the bear market to achieve long-term appreciation of funds.
## Strategy Principle
This strategy is mainly based on the Ichimoku Kinko Hyo indicator. The indicator consists of the reversal line (Tenkan-Sen), the base line (Kijun-Sen), the front line (Senkou-Span A), the leading line (Senkou-Span B) and the delay line (Chikou-Span). When the price is above the cloud, it is a bullish trend, and when the price is below the cloud, it is a bearish trend.
The trading signals for this strategy come from a combination of the following conditions:
1. When the steering line crosses the baseline, it is a bullish signal.
2. When the steering line crosses the baseline, it is a short signal.
3. The upward crossing of the delay line is confirmation for bulls
4. The downward crossing of the delay line is confirmation of short positions.
5. RSI indicator above 50 is a bullish indicator
6. RSI indicator below 50 is a short indicator
7. Price above the cloud chart is a bullish trend
8. The price is in a bearish trend under the cloud chart.
When the above long conditions are met at the same time, enter the market as a long position; when the above conditions for the short position are met at the same time, enter the market as a short position.
## Advantage Analysis
This strategy combines trend following and overbought and oversold indicators to effectively identify the direction of the trend. The main advantages are as follows:
1. The Ichimoku Kinko Hyo indicator can identify medium and long-term trends and avoid being misled by short-term market noise.
2. Combined with the RSI indicator, it can effectively determine the overbought and oversold areas to prevent missing reversal opportunities.
3. Taking into account the stock price volatility conditions, only take action when the volatility is high to avoid invalid transactions.
4. Strict entry and exit mechanisms to avoid risks to the greatest extent.
## Risk Analysis
There are also some risks to be aware of with this strategy:
1. There is a lag in the Ichimoku Kinko Hyo indicator, which may lead to late entry timing.
2. Multi-condition combination trading signals appear less frequently, which can easily lead to insufficient number of transactions.
3. Without considering capital management and position management, there may be the risk of excessive trading.
Corresponding solutions:
1. Appropriately shorten the Ichimoku Kinko Hyo parameters to improve the sensitivity of the indicator.
2. Reduce the stringency of entry conditions and increase transaction frequency.
3. Add fund management and position management modules to control the fund proportion and position of a single transaction.
## Optimization direction
This strategy can be optimized from the following directions:
1. Replace or combine other indicators, such as KDJ, MACD, etc., to enrich signal sources.
2. Optimize Ichimoku Kinko Hyo parameters and improve indicator sensitivity.
3. Add a stop-loss strategy to lock in profits and control risks.
4. Add a position management module to dynamically adjust positions according to the size of funds.
5. Add a futures hedging module to manage long hedging risks.
## Summarize
The overall Ichimoku strategy is a reliable and robust trend following strategy. It addresses an important issue in trend trading - the balance between accuracy in identifying trends and frequency of trade generation. There is still room for optimization through parameter adjustment and module expansion, which is one of the strategies that can be used in the long term.
|| 

## Overview  

The Balancing Trend strategy is a trend following strategy that utilizes the Ichimoku Kinko Hyo indicator. It identifies trend directions by combining multiple indicators, goes long in a bull market and goes short in a bear market, to achieve long-term capital appreciation.   

## Strategy Principle

The core of this strategy is based on the Ichimoku Kinko Hyo indicator, which consists of the Tenkan-Sen (Conversion Line), Kijun-Sen (Base Line), Senkou Span A (Leading Span A), Senkou Span B (Leading Span B) and Chikou Span (Lagging Span). When price is above the cloud, it signals an upward trend. When price is below the cloud, it signals a downward trend.

The trading signals are generated based on the combination of the following conditions:  

1. Tenkan-Sen crosses above Kijun-Sen as bullish signal
2. Tenkan-Sen crosses below Kijun-Sen as bearish signal
3. Chikou Span crossover upward as bullish confirmation  
4. Chikou Span crossover downward as bearish confirmation
5. RSI above 50 as bullish indicator 
6. RSI below 50 as bearish indicator
7. Price above the cloud indicates upward trend  
8. Price below the cloud indicates downward trend

It goes long when all bullish conditions are met and goes short when all bearish conditions are met.

## Advantage Analysis

This strategy combines trend following and overbought-oversold indicators to effectively identify trend directions. The main advantages are:

1. Ichimoku Kinko Hyo can identify medium- to long-term trends, avoiding being misled by short-term market noises.  
2. Incorporating RSI helps determine overbought and oversold zones, preventing missing reversal opportunities.  
3. Only acts when volatility is high enough, avoiding ineffective trades.  
4. Strict entry and exit rules maximally mitigate risks.

## Risk Analysis  

Some risks to note for this strategy:

1. Ichimoku Kinko Hyo has lagging effect, possibly delaying entry timing.  
2. Low frequency of trade signal occurrence with multiple condition combination, leading to insufficient number of trades.   
3. No consideration around position sizing and risk management, risks around over-trading.

Corresponding solutions:

1. Shorten Ichimoku parameters to improve sensitivity. 
2. Reduce strictness of entry conditions to increase trade frequency.  
3. Incorporate risk management and position sizing modules to control per trade risk exposure and overall position.  

## Optimization Directions

The strategy can be improved in the following aspects:  

1. Add or combine additional indicators like KDJ, MACD to diversify signal sources.  
2. Optimize Ichimoku parameters to improve sensitivity. 
3. Add stop loss mechanisms to lock in profits and control risks.
4. Incorporate dynamic position sizing module based on account size.    
5. Add hedging module to manage risks for long positions.   

## Summary

Overall this Balancing Trend strategy is a reliable, robust trend following system. It addresses the key challenge in trend trading - balancing trend identification accuracy and trade generation frequency. There is still room for improvement through parameter tuning and module expansion. It is a strategy that can be applied for the long run.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|22|Tenkan-Sen Bars|
|v_input_2|60|Kijun-Sen Bars|
|v_input_3|120|Senkou-Span B Bars|
|v_input_4|30|Chikou-Span Offset|
|v_input_5|30|Senkou-Span Offset|
|v_input_6|true|Long Entry|
|v_input_7|true|Short Entry|
|v_input_8|2|VolLength|
|v_input_9|0.2|Volatility Target|
|v_input_10|true|From Day|
|v_input_11|true|From Month|
|v_input_12|2019|From Year|
|v_input_13|31|To Day|
|v_input_14|12|To Month|
|v_input_15|2020|To Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-16 00:00:00
end: 2023-11-20 08:00:00
period: 3m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Ichimoku Kinko Hyo: ETH 3h Strategy by tobuno", overlay=true)

//Inputs
ts_bars = input(22, minval=1, title="Tenkan-Sen Bars")
ks_bars = input(60, minval=1, title="Kijun-Sen Bars")
ssb_bars = input(120, minval=1, title="Senkou-Span B Bars")
cs_offset = input(30, minval=1, title="Chikou-Span Offset")
ss_offset = input(30, minval=1, title="Senkou-Span Offset")
long_entry = input(true, title="Long Entry")
short_entry = input(true, title="Short Entry")

//Volatility
vollength = input(defval=2, title="VolLength")
voltarget = input(defval=0.2, type=float, step=0.1, title="Volatility Target")
Difference = abs((close - open)/((close + open)/2) * 100)
MovingAverage = sma(Difference, vollength)
highvolatility = MovingAverage > voltarget

////////////////////////////////////////////////////////////////////////////////
// BACKTESTING RANGE
 
// From Date Inputs
fromDay = input(defval = 1, title = "From Day", minval = 1, maxval = 31)
fromMonth = input(defval = 1, title = "From Month", minval = 1, maxval = 12)
fromYear = input(defval = 2019, title = "From Year", minval = 1970)
 
// To Date Inputs
toDay = input(defval = 31, title = "To Day", minval = 1, maxval = 31)
toMonth = input(defval = 12, title = "To Month", minval = 1, maxval = 12)
toYear = input(defval = 2020, title = "To Year", minval = 1970)
 
// Calculate start/end date and time condition
startDate = timestamp(fromYear, fromMonth, fromDay, 00, 00)
finishDate = timestamp(toYear, toMonth, toDay, 00, 00)
time_cond = true
 
////////////////////////////////////////////////////////////////////////////////

middle(len) => avg(lowest(len), highest(len))

// Ichimoku Components
tenkan = middle(ts_bars)
kijun = middle(ks_bars)
senkouA = avg(tenkan, kijun)
senkouB = middle(ssb_bars)

//RSI
change = change(close)
gain = change >= 0 ? change : 0.0
loss = change < 0 ? (-1) * change : 0.0
avgGain = rma(gain, 14)
avgLoss = rma(loss, 14)
rs = avgGain / avgLoss
rsi = 100 - (100 / (1 + rs))

// Plot Ichimoku Kinko Hyo
plot(tenkan, color=#0496ff, title="Tenkan-Sen")
plot(kijun, color=#991515, title="Kijun-Sen")
plot(close, offset=-cs_offset+1, color=#459915, title="Chikou-Span")
sa=plot(senkouA, offset=ss_offset-1, color=green, title="Senkou-Span A")
sb=plot(senkouB, offset=ss_offset-1, color=red, title="Senkou-Span B")
fill(sa, sb, color = senkouA > senkouB ? green : red, title="Cloud color")

ss_high = max(senkouA[ss_offset-1], senkouB[ss_offset-1])
ss_low = min(senkouA[ss_offset-1], senkouB[ss_offset-1])

// Entry/Exit Signals
tk_cross_bull = tenkan > kijun
tk_cross_bear = tenkan < kijun
cs_cross_bull = mom(close, cs_offset-1) > 0
cs_cross_bear = mom(close, cs_offset-1) < 0
price_above_kumo = close > ss_high
price_below_kumo = close < ss_low
rsi_bullish = rsi > 50
rsi_bearish = rs < 50
bullish = tk_cross_bull and cs_cross_bull and price_above_kumo and rsi_bullish and highvolatility
bearish = tk_cross_bear and cs_cross_bear and price_below_kumo and rsi_bearish and highvolatility

strategy.entry("Long", strategy.long, when=bullish and long_entry and time_cond)
strategy.entry("Short", strategy.short, when=bearish and short_entry and time_cond)

strategy.close("Long", when=bearish and not short_entry and time_cond)
strategy.close("Short", when=bullish and not long_entry and time_cond)

```

> Detail

https://www.fmz.com/strategy/433104

> Last Modified

2023-11-24 14:38:47
