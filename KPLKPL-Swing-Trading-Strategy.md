
> Name

KPL swing tracking strategy KPL-Swing-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
This strategy trades based on the KPL volatility indicator and is a simple trend following mechanical trading system. Go long when the price closes above the 20-day high, and go short when the price closes below the 20-day low, to capture mid- to long-term price fluctuations.
### Strategy Principles
1. Calculate the highest and lowest prices within 20 days
2. When the closing price breaks through the 20-day high, enter long
3. Enter short when the closing price falls below the 20-day low
4. Calculate stop loss level and set stop loss order
Specifically, the strategy first calculates the highest and lowest prices in the past 20 days to construct a shock range. When the closing price breaks through the 20-day high from below, enter the market long; when the closing price falls below the 20-day low from above, enter the market short. At the same time, calculate the stop loss level in the direction of the breakthrough, and set a stop loss order immediately after entering the market to control a single loss.
### Advantage Analysis
1. The transaction logic is simple and intuitive, easy to master
2. Have certain trend tracking capabilities
3. Setting stop-loss orders can effectively control risks
4. No need to predict the target price and avoid subjecitve guessing
5. Emotional trading is less likely to be affected by the outside world
### Risk Analysis
1. There is a certain degree of lagging transaction risk
2. Unable to effectively grasp key points in the trend process
3. May be caught due to shock
4. Potential profits limited by 20-day breakout range
5. Difficult to grasp the best time to hold positions
Risks can be managed by adjusting the observation breakthrough cycle, introducing trend judgment, and optimizing stop-loss strategies.
### Optimization direction
1. Test different observation period parameters
2. Add MACD and other indicators to judge the trading strength
3. Optimize stop loss strategy and implement trailing stop loss
4. Evaluate the impact of different holding times on returns
5. Study the parameter preferences of different varieties
6. Consider adding re-entry and re-entry rules
### Summarize
This strategy is based on the KPL volatility indicator for trend tracking. The advantage is that it is simple and easy to operate, and there is a stop loss; the disadvantage is that there is lag and the potential profit is limited. The disadvantages can be improved while maintaining the advantages through parameter optimization, strategy combination, etc. This strategy helps traders master mechanical indicator-based trading methods.
|| 

### Overview

This strategy trades based on the KPL Swing indicator, which is a simple trend following mechanical system. It goes long on close above 20-day high, and goes short on close below 20-day low to capture medium-long term price swings.

### Strategy Logic

1. Calculate 20-day highest high and lowest low
2. Go long when close breaks out above 20-day high 
3. Go short when close breaks down below 20-day low
4. Calculate stop loss levels and set stop orders

Specifically, it first calculates 20-day range using highest high and lowest low. When close breaks out upward from 20-day high, go long. When close breaks down from 20-day low, go short. Stop loss levels are calculated after entry for both directions to limit losses.

### Advantage Analysis

1. Simple and intuitive logic, easy to grasp
2. Has some trend following capacity 
3. Stop loss effectively controls risk
4. No subjective price target guessing
5. Less emotional trading, minimal external influence

### Risk Analysis

1. Lagging entry risks exist
2. Fails to identify key levels in trends
3. Whipsaws may cause being trapped
4. Profit potential limited by 20-day breakout range
5. Hard to determine optimal holding period

Risks can be managed via adjusting lookback period, adding trend filter, optimizing stop loss etc.

### Optimization Directions

1. Test different lookback periods
2. Add MACD etc. to gauge momentum  
3. Optimize stop loss for trailing stop loss
4. Evaluate holding period impact on profitability
5. Study parameter preference across products
6. Consider adding re-entry and pyramiding rules

### Summary

This strategy trades trend swings based on KPL Swing indicator. Pros are simple operation and built-in stop loss; Cons are lags and profit constraints. Cons can be improved via parameter optimization, strategy combination while retaining pros. It helps traders master mechanical indicator-based trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|no|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-20 00:00:00
end: 2023-09-20 00:00:00
period: 2d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © ceyhun

//@version=4
strategy("KPL Swing Strategy", overlay=true)

no = input(20)
res = highest(high, no)
sup = lowest(low, no)
avd = iff(close > res[1], 1, iff(close < sup[1], -1, 0))
avn = valuewhen(avd != 0, avd, 1)
tsl = iff(avn == 1, sup, res)
sl = iff(close > tsl, highest(lowest(low, no / 2), no / 2), lowest(highest(high, no / 2), no / 2))

plot(tsl, color=#0000FF,title="KPL Swing")
plot(sl,  color=color.white,title="Stoploss")

bgcolor(abs(close - tsl[1]) > close ? color.white : close < tsl ? color.red : color.green, 90, offset=0)

if crossover(close, tsl)
    strategy.entry("Long", strategy.long, comment="Long")

if crossunder(close,tsl)
    strategy.entry("Short", strategy.short, comment="Short")
    
    
    

```

> Detail

https://www.fmz.com/strategy/427453

> Last Modified

2023-09-21 11:09:04
