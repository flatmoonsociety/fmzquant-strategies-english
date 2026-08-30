
> Name

High and low moving average crossover strategy to capture small trends HLHB-Trend-Catcher-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy is designed to capture short-term foreign exchange trends, using EMA crossovers and RSI as trading signals, combined with ADX filters to enter trades, and adopting trend following stops to lock in profits. This strategy works on all currency pairs, but mainly applies to the 1-hour chart of the major currency pairs.
## Strategy Principle
This strategy builds trading signals based on the following indicators and conditions:
- 5-period fast EMA: blue line
- 10-period slow EMA: red line
- 10-period RSI applied to the mid-price closing price (high + low/2)
- 14-period ADX
Trade entry signals:
- Long: Go long when the fast EMA crosses the slow EMA from below, and the RSI line breaks above 50 from the low
- Short: Go short when the fast EMA crosses the slow EMA from above, and the RSI line breaks below 50 from the high
- You can only do long or short when ADX > 25
Exit signal:
- Trailing stop loss, trailing stop loss distance is 150 points, take profit distance is 400 points
- Close positions when new signals appear
- All positions are closed every Friday night
This strategy intensively uses moving average crossover, RSI overbought and oversold, and ADX trend judgment indicators to form a relatively strict entry mechanism. After the trend is generated, it can follow the trend and track the stop loss to lock in profits, thereby effectively capturing the short-term trend.
## Advantage Analysis
This strategy has the following advantages:
1. Use the intersection of EMA fast and slow lines as the basis for trend judgment. If the fast line crosses the slow line upward, it indicates a bullish trend, and if it crosses downward, it indicates a bearish trend. Changes in the trend can be identified.
2. Adding RSI indicator judgment can filter out some false breakthrough signals. RSI overbought and oversold areas are regarded as short-term adjustment signals to avoid unnecessary entry in volatile markets.
3. The ADX indicator is used to determine the existence of a real trend and can effectively filter out some noise. Trading signals are only considered when the ADX value is greater than 25, thus ensuring that there is a clear trend.
4. Adopt trailing stop-loss and take-profit methods to maximize profits, and stop-loss ensures that risks are controllable. The trailing stop-loss distance is 150 points, and the take-profit distance is 400 points, so that you can continue to follow the trend.
5. Close all positions before the market closes every Friday to avoid various risks on weekends and maintain the regularity of operations.
## Risk Analysis
This strategy also has the following risks:
1. The EMA crossover strategy is prone to produce false breakthrough signals, and virtualization may bring losses. You can adjust the moving average parameters appropriately, or add other indicators for filtering.
2. The RSI indicator can only determine overbought and oversold conditions, but cannot confirm trend reversal. Visualization may miss the trend or enter the market in the opposite direction. You can consider using it in combination with other indicators or adjusting parameters.
3. The ADX indicator only determines whether the trend exists, and the entry timing may not be accurate. You can consider adding other criteria or reducing the ADX filtering conditions.
4. The stop-loss and take-profit settings may be too fixed and unable to adapt to market changes. Different parameters can be tested or adjusted manually in a timely manner.
5. Weekly forced liquidation may miss good trend running opportunities. You may consider adjusting it to daily closing or later modifying it to conditional liquidation.
## Optimization direction
This strategy can also be optimized from the following directions:
1. Test different moving average parameter combinations to find the best moving average length. The average slope determination can be introduced.
2. Try different RSI parameters or combine it with KDJ indicators to further optimize the judgment of overbought and oversold.
3. Optimize ADX parameters, find more suitable ADX filtering conditions, and improve entry quality.
4. Test the combination of fixed points of trailing stop loss and take profit and ATR dynamic trailing stop.
5. Introduce the intraday breakout callback strategy and enter the market after the trend is confirmed. You can consider the 5-minute or 15-minute chart.
6. Add a volatility-based position management module to dynamically adjust positions according to market fluctuations.
7. Try machine learning technology to automatically optimize parameters and realize the adaptability of the strategy.
## Summarize
Overall, this strategy is a very simple and direct trend following strategy. It uses moving average crossover to determine the direction of the trend, RSI to filter out false breakthroughs, ADX to determine the existence of the trend, and stop-profit and stop-loss to continuously track the trend and capture profits in the short term. The direction of strategy optimization is mainly to find better indicator combinations, achieve flexibility in trend judgment, and introduce dynamic position management. Through code logic analysis, this strategy has certain feasibility, but it requires further testing and optimization before it can be actually applied.
|| 

## Overview 

The strategy aims to catch short-term forex trends by using EMA crossover and RSI as trading signals, with ADX filter to enter trades, and trailing stop loss to lock in profits. The strategy can be applied to all currency pairs, but is mainly used on 1-hour charts of major pairs.

## Strategy Logic

The strategy is based on the following indicators and conditions to generate trading signals:

- 5-period fast EMA: blue line  
- 10-period slow EMA: red line
- 10-period RSI applied to median price (H+L)/2
- 14-period ADX

Entry signals:
- Long: when fast EMA crosses above slow EMA from below and RSI crosses above 50 from bottom
- Short: when fast EMA crosses below slow EMA from top and RSI crosses below 50 from top
- Only take signals when ADX > 25

Exit signals:  
- Use trailing stop loss, 150 pips trail distance and 400 pips take profit
- Close trade when new signal occurs
- Close all trades before end of week

The strategy combines EMA crossover, RSI overbought/oversold and ADX trend strength to create solid entry rules. It rides the trend after formation and uses trailing stop to maximize profits and control risk. Overall it aims to effectively catch short-term trends.

## Advantage Analysis

The strategy has the following advantages:

1. EMA crossover for trend direction. Upward cross suggests uptrend while downward cross downtrend. Can identify trend changes.

2. Adding RSI filters out some false breakout signals. Oversold/overbought zones indicate short-term pullbacks and avoid unnecessary entries in range markets.

3. ADX for ensuring true trend existence. Only consider trading signals when ADX > 25, guaranteeing a solid trend. 

4. Trailing stop loss and take profit let profits run while controlling risk. 150 pips trail distance and 400 pips profit target continuously ride the trend.

5. Closing all positions before week end avoids weekend risks and enforces trading regularity.

## Risk Analysis

The strategy also has the following risks:

1. EMA crossover systems prone to false breakout signals, leading to losses. Fine tune EMA lengths or add other filters.

2. RSI only identifies overbought/oversold levels, not trend reversals. Could miss trends or reverse. Combine with other indicators.

3. ADX just judges trend existence, entry timing may be off. Add other rules or lower ADX threshold.

4. Fixed stop loss and take profit levels may not adapt to market changes. Test different parameters or manual intervention. 

5. Forced weekly close could miss good trend opportunities. Consider daily close or conditional exits.

## Optimization Directions 

The strategy can be optimized in the following aspects:

1. Test different EMA combinations to find optimal lengths. Consider slope for added trend strength.

2. Try different RSI parameters or combine with KDJ for better overbought/oversold judgment.

3. Optimize ADX parameters for more suitable filtering and higher entry quality.

4. Test combination of fixed stops and ATR-based dynamic trailing.

5. Add intraday breakout pullback entries after trend confirmation, such as lower timeframes. 

6. Introduce volatility-based position sizing for dynamic adjustment based on market volatility.

7. Explore machine learning techniques to auto-optimize parameters for adaptability.

## Summary

In summary this is a simple trend following strategy, identifying trend direction with EMA crossover, filtering with RSI, requiring trend with ADX, and trailing stop for profit. Optimization mainly involves finding better indicator combos for flexibility, and adding dynamic position sizing. The logic has merit but still requires further testing and optimization for practical application.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|5|Fast EMA Length|
|v_input_2|10|Slow EMA Length|
|v_input_3|10|Slow EMA Length|
|v_input_4|16|Weekly Session End (Hour)|
|v_input_5|false|Weekly Session End (Minute)|
|v_input_6|400|Profit Target (Pips/Points)|
|v_input_7|150|Trailing Stop Distance (Pips/Points)|
|v_input_8|true|User ADX Filter|
|v_input_9|25|Minimum ADX Level|
|v_input_10|14|ADX Smoothing|
|v_input_11|14|DI Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-21 00:00:00
end: 2023-09-27 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Hucklekiwi Pip - HLHB Trend-Catcher System", shorttitle="HLHB TCS", overlay=true,
  default_qty_type=strategy.percent_of_equity, default_qty_value=100)

// -----------------------------------------------------------------------------
// HLHB Trend-Catcher System as described on BabyPips.com
//
// Strategy Author: Hucklekiwi Pip 
// Coded By: Backtest Rookies
// -----------------------------------------------------------------------------
//
// Refs:
//   - Original System: https://www.babypips.com/trading/forex-hlhb-system-explained
//   - Updated System: https://www.babypips.com/trading/forex-hlhb-system-20190311
//
//
// Description (From Hucklekiwi Pip)
// 
//   The HLHB System simply aims to catch short-term forex trends.
//   It is patterned after the Amazing Crossover System that Robopip once backtested.
//   In fact, it was one of his highest-scoring mechanical systems in 2014! 
//   The system can be applied to any pair, but since I’m into major pairs, 
//   I’m applying it to the 1-hour charts of EUR/USD and GBP/USD.
// -----------------------------------------------------------------------------
// STRATEGY REQUIREMENTS
// -----------------------------------------------------------------------------
//
// Setup
// -----
//  - EUR/USD 1-hour chart
//  - GBP/USD 1-hour chart
//  - 5 EMA: blue line
//  - 10 EMA: red line
//  - RSI (10) applied to the median price (HL/2)
//  - ADX (14)
//
// Entry
// -----
//  - BUY when the 5 EMA crosses above the 10 EMA from underneath and the RSI 
//    crosses above the 50.0 mark from the bottom.
//  - SELL when the 5 EMA crosses below the 10 EMA from the top and the RSI 
//    crosses below the 50.0 mark from the top.
//  - Make sure that the RSI did cross 50.0 from the top or bottom and not just 
//    ranging tightly around the level.
//  - ADX > 25 for Buy and Sells
//
// Exit
// ----
//  - Use a 50-pip trailing stop and a 200-pip profit target. This increases the 
//    chances of the system riding longer trends.
//  - Close the trade when a new signal materializes.
//  - Close all trades by the end of the week.
// 
// -----------------------------------------------------------------------------

// Strategy Varaibles
// -------------------
ema_fast_len = input(5, title='Fast EMA Length')
ema_slow_len = input(10 , title='Slow EMA Length')
rsi_len = input(10, title='Slow EMA Length')
session_end_hour = input(16, minval=0, maxval=23, title='Weekly Session End (Hour)')
session_end_minute = input(0, minval=0, maxval=59, title='Weekly Session End (Minute)')
// Targets taken from the update post which states 150 & 400 instead of 50 and 200.
profit_target = input(400, title='Profit Target (Pips/Points)')
trailing_stop_dist = input(150, title='Trailing Stop Distance (Pips/Points)')
adx_filt = input(true, title='User ADX Filter')
adx_min = input(25, minval=0, title='Minimum ADX Level')
adx_len = input(14, title="ADX Smoothing")
di_len = input(14, title="DI Length")

// Setup the Indicators
ema_fast = ema(close, ema_fast_len)
ema_slow = ema(close, ema_slow_len)
rsi_ind = rsi(close, rsi_len)

// ADX
adx_dirmov(len) =>
	up = change(high)
	down = -change(low)
	plusDM = na(up) ? na : (up > down and up > 0 ? up : 0)
    minusDM = na(down) ? na : (down > up and down > 0 ? down : 0)
	truerange = rma(tr, len)
	plus = fixnan(100 * rma(plusDM, len) / truerange)
	minus = fixnan(100 * rma(minusDM, len) / truerange)
	[plus, minus]

adx_adx(dilen, adxlen) =>
	[plus, minus] = adx_dirmov(dilen)
	sum = plus + minus
	adx = 100 * rma(abs(plus - minus) / (sum == 0 ? 1 : sum), adxlen)
	[adx, plus, minus]

[adx_sig, adx_plus, adx_minus] = adx_adx(di_len, adx_len)


// Strategy Logic
ema_long_cross = crossover(ema_fast, ema_slow)
ema_short_cross = crossunder(ema_fast, ema_slow)
rsi_long_cross = crossover(rsi_ind, 50)
rsi_short_cross = crossunder(rsi_ind, 50)
adx_check = adx_filt ? adx_sig >= adx_min : true

longCondition = ema_long_cross and rsi_long_cross and adx_check
if (longCondition)
    strategy.entry("Long", strategy.long)

shortCondition = ema_short_cross and rsi_short_cross and adx_check
if (shortCondition)
    strategy.entry("Short", strategy.short)

strategy.exit("SL/TP", "Long", profit=profit_target,  loss=trailing_stop_dist, trail_points=trailing_stop_dist)  
strategy.exit("SL/TP", "Short", profit=profit_target, loss=trailing_stop_dist, trail_points=trailing_stop_dist)  

// Friday = 6
// If we miss the hour for some reason (due to strange timeframe), then close immediately
// Else if we are on the closing hour, then check to see if we are on or passed the close minute
close_time = dayofweek == 6 ? 
  hour[0] > session_end_hour ? true :
  hour[0] == session_end_hour ?
      minute[0] >= session_end_minute :
  false : false

strategy.close_all(when=close_time)

// Plotting
plot(ema_fast, color=blue, title="Fast EMA")
plot(ema_slow, color=red, title="Slow EMA")

plotshape(rsi_long_cross, style=shape.triangleup, size=size.tiny, location=location.belowbar, color=green, title='RSI Long Cross Marker')
plotshape(rsi_short_cross, style=shape.triangledown, size=size.tiny, location=location.abovebar, color=red, title='RSI Short Cross Marker')

// ADX Filter Highlight
bgcolor(adx_filt and adx_check ? orange : na, transp=90)
```

> Detail

https://www.fmz.com/strategy/428067

> Last Modified

2023-09-28 11:44:04
