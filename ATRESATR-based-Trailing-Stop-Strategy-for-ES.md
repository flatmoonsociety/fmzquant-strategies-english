
> Name

ATR-based-Trailing-Stop-Strategy-for-ES
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/73267d9633c369a08282af3b5ac1fd8c015b8d1f3e46a3f5309a71c33f711526.png)
[trans]

## Overview
This strategy is a trailing stop strategy applied to E-mini S&P500 futures (ES). It uses the 10-day ATR as a reference and 3 times the ATR as the stop loss range to set the stop loss lines for long and short positions. The strategy determines the trend through the direction change of the ATR line and generates entry signals at the turning point of the trend. Once entered, it will adjust the stop loss line in real time, allowing the stop loss line to follow the price to achieve profit protection.
## Strategy Principle
This strategy uses hl2 as the price source. First calculate the 10-day ATR, and let the user choose whether to use the SMA method to calculate the ATR or the built-in ATR function. After calculating the ATR, add 3 times the ATR upward and downward as the range. These two range lines are stop loss lines.
The way to judge the trend is that when the price exceeds the upper boundary, it is a long position; when the price falls below the lower boundary, it is a short position. When price pulls back into the range, a trend reversal is confirmed. At this time, if it turns from empty to long, a long entry signal is generated; if it turns from long to short, a short entry signal is generated.
After entering the market, the long stop-loss line is set to move the upper boundary down by 1 point, and the short stop-loss line is set to the lower boundary to move up by 1 point to provide trailing protection for profits.
## Strategic Advantages
1. Using ATR can automatically adapt to changes in market volatility and reduce the probability of stop loss being triggered.
2. The method of tracking trends is simple and effective and avoids the risk of chasing tops and bottoms.
3. Trailing stop loss ensures the protection of profits and avoids losses again after making profits.
## Risk Analysis
1. Improper setting of ATR parameters may cause the stop loss range to be too large or too small.
2. When the underlying volatility changes suddenly, abnormal stop loss may occur.
3. TAILING stop loss may be too conservative and fail to continuously track the trend
## Optimization direction
1. You can consider optimizing ATR parameters in combination with volatility indicators.
2. You can test different TAILING stop loss algorithms, such as balance percentage stop loss, etc.
3. Can combine trend indicators to filter entry signals to avoid non-main trend entries
## Summarize
Overall, this strategy is a more universal trend following strategy. It solves the problem of difficulty in determining the stop loss range and reduces risks through dynamic adjustment of ATR. At the same time, trailing stop loss is used to protect profits. However, there is still room for optimization in ATR parameters, stop loss algorithms, etc. Through further testing and parameter adjustment, this strategy can become a more robust trailing stop loss strategy.
||


## Overview

This strategy is a trailing stop strategy applied to the E-mini S&P500 futures (ES). It uses 10-day ATR as a reference and sets the stop loss range to 3 times ATR to define long and short stop lines. The strategy judges the trend by the direction change of the ATR lines and generates entry signals at turning points of the trend. Once entered, it will adjust the stop loss lines in real time to trail the price movement, protecting profits.

## Strategy Logic  

The strategy uses hl2 as the price source. First it calculates the 10-day ATR, and lets the user choose between using SMA method or built-in ATR function to calculate ATR. After obtaining ATR, it adds 3 times ATR up and down to form the range. The two range lines are the stop loss lines.

The method to judge the trend is when the price exceeds the upper boundary, it is long; when the price breaks the lower boundary, it is short. When the price retraces back into the range, it confirms the trend reversal. At this time, if turned from short to long, it will generate a long entry signal; if turned from long to short, it will generate a short entry signal.

After entering, the long stop loss line is set to the upper boundary minus 1 tick, and the short stop loss line is set to the lower boundary plus 1 tick, trailing to protect profits.

## Advantages

1. Using ATR can automatically adapt to changes in market volatility and reduce the probability of stop loss being triggered. 
2. The trend tracking method is simple and effective to avoid risks of chasing tops and bottoms.
3. Trailing stops lock in profits and avoid giving back profitable trades.

## Risk Analysis  

1. Improper ATR parameter setting may cause the stop loss range to be too large or too small.
2. Drastic changes in the volatility of the underlying may cause abnormal stop loss triggering.  
3. TRAILING stops may be too conservative to keep tracking the trend.

## Optimization Directions

1. Consider optimizing ATR parameters combined with volatility metrics.  
2. Test different trailing stop algorithms like percentage trailing stops etc.
3. Filter entry signals combined with trend indicators to avoid false trend signals.

## Conclusion

In general, this is a robust trend following strategy. It solves the problem of determining stop loss range and reduces risks by adjusting stops dynamically based on ATR. At the same time, trailing stops lock in profits. But there is still room for optimizing parameters like ATR periods, stop algorithms etc. With further testing and tuning, this strategy can become a trend following strategy with high robustness.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|ATR Period|
|v_input_2_hl2|0|Source: hl2|high|low|open|close|hlc3|hlcc4|ohlc4|
|v_input_3|3|ATR Multiplier|
|v_input_4|true|Change ATR Calculation Method ?|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-05 00:00:00
end: 2024-01-11 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("ATR Based Trailing Stop Strategy on ES! [v4]", overlay=true)

// Given ATR study
Periods = input(title="ATR Period", type=input.integer, defval=10)
src = input(hl2, title="Source")
Multiplier = input(title="ATR Multiplier", type=input.float, step=0.1, defval=3.0)
changeATR = input(title="Change ATR Calculation Method ?", type=input.bool, defval=true)
atr2 = sma(tr, Periods)
atr = changeATR ? atr(Periods) : atr2
up = src - (Multiplier * atr)
up1 = nz(up[1], up)
up := close[1] > up1 ? max(up, up1) : up
dn = src + (Multiplier * atr)
dn1 = nz(dn[1], dn)
dn := close[1] < dn1 ? min(dn, dn1) : dn
trend = 1
trend := nz(trend[1], trend)
trend := trend == -1 and close > dn1 ? 1 : trend == 1 and close < up1 ? -1 : trend

// Entry logic based on trend change
longCondition = trend == 1 and trend[1] == -1
shortCondition = trend == -1 and trend[1] == 1

if (longCondition)
    strategy.entry("Long", strategy.long)

if (shortCondition)
    strategy.entry("Short", strategy.short)

// Trailing stop loss logic
// For long positions, trail 1 point below the up plot
longStopPrice = up - 1

// For short positions, trail 1 point above the dn plot
shortStopPrice = dn + 1

strategy.exit("Trailing Stop Long", "Long", trail_offset=longStopPrice)
strategy.exit("Trailing Stop Short", "Short", trail_offset=shortStopPrice)

```

> Detail

https://www.fmz.com/strategy/438505

> Last Modified

2024-01-12 14:52:23
