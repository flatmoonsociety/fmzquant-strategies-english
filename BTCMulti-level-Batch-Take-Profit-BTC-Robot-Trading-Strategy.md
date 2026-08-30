
> Name

Multi-level-Batch-Take-Profit-BTC-Robot-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/13a561d3edc5c4ee6bc.png)

[trans]

## Overview
This strategy is a multi-level batch profit-taking BTC robot trading strategy. It searches for the lowest point to buy entry, and then sets multi-level profit-taking points to exit in batches. At the same time, set stop loss points for risk control. This strategy is suitable for bullish BTC scenarios.
## Strategy Principle
1. Look for entry opportunities: When the CC indicator crosses the 0 axis, a buy signal is generated, and a long order is purchased at this point.
2. Set the stop loss point: Set the stop loss percentage by inputting it, and convert it into a price for stop loss.
3. Set multi-level take-profit points: divided into 4 exit points, set the take-profit percentage of each exit point by inputting, and convert it into price to take profit in batches.
4. Risk control: Set the maximum position, and set the exit volume percentage of each exit point through input to diversify risks.
## Advantage Analysis
This strategy has the following advantages:
1. The entry signal is relatively reliable. Look for the lowest point to buy and avoid buying at the high point.
2. Multi-level take profit can lock in part of the profit while retaining part of the profit to continue running.
3. Set stop loss points for risk control, which can control losses within a certain range.
4. Exiting the market in batches can diversify risks and avoid all losses at once.
5. The retracement can be controlled to a certain extent.
## Risk Analysis
This strategy also has the following risks:
1. The CC indicator cannot determine the lowest point 100%, and buying opportunities may be missed.
2. Improper stop loss setting may cause unnecessary stop loss.
3. Improper batch entry setting may also cause loss of profits.
4. It will be more difficult to stop profits during volatile market conditions.
5. When the market reverses sharply, it may be difficult to stop losses.
## Optimization direction
It can be optimized from the following aspects:
1. Optimize entry signals and add more indicators or machine learning judgments to determine buying opportunities.
2. Optimize the stop loss strategy to make it more flexible and better able to respond to market conditions.
3. Optimize the exit strategy so that it can better adapt to shocks and trend markets.
4. Add strategies such as trailing stop to make the profit stop more flexible.
5. Test different varieties of parameter settings to find the best parameter combination.
## Summarize
Generally speaking, this strategy is a BTC trading strategy based on finding the lowest buying signal and setting multi-level take-profit and stop-loss. It has certain advantages, and there are also directions that can be optimized. Through further optimization, the strategy can be made better in terms of retracement control and profit taking. But overall, this strategy provides a feasible idea for BTC robot trading.
||

## Overview

This is a multi-level batch take profit BTC robot trading strategy. It enters long positions by finding the lowest point and sets multiple take profit points for batch exits. It also sets a stop loss point for risk control. This strategy is suitable when being bullish on BTC.

## Strategy Logic

1. Find entry signals: Generate buy signals when the CC indicator crosses below 0. Buy long positions at this point.

2. Set stop loss: Set stop loss percentage through input, convert to price level for stop loss.

3. Set multiple take profit points: 4 exit points, set take profit percentage for each point through input, convert to price levels. 

4. Risk control: Set maximum position size, set exit percentage for each exit point through input for risk dispersion.

## Advantage Analysis 

The advantages of this strategy are:

1. Reliable entry signal by buying at the lowest point, avoiding buying at highs.

2. Multi-level take profit locks in partial profits while keeping some profits running.

3. Stop loss controls risk and limits losses to a certain range. 

4. Batch exits disperses risks, avoiding full losses all at once.

5. Drawdown can be controlled to some extent.

## Risk Analysis

The risks of this strategy are:

1. CC indicator cannot fully ensure the lowest point, may miss buying opportunities.

2. Improper stop loss setting may cause unnecessary stop loss. 

3. Improper batch exits may also lead to loss of profits.

4. Take profit is more difficult in ranging markets.

5. It may be hard to stop loss in sharp reversals.

## Optimization Directions

Potential optimizations:

1. Optimize entry signals with more indicators or machine learning for better timing.

2. Optimize stop loss strategy to make it more elastic against market moves.

3. Optimize exits for better adaptation in ranging and trending markets.  

4. Add trailing stops for more flexible take profits.

5. Test different assets for best parameter sets.

## Conclusion

In summary, this is a BTC trading strategy based on buying at lowest points with multi-level take profits and stop loss. It has certain advantages and also areas that can be improved. Further optimizations on drawdown control and take profit could make the strategy perform better. Overall it provides a viable approach for BTC algorithmic trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0|Strategy Direction: long|short|all|
|v_input_2|W|higherTF|
|v_input_3|2|factor|
|v_input_4|21|length|
|v_input_5|15| stop loss|
|v_input_6|25| qty_percent1|
|v_input_7|25| qty_percent2|
|v_input_8|25| qty_percent3|
|v_input_9|3| Take profit1|
|v_input_10|5| Take profit2|
|v_input_11|7| Take profit3|
|v_input_12|10| Take profit4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-17 00:00:00
end: 2023-10-17 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
args: [["v_input_1",2]]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © RafaelZioni


// © theCrypster 2020

//@version=4
// strategy(title = "BTC bot", overlay = true, pyramiding=1,initial_capital = 10000, default_qty_type= strategy.percent_of_equity, default_qty_value = 100, calc_on_order_fills=false, slippage=0,commission_type=strategy.commission.percent,commission_value=0.075)
strat_dir_input = input(title="Strategy Direction", defval="long", options=["long", "short", "all"])
strat_dir_value = strat_dir_input == "long" ? strategy.direction.long : strat_dir_input == "short" ? strategy.direction.short : strategy.direction.all
strategy.risk.allow_entry_in(strat_dir_value)
//INPUTS
higherTF = input("W", type=input.resolution)
pc = security(syminfo.tickerid, higherTF, close[1], lookahead=true)
ph = security(syminfo.tickerid, higherTF, high[1], lookahead=true)
pl = security(syminfo.tickerid, higherTF, low[1], lookahead=true)

PP = 0.0,R1 = 0.0, R2 = 0.0, R3 = 0.0,S1 = 0.0, S2 = 0.0, S3 = 0.0

PP := (ph + pl + pc) / 3
R1 := PP     + (PP   - pl)
S1 := PP     - (ph - PP)
R2 := PP     + (ph - pl)
S2 := PP     - (ph - pl)
factor=input(2)
R3 := ph  + factor * (PP   - pl) 
S3 := pl   - 2 * (ph - PP) 

// 
length=input(21)
//
p = close
vrsi = rsi(p, length)
pp=ema(vrsi,length)
d=(vrsi-pp)*5
cc=(vrsi+d+pp)/2
//
low1=crossover(cc,0)

sell=crossover(close[1],R3) 
//
l = low1
s=sell
if l 
    strategy.entry("buy", strategy.long)
if s 
    strategy.entry("sell", strategy.short)
per(pcnt) =>
    strategy.position_size != 0 ? round(pcnt / 100 * strategy.position_avg_price / syminfo.mintick) : float(na)
stoploss=input(title=" stop loss", defval=15, minval=0.01)
los = per(stoploss)
q1=input(title=" qty_percent1", defval=25, minval=1)
q2=input(title=" qty_percent2", defval=25, minval=1)
q3=input(title=" qty_percent3", defval=25, minval=1)
tp1=input(title=" Take profit1", defval=3, minval=0.01)
tp2=input(title=" Take profit2", defval=5, minval=0.01)
tp3=input(title=" Take profit3", defval=7, minval=0.01)
tp4=input(title=" Take profit4", defval=10, minval=0.01)
strategy.exit("x1", qty_percent = q1, profit = per(tp1), loss = los)
strategy.exit("x2", qty_percent = q2, profit = per(tp2), loss = los)
strategy.exit("x3", qty_percent = q3, profit = per(tp3), loss = los)
strategy.exit("x4", profit = per(tp4), loss = los)

```

> Detail

https://www.fmz.com/strategy/429563

> Last Modified

2023-10-18 11:12:39
