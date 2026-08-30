
> Name

Trend-Tracking-EMA-Breakout-Strategy Trend-Tracking-EMA-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/6fb5b021ec727dce7cf4464edf6bcc09a27642d50224cfb9014c0c720bbbe132.png)
[trans]

## Overview
This strategy is a trend-following breakout strategy based on the exponential moving average (EMA). It determines the trend direction on the monthly, weekly and daily time frames, and performs specific entry and exit operations on the daily time frame.
## Strategy Principle
### Trend Judgment
1. On the monthly line, if the price is higher than the 8-day EMA, and the 8-day EMA is higher than the 21-day EMA, it is judged to be a bullish trend;
2. On the weekly line, if the price is higher than the 8-day EMA, and the 8-day EMA is higher than the 21-day EMA, it is judged to be a bullish trend;
3. On the daily line, if the price is higher than the 8-day EMA, and the 8-day EMA is higher than the 21-day EMA, it is judged to be a bullish trend;
### Entry signal
1. There was a downward correction on the daily line, with the low touching yesterday’s 8-day EMA;
2. The callback forms the Ring Low pattern of Lower High and Lower Low;
3. The closing price is higher than the previous day's highest price, which constitutes a trend reversal signal;
### Exit signal
Set stop-profit and stop-loss standards to reach exit.
## Advantage Analysis
1. Judge trends in three time frames and improve judgment accuracy;
2. The callback low hits the EMA to form support, increasing the certainty of entry;
3. Follow the trend and have great profit potential;
## Risk Analysis
1. Inconsistent judgments among the three time frames may trigger false signals;
2. Excessive correction will render the strategy ineffective;
3. A blackout party in the market may sweep the stop loss;
## Optimization direction
1. Add MACD, RSI and other indicators to assist judgment;
2. Optimize EMA parameter settings;
3. Adjust the stop-profit and stop-loss ranges based on volatility indicators;
## Summary
As a whole, this strategy is a trend following strategy and has very good profit potential when the trend is correctly judged. Care needs to be taken to prevent incorrect trend judgment and excessive callbacks from generating false signals. At the same time, optimizing the stop-profit and stop-loss settings is also the key to further improving the strategic advantage.
||


## Overview
This is a trend tracking breakout strategy based on Exponential Moving Average (EMA). It judges the trend direction on the monthly, weekly and daily time frames, and executes specific entry and exit actions on the daily chart.  

## Strategy Logic   
### Trend Judgment
1. On the monthly chart, price is above 8-day EMA and 8-day EMA is above 21-day EMA, indicating an uptrend;
2. On the weekly chart, price is above 8-day EMA and 8-day EMA is above 21-day EMA, indicating an uptrend; 
3. On the daily chart, price is above 8-day EMA and 8-day EMA is above 21-day EMA, indicating an uptrend;

### Entry Signal  
1. A pullback is seen on the daily chart with the low point touching yesterday's 8-day EMA;
2. The pullback forms a Ring Low pattern with lower high and lower low;  
3. The closing price is higher than the previous day's high, forming a trend reversal signal.  

### Exit Signal   
Set profit taking and stop loss standards for exiting.  

## Advantage Analysis  
1. Judging the trend on three time frames improves accuracy; 
2. Pullback to EMA forms support and increases entry certainty;   
3. Tracking trend runs has high profit potential;   

## Risk Analysis
1. Inconsistent judgments across time frames may cause false signals;
2. Excessive pullback magnitude may invalidate the strategy; 
3. Stop loss sweep may occur during flash crashes.   

## Optimization Directions   
1. Add MACD, RSI for supplementary judgment;  
2. Optimize EMA parameter settings; 
3. Adjust profit taking and stop loss range based on volatility.  

## Summary   
The strategy has very good profit potential when the trend is correctly judged. Need to watch out for inaccurate trend judgment and excessive pullback causing false signals. Meanwhile, optimizing profit taking and stop loss settings is key to further improving the edge.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_float_1|10|Profit Target %|
|v_input_float_2|10|Stop Loss %|
|v_input_bool_1|false|Relaxed Entry Rules|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-11 00:00:00
end: 2024-01-11 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © the_daily_trader

//@version=5
// ---------------------        Start of Code        ---------------------
strategy("Swing Trades Validator", overlay=true, margin_long=100, pyramiding = 0)

// Indicator Display Checks
TakeProfitPercent       = input.float(title="Profit Target %", defval=10, minval=1, step=0.05)
StopLossPercent         = input.float(title="Stop Loss %", defval=10, minval=1, step=0.05)
pullbackchoice          = input.bool(false, "Relaxed Entry Rules")

// EMAs
emaH            = ta.ema(close, 8)
emaHyest        = ta.ema(close[1], 8)
emaHyest1       = ta.ema(close[2], 8)
emaHyest2       = ta.ema(close[3], 8)
emaL            = ta.ema(close, 21)
emaLyest        = ta.ema(close[1], 21)
emaLyest1       = ta.ema(close[2], 21)
emaLyest2       = ta.ema(close[3], 21)
emaf            = ta.ema(close, 50)
emath           = ta.ema(close, 200)
emathhigh       = ta.ema(high, 200)
emathlow        = ta.ema(low, 200)
emaslowmonthly  = request.security(syminfo.tickerid, "M", emaL) // Monthly 21ema
emafastmonthly  = request.security(syminfo.tickerid, "M", emaH) // Monthly 8ema
emaslowweekly   = request.security(syminfo.tickerid, "W", emaL) // Weekly 21ema
emafastweekly   = request.security(syminfo.tickerid, "W", emaH) // Weekly 8ema
emaslowdaily    = request.security(syminfo.tickerid, "D", emaL) // Daily 21ema
emafastdaily    = request.security(syminfo.tickerid, "D", emaH) // Daily 8ema
emafdaily       = request.security(syminfo.tickerid, "D", emaf) // Daily 50ema
emathdaily      = request.security(syminfo.tickerid, "D", emath) // Daily ema
emathdailyhigh  = request.security(syminfo.tickerid, "D", emathhigh) // Daily ema High
emathdailylow   = request.security(syminfo.tickerid, "D", emathlow) // Daily ema Low
ema21yest       = request.security(syminfo.tickerid, "D", emaLyest) // Daily 21ema 1 day ago
ema21yest1      = request.security(syminfo.tickerid, "D", emaLyest1) // Daily 21ema 2 days ago
ema21yest2      = request.security(syminfo.tickerid, "D", emaLyest2) // Daily 21ema 3 days ago
ema8yest        = request.security(syminfo.tickerid, "D", emaHyest) // Daily 8ema 1 day ago
ema8yest1       = request.security(syminfo.tickerid, "D", emaHyest1) // Daily 8ema 2 days ago
ema8yest2       = request.security(syminfo.tickerid, "D", emaHyest2) // Daily 8ema 3 days ago


// Prices
monthopen       = request.security(syminfo.tickerid, 'M', open, barmerge.gaps_off, barmerge.lookahead_on)
monthclose      = request.security(syminfo.tickerid, 'M', close, barmerge.gaps_off, barmerge.lookahead_on)
weekopen        = request.security(syminfo.tickerid, 'W', open, barmerge.gaps_off, barmerge.lookahead_on)
weekclose       = request.security(syminfo.tickerid, 'W', close, barmerge.gaps_off, barmerge.lookahead_on)
dayopen         = request.security(syminfo.tickerid, 'D', open, barmerge.gaps_off, barmerge.lookahead_on)
dayclose        = request.security(syminfo.tickerid, 'D', close, barmerge.gaps_off, barmerge.lookahead_on)
threedayhigh    = request.security(syminfo.tickerid, 'D', high[3], barmerge.gaps_off, barmerge.lookahead_on)
twodayhigh      = request.security(syminfo.tickerid, 'D', high[2], barmerge.gaps_off, barmerge.lookahead_on)
yesthigh        = request.security(syminfo.tickerid, 'D', high[1], barmerge.gaps_off, barmerge.lookahead_on)
yestlow         = request.security(syminfo.tickerid, 'D', low[1], barmerge.gaps_off, barmerge.lookahead_on)

// Conditions 
monthlybullish          = emafastmonthly > emaslowmonthly
monthlybullishprice     = close > emafastmonthly
monthlybullishcandle    = monthclose > monthopen
weeklybullish           = emafastweekly > emaslowweekly
weeklybullishprice      = close > emafastweekly
weeklybullishcandle     = weekclose > weekopen
dailybullish1           = emafdaily > emathdaily
dailybullish2           = emafastdaily > emaslowdaily
dailybullishprice       = close > emafastdaily
dailybullishcandle      = dayclose > dayopen
ringlow                 = yestlow <= ema8yest
aggropullback           = twodayhigh < threedayhigh
pullback                = (pullbackchoice ? aggropullback : 0)
pullbackfailure         = dayclose > yesthigh and yesthigh < twodayhigh or pullback
emasetup                = ema8yest > ema21yest and ema8yest1 > ema21yest1 and ema8yest2 > ema21yest2

// Target Profit and Stop Loss Inputs
// Input parameters can be found at the beginning of the code
ProfitTarget        = (close * (TakeProfitPercent / 100)) / syminfo.mintick
StopLoss            = (close * (StopLossPercent / 100)) / syminfo.mintick

longCondition = monthlybullish and monthlybullishprice and weeklybullish and weeklybullishprice and dailybullish1 and dailybullish2 and dailybullishprice and monthlybullishcandle and weeklybullishcandle and dailybullishcandle and ringlow and pullbackfailure and emasetup

if (longCondition)
    strategy.entry("Long", strategy.long)
    strategy.exit ("Exit", "Long", profit = ProfitTarget, loss = StopLoss)
    // strategy.close("Long", qty_percent = 100)


// -----------xxxxxxxxxxx-------------    End of Code     -----------xxxxxxxxxxx---------------
```

> Detail

https://www.fmz.com/strategy/438495

> Last Modified

2024-01-12 14:23:11
