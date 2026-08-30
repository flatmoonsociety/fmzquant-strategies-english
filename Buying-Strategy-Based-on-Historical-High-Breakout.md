
> Name

Buying-Strategy-Based-on-Historical-High-Breakout
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
This strategy is aimed at the bull market. When the stock price breaks through the historical n-day high, buy it and use the EMA moving average to stop the loss. It is a trend following strategy.
## Strategy Principle
1. Calculate the highest price in the past n days as the historical high price.
2. When the current closing price exceeds the historical high price, buy.
3. Use the x-day EMA to stop loss. Stop loss and exit when the price is below the EMA.
4. The n value and x value are adjusted through parameters, and the default is the 200-day highest price and the 90-day EMA.
5. The strategy logic is simple, clear and easy to implement.
## Advantage Analysis
1. Can automatically track trends formed by new high breakthroughs.
2. Use EMA moving average tracking stop loss to lock in most profits.
3. No need to predict the stock price, just follow the buy signal.
4. The default parameters work better for bull market conditions.
5. The code is concise and easy to understand and modify.
## Risk Analysis
1. Big losses can occur at the end of a bull market.
2. Improper stop loss setting may cause the stop loss to be too close or too loose.
3. It is impossible to predict the intensity of the new high breakthrough and the extent of the correction.
4. Highly targeted and not applicable to other market conditions.
5. Parameter optimization may over-fit to historical market conditions.
## Optimization direction
1. Test different parameter combinations to find optimal parameters.
2. Evaluate other stop loss methods such as fixed ratio stop loss.
3. Optimize stop loss parameters to balance stop loss frequency and risk control.
4. Add other filtering conditions to prevent buying due to noise signals.
5. Study how to judge the effectiveness of buying opportunities.
6. You can set up a profit-taking strategy and add a profit locking mechanism.
## Summarize
This strategy implements automatic trend tracking by tracking new high breakthroughs and uses EMA moving averages to stop losses. Although it has certain effects, it is relatively simple and needs to be further expanded and optimized to become a system applicable to the entire market.
||


## Overview

This strategy buys when the price breaks out above the historical n-day high in a bull market, with EMA stop loss. It belongs to trend following strategies.

## Strategy Logic

1. Calculate the highest price over the past n days as the historical high price.

2. Buy when the current close exceeds the historical high price. 

3. Use x-day EMA as the stop loss. Exit when price drops below EMA.

4. Values of n and x adjustable via parameters, default to 200-day high and 90-day EMA.

5. Simple and clear logic easy to implement.

## Advantages

1. Automatically follows trends formed by new highs.

2. EMA trailing stop locks in most profits.

3. No need to predict prices, just follow buy signals.

4. Default parameters work well in bull markets. 

5. Concise code easy to understand and modify.

## Risks

1. Massive losses when bull market ends.

2. Improper stop loss setups lead to premature or delayed stops.

3. Unable to predict strength and pullback of new highs.

4. Strong bias makes it unsuitable for other markets.

5. Parameter optimization risks overfitting to historical data.

## Enhancement

1. Test different parameter combinations for optimum values.

2. Evaluate other stop methods like fixed percentage stops.

3. Optimize stops to balance frequency and risk control.

4. Add filters to avoid buying on noise.

5. Research ways to gauge buy signal strength. 

6. Can add profit taking exits to lock in gains.

## Conclusion

This strategy automates trend following on new highs with EMA trailing stops. Though effective in some cases, it needs expansion and optimization to become robust across all markets.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|200|ATH period|
|v_input_int_2|90|ema line|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-20 00:00:00
end: 2023-09-19 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © gmhfund

//@version=5
strategy("ATH 200d",overlay=1)
plot(close)

bars = input.int(200, "ATH period", minval=5, maxval=2000, step=1)
range_ema = input.int(90,"ema line",minval=100,maxval=400,step=1)

ath_price = ta.highest(bars)[1]
plot(ath_price,color=color.blue)

line_ema = ta.ema(close,range_ema)
exit_condition = ta.crossunder(close,line_ema)
plot(line_ema,color=color.orange)


strategy.entry("Buy", strategy.long, 1, when = close > ath_price) // enter long by market if current open great then previous high
//strategy.close("Buy",when = close < strategy.position_avg_price*0.9 )
strategy.close("Buy",when = exit_condition )
```

> Detail

https://www.fmz.com/strategy/427388

> Last Modified

2023-09-20 15:53:26
