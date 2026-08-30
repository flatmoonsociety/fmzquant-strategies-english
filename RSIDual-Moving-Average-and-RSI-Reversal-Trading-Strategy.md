
> Name

Dual-Moving-Average-and-RSI-Reversal-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1f6e3873916ac74abeb.png)

[trans]

## Overview
This strategy combines double moving averages and the relative strength indicator RSI to look for short-term reversal opportunities in strong trends for trading. When the trend direction is clear, use RSI to identify overbought and oversold conditions and wait for the price to reverse and enter the market. This strategy is suitable for markets with obvious trends and can capture part of the reversal movement without going against the trend.
## Strategy Principle
1. Calculate the 30-day simple moving average SMA and the 200-day exponential moving average EMA to determine the general trend direction.
- SMA>EMA, indicates an upward trend
   - SMA<EMA, it is a downward trend
2. Calculate the 30-day RSI and determine whether it is overbought or oversold.
- RSI<=53 is oversold
   - RSI>=60 is overbought
3. Entry rules:
- Go long when in an uptrend (SMA>EMA) and RSI<=53
   - Go short when in a downtrend (SMA<EMA) and RSI>=60
4. Appearance rules:
- Stop loss or take profit for long orders
   - Stop loss or take profit for short orders
## Strategic advantage analysis
1. Follow the general trend and avoid counter-trend operations
2. RSI parameter settings are relatively conservative, which can reduce false signals
3. Combined with double moving average filtering, entry timing is more accurate
4. Risks are controllable and retracement is not big.
## Risk Analysis
1. A more obvious trending market is required, and the effect of volatile market conditions is not good
2. RSI parameter settings are conservative and may miss some opportunities.
3. The stop loss position needs to be set appropriately to avoid exiting too aggressively.
## Strategy optimization direction
1. Optimize RSI parameters, appropriately reduce parameters to find more entry opportunities
2. Test different moving average combinations
3. Set trend filtering and only operate when the trend is obvious enough
4. Optimize stop loss strategy and strictly control single stop loss
## Summarize
The overall risk of this strategy is controllable and is suitable for medium and long-term position traders. The strategy trades according to the direction of the general trend, using conservative RSI parameters and strict moving average filtering, which can effectively avoid false breakthroughs and thereby increase the winning rate. At the same time, there is also some potential room for improvement. If the parameters are adjusted appropriately, more opportunities can be obtained. You need to pay attention to risk control and maintain a long-term trading mentality.
||


## Overview

This strategy combines dual moving averages and the relative strength index (RSI) to identify short-term reversal opportunities during strong trends. It aims to enter trades against the momentum when the trend direction is clear, by using RSI to detect overbought and oversold conditions and waiting for the price to reverse. The strategy is suitable for markets with obvious trends, capturing partial reversals without trading against the overall trend.

## Strategy Logic

1. Calculate the 30-day simple moving average (SMA) and 200-day exponential moving average (EMA) to determine the overall trend direction.

   - SMA>EMA suggests an upward trend  
   - SMA<EMA suggests a downward trend

2. Calculate the 30-day RSI to identify overbought and oversold conditions. 

   - RSI<=53 is considered oversold
   - RSI>=60 is considered overbought

3. Entry rules:

   - Go long when in an upward trend (SMA>EMA) and RSI<=53
   - Go short when in a downward trend (SMA<EMA) and RSI>=60

4. Exit rules:  

   - Close long position for stop loss or take profit
   - Close short position for stop loss or take profit

## Advantage Analysis  

1. Follows the major trend, avoids trading against the trend

2. Conservative RSI settings avoid false signals 

3. Dual moving average filter improves entry timing accuracy   

4. Controllable risk, small drawdowns

## Risk Analysis

1. Needs obvious trending markets, less effective in ranging markets

2. Conservative RSI settings may miss some opportunities

3. Stop loss placement needs to be reasonable to avoid premature exits

## Improvement Directions

1. Optimize RSI parameters to find more entry opportunities 

2. Test different moving average combinations

3. Add trend filter, only trade when trend is strong enough

4. Optimize stop loss strategy to control loss on single trades

## Conclusion

The strategy has controllable risks overall, suitable for medium-long term position traders. It trades with the major trend direction, uses conservative RSI settings and strict moving average filters to avoid false breakouts, improving win rate. There is also room for potential improvements with parameter tuning to gain more opportunities. Risk control is essential to maintain a long-term trading mentality.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-17 00:00:00
end: 2023-10-17 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
//Based on Larry Connors RSI-2 Strategy - Lower RSI
strategy(title="_CM_RSI_2_Strat_Low", shorttitle="_CM_RSI_2_Strategy_Lower", overlay=false)
src = close, 

//RSI CODE
up = rma(max(change(src), 0), 30)
down = rma(-min(change(src), 0), 30)
rsi = down == 0 ? 100 : up == 0 ? 0 : 100 - (100 / (1 + up / down))
//Criteria for Moving Avg rules
ma50= vwma(close,30)
ma200= vwma(close,200)

//Rule for RSI Color
col = ma50 > ma200 and rsi <=53?lime: ma50 < ma200  and rsi >= 60?red : silver
long = ma50 > ma200 and rsi <= 53
short = ma50 < ma200  and rsi >= 60
//plot(rsi, title="RSI", style=line, linewidth=1,color=col)
//plot(100, title="Upper Line 100",style=line, linewidth=3, color=aqua)
//plot(0, title="Lower Line 0",style=line, linewidth=3, color=aqua)

//band1 = plot(60, title="Upper Line 60",style=line, linewidth=1, color=aqua)
//band0 = plot(44, title="Lower Line 40",style=line, linewidth=1, color=aqua)
//fill(band1, band0, color=silver, transp=90)
strategy.entry ("buy", strategy.long, when=long)
strategy.entry ("sell", strategy.short, when=short)
plot(long,"long",color=green,linewidth=1)
plot(short,"short",color=red,linewidth=1)
```

> Detail

https://www.fmz.com/strategy/429562

> Last Modified

2023-10-18 11:08:35
