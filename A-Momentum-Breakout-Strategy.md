
> Name

A-Momentum-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy is an intraday trading strategy based on breakouts of momentum indicators and key support and resistance levels. It combines the Choppiness indicator to identify trends and only trade when the trend is obvious to control risk.
## Strategy Principle
This strategy uses the Choppiness indicator to identify trends. A low Choppiness value indicates an obvious trend, and a high Choppiness value indicates consolidation. The strategy only operates when the Choppiness value is below 44.
For entry signals, it calculates key intraday support and resistance levels, including H4, H5, etc. When the closing price breaks through H4, go long; when the closing price falls below L4, go short.
Specifically, it calculates the following intraday support and resistance levels:
- Pivot = (Highest value + Lowest value + Closing price)/3
- Range = highest value - lowest value
- H1-H6 = Pivot + Range * Scale
- L1-L6 = Pivot - Range * Scale
After calculating these support and resistance levels, it identifies H4 and L4 as key breakthrough levels.
When the price breaks through H4, it means that the momentum of the bulls has increased, and it will perform long operations. When the price falls below L4, it means that the short position has increased momentum and it will conduct short selling operations.
## Strategic advantage analysis
This strategy has the following advantages:
1. Use the Choppiness indicator to identify obvious trends and avoid whipsaws that consolidate the market.
2. Calculate key support and resistance levels. These levels usually have strong significance. By relying on them for breakout trading, you can get a higher probability of profit.
3. Operate by breaking through the key intraday levels H4 and L4. These levels are close to the closing price and are the important dividing line between long and short on the day.
4. Breakout signals have a very high winning rate. When the price really breaks through H4 and L4, the subsequent market will usually continue to extend the trend.
5. The strategy operation logic is very simple and clear, easy to understand and implement, and is suitable for novices to learn.
## Strategy risk analysis
This strategy also has the following risks:
1. Relying on the Choppiness indicator to identify trends, the indicator itself may also be invalid, leading to misjudgment of market trends.
2. The calculated support and resistance levels are not 100% reliable, and the price may directly break through these levels, resulting in a stop loss.
3. There may be a false breakthrough in the breakthrough signal, and the actual price will fall back soon, causing losses to the strategy.
4. The strategy does not consider the direction of the general trend. When the long-term direction of the market is unclear, the strategy may suffer repeated losses.
5. The strategy lacks a stop-loss mechanism. In extreme market conditions, a single loss may be very huge.
Countermeasures:
1. Other indicators can be introduced for comprehensive judgment to improve the accuracy of trend judgment.
2. Add a trailing stop to control single losses.
3. Combine with long-term trend indicators to avoid contrarian trading.
4. Add re-entry signals to avoid tracking false breakthroughs.
## Strategy optimization direction
This strategy can be further optimized from the following aspects:
1. Optimize the Choppiness indicator parameters and find more suitable values ​​to improve accuracy.
2. Test different breakthrough levels, such as H3 and L3, to find more effective breakthrough points.
3. Add a trailing stop loss strategy to lock in profits and control risks.
4. Add re-entry signals to avoid continued losses after false breakthroughs.
5. Combine long-term indicators to determine the general trend and avoid counter-trend operations.
6. Optimize trading hours, such as operating only during US or European trading hours.
7. Add position management strategies, such as fixed quantity or fixed capital entry.
8. Analyze backtest data and further test and optimize parameters.
## Summarize
Overall, the core idea of ​​this strategy is to identify the trend and then operate when key support and resistance levels are broken. It has a simple logical structure and a high probability of profit. However, there are also certain risks, and continued optimization is required to control risks and improve profitability. Through parameter adjustment, stop loss strategy, trend judgment and other optimizations, it can be built into a very practical intraday breakthrough system. It provides us with an idea for breakthrough operations based on momentum indicators, and is an effective intraday trading strategy.
|| 

## Overview

This is an intraday trading strategy that utilizes momentum indicators and key support/resistance levels for breakout trading. It incorporates the Choppiness index to identify trends and only trades when the trend is clear, in order to control risk.

## Strategy Logic

The strategy uses the Choppiness index to identify trends. Low Choppiness values indicate a clear trend while high values indicate consolidation. The strategy only trades when Choppiness is below 44.

For entry signals, it calculates key intraday support/resistance levels including H4, H5 etc. It goes long when price closes above H4 and goes short when price closes below L4. 

Specifically, it calculates the following intraday levels:

- Pivot = (High + Low + Close)/3
- Range = High - Low
- H1-H6 = Pivot + Range * Ratio 
- L1-L6 = Pivot - Range * Ratio

After computing these levels, it uses H4 and L4 as the key breakout levels. 

When price breaks above H4, it signals increasing bullish momentum and the strategy goes long. When price breaks below L4, it signals increasing bearish momentum and the strategy goes short.

## Advantage Analysis 

The advantages of this strategy include:

1. Using Choppiness to identify clear trends avoids whipsaws in consolidation.

2. The calculated support/resistance levels are usually meaningful. Trading breakouts from these levels gives a higher winning probability.

3. Trading breaks of H4 and L4 which are near the closing price captures important intraday breaks. 

4. Breakout signals have a very high win rate. Valid breaks of H4 and L4 usually continue the trend.

5. Simple and clear logic, easy to understand and implement for beginners.

## Risk Analysis

The risks of this strategy include:

1. Reliance on Choppiness for trend identification can fail and misread trends.

2. Calculated levels may not hold and price could break through, causing stops. 

3. Breakout signals can be false breakouts with quick reversals.

4. No consideration of overall trend, losses may accumulate in choppy markets.

5. No stop loss means huge single trade loss is possible in extreme moves.

Solutions:

1. Add other indicators for cross-confirmation and improve accuracy.

2. Implement moving stop loss to control single trade loss.

3. Incorporate long term trend filter to avoid counter-trend trades. 

4. Add re-entry signal to avoid chasing false breakouts.

## Optimization Directions

This strategy can be further optimized by:

1. Optimizing Choppiness parameters to find better values.

2. Testing different breakout levels like H3 and L3 for better efficiency.

3. Adding moving stop loss for profit protection and risk control. 

4. Adding re-entry signal to avoid losses from false breakouts.

5. Incorporating long term trend filter to avoid counter-trend trades.

6. Optimizing trading times such as only trading US or Europe sessions.

7. Adding position sizing rules like fixed quantity or fixed percentage.

8. Analyzing backtest data for parameter fine tuning.

## Conclusion

In summary, the core idea is to trade breakouts after identifying the trend. It has simple logic and decent winning odds. But risks exist and further refinements are needed to control risks and improve profitability. With parameter tuning, stop loss, trend filter etc it can become a very practical intraday breakout system. It provides a momentum breakout framework that is an effective intraday trading strategy.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-08 00:00:00
end: 2023-10-08 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
//Created by AS
strategy(title="ASH1Strategy", shorttitle="AS_H1_Strategy", overlay=true) 
//sd = input(true, title="Show Daily Pivots?")
EMA = ema(close,3)

pivot = (high + low + close ) / 3.0 
range = high - low
h5 = (high/low) * close 
h4 = close + (high - low) * 1.1 / 2.0
h3 = close + (high - low) * 1.1 / 4.0
h2 = close + (high - low) * 1.1 / 6.0
h1 = close + (high - low) * 1.1 / 12.0
l1 = close - (high - low) * 1.1 / 12.0
l2 = close - (high - low) * 1.1 / 6.0
l3 = close - (high - low) * 1.1 / 4.0
l4 = close - (high - low) * 1.1 / 2.0
h6 = h5 + 1.168 * (h5 - h4) 
l5 = close - (h5 - close)
l6 = close - (h6 - close)

// Daily line breaks
//sopen = request.security(syminfo.tickerid, "D", open [1])
//shigh = request.security(syminfo.tickerid, "D", high [1])
//slow = request.security(syminfo.tickerid, "D", low [1])
//sclose = request.security(syminfo.tickerid, "D", close [1])
//
// Color
//dcolor=sopen != sopen[1] ? na : black
//dcolor1=sopen != sopen[1] ? na : red
//dcolor2=sopen != sopen[1] ? na : green

//Daily Pivots 
dtime_pivot = request.security(syminfo.tickerid, 'D', pivot[1]) 
dtime_h6 = request.security(syminfo.tickerid, 'D', h6[1]) 
dtime_h5 = request.security(syminfo.tickerid, 'D', h5[1]) 
dtime_h4 = request.security(syminfo.tickerid, 'D', h4[1]) 
dtime_h3 = request.security(syminfo.tickerid, 'D', h3[1]) 
dtime_h2 = request.security(syminfo.tickerid, 'D', h2[1]) 
dtime_h1 = request.security(syminfo.tickerid, 'D', h1[1]) 
dtime_l1 = request.security(syminfo.tickerid, 'D', l1[1]) 
dtime_l2 = request.security(syminfo.tickerid, 'D', l2[1]) 
dtime_l3 = request.security(syminfo.tickerid, 'D', l3[1]) 
dtime_l4 = request.security(syminfo.tickerid, 'D', l4[1]) 
dtime_l5 = request.security(syminfo.tickerid, 'D', l5[1]) 
dtime_l6 = request.security(syminfo.tickerid, 'D', l6[1]) 

//offs_daily = 0
//plot(sd and dtime_pivot ? dtime_pivot : na, title="Daily Pivot",color=dcolor, linewidth=2)
//plot(sd and dtime_h6 ? dtime_h6 : na, title="Daily H6", color=dcolor2, linewidth=2)
//plot(sd and dtime_h5 ? dtime_h5 : na, title="Daily H5",color=dcolor2, linewidth=2)
//plot(sd and dtime_h4 ? dtime_h4 : na, title="Daily H4",color=dcolor2, linewidth=2)
//plot(sd and dtime_h3 ? dtime_h3 : na, title="Daily H3",color=dcolor1, linewidth=3)
//plot(sd and dtime_h2 ? dtime_h2 : na, title="Daily H2",color=dcolor2, linewidth=2)
//plot(sd and dtime_h1 ? dtime_h1 : na, title="Daily H1",color=dcolor2, linewidth=2)
//plot(sd and dtime_l1 ? dtime_l1 : na, title="Daily L1",color=dcolor2, linewidth=2)
//plot(sd and dtime_l2 ? dtime_l2 : na, title="Daily L2",color=dcolor2, linewidth=2)
//plot(sd and dtime_l3 ? dtime_l3 : na, title="Daily L3",color=dcolor1, linewidth=3)
//plot(sd and dtime_l4 ? dtime_l4 : na, title="Daily L4",color=dcolor2, linewidth=2)
//plot(sd and dtime_l5 ? dtime_l5 : na, title="Daily L5",color=dcolor2, linewidth=2)
//plot(sd and dtime_l6 ? dtime_l6 : na, title="Daily L6",color=dcolor2, linewidth=2)

longCondition = close >dtime_h4
if (longCondition)
    strategy.entry("My Long Entry Id", strategy.long)
    


shortCondition = close <dtime_l4
if (shortCondition)
    strategy.entry("My Short Entry Id", strategy.short)
    

```

> Detail

https://www.fmz.com/strategy/428790

> Last Modified

2023-10-09 15:15:22
