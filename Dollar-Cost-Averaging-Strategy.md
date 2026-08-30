
> Name

Regular fixed amount accumulation average price strategy Dollar-Cost-Averaging-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]
This strategy is called a regular fixed-amount cumulative average price strategy. This strategy gradually reaches the target position through regular fixed-amount purchases and achieves long-term holding of assets.
How the strategy works:
1. Set a fixed purchase amount and purchase frequency.
2. Purchase assets regularly according to the set amount within a fixed period.
3. When the cumulative position reaches the threshold, close the position and cash out.
4. Repeat the above steps to continue accumulating positions regularly.
Specific operation process:
1. Purchase a fixed amount of assets (such as $200) every certain period (such as every month).
2. When the cumulative position exceeds the set threshold (such as 200 shares), all positions will be closed.
3. Then restart the regular buying process and continue to accumulate positions.
Advantages of this strategy:
1. Reduce long-term holding costs and achieve profitability through average prices.
2. The risk of retracement is small, and there will be no high buying point for targeted pursuit.
3. Easy to execute continuously and does not require frequent attention to the market.
Risks of this strategy:
1. It requires long-term holding and cannot cope with short-term price fluctuations.
2. When prices fall for a long time, you may face losses.
3. If you choose the wrong time to sell, you may miss the best shipping point.
In short, the regular quota strategy accumulates assets by building positions in batches, which is more friendly to long-term investors. However, traders still need to pay attention to the risks of big market conditions, optimize sales strategies, and maximize profits by closing positions in batches at market highs.
|| 

This strategy is called the Dollar Cost Averaging Strategy. It aims to accumulate a target position size through periodic fixed-amount purchases, enabling long-term holdings.

How it works:
1. Set a fixed purchase amount and frequency.  
2. Make periodic purchases of the asset at fixed intervals according to set amount.
3. Sell when accumulated position size reaches a threshold.
4. Repeat to continue accumulating positions periodically.

Typical workflow:
1. Buy a fixed amount of assets periodically (e.g. $200 every month).
2. Sell all when accumulated position size exceeds a threshold (e.g. 200 shares).
3. Restart periodic buying to continue accumulating positions.

Advantages of this strategy:
1. Lower averaged cost through long-term holdings.
2. Lower drawdown risks, avoids buying at high points.  
3. Easy to execute consistently without frequent market monitoring.

Risks of this strategy:  
1. Requires long holding periods, cannot adapt to short-term price swings.
2. May face losses during prolonged downtrends.
3. Suboptimal exit timing may miss best selling point.

In summary, the dollar cost averaging strategy accumulates assets through batched buys, friendly to long-term investors. But traders still need to watch out for broad market risks and optimize exit strategies to maximize profits through batched sells at highs.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-08 00:00:00
end: 2023-09-14 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © tanoshimooo

//@version=5
strategy ("DCA", initial_capital=44700, overlay=true)

// To start script at a given date
tz = 0 //timezone
timeadj = time + tz * 60 * 60 * 1000 //adjust the time (unix)
t1 = timeadj >= timestamp(2003, 03, 01, 0, 0) ? 1 : 0 //get the starting time

// Variables
var float lastRef = na
if barstate.isfirst
    lastRef := close
var float cash = 50000 // available money
var float sell_contracts = na
var bool first_trade_done = false

// Parameters
var float sell_min = 200 //200 sell more than sell_min or sell all
var float buy_dollars = 200

var int bi = 90

// LONGS
// if bar_index < bi
strategy.order("Long", strategy.long, int(buy_dollars/close))
cash := cash - int(buy_dollars/close)*close
// label.new(bar_index, na, na, xloc.bar_index, yloc.abovebar, color.blue, label.style_triangleup, color.blue, size.tiny)

//plot(cash)

// SHORTS
// if longExit  
//     if (strategy.position_size*sf*close > sell_min) and (strategy.position_size*sf >= 1)
//         strategy.order ("Long", strategy.short, strategy.position_size*sf)
//         cash := cash + strategy.position_size*sf*close
//     else 
//         strategy.order ("Long", strategy.short, strategy.position_size)
//         cash := cash + strategy.position_size*close
//     lastRef := close
//     label.new(bar_index, na, na, xloc.bar_index, yloc.belowbar, color.red, label.style_triangledown, color.red, size.tiny)

if bar_index == last_bar_index - 2 // bi
    strategy.order ("Long", strategy.short, strategy.position_size)
```

> Detail

https://www.fmz.com/strategy/426936

> Last Modified

2023-09-15 16:52:06
