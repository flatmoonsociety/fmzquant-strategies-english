
> Name

SuperTrend-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
This strategy is based on the super trend indicator to determine the direction of the price trend and generate trading signals accordingly. It belongs to the trend following strategy type. This strategy was specifically tested on the Tesla (TSLA) 1-minute line, and the performance was acceptable.
## Strategy Principle
1. Calculate ATR, the average of the highest price and the lowest price, and use the super trend multiplier to determine the upper and lower rails.
2. Determine whether the price breaks through the upper or lower track to determine the direction of the super trend.
3. A bullish signal is generated when the price crosses the upper rail and a bearish signal is generated when the price crosses the upper rail.
4. You can choose to enter the market on the opening day after the signal is confirmed, or you can choose to enter the market immediately when the price touches the super trend track.
## Strategic Advantages
1. The super trend indicator’s trend judgment is simple and clear, and easy to program.
2. The entry timing can be flexibly selected to meet the needs of different traders.
3. It can quickly capture short- and medium-term trends and is suitable for trend tracking.
4. The strategy has frequent transactions and can be expanded and optimized.
## Strategy Risk
1. The super trend indicator lags behind and may miss the best entry opportunity.
2. Frequent transactions bring greater slippage costs.
3. There are no risk control methods such as stop loss.
4. The backtest data is only based on Tesla’s 1-minute line, which makes it difficult to prove the effectiveness of the strategy.
Corresponding solutions:
1. Adjust parameters to reduce the probability of lag.
2. Add slippage control to ensure that transaction costs are not too high.
3. Add stop-loss tools to control single losses.
4. Backtest on more varieties and cycles to verify the robustness of the strategy.
## Strategy optimization direction
1. Test different super trend parameter combinations to reduce lag.
2. Add a filter to avoid being trapped.
3. Optimize fund management strategies and improve strategy efficiency.
4. Introduce machine learning to predict super trends.
5. Combine with other indicators to verify signals and improve strategy stability.
## Summarize
This strategy uses super trend indicators to determine the direction of short- and medium-term trends and generate trading signals. It is a typical trend following strategy. The overall framework is simple and effective, but can further optimize entry opportunities, risk control, parameter selection, etc. If more types of historical data can be obtained and technologies such as machine learning are added, the stability and profitability of the strategy can be greatly improved.
|| 

## Overview

This strategy uses the SuperTrend indicator to determine price trend direction and generate trading signals, belonging to the trend following strategy category. It is specifically tested on Tesla (TSLA) 1-minute chart with decent results.

## Strategy Logic 

1. Calculate ATR and average of highest high and lowest low to determine SuperTrend upper and lower bands based on multiplier.

2. Determine if price breaks above upper band or below lower band to identify SuperTrend direction.

3. Long signal when price crosses above lower band. Short signal when price crosses below upper band.

4. Can choose to enter on next bar's open when signal is triggered, or immediately when price hits SuperTrend bands.

## Advantages

1. SuperTrend clearly identifies trends, easy to program.

2. Flexible entry options suit different trader preferences. 

3. Can quickly capture medium-term trends, suitable for trend following.

4. Frequent trading allows expansions and enhancements.

## Risks

1. SuperTrend lags potentially missing best entries. 

2. High trading frequency leads to larger slippage costs.

3. No risk control tools like stop loss.

4. Backtest solely on Tesla 1-min data, hard to prove strategy validity.

Possible Solutions:

1. Adjust parameters to reduce lag.

2. Add slippage control to limit costs.

3. Incorporate stop loss to control loss per trade.

4. Backtest across more products and timeframes for robustness.

## Optimization Directions

1. Test different parameter sets to reduce lag.

2. Add filters to avoid whipsaws.

3. Optimize money management for higher efficiency. 

4. Incorporate machine learning to predict SuperTrend direction.

5. Add other indicators to verify signals and improve stability.

## Summary

This strategy uses SuperTrend to identify medium-term trend direction for trading signals, typical of trend following strategies. The overall framework is simple and effective, but can be further improved in areas like entry opportunities, risk management, parameter selection etc. With more historical data across products and integrated techniques like machine learning, it can be significantly enhanced in stability and profitability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|3|SuperTrend Multiplier|
|v_input_2|120|SuperTrend Period|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-24 00:00:00
end: 2023-09-23 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("QuantNomad - SuperTrend - TSLA - 1m", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100)

// INPUTS //
st_mult   = input(3,   title = 'SuperTrend Multiplier', minval = 0, maxval = 100, step = 0.01)
st_period = input(120, title = 'SuperTrend Period',     minval = 1)

// CALCULATIONS //
up_lev = hl2 - (st_mult * atr(st_period))
dn_lev = hl2 + (st_mult * atr(st_period))

up_trend   = 0.0
up_trend   := close[1] > up_trend[1]   ? max(up_lev, up_trend[1])   : up_lev

down_trend = 0.0
down_trend := close[1] < down_trend[1] ? min(dn_lev, down_trend[1]) : dn_lev

// Calculate trend var
trend = 0
trend := close > down_trend[1] ? 1: close < up_trend[1] ? -1 : nz(trend[1], 1)

// Calculate SuperTrend Line
st_line = trend ==1 ? up_trend : down_trend

// Plotting
plot(st_line, color = trend == 1 ? color.green : color.red , style = plot.style_line, linewidth = 2, title = "SuperTrend")

plotshape(crossover( close, st_line), location = location.belowbar, color = color.green)
plotshape(crossunder(close, st_line), location = location.abovebar, color = color.red)

// Strategy with "when"
//strategy.entry("long",  true,  when = crossover( close, down_trend[1]))
//strategy.entry("short", false, when = crossunder(close, up_trend[1]))

// Strategy with stop orders
strategy.entry("long",  true,  stop = down_trend[1])
strategy.entry("short", false, stop = up_trend[1])
```

> Detail

https://www.fmz.com/strategy/427732

> Last Modified

2023-09-24 13:19:47
